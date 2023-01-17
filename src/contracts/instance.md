# The instance contract
This contract holds the core logic for multicall. Each DAO gets its own Multicall Instance (MI) contract to use. The contract consists of three main features:
1. The **main method** in this contract is:  
`multicall ( calls: BatchCall[][] )`  
It executes a bunch of `BatchCall` arrays.  
Each `BatchCall` has information for making a batch of function-calls: a target address and an array on function-calls to execute on that target. Each function-call has a function name, arguments encoded in base64, gas to use (u64 encoded as string) and amount of yoctoNEAR attached deposit (u128 encoded as string).  
Batches inside one array run one after another, as a promise chain.  
Different arrays of batches run in parallel.  
Example:  
    ```
    calls = [
        [ Batch_11, Batch_12, Batch_13 ],
        [ Batch_21, Batch_22]
    ]
    ```  
    In this example we have 2 arrays of batches. In the first one `Batch_12` waits for `Batch_11` and `Batch_13` waits for `Batch_12`. In the second array `Batch_22` waits for `Batch_21`. Both arrays start executing in the same block and are independent of each other.

2. **Permissioned interactions** with the contract through whitelisting of addresses:  
Due to the async nature of Near, funds can sit in the contract during multiple blocks awaiting the execution of cross-contract calls. To prevent stealing of funds, we require an address to be whitelisted before calling one of the contract's critical methods.
there are two main whitelists:  
`admins whitelist` holds addresses that can interact with the contract, they can add or remove others from the whitelist.  
`tokens whitelist` holds token addresses that can be attached to function calls, as the contract implements ft_on_transfer.  
The contract's address is whitelisted by default, this allows nesting multiple contract methods for convenience.  

3. **Jobs**:  
Multicall executions can be scheduled to run at a certain time in the future, made possible by integrating [croncat](https://cron.cat/). Anyone can register a job on the multicall contract, but an admin has to approve it. Admins can pause/resume job executions and also edit a job's multicall arguments.  
The following must be specified when creating a job:
    ```ts
    function job_add (
        job_multicalls: MulticallArgs[],
        job_cadence: string, // cron expression
        job_trigger_gas: u64,
        job_total_budget: u128,
        job_start_at: u64 = context.blockTimestamp
    ): u32 
    ```

## Example Calls

### Call structure
example multicall arguments:
```json=
{
    "calls": [
        [ 
            {
                "address": "hello.lennczar.testnet",
                "actions": [
                    {
                        "func": "hello",
                        "args": "eyJ0aGluZyI6IldvcmxkIn0=", // base64 encoding for {"thing":"World"}
                        "gas": "10000000000000",
                        "depo": "0"
                    },
                    {
                        "func": "hello",
                        "args": "eyJ0aGluZyI6IldvcmxkIn0=", // base64 encoding for {"thing":"World"}
                        "gas": "10000000000000",
                        "depo": "0"
                    }
                ]
            },
            {
                "address": "hello.lennczar.testnet",
                "actions": [
                    {
                        "func": "hello",
                        "args": "eyJ0aGluZyI6IldvcmxkIn0=", // base64 encoding for {"thing":"World"}
                        "gas": "10000000000000",
                        "depo": "0"
                    }
                ]
            }
        ],
        [
            {
                "address": "hello.lennczar.testnet",
                "actions": [
                    {
                        "func": "hello",
                        "args": "eyJ0aGluZyI6IldvcmxkIn0=", // base64 encoding for {"thing":"World"}
                        "gas": "10000000000000",
                        "depo": "0"
                    }
                ]
            }
        ]
    ]
}
```
This example calls the function `hello(thing: string): string` in the contract `hello.lennczar.testnet`.  
We see two arrays of batches: in the first array we have 2 batches that will be run as a promise chain (i.e. second batch will wait for the first batch). The first batch calls the function twice and the second batch calls it only once. In the second array we have one batch that calls the function once, it will run in parallel independently of the two previously mentioned batches.  
Running this results in the following [transaction](https://explorer.testnet.near.org/transactions/HHEDj5FnRXJpGwR68PegHNWgpGjXcFWFyq2Nw27sDkx2)  