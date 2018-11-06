# Introduction to Peercoin

Hello, and welcome to the Peercoin Documentation website. We hope to help you understand more about this coin, its philosophy and technologies that runs behind it. Before getting too technical, we invite you to dive a little bit into the history of Peercoin, learning why it was created, and the purposes behind it.

## Peercoin Genesis: 2012

Since the creation of Bitcoin (Nakamoto 2008), Proof-of-Work has been the predominant design of peer-to-peer cryptocurrency. The concept of Proof-of-Work has been the backbone of mining and security model of Nakamoto’s design. In 2012, Sunny King and Scott Nadal proposed an alternative form of consensus that was both more secure, but also energy efficient.  Proof-of-Work, however is subject to centralized mining, large amounts of power consumption, and majority attacks.  Centralized mining comes about due to the increased profits and production from large scale mining operations.  Proof-of-Stake sought to provide sustainability and improved security through energy efficient staking and time-based confirmations (coin age).  Instead of electricity and computing power, time could be used as a verification method that would prevent many of the issues plaguing Proof-of-Work consensus.  Proof-of-Stake guards the blockchain, keeping users safe, while dynamic Proof-of-Work mining provides economic competition and maintains a balance in distribution.  Dynamic mining and staking allow for around 1% inflation a year, making it extremely practical for long term use.

Since its first block in 2012, Peercoin has remained one of the most energy effective, secure, and size effective blockchains in existence. Many projects have been created using Proof-of-Stake or derivatives, and all can be traced back to Peercoin's original model. Off-chain transactions are extremely compatible with Proof-of-Stake, meaning future developments and scaling will be easy to develop and deploy with Peercoin.

---

## Official client implementation

Once you install official Peercoin client from peercoin.net, you’ll have access to three executables: peercoind, peercoin-qt, and peercoin-cli.

### [Peercoin-qt](003-peercoin-core-wallet.md)

`peercoin-qt` provides a combination full Peercoin network client and wallet. Peercoin-qt is highly portable application written in QT5 framework.
From the Help menu, you can access a console where you can enter the RPC commands so power-user features are still available.

### peercoind

`peercoind` provides a full peer which you can interact with through JSON-RPC interface on port 9904 (902 for testnet).

For more information on how to use the JSON-RPC interface see the [json-rcp-api-reference article](./006-json-rpc-api-reference.md)

### peercoin-cli

`peercoin-cli` allows you to send JSON-RPC commands to running instance of `peercoind` from the command line.
For example:
> peercoin-cli help

> peercoin-cli getinfo

All three programs get settings from peercoin.conf in the Peercoin application directory:

> Windows: %APPDATA%\Peercoin\

> OSX: $HOME/Library/Application Support/PPCoin/

>Linux: $HOME/.peercoin/

To use `peercoind` and `peercoin-cli`, you will need to add a RPC password to your peercoin.conf file. Both programs will read from the same file if both run on the same system as the same user, so any long random password will work:

> rpcpassword=change_this_to_a_long_random_password

You should also make the peercoin.conf file only readable to its owner.
On Linux, Mac OSX, and other Unix-like systems, this can be accomplished by running the following command in the Peercoin application directory:

> chmod 0600 peercoin.conf

##  Unofficial client implementations

### Coinomi

https://www.coinomi.com/

### Coinspot

https://www.coinspot.com.au

### CoinVault

https://www.coinvault.io/

### Cryptonator

https://www.cryptonator.com/

### HolyTransaction

https://holytransaction.com/

### Ledger

https://www.ledger.com/

### Magnum

Airdrop focused wallet

https://magnumwallet.co

### UberPay

http://uberpay.io/
