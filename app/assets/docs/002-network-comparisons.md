# Comparison with other blockchain networks

Historically, Peercoin originated as a fork of Bitcoin with added functionalities and protocol tuning to support Proof-of-Stake.  Peercoin was invented as a response to increasing concerns about the efficiency of the Bitcoin PoW consensus model, as well as its increasing centralization and conflict of interests between miners.  Peercoin keeps much of the core code from Bitcoin, though it fundamentally changes the consensus model as well as introducing a number of new protocol paradigms and economics, including breaking the deflationary model of Bitcoin in favor of a sane and accountable level of inflation.

The fee market is also a subject where Peercoin and Bitcoin differ. By moving to a fixed-fee model, the entire perspective of the blocksize limit and blockchain bandwidth is flipped upside down. While Bitcoin has a fee market by which miners (PoW block creators) are paid to process transactions so that the total supply can remain deflationary, in Peercoin the minters (PoS block creators) are always rewarded for their participation with a proportional amount of inflation.  As such, Peercoin is free to burn the transaction fees such that the virtual-revenue of a transaction is shared by the entire network. By looking at the bandwidth problem as a community rather than individual nodes, we adopt a fixed fee level of 0.01 PPC/KB that allows for long-term prediction of transaction fee costs. The entirety of Peercoin's blockchain is on the order of 1 GB, so blocksize limitations have never been tested. However, there is vast consensus in the community that if the blocksize approached the current limit, the limit would be lifted.

## Consensus algorithm

Peercoin is secured by Proof-of-Stake consensus. Proof-of-Work uses computational power as a scarce resource as a means of selecting the producer of a block, while Proof-of-Stake uses time continuously invested in the system measured in "coin age". Once an output to a transaction has reached an age of 30 days, the coins at this output become mature and are eligible for participation in the consensus process. Mature outputs are used as proof of having a stake in the system and are presented as evidence through the "coinstake" transaction of a new block. Each second of the timestamp is used as the nonce in the block hashing function to try to achieve the target difficulty. In conjunction with the number of coins, the probability of minting is proportional to the number of days since the 30 day mark with a maximum of 90 days, at which point the output has reached maximum maturity. Upon minting, the output will gain a block reward that is linearly related to the coinage, and the stake used to mint will be locked for 520 blocks (about 3 days). Minting can be done on almost any computer with the standard client installed, including compact computers like raspberry pi's, making the process objectively energy efficient when compared with computational hash-based proof algorithms. Simply put, Peercoin evens out the race between high and low power computers by limiting the number of hashes you can perform to 1 per second.

The Proof-of-Stake mechanism requires attackers to be monetarily invested in the system. They must undergo a good bit of opportunity cost as well as risking a large amount of stake in order to manipulate the consensus maliciously. In Proof-of-Work, any coordinated collection of powerful computers is a threat to the system. In Proof-of-Stake, any would-be attacker is conflicting with their own interests by attacking a system they are invested in. Beyond this base-level trust mechanism, giving the holders of the coins direct say over the protocol used to secure their stake generates more direct engagement between the the code and its users. The self-sufficiency of Peercoin is the ability to govern itself through an efficient consensus model that consolidates power in the hands of the users.

## Distribution and Block Rewards

Peercoin is created through the process of creating blocks, both PoW and PoS, and has no true upper limit on supply (the 'MAX_MONEY' variable in the code is only used as a precaution). PoW block rewards are used to create a fair initial distribution of coins in the network. The algorithm for PoW rewards is logarithmically decaying as the difficulty and computational power of the network increases. The trending development of SHA256 ASIC miners as the industry standard allows for efficient distribution that naturally eclipses as cryptocurrency gains widespread adoption.

Proof-of-Work reward formula is: `block_subsidy = 9999 / difficulty ^ (1/4)`

Proof-of-Work coin mint rate is a function of difficulty, for every 16x in difficulty mint rate is halved.

PoS rewards are given to those securing the network against attackers and are determined by a linear function with two components. The first dynamic portion results in 3% of the coins used to mint annually. The second static portion results in an additional 0.25% inflation of the coin supply distributed evenly amongst the blocks expected in a year, which approximately equals 1.25 ppc but scales with the size of the supply.

Proof-of-Stake reward formula is:
Proof-of-Stake coin mint rate is ~3-5% interest per year

At current network parameters, the inflation due to PoS is ~0.95%, while the inflation due to PoW is ~1.45%.  The total current annual inflation rate of ~2.4% is within the 1-3% window that is generally considered healthy for a currency or a broadly used unit of account.

## Burned and Fixed Fees
Peercoin's fees are fixed at 0.01 PPC per kB and are naturally burned with each transaction. The ease of provably burning coins is in contrast to many Proof-of-Work coins that recycle their transaction fees to miners in order to prepare for deflationary economies. Recycling fees back to block producers results in a 'fee market' that is inefficient and burdensome to the user experience. Peercon's economics allow for decentralized burning of a fixed fee when using the common resource of the Peercoin blockchain. As a result, block size limitations that plague other cryptocurrencies are not relevant to Peercoin. While the block size in Peercoin is set at 1 MB to protect against attacks, the community has been clear that higher blocksizes would be welcomed if the enhanced throughput were needed. As of writing, the Peercoin blockchain is very small (~1GB) and the fees are very low (~$0.005/txn), due in large part to the burned fixed-fee approach.

Peercoin block producers are motivated to include transactions in a block because the reduction in supply from burning fees increases the relative value of their stake. Proof-of-Work has inherent issues with this concept because every bit of computation resource is needed to find a block, so addition of transactions must be motivated by recycled fees. In Proof-of-Stake, the computation required in order to mint is minimal such that including transactions comes at practically no cost to the block producer.

## Block size limit and block time spacing

We will now compare Peercoin's network parameters directly with Bitcoin and Ethereum, which are vastly different blockchains.
Bitcoin features the 1MB block size limits which serves to place the upward pressure on the transaction fee price, Peercoin copies this parameter from the Bitcoin but it's economic model does not depend on scarcity of the block space.
While block generation is a stochastic process, each chain is targeted to generate blocks based on a real time interval. Bitcoin generates a block every 10 minutes, akin to Peercoin PoS block generation, while Ethereum generates a block every 12 seconds.  Peercoin PoW block generation is targeted at 1 hour, such that the total block time of Peercoin can be empirically estimated to be 8.57 minutes. Considering this and the block size limit of 1MB, Bitcoin has a transaction per second (TPS) of about 7 tps, Peercoin has an estimated 8 tps, and Ethereum has about 25 tps. However, it should be understood that Peercoin has never hit this transaction rate consistently, and the block size limit would very likely be raised if this were to happen.

<table>
<thead>
<tr>
<th>Features</th>
<th>Bitcoin</th>
<th>Peercoin</th>
<th>Ethereum</th>
</tr>
</thead>
<tbody>
<tr>
<td>Main use-case:</td>
<td>p2p financial transactions / store of value</td>
<td>p2p financial transactions / store of value</td>
<td>Turing complete smart contracts</td>
</tr>
<tr>
<td>Consensus algorithm:</td>
<td>PoW</td>
<td>PoS</td>
<td>PoW</td>
</tr>
<tr>
<td>Active since:</td>
<td>2009</td>
<td>2012</td>
<td>2015</td>
</tr>
</tr>
<tr>
<td>Distribution method:</td>
<td>PoW block reward</td>
<td>PoW block reward / PoS block reward</td>
<td>Initial Coin Offering / PoW block reward</td>
</tr>
<tr>
<td>Distribution:</td>
<td>Limited, until 21M tokens exist in the system.</td>
<td>Unlimited.</td>
<td>Unlimited.</td>
</tr>
</tr>
<tr>
<td>Transaction fee:</td>
<td>Fee market (~100 satoshis/byte, ~$20/txn)</td>
<td>Static (0.01 PPC/kb, ~$0.005/txn)</td>
<td>Fee market (~100 Gwei/byte, ~$20/txn)</td>
</tr>
<tr>
<td>Estimated transaction bandwidth:</td>
<td>7 tx/sec</td>
<td>8 tx/sec</td>
<td>25 tx/sec</td>
</tr>
<tr>
<td>Block time:</td>
<td>10 minutes</td>
<td>8.57 minutes</td>
<td>12 seconds</td>
</tr>
<tr>
<td>Block size:</td>
<td>1MB</td>
<td>1MB</td>
<td>Dynamic</td>
</tr>
<tr>
<td>Extra transaction data size limit:</td>
<td>80 Byte<br />(OP_RETURN)</td>
<td>256 Byte<br />(OP_RETURN)</td>
<td>Dynamic<br />(5 gas / byte)</td>
</tr>
<tr>
<td>Topology:</td>
<td>Public blockchain</td>
<td>Public blockchain</td>
<td>Public blockchain</td>
</tr>
</tbody>
</table>
Table 1. Comparison of Crypto currency attributes
(prices of transactions at the time of writing)

---
