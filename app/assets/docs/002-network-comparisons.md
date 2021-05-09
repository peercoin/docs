# Comparison with other blockchain networks

Historically, Peercoin originated as a fork of Bitcoin with added functionalities and protocol tuning to support Proof-of-Stake.  Peercoin was invented as a response to increasing concerns about the efficiency of the Bitcoin PoW consensus model, as well as its increasing centralization and conflict of interests between miners.  Peercoin keeps much of the core code from Bitcoin, though it fundamentally changes the consensus model as well as introducing a number of new protocol paradigms and economics, including breaking the deflationary model of Bitcoin in favor of a sane and accountable level of inflation.

The fee market is also a subject where Peercoin and Bitcoin differ. By moving to a fixed-fee model, the entire perspective of the blocksize limit and blockchain bandwidth is flipped upside down. While Bitcoin has a fee market by which miners (PoW block creators) are paid to process transactions so that the total supply can remain deflationary, in Peercoin the minters (PoS block creators) are always rewarded for their participation with a proportional amount of inflation.  As such, Peercoin is free to burn the transaction fees such that the virtual-revenue of a transaction is shared by the entire network. By looking at the bandwidth problem as a community rather than individual nodes, we adopt a fixed fee level of 0.01 PPC/KB that allows for long-term prediction of transaction fee costs. The entirety of Peercoin's blockchain is on the order of 1 GB, so blocksize limitations have never been tested. However, there is vast consensus in the community that if the blocksize approached the current limit, the limit would be lifted.

## Consensus algorithm

Peercoin is secured by Proof-of-Stake type of consensus. Proof-of-Work uses computational power as a scarce resource to verify transactions, while Proof-of-Stake uses time continuously invested in the system measured in "coin age". Once an output to a transaction has reached an age of thirty (30) days, the coins at this output become eligible for minting. Each second of time is used as the nonce in the block hashing function to try to achieve the target. **cite code** The probability of minting is also proportional to the number of days since the 30 day mark, with a maximum of ninety (90) days, at which point the output has reached maximum maturity. **cite code** Upon minting, the output will gain a block reward that is linearly related to the coinage, and the coins used to mint called the 'stake' will be locked for 520 blocks (about 3 days) **cite code** Minting can be done on almost any computer with the standard client installed, including compact computers like raspberry pi's, making the process objectively energy efficient when compared with computational hash-based proof algorithms. Simply put, Peercoin evens out the race between high and low power computers by limiting the number of hashes you can perform to 1 per second.

The Proof-of-Stake mechanism requires attachers to be monetarily invested in the system. They must undergo a good bit of opportunity cost as well as risking a large amount of stake in order to manipulate the consensus maliciously. In Proof-of-Work, any coordinated collection of powerful computers is a threat to the system. In Proof-of-Stake, any would-be attacker is conflicting with their own interests by attacking a system they are invested in. Beyond this base-level trust mechanism, giving the holders of the coins direct say over the protocol used to secure their stake generates more direct engagement between the the code and its users. The self-sufficiency of Peercoin is the ability to govern itself through an efficient consensus model that consolidates power in the hands of the users.

## Distribution and Block Rewards

Peercoin is created through the process of creating blocks, both PoW and PoS, and has no true upper limit on supply (the 'MAX_MONEY' variable in the code is only used as a precaution). PoW block rewards are used to create a fair initial distribution of coins in the network. The algorithm for PoW rewards is logarithmically decaying as the difficulty and computational power of the network increases. The trending development of SHA256 ASIC miners as the industry standard allows for efficient distribution that naturally eclipses as cryptocurrency gains widespread adoption.

**cite code** 
Proof-of-Work reward formula is:  `difficulty == (9999 / (mint per block)) ** 4`
Proof-of-Work coin mint rate is a function of difficulty, for every 16x in difficulty mint rate is halved.

PoS rewards are given to those securing the network against attackers and are determined by a linear function with two components. The first dynamic portion results in 3% of the coins used to mint annually. The second static portion results in an additional 0.25% inflation of the coin supply distributed evenly amongst the blocks expected in a year, which approximately equals 1.25 ppc but scales with the size of the supply.

**cite code**
Proof-of-Stake reward formula is:
Proof-of-Stake coin mint rate is ~3-5% interest per year

At current network parameters, the inflation due to PoS is ~1%, while the inflation due to PoW is ~1.75%.  The total current annual inflation rate of ~2.75% is within the 1-3% window that is generally considered healthy for a currency or a broadly used unit of account.

## Fee market
**I think we should remove this entire section and replace it with a bunch of citations you can use to look this stuff up**
**Maybe put in some code citations for the 1MB block and how easy it is to change the limit**


The fee market provides a mechanism to decide which transactions have priority over the others, and to create economic incentives for the transaction validators who usually claim the fees as rewards. Transaction fees are claimed by the block miner in both Bitcoin and Ethereum economic systems. This provides the miners the incentive to validate and include transactions in the blocks they mine. If Alice wants her transaction to be included in the next block, she should set transaction fee higher and pay more then other network users, ie. outbid them. It is presumed that miners, as rational subjects, will first include transactions which carry the most Bitcoin value. If Alice pays a transaction fee which is under the average fee at the time she might wait for several blocks (or hundreds of blocks) to see her transaction included and confirmed. So, it is obvious that the fee market serves as the incentive for miners to process and include the transactions in the blocks they mine.
With Bitcoin's block size limit set to 1MB there exists an artificial upward pressure on the price of transaction fees - incentivizing miners to validate the transactions. This is especially important as Bitcoin's economy is expected to run on transaction fees alone when the block subsidies eventually stop.

Peercoin's fees are fixed at 0.01 PPC per kb and are burned. This is equivalent to paying the transaction fee to each Peercoin holder in proportion to their Peercoin holdings since the fee decreases the total supply of Peercoins. This property eliminates the need for a fee market on Peercoin's network and allows every transaction to get included in the very next block. Peercoin retains the 1MB block size limit as it is based on the Bitcoin code, but it has no intricate need to keep it. The block size limit will definitely be increased as Peercoin's network grows in usage. Peercoin developers have already hinted that Peercoin will feature a dynamic block size in the near future.
Due to these economic properties of Peercoin a question arises: Why do Peercoin miners bother processing the transactions?

From a spectator looking at this from a Bitcoin oriented perspective the answer is that Peercoin block miners want to process transactions so they allow Peercoins to be burned - thus making their own stake in the network more valuable.
However when the intricacies of PoS are learned it is understood that with Peercoin minters (PoS miners) include transactions because it doesn't cost much to include them, while producing empty blocks reduces the value of the blockchain, and therefore of their stake. The burned fees are not really an argument as the effect on their holdings is negligible.
Bitcoin miners always start off mining an empty block, otherwise they lose the time it takes to validate the transactions and signatures, as time is money on the Bitcoin network. Only after they have validated the txns to include and have computed the merkle root, they start mining blocks with txns.
While for PoS, the time advantage is negligible as you can still use the stake hash of a few seconds ago. (hrobeers, 30.08.2017)

## Block size limit and block time spacing

**I actually think this section is somewhat diluded because we don't really believe in the 1 MB blocksize limit**

We will now compare Peercoin's network parameters directly with Bitcoin and Ethereum, which is another vastly different blockchain.
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
