# Introduction to Peercoin

Hello, and welcome to the Peercoin Documentation website. We hope to help you understand more about this coin, its philosopy and technologies that runs behind it. Before getting too technical, we invite you to dive a little bit into the history of Peercoin, learning why it was created, and the purposes behind it.

## Peercoin Genesis: 2012

Since the creation of Bitcoin (Nakamoto 2008), proof-of-work has been the predominant design of peer-to-peer crypto currency. The concept of proof-of-work has been the backbone of minting and security model of Nakamoto’s design.

---

## Official client implementation

Once you install official Peercoin client from peercoin.net, you’ll have access to three executables: peercoind, peercoin-qt, and peercoin-cli.

### Peercoin-qt

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
