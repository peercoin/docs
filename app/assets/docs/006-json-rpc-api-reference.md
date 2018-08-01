# JSON-RPC API reference

Peercoin daemon offers JSON-RPC interface which can be used to control the daemon or integrate it with software stack.
You can send commands to the daemon by using `peercoin-cli` tool.

There are two official wrappers for this interface, a PHP one and a Python2.7+ one.

> Peercoin_rpc is a simple and minimal library made for communication with peercoind via JSON-RPC protocol. It has a single dependency - a Python requests library and it supports both mainnet and testnet peercoin network with authentication or SSL encryption. There is a single class to be imported from the library - Client.

https://github.com/peercoin/peercoin_rpc

> peercoin-php-rpc is a simple and minimal library made for communication with peercoind via JSON-RPC protocol for PHP 7.1+. Easiest way to use is to use composer. Otherwise include RpcClient class in your project an you are good to go.

https://github.com/peercoin/peercoin-php-rpc

## List of JSON-RPC calls

| Command            | Parameters  | Description    | Requires unlocked wallet? (yes/no)  |
|--------------------|-------------|---------------------------------|--------------------|
| `getinfo`          |             |Returns an object containing various state info.|no|
| `getblock`         |  `hash`     |Returns information about the block with the given hash.|no|
| `getblockcount`    |             |Returns the number of blocks in the longest block chain.|no|
| `getblockhash`     |`block_num`  |Returns hash of block in best-block-chain at `block_num`; 0 is the genesis block|no|
| `gettransaction`   | `txid`        |Returns an object about the given transaction containing:<br>  "amount" : total amount of the transaction<br>"confirmations" : number of confirmations of the transaction<br>"txid" : the transaction ID<br>"time" : time associated with the transaction|no|
| `walletpassphrase` | `passphrase`   `timeout` |Stores the wallet decryption key in memory for `timeout` seconds.|no|
| `getbalance`       |[account] [minconf=1]|If [account] is not specified, returns the server's total available balance.<br>If [account] is specified, returns the balance in the account.|no|
| `getreceivedbyaddress`| `address` [minconf=1] |Returns the amount received by `address` in transactions with at least [minconf] confirmations. It correctly handles the case where someone has sent to the address in multiple transactions. Keep in mind that addresses are only ever used for receiving transactions.<br>Works only for addresses in the local wallet, external addresses will always show 0.|no|
| `getdifficulty`    |  |Returns proof-of-stake and proof-of-work difficulty|no|
| `getpeerinfo`      |  |Returns data about each connected node.|no|
| `getaddressesbyaccount`| `account` |Returns the list of addresses for the given account.|no|
| `getnewaddress`    | [account] |Returns a new address for receiving payments.<br>If [account] is specified payments received with the address will be credited to [account].|no|
| `getaccount`       | `address` |Returns the account associated with the given `address`.|no|
| `getaccountaddress`| `account` |Returns the current address for receiving payments to this account.<br>If `account` does not exist, it will be created along with an associated new address that will be returned.|no|
| `sendtoaddress`    | `address` `amount` [comment] [comment-to] |  `amount` is a real and is rounded to 6 decimal places. Returns the transaction ID `txid` if successful.|yes|
| `sendfrom`         | `fromaccount` `topeercoinaddress` `amount` [minconf=1] [comment] [comment-to] |`amount` is a real and is rounded to 6 decimal places. Will send the given amount to the given address, ensuring the account has a valid balance using [minconf] confirmations. Returns the transaction ID if successful (not in JSON object).|yes|
| `sendmany`         | `fromaccount` {address:amount,...} [minconf=1] [comment] |  amounts are double-precision floating point numbers |yes|
| `getconnectioncount`|    |Returns the number of connections to other nodes.|no|
| `getrawtransaction`|  `txid` [verbose=0] |Returns raw transaction representation for given transaction id.|no| 
| `getrawmempool`    |  |Returns all transaction ids in memory pool.|no|
| `listtransactions` | [account] [count=10] [from=0] | Returns up to [count] most recent transactions skipping the first [from] transactions for account [account]. If [account] not provided it'll return recent transactions from all accounts.|no|
| `listreceivedbyaddress`| [minconf=1] [includeempty=false] |Returns an array of objects containing:<br>"address" : receiving address<br>"account" : the account of the receiving address<br>"amount" : total amount received by the address<br>"confirmations" : number of confirmations of the most recent transaction included<br>To get a list of accounts on the system, execute `peercoin-cli listreceivedbyaddress 0 true`|no|
| `listreceivedbyaccount`| [minconf=1] [includeempty=false] |Returns an array of objects containing:<br>"account" : the account of the receiving addresses<br>"amount" : total amount received by addresses with this account<br>"confirmations" : number of confirmations of the most recent transaction included|no|
| `listaccounts` | [minconf=1] |Returns Object that has account names as keys, account balances as values.|no|
| `listunspent`  | [minconf=1] [maxconf=999999] |Returns array of unspent transaction inputs in the wallet.|no|
| `dumpprivkey`  | `address`   |Reveals the private key corresponding to `address`.|yes|
| `importprivkey`|  `privkey` [label] [rescan=true]|Adds a private key (as returned by dumpprivkey) to your wallet. This may take a while, as a rescan is done, looking for existing transactions.|yes|
| `createrawtransaction`| [{"txid":txid,"vout":n},...] {address:amount,...} |Creates a raw transaction spending given inputs.|no|
| `decoderawtransaction`| `hex_string` |Produces a human-readable JSON object for a raw transaction.|no|
| `signrawtransaction`  | `hex_string` [{"txid":txid,"vout":n,"scriptPubKey":hex},...] [`privatekey1`,...]|Adds signatures to a raw transaction and returns the resulting raw transaction.|yes|
| `signmessage`         | `address` `message` |Sign a message with the private key of an address.|yes|
| `verifymessage`       | `address` `signature` `message` |Verify a signed message.|no|
| `sendrawtransaction`  | `hex_string` |Submits raw transaction (serialized, hex-encoded) to local node and network.|no|
| `validateaddress`     | `address` |Return information about `address`.|no|
| `encryptwallet`       | `passphrase` |Encrypts the wallet with `passphrase`|no|
| `enforcecheckpoint`   | `bool` |`enforce` is true or false to enable or disable enforcement of broadcasted checkpoints by developer.|no|
| `keypoolrefill`       | `size` |Fills the key pool with new keys [default 100 new keys]|yes|