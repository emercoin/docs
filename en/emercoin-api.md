<div class="boxOverflow">
	<img src="/images/Gui-debug-console.png" alt="The debug console in the emercoin-qt GUI" width="512">
</div>

# Emercoin API

As with <a target="_blank" rel="nofollow" href="https://en.bitcoin.it/wiki/Running_Bitcoin">Bitcoin</a>, Application programming interface (API) is available via:

-   the "debug console" in [Emercoin Core GUI](/en/install-software/core-wallets/gui-wallet.md).
-   <a target="_blank" rel="nofollow" href="https://en.bitcoin.it/wiki/API_reference_%28JSON-RPC%29">JSONRPC</a>, per settings in your <b>emercoin.conf</b>.
-   Directly on the command line interface (emercoin-cli).

API commands
------------

The API allows you or applications to query the blockchain and send transactions, etc. For example, to check on your EMC balance and status of the blockchain you type: 

	$ emc getinfo
	
Or to get a list of all possible commands:	

	$ emc help

The following API commands are accurate as of Emercoin Core version <b>v0.6.3</b>:


```text
== Blockchain ==
getbestblockhash
getblock "blockhash" ( verbose )
getblockchaininfo
getblockcount
getblockhash height
getblockheader "hash" ( verbose )
getchaintips
getdifficulty
getmempoolancestors txid (verbose)
getmempooldescendants txid (verbose)
getmempoolentry txid
getmempoolinfo
getrawmempool ( verbose )
gettxlistfor <fromblock> <toblock> <address> [type=0] [verbose=0]
gettxout "txid" n ( include_mempool )
gettxoutproof ["txid",...] ( blockhash )
gettxoutsetinfo
name_filter [regexp] [maxage=0] [from=0] [nb=0] [stat] [valuetype]
name_history <name> [fullhistory] [valuetype]
name_mempool [valuetype]
name_scan [start-name] [max-returned] [max-value-length=0] [valuetype]
name_scan_address <address> [max-value-length=0] [valuetype]
name_show <name> [valuetype] [filepath]
preciousblock "blockhash"
verifychain ( checklevel nblocks )
verifytxoutproof "proof"

== Control ==
getinfo
getmemoryinfo
help ( "command" )
stop

== Generating ==
generate nblocks ( maxtries )
generatetoaddress nblocks address (maxtries)
getgenerate
setgenerate generate ( genproclimit )

== Mining ==
getauxblock [<hash> <auxpow>]
getblocktemplate ( TemplateRequest )
getmininginfo
getnetworkhashps ( nblocks height )
prioritisetransaction <txid> <priority delta> <fee delta>
submitblock "hexdata" ( "jsonparametersobject" )

== Network ==
addnode "node" "add|remove|onetry"
clearbanned
disconnectnode "address" 
getaddednodeinfo ( "node" )
getcheckpoint
getconnectioncount
getnettotals
getnetworkinfo
getpeerinfo
listbanned
ping
setban "subnet" "add|remove" (bantime) (absolute)
setnetworkactive true|false

== Rawtransactions ==
createrawtransaction [{"txid":"id","vout":n},...] {"address":amount,"data":"hex",...} ( locktime )
decoderawtransaction "hexstring"
decodescript "hexstring"
fundrawtransaction "hexstring" ( options )
getrawtransaction "txid" ( verbose )
sendrawtransaction "hexstring" ( allowhighfees )
signrawtransaction "hexstring" ( [{"txid":"id","vout":n,"scriptPubKey":"hex","redeemScript":"hex"},...] ["privatekey1",...] sighashtype )

== Util ==
createmultisig nrequired ["key",...]
estimatefee nblocks
estimatepriority nblocks
estimatesmartpriority nblocks
signmessagewithprivkey "privkey" "message"
validateaddress "emercoinaddress"
verifymessage "address" "signature" "message"

== Wallet ==
abandontransaction "txid"
addmultisigaddress nrequired ["key",...] ( "account" )
addwitnessaddress "address"
backupwallet "destination"
bumpfee "txid" ( options ) 
dumpprivkey "address"
dumpwallet "filename"
encryptwallet "passphrase"
getaccount "address"
getaccountaddress "account"
getaddressesbyaccount "account"
getbalance ( "account" minconf include_watchonly )
getnewaddress ( "account" )
getrawchangeaddress
getreceivedbyaccount "account" ( minconf )
getreceivedbyaddress "address" ( minconf )
gettransaction "txid" ( include_watchonly )
getunconfirmedbalance
getwalletinfo
importaddress "address" ( "label" rescan p2sh )
importmulti "requests" "options"
importprivkey "emercoinprivkey" ( "label" ) ( rescan )
importprunedfunds
importpubkey "pubkey" ( "label" rescan )
importwallet "filename"
keypoolrefill ( newsize )
listaccounts ( minconf include_watchonly)
listaddressgroupings
listlockunspent
listreceivedbyaccount ( minconf include_empty include_watchonly)
listreceivedbyaddress ( minconf include_empty include_watchonly)
listsinceblock ( "blockhash" target_confirmations include_watchonly)
listtransactions ( "account" count skip include_watchonly)
listunspent ( minconf maxconf  ["addresses",...] [include_unsafe] )
lockunspent unlock ([{"txid":"txid","vout":n},...])
makekeypair [prefix]
move "fromaccount" "toaccount" amount ( minconf "comment" )
name_delete <name>
name_list [name] [valuetype]
name_new <name> <value> <days> [toaddress] [valuetype]
name_update <name> <value> <days> [toaddress] [valuetype]
removeprunedfunds "txid"
reservebalance [<reserve> [amount]]
sendfrom "fromaccount" "toaddress" amount ( minconf "comment" "comment_to" )
sendmany "fromaccount" {"address":amount,...} ( minconf "comment" ["address",...] )
sendtoaddress "address" amount ( "comment" "comment_to" subtractfeefromamount )
sendtoname <name> <amount> [comment] [comment-to]
setaccount "address" "account"
settxfee amount
signmessage "address" "message"
```

<b><h3>== Blockchain ==</h3></b>

<b>`getbestblockhash`</b>

```
Returns the hash of the best (tip) block in the longest blockchain.

Result:
"hex" (string) the block hash hex encoded

Examples:
> emercoin-cli getbestblockhash
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getbestblockhash", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getblock "blockhash" ( verbose )`</b>

```
If verbose is false, returns a string that is serialized, hex-encoded data for block 'hash'.
If verbose is true, returns an Object with information about block <hash>.

Arguments:
1. "blockhash" (string, required) The block hash
2. verbose (boolean, optional, default=true) true for a json object, false for the hex encoded data

Result (for verbose = true):
{
"hash" : "hash", (string) the block hash (same as provided)
"confirmations" : n, (numeric) The number of confirmations, or -1 if the block is not on the main chain
"size" : n, (numeric) The block size
"strippedsize" : n, (numeric) The block size excluding witness data
"weight" : n (numeric) The block weight as defined in BIP 141
"height" : n, (numeric) The block height or index
"version" : n, (numeric) The block version
"versionHex" : "00000000", (string) The block version formatted in hexadecimal
"merkleroot" : "xxxx", (string) The merkle root
"tx" : [ (array of string) The transaction ids
"transactionid" (string) The transaction id
,...
],
"time" : ttt, (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
"mediantime" : ttt, (numeric) The median block time in seconds since epoch (Jan 1 1970 GMT)
"nonce" : n, (numeric) The nonce
"bits" : "1d00ffff", (string) The bits
"difficulty" : x.xxx, (numeric) The difficulty
"chainwork" : "xxxx", (string) Expected number of hashes required to produce the chain up to this block (in hex)
"previousblockhash" : "hash", (string) The hash of the previous block
"nextblockhash" : "hash" (string) The hash of the next block
}

Result (for verbose=false):
"data" (string) A string that is serialized, hex-encoded data for block 'hash'.

Examples:
> emercoin-cli getblock "00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblock", "params": ["00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getblockchaininfo`</b>

```
Returns an object containing various state info regarding blockchain processing.

Result:
{
"chain": "xxxx", (string) current network name as defined in BIP70 (main, test, regtest)
"blocks": xxxxxx, (numeric) the current number of blocks processed in the server
"headers": xxxxxx, (numeric) the current number of headers we have validated
"bestblockhash": "...", (string) the hash of the currently best block
"difficulty": xxxxxx, (numeric) the current difficulty
"mediantime": xxxxxx, (numeric) median time for the current best block
"verificationprogress": xxxx, (numeric) estimate of verification progress [0..1]
"chainwork": "xxxx" (string) total amount of work in active chain, in hexadecimal
"pruned": xx, (boolean) if the blocks are subject to pruning
"pruneheight": xxxxxx, (numeric) lowest-height complete block stored
"softforks": [ (array) status of softforks in progress
{
"id": "xxxx", (string) name of softfork
"version": xx, (numeric) block version
"reject": { (object) progress toward rejecting pre-softfork blocks
"status": xx, (boolean) true if threshold reached
},
}, ...
],
}

Examples:
> emercoin-cli getblockchaininfo
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockchaininfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getblockcount`</b>

```
Returns the number of blocks in the longest blockchain.

Result:
n (numeric) The current block count

Examples:
> emercoin-cli getblockcount
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockcount", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getblockhash height`</b>

```
Returns hash of block in best-block-chain at height provided.

Arguments:
1. height (numeric, required) The height index

Result:
"hash" (string) The block hash

Examples:
> emercoin-cli getblockhash 1000
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockhash", "params": [1000] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getblockheader "hash" ( verbose )`</b>

```
If verbose is false, returns a string that is serialized, hex-encoded data for blockheader 'hash'.
If verbose is true, returns an Object with information about blockheader <hash>.

Arguments:
1. "hash" (string, required) The block hash
2. verbose (boolean, optional, default=true) true for a json object, false for the hex encoded data

Result (for verbose = true):
{
"hash" : "hash", (string) the block hash (same as provided)
"confirmations" : n, (numeric) The number of confirmations, or -1 if the block is not on the main chain
"height" : n, (numeric) The block height or index
"version" : n, (numeric) The block version
"versionHex" : "00000000", (string) The block version formatted in hexadecimal
"merkleroot" : "xxxx", (string) The merkle root
"time" : ttt, (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
"mediantime" : ttt, (numeric) The median block time in seconds since epoch (Jan 1 1970 GMT)
"nonce" : n, (numeric) The nonce
"bits" : "1d00ffff", (string) The bits
"difficulty" : x.xxx, (numeric) The difficulty
"chainwork" : "0000...1f3" (string) Expected number of hashes required to produce the current chain (in hex)
"previousblockhash" : "hash", (string) The hash of the previous block
"nextblockhash" : "hash", (string) The hash of the next block
}

Result (for verbose=false):
"data" (string) A string that is serialized, hex-encoded data for block 'hash'.

Examples:
> emercoin-cli getblockheader "00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockheader", "params": ["00000000c937983704a73af28acdec37b049d214adbda81d7e2a3dd146f6ed09"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getchaintips`</b>

```
Return information about all known tips in the block tree, including the main chain as well as orphaned branches.

Result:
[
  {
    "height": xxxx,         (numeric) height of the chain tip
    "hash": "xxxx",         (string) block hash of the tip
    "branchlen": 0          (numeric) zero for main chain
    "status": "active"      (string) "active" for the main chain
  },
  {
    "height": xxxx,
    "hash": "xxxx",
    "branchlen": 1          (numeric) length of branch connecting the tip to the main chain
    "status": "xxxx"        (string) status of the chain (active, valid-fork, valid-headers, headers-only, invalid)
  }
]
Possible values for status:
1.  "invalid"               This branch contains at least one invalid block
2.  "headers-only"          Not all blocks for this branch are available, but the headers are valid
3.  "valid-headers"         All blocks are available for this branch, but they were never fully validated
4.  "valid-fork"            This branch is not part of the active chain, but is fully validated
5.  "active"                This is the tip of the active main chain, which is certainly valid

Examples:
> emercoin-cli getchaintips 
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getchaintips", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getdifficulty`</b>

```
Returns the proof-of-work difficulty as a multiple of the minimum difficulty.

Result:
n.nnn (numeric) the proof-of-work difficulty as a multiple of the minimum difficulty.

Examples:
> emercoin-cli getdifficulty
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getdifficulty", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getmempoolancestors txid (verbose)`</b>

```
If txid is in the mempool, returns all in-mempool ancestors.

Arguments:
1. "txid" (string, required) The transaction id (must be in mempool)
2. verbose (boolean, optional, default=false) True for a json object, false for array of transaction ids

Result (for verbose=false):
[ (json array of strings)
"transactionid" (string) The transaction id of an in-mempool ancestor transaction
,...
]

Result (for verbose=true):
{ (json object)
"transactionid" : { (json object)
"size" : n, (numeric) virtual transaction size as defined in BIP 141. This is different from actual serialized size for witness transactions as witness data is discounted.
"fee" : n, (numeric) transaction fee in EMC
"modifiedfee" : n, (numeric) transaction fee with fee deltas used for mining priority
"time" : n, (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
"height" : n, (numeric) block height when transaction entered pool
"startingpriority" : n, (numeric) DEPRECATED. Priority when transaction entered pool
"currentpriority" : n, (numeric) DEPRECATED. Transaction priority now
"descendantcount" : n, (numeric) number of in-mempool descendant transactions (including this one)
"descendantsize" : n, (numeric) virtual transaction size of in-mempool descendants (including this one)
"descendantfees" : n, (numeric) modified fees (see above) of in-mempool descendants (including this one)
"ancestorcount" : n, (numeric) number of in-mempool ancestor transactions (including this one)
"ancestorsize" : n, (numeric) virtual transaction size of in-mempool ancestors (including this one)
"ancestorfees" : n, (numeric) modified fees (see above) of in-mempool ancestors (including this one)
"depends" : [ (array) unconfirmed transactions used as inputs for this transaction
"transactionid", (string) parent transaction id
... ]
}, ...
}

Examples:
> emercoin-cli getmempoolancestors "mytxid"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempoolancestors", "params": ["mytxid"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getmempooldescendants txid (verbose)`</b>

```
If txid is in the mempool, returns all in-mempool descendants.

Arguments:
1. "txid" (string, required) The transaction id (must be in mempool)
2. verbose (boolean, optional, default=false) True for a json object, false for array of transaction ids

Result (for verbose=false):
[ (json array of strings)
"transactionid" (string) The transaction id of an in-mempool descendant transaction
,...
]

Result (for verbose=true):
{ (json object)
"transactionid" : { (json object)
"size" : n, (numeric) virtual transaction size as defined in BIP 141. This is different from actual serialized size for witness transactions as witness data is discounted.
"fee" : n, (numeric) transaction fee in EMC
"modifiedfee" : n, (numeric) transaction fee with fee deltas used for mining priority
"time" : n, (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
"height" : n, (numeric) block height when transaction entered pool
"startingpriority" : n, (numeric) DEPRECATED. Priority when transaction entered pool
"currentpriority" : n, (numeric) DEPRECATED. Transaction priority now
"descendantcount" : n, (numeric) number of in-mempool descendant transactions (including this one)
"descendantsize" : n, (numeric) virtual transaction size of in-mempool descendants (including this one)
"descendantfees" : n, (numeric) modified fees (see above) of in-mempool descendants (including this one)
"ancestorcount" : n, (numeric) number of in-mempool ancestor transactions (including this one)
"ancestorsize" : n, (numeric) virtual transaction size of in-mempool ancestors (including this one)
"ancestorfees" : n, (numeric) modified fees (see above) of in-mempool ancestors (including this one)
"depends" : [ (array) unconfirmed transactions used as inputs for this transaction
"transactionid", (string) parent transaction id
... ]
}, ...
}

Examples:
> emercoin-cli getmempooldescendants "mytxid"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempooldescendants", "params": ["mytxid"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getmempoolentry txid`</b>

```
Returns mempool data for given transaction

Arguments:
1. "txid" (string, required) The transaction id (must be in mempool)

Result:
{ (json object)
"size" : n, (numeric) virtual transaction size as defined in BIP 141. This is different from actual serialized size for witness transactions as witness data is discounted.
"fee" : n, (numeric) transaction fee in EMC
"modifiedfee" : n, (numeric) transaction fee with fee deltas used for mining priority
"time" : n, (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
"height" : n, (numeric) block height when transaction entered pool
"startingpriority" : n, (numeric) DEPRECATED. Priority when transaction entered pool
"currentpriority" : n, (numeric) DEPRECATED. Transaction priority now
"descendantcount" : n, (numeric) number of in-mempool descendant transactions (including this one)
"descendantsize" : n, (numeric) virtual transaction size of in-mempool descendants (including this one)
"descendantfees" : n, (numeric) modified fees (see above) of in-mempool descendants (including this one)
"ancestorcount" : n, (numeric) number of in-mempool ancestor transactions (including this one)
"ancestorsize" : n, (numeric) virtual transaction size of in-mempool ancestors (including this one)
"ancestorfees" : n, (numeric) modified fees (see above) of in-mempool ancestors (including this one)
"depends" : [ (array) unconfirmed transactions used as inputs for this transaction
"transactionid", (string) parent transaction id
... ]
}

Examples:
> emercoin-cli getmempoolentry "mytxid"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempoolentry", "params": ["mytxid"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getmempoolinfo`</b>

```
Returns details on the active state of the TX memory pool.

Result:
{
"size": xxxxx, (numeric) Current tx count
"bytes": xxxxx, (numeric) Sum of all virtual transaction sizes as defined in BIP 141. Differs from actual serialized size because witness data is discounted
"usage": xxxxx, (numeric) Total memory usage for the mempool
"maxmempool": xxxxx, (numeric) Maximum memory usage for the mempool
"mempoolminfee": xxxxx (numeric) Minimum fee for tx to be accepted
}

Examples:
> emercoin-cli getmempoolinfo
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmempoolinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getrawmempool ( verbose )`</b>

```
Returns all transaction ids in memory pool as a json array of string transaction ids.

Arguments:
1. verbose (boolean, optional, default=false) True for a json object, false for array of transaction ids

Result: (for verbose = false):
[ (json array of string)
"transactionid" (string) The transaction id
,...
]

Result: (for verbose = true):
{ (json object)
"transactionid" : { (json object)
"size" : n, (numeric) virtual transaction size as defined in BIP 141. This is different from actual serialized size for witness transactions as witness data is discounted.
"fee" : n, (numeric) transaction fee in EMC
"modifiedfee" : n, (numeric) transaction fee with fee deltas used for mining priority
"time" : n, (numeric) local time transaction entered pool in seconds since 1 Jan 1970 GMT
"height" : n, (numeric) block height when transaction entered pool
"startingpriority" : n, (numeric) DEPRECATED. Priority when transaction entered pool
"currentpriority" : n, (numeric) DEPRECATED. Transaction priority now
"descendantcount" : n, (numeric) number of in-mempool descendant transactions (including this one)
"descendantsize" : n, (numeric) virtual transaction size of in-mempool descendants (including this one)
"descendantfees" : n, (numeric) modified fees (see above) of in-mempool descendants (including this one)
"ancestorcount" : n, (numeric) number of in-mempool ancestor transactions (including this one)
"ancestorsize" : n, (numeric) virtual transaction size of in-mempool ancestors (including this one)
"ancestorfees" : n, (numeric) modified fees (see above) of in-mempool ancestors (including this one)
"depends" : [ (array) unconfirmed transactions used as inputs for this transaction
"transactionid", (string) parent transaction id
... ]
}, ...
}

Examples:
> emercoin-cli getrawmempool true
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawmempool", "params": [true] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`gettxlistfor <fromblock> <toblock> <address> [type=0] [verbose=0]`</b>

```
[type]: 0 - sent/received, 1 - received, 2 - sent
[verbose]: 0 - false, 1 - true
```

<b>`gettxout "txid" n ( include_mempool )`</b>

```
Returns details about an unspent transaction output.

Arguments:
1. "txid" (string, required) The transaction id
2. n (numeric, required) vout number
3. include_mempool (boolean, optional) Whether to include the mempool

Result:
{
"bestblock" : "hash", (string) the block hash
"confirmations" : n, (numeric) The number of confirmations
"value" : x.xxx, (numeric) The transaction value in EMC
"scriptPubKey" : { (json object)
"asm" : "code", (string)
"hex" : "hex", (string)
"reqSigs" : n, (numeric) Number of required signatures
"type" : "pubkeyhash", (string) The type, eg pubkeyhash
"addresses" : [ (array of string) array of emercoin addresses
"address" (string) emercoin address
,...
]
},
"version" : n, (numeric) The version
"coinbase" : true|false (boolean) Coinbase or not
}

Examples:

Get unspent transactions
> emercoin-cli listunspent

View the details
> emercoin-cli gettxout "txid" 1

As a json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettxout", "params": ["txid", 1] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`gettxoutproof ["txid",...] ( blockhash )`</b>

```
Returns a hex-encoded proof that "txid" was included in a block.

NOTE: By default this function only works sometimes. This is when there is an
unspent output in the utxo for this transaction. To make it always work,
you need to maintain a transaction index, using the -txindex command line option or
specify the block in which the transaction is included manually (by blockhash).

Arguments:
1. "txids" (string) A json array of txids to filter
[
"txid" (string) A transaction hash
,...
]
2. "blockhash" (string, optional) If specified, looks for txid in the block with this hash

Result:
"data" (string) A string that is a serialized, hex-encoded data for the proof.
```

<b>`gettxoutsetinfo`</b>

```
Returns statistics about the unspent transaction output set.
Note this call may take some time.

Result:
{
"height":n, (numeric) The current block height (index)
"bestblock": "hex", (string) the best block hash hex
"transactions": n, (numeric) The number of transactions
"txouts": n, (numeric) The number of output transactions
"bytes_serialized": n, (numeric) The serialized size
"hash_serialized": "hash", (string) The serialized hash
"total_amount": x.xxx (numeric) The total amount
}

Examples:
> emercoin-cli gettxoutsetinfo
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettxoutsetinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`name_filter [regexp] [maxage=0] [from=0] [nb=0] [stat] [valuetype]`</b>

```
scan and filter names
[regexp] : apply [regexp] on names, empty means all names
[maxage] : look in last [maxage] blocks
[from] : show results from number [from]
[nb] : show [nb] results, 0 means all
[stat] : show some stats instead of results
[valuetype] : if "hex" or "base64" is specified then it will print value in corresponding format instead of string.
name_filter "" 5 # list names updated in last 5 blocks
name_filter "^id/" # list all names from the "id" namespace
name_filter "^id/" 0 0 0 stat # display stats (number of names) on active names from the "id" namespace
```

<b>`name_history <name> [fullhistory] [valuetype]`</b>

```
Look up the current and all past data for the given name.

Arguments:
1. name (string, required) the name to query for
2. fullhistory (boolean, optional) shows full history, even if name is not active
3. valuetype (string, optional) If "hex" or "base64" is specified then it will print value in corresponding format instead of string.

Result:
[
{
"txid": "xxxx", (string) transaction id "time": xxxxx, (numeric) transaction time "height": xxxxx, (numeric) height of block with this transaction "address": "xxxx", (string) address to which transaction was sent "address_is_mine": "xxxx", (string) shows "true" if this is your address, otherwise not visible "operation": "xxxx", (string) name operation that was performed in this transaction "days_added": xxxx, (numeric) days added (1 day = 175 blocks) to name expiration time, not visible if 0 "value": xxxx, (numeric) name value in this transaction; not visible when name_delete was used }
]

Examples:
> emercoin-cli name_history "myname"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "name_history", "params": ["myname"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`name_mempool [valuetype]`</b>

```
Arguments:
1. valuetype (string, optional) If "hex" or "base64" is specified then it will print value in corresponding format instead of string.

List pending name transactions in mempool.

Result:
[
{
"name": "xxxx", (string) name "txid": "xxxx", (string) transaction id "time": xxxxx, (numeric) transaction time "address": "xxxx", (string) address to which transaction was sent "address_is_mine": "xxxx", (string) shows "true" if this is your address, otherwise not visible "operation": "xxxx", (string) name operation that was performed in this transaction "days_added": xxxx, (numeric) days added (1 day = 175 blocks) to name expiration time, not visible if 0 "value": xxxx, (numeric) name value in this transaction; not visible when name_delete was used }
]

Examples:
> emercoin-cli name_mempool
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "name_mempool", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`name_scan [start-name] [max-returned] [max-value-length=0] [valuetype]`</b>

```
Scan all names, starting at [start-name] and returning [max-returned] number of entries (default 500)
[max-value-length] : control how much of value is shown (0 = full value)
[valuetype] : if "hex" or "base64" is specified then it will print value in corresponding format instead of a string.
```

<b>`name_scan_address <address> [max-value-length=0] [valuetype]`</b>

```
Print names that belong to specific address
[max-value-length] : control how much of name value is shown (0 = full value)
[valuetype] : if "hex" or "base64" is specified then it will print value in corresponding format instead of a string.
```

<b>`name_show <name> [valuetype] [filepath]`</b>

```
Show values of a name.

Arguments:
1. name (string, required).
2. valuetype (string, optional) If "hex" or "base64" is specified then it will print value in corresponding format instead of string.
3. filepath (string, optional) save name value in binary format in specified file (file will be overwritten!).
```

<b>`preciousblock "blockhash"`</b>

```
Treats a block as if it were received before others with the same work.

A later preciousblock call can override the effect of an earlier one.

The effects of preciousblock are not retained across restarts.

Arguments:
1. "blockhash" (string, required) the hash of the block to mark as precious

Result:

Examples:
> emercoin-cli preciousblock "blockhash"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "preciousblock", "params": ["blockhash"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`verifychain ( checklevel nblocks )`</b>

```
Verifies blockchain database.

Arguments:
1. checklevel (numeric, optional, 0-4, default=3) How thorough the block verification is.
2. nblocks (numeric, optional, default=6, 0=all) The number of blocks to check.

Result:
true|false (boolean) Verified or not

Examples:
> emercoin-cli verifychain
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "verifychain", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`verifytxoutproof "proof"`</b>

```
Verifies that a proof points to a transaction in a block, returning the transaction it commits to
and throwing an RPC error if the block is not in our best chain

Arguments:
1. "proof" (string, required) The hex-encoded proof generated by gettxoutproof

Result:
["txid"] (array, strings) The txid(s) which the proof commits to, or empty array if the proof is invalid
```

<b><h3>== Control ==</h3></b>

<b>`getinfo`</b>

```
DEPRECATED. Returns an object containing various state info.

Result:
{
"version": xxxxx, (numeric) the server version
"protocolversion": xxxxx, (numeric) the protocol version
"walletversion": xxxxx, (numeric) the wallet version
"balance": xxxxxxx, (numeric) the total emercoin balance of the wallet
"blocks": xxxxxx, (numeric) the current number of blocks processed in the server
"timeoffset": xxxxx, (numeric) the time offset
"connections": xxxxx, (numeric) the number of connections
"proxy": "host:port", (string, optional) the proxy used by the server
"difficulty": xxxxxx, (numeric) the current difficulty
"testnet": true|false, (boolean) if the server is using testnet or not
"keypoololdest": xxxxxx, (numeric) the timestamp (seconds since Unix epoch) of the oldest pre-generated key in the key pool
"keypoolsize": xxxx, (numeric) how many new keys are pre-generated
"unlocked_until": ttt, (numeric) the timestamp in seconds since epoch (midnight Jan 1 1970 GMT) that the wallet is unlocked for transfers, or 0 if the wallet is locked
"paytxfee": x.xxxx, (numeric) the transaction fee set in EMC/kB
"relayfee": x.xxxx, (numeric) minimum relay fee for non-free transactions in EMC/kB
"errors": "..." (string) any error messages
}

Examples:
> emercoin-cli getinfo
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getmemoryinfo`</b>

```
Returns an object containing information about memory usage.

Result:
{
"locked": { (json object) Information about locked memory manager
"used": xxxxx, (numeric) Number of bytes used
"free": xxxxx, (numeric) Number of bytes available in current arenas
"total": xxxxxxx, (numeric) Total number of bytes managed
"locked": xxxxxx, (numeric) Amount of bytes that succeeded locking. If this number is smaller than total, locking pages failed at some point and key data could be swapped to disk.
"chunks_used": xxxxx, (numeric) Number allocated chunks
"chunks_free": xxxxx, (numeric) Number unused chunks
}
}

Examples:
> emercoin-cli getmemoryinfo
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmemoryinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`help ( "command" )`</b>

```
List all commands, or get help for a specified command.

Arguments:
1. "command" (string, optional) The command to get help on

Result:
"text" (string) The help text
```

<b>`stop`</b>

```
Stop Emercoin server.
```

<b><h3>== Generating ==</h3></b>

<b>`generate nblocks ( maxtries )`</b>

```
Mine up to nblocks blocks immediately (before the RPC call returns)

Arguments:
1. nblocks (numeric, required) How many blocks are generated immediately.
2. maxtries (numeric, optional) How many iterations to try (default = 1000000).

Result:
[ blockhashes ] (array) hashes of blocks generated

Examples:

Generate 11 blocks
> emercoin-cli generate 11
```

<b>`generatetoaddress nblocks address (maxtries)`</b>

```
Mine blocks immediately to a specified address (before the RPC call returns)

Arguments:
1. nblocks (numeric, required) How many blocks are generated immediately.
2. address (string, required) The address to send the newly generated emercoin to.
3. maxtries (numeric, optional) How many iterations to try (default = 1000000).

Result:
[ blockhashes ] (array) hashes of blocks generated

Examples:

Generate 11 blocks to myaddress
> emercoin-cli generatetoaddress 11 "myaddress"
```

<b>`getgenerate`</b>

```
Return if the server is set to generate coins or not. The default is false.
It is set with the command line argument -gen (or emercoin.conf setting gen)
It can also be set with the setgenerate call.

Result
true|false (boolean) If the server is set to generate coins or not

Examples:
> emercoin-cli getgenerate
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getgenerate", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`setgenerate generate ( genproclimit )`</b>

```
Set 'generate' true or false to turn generation on or off.
Generation is limited to 'genproclimit' processors, -1 is unlimited.
See the getgenerate call for the current setting.

Arguments:
1. generate (boolean, required) Set to true to turn on generation, off to turn off.
2. genproclimit (numeric, optional) Set the processor limit for when generation is on. Can be -1 for unlimited.

Examples:

Set the generation on with a limit of one processor
> emercoin-cli setgenerate true 1

Check the setting
> emercoin-cli getgenerate

Turn off generation
> emercoin-cli setgenerate false

Using json rpc
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "setgenerate", "params": [true, 1] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b><h3>== Mining ==</h3></b>

<b>`getauxblock [<hash> <auxpow>]`</b>

```
create a new blockIf <hash>, <auxpow> is not specified, returns a new block hash.
If <hash>, <auxpow> is specified, tries to solve the block based on the aux proof of work and returns true if it was successful.
```

<b>`getblocktemplate ( TemplateRequest )`</b>

```
If the request parameters include a 'mode' key, that is used to explicitly select between the default 'template' request or a 'proposal'.
It returns data needed to construct a block to work on.
For full specification, see BIPs 22, 23, 9, and 145:
https://github.com/bitcoin/bips/blob/master/bip-0022.mediawiki
https://github.com/bitcoin/bips/blob/master/bip-0023.mediawiki
https://github.com/bitcoin/bips/blob/master/bip-0009.mediawiki#getblocktemplate_changes
https://github.com/bitcoin/bips/blob/master/bip-0145.mediawiki

Arguments:
1. template_request (json object, optional) A json object in the following spec
{
"mode":"template" (string, optional) This must be set to "template", "proposal" (see BIP 23), or omitted
"capabilities":[ (array, optional) A list of strings
"support" (string) client side supported feature, 'longpoll', 'coinbasetxn', 'coinbasevalue', 'proposal', 'serverlist', 'workid'
,...
],
"rules":[ (array, optional) A list of strings
"support" (string) client side supported softfork deployment
,...
]
}


Result:
{
"version" : n, (numeric) The preferred block version
"rules" : [ "rulename", ... ], (array of strings) specific block rules that are to be enforced
"previousblockhash" : "xxxx", (string) The hash of current highest block
"transactions" : [ (array) contents of non-coinbase transactions that should be included in the next block
{
"data" : "xxxx", (string) transaction data encoded in hexadecimal (byte-for-byte)
"txid" : "xxxx", (string) transaction id encoded in little-endian hexadecimal
"hash" : "xxxx", (string) hash encoded in little-endian hexadecimal (including witness data)
"depends" : [ (array) array of numbers
n (numeric) transactions before this one (by 1-based index in 'transactions' list) that must be present in the final block if this one is
,...
],
"fee": n, (numeric) difference in value between transaction inputs and outputs (in Satoshis); for coinbase transactions, this is a negative Number of the total collected block fees (ie, not including the block subsidy); if key is not present, fee is unknown and clients MUST NOT assume there isn't one
"sigops" : n, (numeric) total SigOps cost, as counted for purposes of block limits; if key is not present, sigop cost is unknown and clients MUST NOT assume it is zero
"weight" : n, (numeric) total transaction weight, as counted for purposes of block limits
"required" : true|false (boolean) if provided and true, this transaction must be in the final block
}
,...
],
"coinbaseaux" : { (json object) data that should be included in the coinbase's scriptSig content
"flags" : "xx" (string) key name is to be ignored, and value included in scriptSig
},
"coinbasevalue" : n, (numeric) maximum allowable input to coinbase transaction, including the generation award and transaction fees (in Satoshis)
"coinbasetxn" : { ... }, (json object) information for coinbase transaction
"target" : "xxxx", (string) The hash target
"mintime" : xxx, (numeric) The minimum timestamp appropriate for next block time in seconds since epoch (Jan 1 1970 GMT)
"mutable" : [ (array of string) list of ways the block template may be changed
"value" (string) A way the block template may be changed, e.g. 'time', 'transactions', 'prevblock'
,...
],
"noncerange" : "00000000ffffffff",(string) A range of valid nonces
"sigoplimit" : n, (numeric) limit of sigops in blocks
"sizelimit" : n, (numeric) limit of block size
"weightlimit" : n, (numeric) limit of block weight
"curtime" : ttt, (numeric) current timestamp in seconds since epoch (Jan 1 1970 GMT)
"bits" : "xxxxxxxx", (string) compressed target of next block
"height" : n (numeric) The height of the next block
}

Examples:
> emercoin-cli getblocktemplate
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblocktemplate", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getmininginfo`</b>

```
Returns a json object containing mining-related information.
Result:
{
"blocks": nnn, (numeric) The current block
"currentblocksize": nnn, (numeric) The last block size
"currentblockweight": nnn, (numeric) The last block weight
"currentblocktx": nnn, (numeric) The last block transaction
"difficulty": xxx.xxxxx (numeric) The current difficulty
"errors": "..." (string) Current errors
"generate": true|false (boolean) If the generation is on or off (see getgenerate or setgenerate calls)
"genproclimit": n (numeric) The processor limit for generation. -1 if no generation. (see getgenerate or setgenerate calls)
"networkhashps": nnn, (numeric) The network hashes per second
"pooledtx": n (numeric) The size of the mempool
"chain": "xxxx", (string) current network name as defined in BIP70 (main, test, regtest)
}

Examples:
> emercoin-cli getmininginfo
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getmininginfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getnetworkhashps ( nblocks height )`</b>

```
Returns the estimated network hashes per second based on the last n blocks.
Pass in [blocks] to override # of blocks, -1 specifies since last difficulty change.
Pass in [height] to estimate the network speed at the time when a certain block was found.

Arguments:
1. nblocks (numeric, optional, default=120) The number of blocks, or -1 for blocks since last difficulty change.
2. height (numeric, optional, default=-1) To estimate at the time of the given height.

Result:
x (numeric) Hashes per second estimated

Examples:
> emercoin-cli getnetworkhashps
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnetworkhashps", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`prioritisetransaction <txid> <priority delta> <fee delta>`</b>

```
Accepts the transaction into mined blocks at a higher (or lower) priority

Arguments:
1. "txid" (string, required) The transaction id.
2. priority_delta (numeric, required) The priority to add or subtract.
The transaction selection algorithm considers the tx as it would have a higher priority.
(priority of a transaction is calculated: coinage * value_in_satoshis / txsize)
3. fee_delta (numeric, required) The fee value (in satoshis) to add (or subtract, if negative).
The fee is not actually paid, only the algorithm for selecting transactions into a block
considers the transaction as it would have paid a higher (or lower) fee.

Result:
true (boolean) Returns true

Examples:
> emercoin-cli prioritisetransaction "txid" 0.0 10000
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "prioritisetransaction", "params": ["txid", 0.0, 10000] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`submitblock "hexdata" ( "jsonparametersobject" )`</b>

```
Attempts to submit new block to network.
The 'jsonparametersobject' parameter is currently ignored.
See https://en.bitcoin.it/wiki/BIP_0022 for full specification.

Arguments
1. "hexdata" (string, required) the hex-encoded block data to submit
2. "parameters" (string, optional) object of optional parameters
{
"workid" : "id" (string, optional) if the server provided a workid, it MUST be included with submissions
}

Result:

Examples:
> emercoin-cli submitblock "mydata"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "submitblock", "params": ["mydata"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b><h3>== Network ==</h3></b>

<b>`addnode "node" "add|remove|onetry"`</b>

```
Attempts add or remove a node from the addnode list.
Or try a connection to a node once.

Arguments:
1. "node" (string, required) The node (see getpeerinfo for nodes)
2. "command" (string, required) 'add' to add a node to the list, 'remove' to remove a node from the list, 'onetry' to try a connection to the node once

Examples:
> emercoin-cli addnode "192.168.0.6:8333" "onetry"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "addnode", "params": ["192.168.0.6:8333", "onetry"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`clearbanned`</b>

```
Clear all banned IPs.

Examples:
> emercoin-cli clearbanned
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "clearbanned", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`disconnectnode "address"`</b>

```
Immediately disconnects from the specified node.

Arguments:
1. "address" (string, required) The IP address/port of the node

Examples:
> emercoin-cli disconnectnode "192.168.0.6:8333"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "disconnectnode", "params": ["192.168.0.6:8333"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getaddednodeinfo ( "node" )`</b>

```
Returns information about the given added node, or all added nodes
(note that onetry addnodes are not listed here)

Arguments:
1. "node" (string, optional) If provided, return information about this specific node, otherwise all nodes are returned.

Result:
[
{
"addednode" : "192.168.0.201", (string) The node ip address or name (as provided to addnode)
"connected" : true|false, (boolean) If connected
"addresses" : [ (list of objects) Only when connected = true
{
"address" : "192.168.0.201:8333", (string) The emercoin server IP and port we're connected to
"connected" : "outbound" (string) connection, inbound or outbound
}
]
}
,...
]

Examples:
> emercoin-cli getaddednodeinfo true
> emercoin-cli getaddednodeinfo true "192.168.0.201"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddednodeinfo", "params": [true, "192.168.0.201"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getcheckpoint`</b>

```
Show info of synchronized checkpoint.
```

<b>`getconnectioncount`</b>

```
Returns the number of connections to other nodes.

Result:
n (numeric) The connection count

Examples:
> emercoin-cli getconnectioncount
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getconnectioncount", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getnettotals`</b>

```
Returns information about network traffic, including bytes in, bytes out,
and current time.

Result:
{
"totalbytesrecv": n, (numeric) Total bytes received
"totalbytessent": n, (numeric) Total bytes sent
"timemillis": t, (numeric) Current UNIX time in milliseconds
"uploadtarget":
{
"timeframe": n, (numeric) Length of the measuring timeframe in seconds
"target": n, (numeric) Target in bytes
"target_reached": true|false, (boolean) True if target is reached
"serve_historical_blocks": true|false, (boolean) True if serving historical blocks
"bytes_left_in_cycle": t, (numeric) Bytes left in current time cycle
"time_left_in_cycle": t (numeric) Seconds left in current time cycle
}
}

Examples:
> emercoin-cli getnettotals
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnettotals", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getnetworkinfo`</b>

```
Returns an object containing various state info regarding P2P networking.

Result:
{
"version": xxxxx, (numeric) the server version
"subversion": "/Satoshi:x.x.x/", (string) the server subversion string
"protocolversion": xxxxx, (numeric) the protocol version
"localservices": "xxxxxxxxxxxxxxxx", (string) the services we offer to the network
"localrelay": true|false, (bool) true if transaction relay is requested from peers
"timeoffset": xxxxx, (numeric) the time offset
"connections": xxxxx, (numeric) the number of connections
"networkactive": true|false, (bool) whether p2p networking is enabled
"networks": [ (array) information per network
{
"name": "xxx", (string) network (ipv4, ipv6 or onion)
"limited": true|false, (boolean) is the network limited using -onlynet?
"reachable": true|false, (boolean) is the network reachable?
"proxy": "host:port" (string) the proxy that is used for this network, or empty if none
"proxy_randomize_credentials": true|false, (string) Whether randomized credentials are used
}
,...
],
"relayfee": x.xxxxxxxx, (numeric) minimum relay fee for non-free transactions in EMC/kB
"incrementalfee": x.xxxxxxxx, (numeric) minimum fee increment for mempool limiting or BIP 125 replacement in EMC/kB
"localaddresses": [ (array) list of local addresses
{
"address": "xxxx", (string) network address
"port": xxx, (numeric) network port
"score": xxx (numeric) relative score
}
,...
]
"warnings": "..." (string) any network warnings
}

Examples:
> emercoin-cli getnetworkinfo
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnetworkinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`getpeerinfo`</b>

```
Returns data about each connected network node as a json array of objects.

Result:
[
{
"id": n, (numeric) Peer index
"addr":"host:port", (string) The ip address and port of the peer
"addrlocal":"ip:port", (string) local address
"services":"xxxxxxxxxxxxxxxx", (string) The services offered
"relaytxes":true|false, (boolean) Whether peer has asked us to relay transactions to it
"lastsend": ttt, (numeric) The time in seconds since epoch (Jan 1 1970 GMT) of the last send
"lastrecv": ttt, (numeric) The time in seconds since epoch (Jan 1 1970 GMT) of the last receive
"bytessent": n, (numeric) The total bytes sent
"bytesrecv": n, (numeric) The total bytes received
"conntime": ttt, (numeric) The connection time in seconds since epoch (Jan 1 1970 GMT)
"timeoffset": ttt, (numeric) The time offset in seconds
"pingtime": n, (numeric) ping time (if available)
"minping": n, (numeric) minimum observed ping time (if any at all)
"pingwait": n, (numeric) ping wait (if non-zero)
"version": v, (numeric) The peer version, such as 7001
"subver": "/Satoshi:0.8.5/", (string) The string version
"inbound": true|false, (boolean) Inbound (true) or Outbound (false)
"addnode": true|false, (boolean) Whether connection was due to addnode and is using an addnode slot
"startingheight": n, (numeric) The starting height (block) of the peer
"banscore": n, (numeric) The ban score
"synced_headers": n, (numeric) The last header we have in common with this peer
"synced_blocks": n, (numeric) The last block we have in common with this peer
"inflight": [
n, (numeric) The heights of blocks we're currently asking from this peer
...
],
"whitelisted": true|false, (boolean) Whether the peer is whitelisted
"bytessent_per_msg": {
"addr": n, (numeric) The total bytes sent aggregated by message type
...
},
"bytesrecv_per_msg": {
"addr": n, (numeric) The total bytes received aggregated by message type
...
}
}
,...
]

Examples:
> emercoin-cli getpeerinfo
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getpeerinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`listbanned`</b>

```
List all banned IPs/Subnets.

Examples:
> emercoin-cli listbanned
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listbanned", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`ping`</b>

```
Requests that a ping be sent to all other nodes, to measure ping time.
Results provided in getpeerinfo, pingtime and pingwait fields are decimal seconds.
Ping command is handled in queue with all other commands, so it measures processing backlog, not just network ping.

Examples:
> emercoin-cli ping
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "ping", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`setban "subnet" "add|remove" (bantime) (absolute)`</b>

```
Attempts add or remove a IP/Subnet from the banned list.

Arguments:
1. "subnet" (string, required) The IP/Subnet (see getpeerinfo for nodes ip) with a optional netmask (default is /32 = single ip)
2. "command" (string, required) 'add' to add a IP/Subnet to the list, 'remove' to remove a IP/Subnet from the list
3. "bantime" (numeric, optional) time in seconds how long (or until when if [absolute] is set) the ip is banned (0 or empty means using the default time of 24h which can also be overwritten by the -bantime startup argument)
4. "absolute" (boolean, optional) If set, the bantime must be a absolute timestamp in seconds since epoch (Jan 1 1970 GMT)

Examples:
> emercoin-cli setban "192.168.0.6" "add" 86400
> emercoin-cli setban "192.168.0.0/24" "add"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "setban", "params": ["192.168.0.6", "add", 86400] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>`setnetworkactive true|false`</b>

```
Disable/enable all p2p network activity.

Arguments:
1. "state" (boolean, required) true to enable networking, false to disable
```


*Note: An important command, `reencodeoldprivkey`, is missing from the current debug help that may be helpful for users of older wallet versions prior to 0.5.x:*

```text
reencodeoldprivkey XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```


The command `reencodeoldprivkey` returns the same key to you, but in a format suitable for Emercoin version 0.5.x and higher. Then you can use `importprivkey` as usual.

Additional help for each API command
---------------

Additional help can be requested for any of the above API commands. e.g:

	$ emc help name_new



```text
name_new <name> <value> <days> [toaddress] [valuetype]
Creates new key->value pair which expires after specified number of days.
Cost is square root of (1% of last PoW + 1% per year of last PoW).
Arguments:
1. name      (string, required) Name to create.
2. value     (string, required) Value to write.
3. toaddress (string, optional) Address of recipient. Empty string = transaction to yourself.
4. valuetype (string, optional) Interpretation of value string. Can be "hex", "base64" or filepath.
   not specified or empty - Write value as a unicode string.
   "hex" or "base64" - Decode value string as a binary data in hex or base64 string format.
   otherwise - Decode value string as a filepath from which to read the data.
```



	$ emc help sendtoaddress
	
	
	
```text
sendtoaddress "emercoinaddress" amount ( "comment" "comment-to" )

Send an amount to a given address. The amount is a real and is rounded to the nearest 0.00000001

Requires wallet passphrase to be set with walletpassphrase call.
Arguments:
1. "emercoinaddress"  (string, required) The emercoin address to send to.
2. "amount"      (numeric, required) The amount in emc to send. eg 0.1
3. "comment"     (string, optional) A comment used to store what the transaction is for. 
                             This is not part of the transaction, just kept in your wallet.
4. "comment-to"  (string, optional) A comment to store the name of the person or organization 
                             to which you're sending the transaction. This is not part of the 
                             transaction, just kept in your wallet.

Result:
"transactionid"  (string) The transaction id.

Examples:
> emercoin-cli sendtoaddress "1M72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd" 0.1
> emercoin-cli sendtoaddress "1M72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd" 0.1 "donation" "seans outpost"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendtoaddress", "params": ["1M72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd", 0.1, "donation", "seans outpost"] }' -H 'content-type: text/plain;' http://127.0.0.1:6662/
```
