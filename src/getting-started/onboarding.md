# Onboard your DAO
```admonish note
In order to create a multicall instance for your DAO, you must have permissions to create function-call proposals on the DAO. 
```

1. Go to <a href="https://multicall.app/#/dao" target="_blank">https://multicall.app/#/dao</a>
2. In the lower left hand corner log in with your wallet (1.) and select the DAO you would like to use multicall with (2.).

![](https://i.imgur.com/PiS2KTW.png)


```admonish tip
If the DAO symbol lights up red, the address is not a valid dao address - please check for typos. Instead the symbol should be yellow, indicating that while the DAO exists, there is no belonging multicall instance yet.
```

3. In the middle of the page you see requirements that need to be met in order to create a multicall instance for the specified dao. If all except "*DAO has no multicall instance*" are met, a green button shows up, click it to propose a multicall creation proposal.

![](https://i.imgur.com/9fntsfD.png)

The website will also show a blue button, if a creation proposal already exists, click it to vote yes (You can also vote using AstroDAO).

![](https://i.imgur.com/mQpHGcu.png)

4. Once the proposal passes, a multicall instance will be deployed to **[dao&#x2011;name].v1.multicall.near**. If a multicall instance exists for the chosen DAO, the website will display its state, such as whitelisted tokens and job bond.

![](https://i.imgur.com/IIQYxOs.png)
