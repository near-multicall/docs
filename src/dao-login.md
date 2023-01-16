# DAO login
Near-multicall allows DAOs to interact more freely with other DApps on NEAR. However, it's not always easy to see the results of these interactions. DApp interfaces provide invaluable information to their users, such as:
- Overview of Defi positions 
- View into pending or unclaimed rewards
- Usage history and statistics

Hence the need for DAO members to login into DApps using their DAO's address.

## Here's how to do it: 
1. Open the DApp to be used. Example: [Ref-finance](https://app.ref.finance/)
2. If you're already logged in with your personal wallet there, Log out.
3. On Ref, click login, choose NEAR wallet, and then close that tab.
4. Open [Multicall](https:///www.multicall.app/#/app/) on a seperate tab. 
5. Click the DAO/Multicall login dialog.
6. Paste the DApp URL in the input field.
7. Click on Proceed.

Here's a GIF going over the same steps using [Ref-finance](https://app.ref.finance/)

![](https://i.imgur.com/xv2BMVn.gif)

```admonish note
- This only works with DApps that support either [NEAR wallet](https://wallet.near.org/) or [MyNearWallet](https://mynearwallet.com/)
- Login will be in "read-only" mode, so the DAO's account will not initiate transactions using the DApp's interface
```
