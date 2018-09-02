# Peercoin proof of stake

>Peercoin uses both the Proof-of-Work and Proof-of-Stake algorithms. The PoW algorithm is used to spread the distribution of new coins. Up to 99% of all peercoins is created with POW. Proof-of-Stake is used to secure the network: The chain with longest POS coin age wins in case of a blockchain split-up.

`Minting`, as it is called in Peercoin to make a proof-of-stake block, is based on metrics of an unspent transaction.
If we take a look at the number one spot of the rich list, transaction c7293fc60c80bdcc374775d1f0734e0766465b905bae1a312fe487793be3b8f7 has among others the following characteristics:

* The transaction appeared in block 376161 at timestamp 1531750952 (Unix time).
* The transaction in the block has an offset of 383 bytes. It is the third transaction in the block. The size of the first two transactions in the block are respectively 78 and 224 bytes.
* The transaction timestamp is 1531750624.
* The second recipient (index 1) received 1786301.06651300 Peercoins which, at the moment, is still unspent.

These metrics, along with two more data points serves as a basis to calculate a hash for POS minting:

* a future timestamp X (in Unix time notation) in which the stake could win;
* a block modifier that was set by the network 1830080 seconds (~21 days) earlier than X.

Every 6 hours the network calculates a new block modifier to be used for POS minting.

The win in proof-of-stake minting, the calculated hash is compared to the current difficulty minus the coinage. The chances of finding a stake therefor improves when either the coinage increases or when the difficulty of the network decreases.

## Peercoin minting behaviour

* Minting process can only start after 30 days of coinage.
* Minting coinage is maxed out after 90 days. Which means that after 90 days the only variable left in PoS is the current difficulty.
* Minting is predictable and not random. For a given transaction, you can calculate the maximum network PoS difficulty over time for your transaction to be able to mint a PoS block.
* Whenever this PoS difficulty is higher than the current network PoS difficulty your Peercoin client can mint a PoS block.
* PoS blocks can be rejected (orphans) if several people mint a PoS block within a given window (2 hours also called timedrift). Only one (the chain with longest coin age) will be accepted.
* Minting splits the transaction in two if coinage < 90 days.
* PoS block reward is 1% annual. This 1% is factor of your coinage, and is not maxed out.
* A transaction that just staked has its coins is locked for 520 confirmations (3-4 days).
* Merging transactions, spending coins, etc. burns coinage (resets it to 0).
* PoS reward is directly added to your transaction which staked (if this transaction is split in two because coinage < 90 days, the reward is equally distributed to both resulting transactions).

## Peercoin v0.5 Proof-of-Stake protocol

![Peercoin PoS diagram](../img/pos-diagram.svg)

## Qualities of Proof-of-Stake Consensus

### Efficient
Proof-of-stake in Peercoin is efficient because network security is not dependent on wasting massive amounts of electrical energy (proof-of-energy-burn). Instead minters invest their coins and time to emulate the PoW process. This is done by simply need to open up their wallet app, send coins to their address and let them sit while they are occasionally selected by the protocol to mint the next block. This process is both energy and cost efficient.

### Aligning interests
Because coin owners are the ones who produce new blocks in Proof-of-Stake, this means security providers and users of the network are ultimately the same group of people.
No longer is there a separate group of security providers who only care about making profit and are not financially tied to the network itself. All security providers are forced to own a stake in the network through ownership of Peercoin. This causes everyone to have a similar financial interest in the long-term future of the network, which leads to much less conflict between factions with different ideas about how the blockchain should develop and evolve.

### User governance
Because users in Peercoin have the ability to produce blocks, they also have the power to influence and determine the future direction of the network. User governance comes in pair with PoS consensus mechanism. Peercoin is the very first blockchain capable of allowing its protocol rules to be governed directly by its users.

### Global network
As a direct consequence of resource efficient consensus mechanism, the number of people capable of participating in the block creating race is much expanded. Security providers are no longer drawn to geographical locations with cheap electricity. Due to how cost efficient proof-of-stake is to operate a node, minting nodes can be setup anywhere in the world. This allows Peercoin to maximize its level of decentralization and achieve global security from minting users all around the world.

### Network security is price independent
Unlike proof-of-work where miners are completely dependent on the market price of a blockchain's native token to ensure profitability, Peercoin contains no such price dependency. Proof-of-stake minters are compensated as motivation to provide consistent security, however since this process is so inexpensive to perform minters actually have the ability to voluntarily operate a minting node without compensation if they want to.
Even without compensation from the network, the process of minting helps to secure the blockchain and along with it a stakeholder's overall investment. The ability to decide which version of the protocol to run also gives a minter the opportunity to make their voice heard concerning future upgrades to the network. These are two important reasons a stakeholder may have to want to run a node for free, however compensation is automatically provided which makes it even better to participate. Voluntarily running a proof-of-work mining node is just not possible due to the requirement of being profitable enough in order to afford the associated costs of participating.
Since 2012 though it has been proven that Peercoin is capable of sustaining its network security even during the lowest periods of demand where market price was close to zero. If the network is capable of surviving extremely stressful conditions like these then it can likely survive anything the market throws at it.

### Higher Resistance to Censorship
As explained above, the efficiency of proof-of-stake results in a blockchain network that can easily be secured by people all over the world who hold some amount of Peercoin. This global decentralized security makes the Peercoin network incredibly difficult to censor and shut down.
It is similar to downloading files through a bittorrent network. In bittorrent network, many people around the world operate nodes where they hold a full copy of the file that is trying to be downloaded. Pieces of the file are downloaded from different nodes until the full file has finished downloading. If a government were to deem this file sharing illegal and attempt to shut down the torrent network, they would be forced to target every single node on the network no matter where they happen to exist in the world. Even then, there is nothing stopping more torrent nodes from popping up that share the exact same file. As long as one node exists that shares the file, it can be downloaded and spread to others.

Peercoin works in a similar way where minting nodes that process transactions can be operated from anywhere in the world as long as the minter has access to a computer, minimal electricity, some amount of Peercoin and an internet connection. Geographical decentralization of minting nodes makes it incredibly difficult to shut down the Peercoin network, but when the number of nodes around the world expands to thousands or even tens of thousands then it essentially becomes impossible to censor.
In systems like these, individual nodes are usually called peers. Together they act as a peer-to-peer network. This is where Peercoin obtained its name. It was originally introduced by Sunny King as ppcoin, which stood for peer-to-peer coin. Shortly after it was renamed to Peercoin.