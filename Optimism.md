---
id: 
slug: introduction-to-optimism
description: Intro to Optimism
---


<Section name="1. Introduction" description="Introduction to Optimism">

## 1. Introduction
  
The [Optimism Collective](https://app.optimism.io/announcement) is a band of companies, communities, and citizens working together to reward public goods and build a sustainable future for Ethereum.

Together we will dispel the myth that public goods cannot be profitable. Public goods (such as Optimism and Ethereum) often go underfunded when incentives aren't properly aligned, forcing many to make trade-offs between earning a profit and building for the common good. We are bound by a mutually beneficial pact, [our vision](https://www.optimism.io/vision) can be summed up with the equation **Impact = Profit**.

[You can read more about who we are and what we are doing here](http://localhost:8080/docs/governance/#how-can-we-achieve-this).
  
</Section>

<Section name="2. How It Works" description="What are optimistic rollups, and how Optimism offers Ethereum-level security at a fraction of the cost">
  
## 2. How It Works
  
[Ethereum has limited capacity](https://ethereum.org/en/layer-2/) because of the [blockchain trilemma](https://medium.com/certik/the-blockchain-trilemma-decentralized-scalable-and-secure-e9d8c41a87b3). 
To have decentralization we need to enable as many people as possible to run a node, which means that the number of transactions that can be processed per minute is limited by the capacity of standard hardware. 
This limits our ability to scale, unless we accept the security implication of not having every node process every transaction.

Solutions that build on top on Ethereum are called layer 2 or L2 (with Ethereum itself called layer 1 or L1). 
Optimism uses a type of solution called an [optimistic rollup](https://ethereum.org/en/developers/docs/scaling/optimistic-rollups/).
*Rollups* post all transactions on layer 1, so data integrity and availability are provided by Ethereum. 
 
*Optimistic Rollups* use economic incentives to ensure the data processing, done offchain, is done correctly. 
The sequencer posts the merkle root of the blockchain state on L1 (called the *state root*).
Other nodes, called verifiers, can issue a *fault challenge* if they believe the state root is incorrect.
In the case of a fault challenge part of the transaction is executed on L1 to verify which is the correct state root.
  
Sequencers that post correct state roots, and verifiers that challenge incorrect ones, are rewarded.
Sequencers that post incorrest state roots, and verifiers that challenge correct ones, are penalized.
Because 

</Section>

<Section name="3. Using Optimism" description="A simple exercise to use the Optimism network">  
  
## 3. Using Optimism
  
[Follow the steps in this exercise](https://github.com/ethereum-optimism/optimism-tutorial/tree/main/getting-started) to interact with Optimism using your favorite development stack.

</Section>

<Section name="4. What Else?" description="Other things you can do on Optimism">  

## 4. What Else?  
  
### NFTs
  
### Launching a token
  
### Deploying a Dapp  

</Section>

<Section name="5. Getting Involved" description="Ways to get involved with Optimism">   
  
## 5. Getting Involved  
  
- [User docs](https://help.optimism.io/hc/en-us)
- [Developer docs](https://community.optimism.io/)
- [Discord](https://discord-gateway.optimism.io/)
- [If you don't know what to build]()
  
</Section>  
  
