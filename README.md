# OP-ETHGLOBAL-Guides

---


<Section name="1. Introduction" description="Introduction to Optimism">

## Introduction
Hello! By the time you've finished reading this page you should have a foundational understanding of how Optimism makes Ethereum transactions cheaper and faster, the approach that Optimism is taking to scaling both Ethereum and Ethereum's values, and why Optimism is the best place to build your next Ethereum-native app.

We've tried to make this guide as comprehensive as possible while still keeping the content accessible to most readers. Some content on this page is geared towards readers with a technical background but should still be comprehensible to those with a basic understanding of how blockchains work. Generally speaking, we err on the side of simplicity and approachability.

Without further ado, let's find out How Optimism Works!


## Design Philosophy
Optimism is built according to a strong design philosophy that stands on four main pillars: simplicity, pragmatism, sustainability, and, of course, optimism. It's important to understand these pillars as they heavily influence the design of Optimism as a whole.

#Simplicity 
Optimism is designed to be as simple as possible for the featureset it provides. Ideally, Optimism should be composed of the minimum number of moving parts required for a secure, scalable, and flexible L2 system. This simplicity gives Optimism's design a number of significant advantages over other more complex L2 constructions.

Simplicity reduces engineering overhead, which in turn means we can spend our time working on new features instead of re-creating existing ones. Optimism prefers to use existing battle-tested Ethereum code and infrastructure where possible. The most visible example of this philosophy in practice is the choice to use Geth as Optimism's client software.

When dealing with critical infrastructure, simplicity is also security. Every line of code we write is an opportunity to introduce unintentional bugs. A simple protocol means there's less code to write and, as a result, less surface area for potential mistakes. A clean and minimal codebase is also more accessible to external contributors and auditors. All of this serves to maximize the security and correctness of the Optimism protocol.

Simplicity is also important for the long-term vision of Optimism. By limiting the amount of code that we write on top of Ethereum tooling, we're able to spend most of our time working directly with existing codebases. Engineering effort that goes into Optimism can also directly benefit Ethereum, and vice versa. This will only become more pronounced as the Optimism protocol solidifies and existing resources can be redirected towards core Ethereum infrastructure.

# Pragmatism 

For all its idealism, the design process behind Optimism is ultimately driven by pragmatism. The core Optimism team has real-world constraints, the projects that build on Optimism have real-world needs, and the users that engage with Optimism have real-world problems. Optimism's design philosophy prioritizes user and developer needs over theoretical perfection. Sometimes the best solution isn't the prettiest one.

Optimism is also developed with the understanding that any core team will have limited areas of expertise. Optimism is developed iteratively and strives to continuously pull feedback from users. Many core Optimism features today (like EVM Equivalence) were only made possible by this iterative approach to protocol development.

# Sustainability
Optimism is in it for the long haul. Application developers need assurance that the platform they're building on will remain not only operational but competitive over long periods of time. Optimism's design process is built around the idea of long-term sustainability and not taking shortcuts to scalability. At the end of the day, a scalable system means nothing without the ecosystem that sustains it.

Sustainability actively influences Optimism's protocol design in ways that go hand-in-hand with our philosophy of simplicity. The more complex a codebase, the more difficult it is for people outside of the core development team to actively contribute. By keeping our codebase simple we're able to build a bigger community of contributors who can help maintain the protocol long-term.

# Optimism 
Of course, none of this would be possible without a sense of optimism. Our optimism about the Ethereum vision keeps this project moving forward. We believe in an optimistic future for Ethereum, a future where we get to redesign our relationships to the institutions that coordinate our lives.

Although Optimism looks like a standalone blockchain, it's ultimately designed as an extension to Ethereum. We keep this in mind whenever we're creating new features or trying to simplify existing ones. Optimism is as close to Ethereum as possible not only for pragmatic reasons, but because Optimism exists so that Ethereum can succeed. We hope that you can see the influence of this philosophy when looking at Optimism's design.

<Quiz id={"n/a"} />

Optimism is a 
- New blockchain with fast speeds and low fees
- A layer built on top of Ethereum to reduce user fees and increase speed [✅]

</Section>

<Section name="2. How does Optimism work?" description="Understanding Optimism">

## Rollup Protocol

We've covered most of the "why" behind Optimism. Now it's time to explain the big idea that makes Optimism possible: the Optimistic Rollup. We'll go through a brief explainer of how Optimistic Rollups work at a high level. Then we'll explain why Optimism is built as an Optimistic Rollup and why we believe it's the best option for a system that addresses all of our design goals.

#TLDR
Optimism is an "Optimistic Rollup," which is basically just a fancy way of describing a blockchain that piggy-backs off of the security of another "parent" blockchain. Specifically, Optimistic Rollups take advantage of the consensus mechanism (like PoW or PoS) of their parent chain instead of providing their own. In Optimism's case this parent blockchain is Ethereum.

## Block Storage 
All Optimism blocks are stored within a special smart contract on Ethereum called the [CanonicalTransactionChain](https://etherscan.io/address/0x5E4e65926BA27467555EB562121fac00D24E9dD2)(or CTC for short). Optimism blocks are held within an append-only list inside of the CTC (we'll explain exactly how blocks are added to this list in the next section). This append-only list forms the Optimism blockchain.

The CanonicalTransactionChain includes code that guarantees that the existing list of blocks cannot be modified by new Ethereum transactions. However, this guarantee can be broken if the Ethereum blockchain itself is reorganized and the ordering of past Ethereum transactions is changed. The Optimism mainnet is configured to be robust against block reorganizations of up to 50 Ethereum blocks. If Ethereum experiences a reorg larger than this, Optimism will reorg as well.

Of course, it's a key security goal of Ethereum to not experience these sort of significant block reorganizations. Optimism is therefore secure against large block reorganizations as long as the Ethereum consensus mechanism is too. It's through this relationship (in part, at least) that Optimism derives its security properties from Ethereum.

## Block Production
Optimism block production is primarily managed by a single party, called the "sequencer," which helps the network by providing the following services:

Providing instant transaction confirmations and state updates.
Constructing and executing L2 blocks.
Submitting user transactions to L1.
The sequencer has no mempool and transactions are immediately accepted or rejected in the order they were received. When a user sends their transaction to the sequencer, the sequencer checks that the transaction is valid (i.e. pays a sufficient fee) and then applies the transaction to its local state as a pending block. These pending blocks are periodically submitted in large batches to Ethereum for finalization. This batching process significantly reduces overall transaction fees by spreading fixed costs over all of the transactions within a given batch. The sequencer also applies some basic compression techniques to minimize the amount of data published to Ethereum.

Because the sequencer is given priority write access to the L2 chain, the sequencer can provide a strong guarantee of what state will be finalized as soon as it decides on a new pending block. In other words, it is precisely known what will be the impact of the transaction. As a result, the L2 state can be reliably updated extremely quickly. Benefits of this include a snappy, instant user experience, with things like near-real-time Uniswap price updates.

Alternatively, users can skip the sequencer entirely and submit their transactions directly to the CanonicalTransactionChain via an Ethereum transaction. This is typically more expensive because the fixed cost of submitting this transaction is paid entirely by the user and is not amortized over many different transactions. However, this alternative submission method has the advantage of being resistant to censorship by the sequencer. Even if the sequencer is actively censoring a user, the user can always continue to send transactions on Optimism.

## Block Execution
Ethereum nodes download blocks from Ethereum's p2p network. Optimism nodes instead download blocks directly from the append-only list of blocks held within the CanonicalTransactionChain contract. See the above section regarding block storage for more information about how blocks are stored within this contract.

