# The factory contract
The main method on the factory contract is `create()`. It must be called from a DAO using a FunctionCall proposal.
Here's the singature of the method:
```TypeScript
export function create(
    multicall_init_args: { 
        admin_accounts: string[];
        croncat_manager: string;
        job_bond: u128;
    },
    public_key: string = ""
): ContractPromiseBatch
```
- `admin_accounts`: a list of NEAR accounts that will have absolute control over the instance, including its funds. We recommend that only the DAO is included here so the created instance only executes instructions approved by the DAO.
- `croncat_manager`: address of the <a href="https://cron.cat/" target="_blank">Croncat</a> manager contract. It is used by our scheduling features.
- `job_bond`: the job bond is the $NEAR amount to be paid by users wishing to submit scheduled multicall proposals to the DAO. The proposer will be re-imbursed upon approval of his proposal. By default we set it to be equal to the DAO's proposal bond.
- `public_key`: this is **optional**. When provided, this key will added as a <a href="https://docs.near.org/concepts/basics/accounts/access-keys#full-access-keys" target="_blank">fullAccess key</a> on the multicall instance. 
```admonish important
If a public key is provided, do not include the "ed25519:" prefix.
```
