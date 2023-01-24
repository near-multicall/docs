# Make a multicall proposal

<a href="https://multicall.app/#/dao" target="_blank">Our website</a> offers a space to build your proposals. Simply drag a _card_ from the side menu into the column in the middle of the page. This column will contain the instructions given to the Multicall Instance (MI), and they are executed in **sequence** from top to bottom. For advanced usage, you can add more columns by clicking the _+_ icon on top of the columns. The instructions in all columns will run **concurrently**.  

![](https://i.imgur.com/UtFmnOt.gif)

Let's talk a little about the cards. Cards serve as building blocks of the proposal. They hold information about what contract and function to call with what parameters. Click the pen icon (<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200" /><span class="material-symbols-outlined">
edit</span>) in the top right corner of a card to open the card's editor where you specify the required parameter. Any interaction can be modeled using the custom card, but we're always expanding our selection of cards for sepecific purposes to lower the technical barriers for users.

``` admonish info
Think we're missing an important card? Let us know on our <a href="https://discord.gg/wc6T6bPvdr" target="_blank">Discord</a> !
```

Once you are satisfied with your proposal, click on the _Export_ tab in the side menu. You will be asked to put a proposal description that will be displayed on AstroDao. If everything is fine, i.e. you don't have any unresolved input errors and you have the rights to make proposals on the DAO, the propose button at the bottom of the menu will turn green. Click it to make the proposal on the DAO.  

```admonish note
A small amount of NEAR will be required to make the transaction. It represents a proposal bond paid to the DAO, and will be reimbursed once your DAO proposal is approved. The amount is set in the DAO configuration, near-multicall does not charge any fees.
```

## Dealing with funds

As we have seen in _[The multicall instance](introduction.md#the-multicall-instance-mi)_ the MI serves as a proxy contract for the DAO. Since the DAO and MI are not the same contract, the MI cannot access funds belonging to the DAO. This is a good thing when it comes to security, but does bring some inconveniences. Any funds that are need for a multicall proposal should be transferred to the MI prior to the execution of said proposal. We suggest to have a small tokens' allowance on the MI for quick access, while keeping the main DAO's treasury on the DAO. The funds on the MI are only accessible by the MI admins (per default, only the DAO).
```admonish caution
Near-multicall is a beta software and we do not guarantee the safety of assets on the MI. Our contracts are open source, and can be found on <a href="https://github.com/near-multicall/contracts" target="_blank">this repository</a>. Use at your own risk.
```

![](https://i.imgur.com/myT7aaY.png)


You can easily see the available funds on the MI via the _Funds_ tab on the <a href="https://multicall.app/#/dao" target="_blank"><i>DAO page</i></a>.  
When making a multicall proposal, keep in mind that the actions will be called from the MI's address, and not the DAO address. Say you want to interact with a Dapp, it will be the MI's Dapp account that is used, not the DAO's.
