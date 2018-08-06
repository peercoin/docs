# Bootstrapping

## What is it?

> In computer technology the term (usually shortened to booting) usually
> refers to the process of loading the basic software into the memory of
> a computer after power-on or general reset, especially the operating
> system which will then take care of loading other software as needed.<sup>[9.1](#footnote-9.1)</sup>

For Peercoin it means loading all of the block chain history from a special
file containing a snapshot of block data.

This special file, named `bootstrap.dat`, allows the Peercoin client to
sync from your hard drive instead of the internet. Using a
`bootstrap.dat` file is faster and reduces stress on the Peercoin network to sync new nodes.

## How do I make a `bootstrap.dat`?

Any synced client has the ability to make a `bootstrap.dat` file. Assuming
you're running linux you can do the following to manufacture your own.

First, shutdown your client. Allow it to cleanly exit so we know the block
data is settled.

Now, navigate to the directory `~/.peercoin/blocks` in your terminal and
notice the files named `blk00000.dat`, `blk00001.dat`, `blk00002.dat`, etc.
These are the raw block data files that can be combined to form the
`bootstrap.dat`!

The command `cat blk*.dat > bootstrap.dat` will produce the `bootstrap.dat`.
The file is often then compressed (zip'ed, tar/gzip'ed) and shared.

## How do I use a `bootstrap.dat`?

Assuming you're on linux and you haven't started the Peercoin client yet.

Make the directory `~/.peercoin` if it doesn't exist and then move the
`bootstrap.dat` into the `~/.peercoin` directory.

Start the Peercoin client. You should see the status `Importing blocks from disk...` if the client has found the `bootstrap.dat` and is using it to
sync the block chain.

## Where can I download a `booststrap.dat`?

We've put some recent copies on our file server :)

* Mainnet, zip file: [bootstrap.dat.zip](https://files.peercoin.net/download/peercoin_mainnet_2018_08_06_bootstrap.dat.zip)
* Mainnet, tar/gzip file: [bootstrap.dat.tar.gz](https://files.peercoin.net/download/peercoin_mainnet_2018_08_06_bootstrap.dat.tar.gz)
* Testnet, zip file: [bootstrap.dat.zip](https://files.peercoin.net/download/peercoin_testnet_2018_08_06_bootstrap.dat.zip)
* Testnet, tar/gzip file: [bootstrap.dat.tar.gz](https://files.peercoin.net/download/peercoin_testnet_2018_08_06_bootstrap.dat.tar.gz)

## Footnotes

<a id="footnote-9.1">9.1</a>: https://en.wikipedia.org/wiki/Bootstrapping
