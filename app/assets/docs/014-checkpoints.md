# Checkpoints

Checkpoints are chosen block heights for which the checksum is saved the Peercoin client. With the help of checkpoints, your client is able to identify if it has downloaded the correct blockchain or if an attacker attempts to provide it with a chain featuring "fake history".

## Deep chain reorganizations

> If a single miner has more resources than the entirety of the rest of the network, this miner could pick an arbitrary previous block from which to extend an alternative block history, eventually outpacing the block history produced by the rest of the network and defining a new canonical transaction history.

This is called a “chain reorganization,” or “reorg” for short. All reorgs have a “depth,” which is the number of blocks that were replaced, and a “length,” which is the number of new blocks that did the replacing.

Deep reorganizations of the blockchain can be result of an attack on the network, whether it's PoS or PoW network. Just about 15h before this article is written there was an attack on Ethereum-Classic (a PoW network) which resulted in rollback of some 100 blocks and multiple double-spend attempts. [Read more](https://blog.coinbase.com/ethereum-classic-etc-is-currently-being-51-attacked-33be13ce32de)

Checkpoints serve to protect the history of the blockchain and prevent deep chain reorganization. Most of public blockchains use checkpoints, usually in the form of a "hardened checkpoints" which are hard-coded in the source code of the client. No blockchain reorganization is allowed deeper than the last known checkpoints.

### Nothing-at-Stake

Deep chain reorganizations are theoretically easier to accomplish on a Proof-of-Stake system as an attacker can fabricate the history "for free", this is commonly referred to as Nothing-at-Stake attack and is probably the most criticized element of all the Proof-of-Stake systems.

As of time of the writing Peercoin uses both centrally broadcast checkpoints which are signed with the developer's private key and hardened checkpoints encoded in the client itself.
Alternative public PoS blockchains have approached the matter in somewhat different manner, like NXT and it's 720 block anti-rollback protection, Decred with PoW based timestamping<sup>[1](#footnote-1)</sup> and few alternative proposals like checkpointing against the Bitcoin network by periodically etching messages into the Bitcoin blockchain.

We are confident that the Nothing-at-stake attack is orders of magnitude less likely to occur then it's usually portrayed in the mainstream "blockchain" media.
It's incredibly expensive to construct and organize the attack.

## Why is Peercoin still keeping the checkpoints?

> Checkpoints system is probably the most criticized design choice of Peercoin, frequently used to undermine the project.

> Common myth is that Peercoin concesus is not safe without the centralized checkpoints, but that is absolutely not true.

As of version 0.2, centrally-broadcasted checkpointing is no longer a critical part of the protocol.
It's purpose is to defend the network during the initial growth period, and to help ensure a smooth upgrade path, however it was largely kept because of inertia and low interest for the Peercoin blockchain in period between early 2015 and late 2016. The checkpoints exist solely as a security measure: if something terrible were to happen, we have the checkpoints as a backup.

As of version 0.6 the official client allows for opting-out of the checkpoints entirely, while checkpoint system itself will likely be obsoleted and removed after the process of re-basing Peercoin against modern Bitcoin-core codebase is complete.

As of version 0.10 support for checkpoints has been from official Peercoin client.

## Footnotes

<a id="footnote-1">1</a>: https://en.wikipedia.org/wiki/Proof-of-stake#Criticism
