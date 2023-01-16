# Introduction
Before starting to use near-multicall for making DAO proposals, we first need to establish a general idea of how things work. 

## The multicall instance (MI)
The regular DAO contract (SputnikDAO) only allows calling one target contract per proposal. That's why for proposals that call multiple smart contracts, we need a proxy contract that will handle all desired function calls. Multicall instances serve this purpose. Every DAO has its own private multicall instance to work with. 
![](https://i.imgur.com/jUgiHru.png)
The DAO will call its MI and pass it some instructions, the MI will follow those instructions to call the desired functions on the target contracts.

```admonish info
The MI address is always derived from the DAO address. It's easy to explain it with an example:
If the DAO address is `marmaj.sputnik-dao.near` then it will have a MI deployed at `marmaj.v1.multicall.near`
```

DAOs need to create a multicall instance (MI) before using it for the first time. You can think of this as an installation step that only happens once. Instructions for this can be found on the [onboarding guide](onboarding.md).
