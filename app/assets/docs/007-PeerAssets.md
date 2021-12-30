# PeerAssets

> PeerAssets offers the framework that enables communities and organizations to issue and transact with blockchain assets.

PeerAssets is a blockchain token protocol invented in 2016 by `peerchemist` as a minimalist method to efficiently support tokenization.  PeerAssets is tailored to work with the Peercoin blockchain, however its design is general and can be ported to other blockchains like Bitcoin with cross-chain compatibility.
PeerAssets transactions are standard Peercoin transactions, relayed by the standard nodes and processed by miners as any other transaction. Unlike many similar protocols ([Omni](http://www.omnilayer.org/), [CounterParty](http://counterparty.io/)), PeerAssets does not use so called "auxilary" tokens (Omni and XCP respectively), it only uses blockchain's native currency which is used to pay transaction fees. PeerAssets protocol does not require hard nor soft fork of the host network, but it requires development of a PeerAssets aware client. PeerAssets is also inspired by the original idea of "Colored Coins" and uses OP_RETURN to write data on the blockchain, but offers some optimizations to reduce amount of data written in the OP_RETURN and reducing blockchain bloat.
PeerAssets enables easy querying of the blockchain for relevant transactions via the use P2TH, which allows development of very light clients and does not mandate the use of resource intense blockchain-parsing nodes which are common with competing protocols.

PeerAsset tokens can be utilized to represent any type of asset like bonds or equity. PeerAssets can also represent real life objects in the form of non-fungible tokens, and allow for authentification via the blockchain.  The possibilities are wide enough to encompass most use cases for tokenization, without sacrificing the efficiency of the design.


### Nomenclature

PeerAssets uses a friendly phrasing to succinctly describe the protocol and it's interactions. In PeerAssets terminology assets are named “decks” and each transaction on the deck is called a “card”. Deck creation and card manipulation are types of transactions parsed by the PeerAsset client, which uses the known protocol rules to calculate card balances and the total state of the deck.  A deck with a single card, for example, would act as a non-fungible token.

`Deck - named asset`

`Card - individual token`

## Transaction types

PeerAssets protocol has four elemental transaction types:

* **Deck spawning transaction**

Creates a new token at a given Peercoin address. Asset is described by:
* token name,
* descriptive metadata,
* how divisible the token is (number of decimals),
* the deck issue mode.

Deck issue modes can be understood as light smart contracts as they allow great flexibility when defining common rules of token economics such as ONCE, MULTI, or CUSTOM.

* **Card issue transaction**

Creates new tokens of `deck` at given Peercoin address.

* **Card burn transaction**

Destroys tokens and removes them from the supply.

* **Card transfer transaction**

Standard p2p token transaction, transfer a token from the address where they reside to a new address.

## Tools

### pacli

This command line program is useful as companion utility during PeerAssets development and testing. It is built for console usage via intuitive and easy to learn set of commands. It stores the privkey in OS's native keystore, which is automatically unlocked upon logging into active user session.

github: https://github.com/PeerAssets/pacli

### pypeerassets

Official Python implementation of the PeerAssets protocol.

github: https://github.com/PeerAssets/pypeerassets

### papi

PeerAssets API provider, implemented using pypeerassets.

github: https://github.com/PeerAssets/papi

## Wallets

### chizukeki

A light, cross-platform Peercoin wallet with baked-in support for the PeerAssets.

code: https://github.com/peerassets/chizukeki

deployed: https://peerassets.github.io/chizukeki/

## Future plans & research

The PeerAssets project has adopted [RFC](https://en.wikipedia.org/wiki/Request_for_Comments) schema of sharing new ideas and establishing standards like the Peercoin project.
RFC's are submitted on the PeerAssets [github repo](https://github.com/PeerAssets/peerassets-rfcs) and peer-reviewed, after which code experimentation and final implementation proceeds.

Some RFCs that show the wide array of possible applications for PeerAssets includes:

[PeerAssets Alias/Proof-of-identity protocol specification](https://github.com/PeerAssets/peerassets-rfcs/blob/master/0003-peerassets-alias-poid-protocol-specification.md)

> Extension of PeerAssets protocol specifies using singlet PeerAsset deck to alias the Peercoin address with any UTF-8 string with added secondary functionality of using descriptive information contained in the PeerAssets token to allow proof-of-identity verification of the privkey owner.

[PeerAssets on-chain voting protocol specification](https://github.com/PeerAssets/peerassets-rfcs/blob/master/0005-on-chain-voting-protocol-proposal.md)

> PeerAssets on-chain voting protocol. Aim is to deliver a standardized way to organize and operate peer-to-peer voting and opinion polls in fully decentralized and trustless fashion. Both vote and poll initialization and counting must be done in completely decentralized and trustless fashion without dependency on 3rd party services.

[PeerAssets Data Audit Protocol](https://github.com/PeerAssets/peerassets-rfcs/blob/master/0009-data-audit.md)

> The primary purpose of this protocol is to record cryptographic hashes of successive revisions of single-file documents in a public blockchain, in a manner which enables thin clients to easily query and verify document histories. Such histories inherit useful properties from the underlying blockchain, namely immutability and massive replication, and can therefore serve as proofs of existence.

## Articles
[Whitepaper](http://peerassets.github.io/WhitePaper/)

[PeerAssets deck issue modes](https://medium.com/peercoin/peerassets-deck-issue-modes-c419f38f7800)

[The benefits of PeerAssets](https://medium.com/peercoin/the-benefits-of-peerassets-77bad7693925)

[[Tutorial] PeerAssets Peer to Peer (p2p) Transactions](https://talk.peercoin.net/t/tutorial-peerassets-peer-to-peer-p2p-transactions/8640)

[[Tutorial] Basic Deck Creation with PeerAssets](https://talk.peercoin.net/t/tutorial-basic-deck-creation-with-peerassets/8639)
