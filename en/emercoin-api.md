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

<b>== Blockchain ==</br>
getbestblockhash</b>
```
Returns the hash of the best (tip) block in the longest blockchain.

Result:
"hex" (string) the block hash hex encoded

Examples:
> emercoin-cli getbestblockhash
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getbestblockhash", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>getblock "blockhash" ( verbose )</b>
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
<b>getblockchaininfo</b>
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
<b>getblockcount</b>
```
Returns the number of blocks in the longest blockchain.

Result:
n (numeric) The current block count

Examples:
> emercoin-cli getblockcount
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockcount", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>getblockhash height</b>
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
<b>getblockheader "hash" ( verbose )</b>
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
<b>getchaintips</b>
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
<b>getdifficulty</b>
```
Returns the proof-of-work difficulty as a multiple of the minimum difficulty.

Result:
n.nnn (numeric) the proof-of-work difficulty as a multiple of the minimum difficulty.

Examples:
> emercoin-cli getdifficulty
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getdifficulty", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>getmempoolancestors txid (verbose)</b>
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
<b>getmempooldescendants txid (verbose)</b>
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
<b>getmempoolentry txid</b>
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
<b>getmempoolinfo</b>
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
<b>getrawmempool ( verbose )</b>
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
<b>gettxlistfor &lt;fromblock&gt; &lt;toblock&gt; &lt;address&gt; &#91;type=0&#93; &#91;verbose=0&#93;</b>
```
[type]: 0 - sent/received, 1 - received, 2 - sent
[verbose]: 0 - false, 1 - true
```
<b>gettxout "txid" n ( include_mempool )</b>
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
<b>gettxoutproof &#91;"txid",...&#93; ( blockhash )</b>
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
<b>gettxoutsetinfo</b>
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
<b>name_filter &#91;regexp&#93; &#91;maxage=0&#93; &#91;from=0&#93; &#91;nb=0&#93; &#91;stat&#93; &#91;valuetype&#93;</b>
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
<b>name_history &lt;name&gt; &#91;fullhistory&#93; &#91;valuetype&#93;</b>
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
<b>name_mempool &#91;valuetype&#93;</b>
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
<b>name_scan &#91;start-name&#93; &#91;max-returned&#93; &#91;max-value-length=0&#93; &#91;valuetype&#93;</b>
```
Scan all names, starting at [start-name] and returning [max-returned] number of entries (default 500)
[max-value-length] : control how much of value is shown (0 = full value)
[valuetype] : if "hex" or "base64" is specified then it will print value in corresponding format instead of a string.
```
<b>name_scan_address &lt;address&gt; &#91;max-value-length=0&#93; &#91;valuetype&#93;</b>
```
Print names that belong to specific address
[max-value-length] : control how much of name value is shown (0 = full value)
[valuetype] : if "hex" or "base64" is specified then it will print value in corresponding format instead of a string.
```
<b>name_show &lt;name&gt; &#91;valuetype&#93; &#91;filepath&#93;</b>
```
Show values of a name.

Arguments:
1. name (string, required).
2. valuetype (string, optional) If "hex" or "base64" is specified then it will print value in corresponding format instead of string.
3. filepath (string, optional) save name value in binary format in specified file (file will be overwritten!).
```
<b>preciousblock "blockhash"</b>
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
<b>verifychain ( checklevel nblocks )</b>
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
<b>verifytxoutproof "proof"</b>
```
Verifies that a proof points to a transaction in a block, returning the transaction it commits to
and throwing an RPC error if the block is not in our best chain

Arguments:
1. "proof" (string, required) The hex-encoded proof generated by gettxoutproof

Result:
["txid"] (array, strings) The txid(s) which the proof commits to, or empty array if the proof is invalid
```
<b>== Control ==</br>
getinfo</b>
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
<b>getmemoryinfo</b>
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
<b>help ( "command" )</b>
```
List all commands, or get help for a specified command.

Arguments:
1. "command" (string, optional) The command to get help on

Result:
"text" (string) The help text
```
<b>stop</b>
```
Stop Emercoin server.
```
<b>== Generating ==</br>
generate nblocks ( maxtries )</b>
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
<b>generatetoaddress nblocks address (maxtries)</b>
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
<b>getgenerate</b>
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
<b>setgenerate generate ( genproclimit )</b>
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
<b>== Mining ==</br>
getauxblock &#91;&lt;hash&gt; &lt;auxpow&gt;&#93;</b>
```
create a new blockIf <hash>, <auxpow> is not specified, returns a new block hash.
If <hash>, <auxpow> is specified, tries to solve the block based on the aux proof of work and returns true if it was successful.
```
<b>getblocktemplate ( TemplateRequest )</b>
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
<b>getmininginfo</b>
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
<b>getnetworkhashps ( nblocks height )</b>
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
<b>prioritisetransaction &lt;txid&gt; &lt;priority delta&gt; &lt;fee delta&gt;</b>
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
<b>submitblock "hexdata" ( "jsonparametersobject" )</b>
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

<b>== Network ==</br>
addnode "node" "add|remove|onetry"</b>
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
<b>clearbanned</b>
```
Clear all banned IPs.

Examples:
> emercoin-cli clearbanned
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "clearbanned", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>disconnectnode "address"</b>
```
Immediately disconnects from the specified node.

Arguments:
1. "address" (string, required) The IP address/port of the node

Examples:
> emercoin-cli disconnectnode "192.168.0.6:8333"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "disconnectnode", "params": ["192.168.0.6:8333"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>getaddednodeinfo ( "node" )</b>
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
<b>getcheckpoint</b>
```
Show info of synchronized checkpoint.
```
<b>getconnectioncount</b>
```
Returns the number of connections to other nodes.

Result:
n (numeric) The connection count

Examples:
> emercoin-cli getconnectioncount
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getconnectioncount", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>getnettotals</b>
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
<b>getnetworkinfo</b>
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
<b>getpeerinfo</b>
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
<b>listbanned</b>
```
List all banned IPs/Subnets.

Examples:
> emercoin-cli listbanned
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listbanned", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>ping</b>
```
Requests that a ping be sent to all other nodes, to measure ping time.
Results provided in getpeerinfo, pingtime and pingwait fields are decimal seconds.
Ping command is handled in queue with all other commands, so it measures processing backlog, not just network ping.

Examples:
> emercoin-cli ping
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "ping", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>setban "subnet" "add|remove" (bantime) (absolute)</b>
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
<b>setnetworkactive true|false</b>
```
Disable/enable all p2p network activity.

Arguments:
1. "state" (boolean, required) true to enable networking, false to disable
```

<b>== Rawtransactions ==</br>
createrawtransaction &#91;{"txid":"id","vout":n},...&#93; {"address":amount,"data":"hex",...} ( locktime )</b>
```
Create a transaction spending the given inputs and creating new outputs.
Outputs can be addresses or data.
Returns hex-encoded raw transaction.
Note that the transaction's inputs are not signed, and
it is not stored in the wallet or transmitted to the network.

Arguments:
1. "inputs" (array, required) A json array of json objects
[
{
"txid":"id", (string, required) The transaction id
"vout":n, (numeric, required) The output number
"sequence":n (numeric, optional) The sequence number
}
,...
]
2. "outputs" (object, required) a json object with outputs
{
"address": x.xxx, (numeric or string, required) The key is the emercoin address, the numeric value (can be string) is the EMC amount
"data": "hex" (string, required) The key is "data", the value is hex encoded data
,...
}
3. locktime (numeric, optional, default=0) Raw locktime. Non-0 value also locktime-activates inputs

Result:
"transaction" (string) hex string of the transaction

Examples:
> emercoin-cli createrawtransaction "[{\"txid\":\"myid\",\"vout\":0}]" "{\"address\":0.01}"
> emercoin-cli createrawtransaction "[{\"txid\":\"myid\",\"vout\":0}]" "{\"data\":\"00010203\"}"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createrawtransaction", "params": ["[{\"txid\":\"myid\",\"vout\":0}]", "{\"address\":0.01}"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createrawtransaction", "params": ["[{\"txid\":\"myid\",\"vout\":0}]", "{\"data\":\"00010203\"}"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>decoderawtransaction "hexstring"</b>
```
Return a JSON object representing the serialized, hex-encoded transaction.

Arguments:
1. "hexstring" (string, required) The transaction hex string

Result:
{
"txid" : "id", (string) The transaction id
"hash" : "id", (string) The transaction hash (differs from txid for witness transactions)
"size" : n, (numeric) The transaction size
"vsize" : n, (numeric) The virtual transaction size (differs from size for witness transactions)
"version" : n, (numeric) The version
"locktime" : ttt, (numeric) The lock time
"vin" : [ (array of json objects)
{
"txid": "id", (string) The transaction id
"vout": n, (numeric) The output number
"scriptSig": { (json object) The script
"asm": "asm", (string) asm
"hex": "hex" (string) hex
},
"txinwitness": ["hex", ...] (array of string) hex-encoded witness data (if any)
"sequence": n (numeric) The script sequence number
}
,...
],
"vout" : [ (array of json objects)
{
"value" : x.xxx, (numeric) The value in EMC
"n" : n, (numeric) index
"scriptPubKey" : { (json object)
"asm" : "asm", (string) the asm
"hex" : "hex", (string) the hex
"reqSigs" : n, (numeric) The required sigs
"type" : "pubkeyhash", (string) The type, eg 'pubkeyhash'
"addresses" : [ (json array of string)
"12tvKAXCxZjSmdNbao16dKXC8tRWfcF5oc" (string) emercoin address
,...
]
}
}
,...
],
}

Examples:
> emercoin-cli decoderawtransaction "hexstring"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "decoderawtransaction", "params": ["hexstring"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>decodescript "hexstring"</b>
```
Decode a hex-encoded script.

Arguments:
1. "hexstring" (string) the hex encoded script

Result:
{
"asm":"asm", (string) Script public key
"hex":"hex", (string) hex encoded public key
"type":"type", (string) The output type
"reqSigs": n, (numeric) The required signatures
"addresses": [ (json array of string)
"address" (string) emercoin address
,...
],
"p2sh","address" (string) address of P2SH script wrapping this redeem script (not returned if the script is already a P2SH).
}

Examples:
> emercoin-cli decodescript "hexstring"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "decodescript", "params": ["hexstring"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>fundrawtransaction "hexstring" ( options )</b>
```
Add inputs to a transaction until it has enough in value to meet its out value.
This will not modify existing inputs, and will add at most one change output to the outputs.
No existing outputs will be modified unless "subtractFeeFromOutputs" is specified.
Note that inputs which were signed may need to be resigned after completion since in/outputs have been added.
The inputs added will not be signed, use signrawtransaction for that.
Note that all existing inputs must have their previous output transaction be in the wallet.
Note that all inputs selected must be of standard form and P2SH scripts must be
in the wallet using importaddress or addmultisigaddress (to calculate fees).
You can see whether this is the case by checking the "solvable" field in the listunspent output.
Only pay-to-pubkey, multisig, and P2SH versions thereof are currently supported for watch-only

Arguments:
1. "hexstring" (string, required) The hex string of the raw transaction
2. options (object, optional)
{
"changeAddress" (string, optional, default pool address) The emercoin address to receive the change
"changePosition" (numeric, optional, default random) The index of the change output
"includeWatching" (boolean, optional, default false) Also select inputs which are watch only
"lockUnspents" (boolean, optional, default false) Lock selected unspent outputs
"reserveChangeKey" (boolean, optional, default true) Reserves the change output key from the keypool
"feeRate" (numeric, optional, default not set: makes wallet determine the fee) Set a specific feerate (EMC per KB)
"subtractFeeFromOutputs" (array, optional) A json array of integers.
The fee will be equally deducted from the amount of each specified output.
The outputs are specified by their zero-based index, before any change output is added.
Those recipients will receive less emercoins than you enter in their corresponding amount field.
If no outputs are specified here, the sender pays the fee.
[vout_index,...]
}
for backward compatibility: passing in a true instead of an object will result in {"includeWatching":true}

Result:
{
"hex": "value", (string) The resulting raw transaction (hex-encoded string)
"fee": n, (numeric) Fee in EMC the resulting transaction pays
"changepos": n (numeric) The position of the added change output, or -1
}

Examples:

Create a transaction with no inputs
> emercoin-cli createrawtransaction "[]" "{\"myaddress\":0.01}"

Add sufficient unsigned inputs to meet the output value
> emercoin-cli fundrawtransaction "rawtransactionhex"

Sign the transaction
> emercoin-cli signrawtransaction "fundedtransactionhex"

Send the transaction
> emercoin-cli sendrawtransaction "signedtransactionhex"
```
<b>getrawtransaction "txid" ( verbose )</b>
```
NOTE: By default this function only works for mempool transactions. If the -txindex option is
enabled, it also works for blockchain transactions.
DEPRECATED: for now, it also works for transactions with unspent outputs.

Return the raw transaction data.

If verbose is 'true', returns an Object with information about 'txid'.
If verbose is 'false' or omitted, returns a string that is serialized, hex-encoded data for 'txid'.

Arguments:
1. "txid" (string, required) The transaction id
2. verbose (bool, optional, default=false) If false, return a string, otherwise return a json object

Result (if verbose is not set or set to false):
"data" (string) The serialized, hex-encoded data for 'txid'

Result (if verbose is set to true):
{
"hex" : "data", (string) The serialized, hex-encoded data for 'txid'
"txid" : "id", (string) The transaction id (same as provided)
"hash" : "id", (string) The transaction hash (differs from txid for witness transactions)
"size" : n, (numeric) The serialized transaction size
"vsize" : n, (numeric) The virtual transaction size (differs from size for witness transactions)
"version" : n, (numeric) The version
"locktime" : ttt, (numeric) The lock time
"vin" : [ (array of json objects)
{
"txid": "id", (string) The transaction id
"vout": n, (numeric)
"scriptSig": { (json object) The script
"asm": "asm", (string) asm
"hex": "hex" (string) hex
},
"sequence": n (numeric) The script sequence number
"txinwitness": ["hex", ...] (array of string) hex-encoded witness data (if any)
}
,...
],
"vout" : [ (array of json objects)
{
"value" : x.xxx, (numeric) The value in EMC
"n" : n, (numeric) index
"scriptPubKey" : { (json object)
"asm" : "asm", (string) the asm
"hex" : "hex", (string) the hex
"reqSigs" : n, (numeric) The required sigs
"type" : "pubkeyhash", (string) The type, eg 'pubkeyhash'
"addresses" : [ (json array of string)
"address" (string) emercoin address
,...
]
}
}
,...
],
"blockhash" : "hash", (string) the block hash
"confirmations" : n, (numeric) The confirmations
"time" : ttt, (numeric) The transaction time in seconds since epoch (Jan 1 1970 GMT)
"blocktime" : ttt (numeric) The block time in seconds since epoch (Jan 1 1970 GMT)
}

Examples:
> emercoin-cli getrawtransaction "mytxid"
> emercoin-cli getrawtransaction "mytxid" true
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawtransaction", "params": ["mytxid", true] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>sendrawtransaction "hexstring" ( allowhighfees )</b>
```
Submits raw transaction (serialized, hex-encoded) to local node and network.

Also see createrawtransaction and signrawtransaction calls.

Arguments:
1. "hexstring" (string, required) The hex string of the raw transaction)
2. allowhighfees (boolean, optional, default=false) Allow high fees

Result:
"hex" (string) The transaction hash in hex

Examples:

Create a transaction
> emercoin-cli createrawtransaction "[{\"txid\" : \"mytxid\",\"vout\":0}]" "{\"myaddress\":0.01}"
Sign the transaction, and get back the hex
> emercoin-cli signrawtransaction "myhex"

Send the transaction (signed hex)
> emercoin-cli sendrawtransaction "signedhex"

As a json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendrawtransaction", "params": ["signedhex"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>signrawtransaction "hexstring" ( &#91;{"txid":"id","vout":n,"scriptPubKey":"hex","redeemScript":"hex"},...&#93; &#91;"privatekey1",...&#93; sighashtype )</b>
```
Sign inputs for raw transaction (serialized, hex-encoded).
The second optional argument (may be null) is an array of previous transaction outputs that
this transaction depends on but may not yet be in the block chain.
The third optional argument (may be null) is an array of base58-encoded private
keys that, if given, will be the only keys used to sign the transaction.


Arguments:
1. "hexstring" (string, required) The transaction hex string
2. "prevtxs" (string, optional) An json array of previous dependent transaction outputs
[ (json array of json objects, or 'null' if none provided)
{
"txid":"id", (string, required) The transaction id
"vout":n, (numeric, required) The output number
"scriptPubKey": "hex", (string, required) script key
"redeemScript": "hex", (string, required for P2SH or P2WSH) redeem script
"amount": value (numeric, required) The amount spent
}
,...
]
3. "privkeys" (string, optional) A json array of base58-encoded private keys for signing
[ (json array of strings, or 'null' if none provided)
"privatekey" (string) private key in base58-encoding
,...
]
4. "sighashtype" (string, optional, default=ALL) The signature hash type. Must be one of
"ALL"
"NONE"
"SINGLE"
"ALL|ANYONECANPAY"
"NONE|ANYONECANPAY"
"SINGLE|ANYONECANPAY"

Result:
{
"hex" : "value", (string) The hex-encoded raw transaction with signature(s)
"complete" : true|false, (boolean) If the transaction has a complete set of signatures
"errors" : [ (json array of objects) Script verification errors (if there are any)
{
"txid" : "hash", (string) The hash of the referenced, previous transaction
"vout" : n, (numeric) The index of the output to spent and used as input
"scriptSig" : "hex", (string) The hex-encoded signature script
"sequence" : n, (numeric) Script sequence number
"error" : "text" (string) Verification or signing error related to the input
}
,...
]
}

Examples:
> emercoin-cli signrawtransaction "myhex"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "signrawtransaction", "params": ["myhex"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>== Util ==</br>
createmultisig nrequired &#91;"key",...&#93;</b>
```
Creates a multi-signature address with n signature of m keys required.
It returns a json object with the address and redeemScript.

Arguments:
1. nrequired (numeric, required) The number of required signatures out of the n keys or addresses.
2. "keys" (string, required) A json array of keys which are emercoin addresses or hex-encoded public keys
[
"key" (string) emercoin address or hex-encoded public key
,...
]

Result:
{
"address":"multisigaddress", (string) The value of the new multisig address.
"redeemScript":"script" (string) The string value of the hex-encoded redemption script.
}

Examples:

Create a multisig address from 2 addresses
> emercoin-cli createmultisig 2 "[\"16sSauSf5pF2UkUwvKGq4qjNRzBZYqgEL5\",\"171sgjn4YtPu27adkKGrdDwzRTxnRkBfKV\"]"

As a json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "createmultisig", "params": [2, "[\"16sSauSf5pF2UkUwvKGq4qjNRzBZYqgEL5\",\"171sgjn4YtPu27adkKGrdDwzRTxnRkBfKV\"]"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>estimatefee nblocks</b>
```
Estimates the approximate fee per kilobyte needed for a transaction to begin
confirmation within nblocks blocks. Uses virtual transaction size of transaction
as defined in BIP 141 (witness data is discounted).

Arguments:
1. nblocks (numeric, does nothing - backward compatability with emercoin RPC)

Result:
n (numeric) estimated fee-per-kilobyte

A negative value is returned if not enough transactions and blocks
have been observed to make an estimate.
-1 is always returned for nblocks == 1 as it is impossible to calculate
a fee that is high enough to get reliably included in the next block.

Example:
> emercoin-cli estimatefee 6
```
<b>estimatepriority nblocks</b>
```
DEPRECATED. Estimates the approximate priority a zero-fee transaction needs to begin
confirmation within nblocks blocks.

Arguments:
1. nblocks (numeric, required)

Result:
n (numeric) estimated priority

A negative value is returned if not enough transactions and blocks
have been observed to make an estimate.

Example:
> emercoin-cli estimatepriority 6
```
<b>estimatesmartpriority nblocks</b>
```
DEPRECATED. WARNING: This interface is unstable and may disappear or change!

Estimates the approximate priority a zero-fee transaction needs to begin
confirmation within nblocks blocks if possible and return the number of blocks
for which the estimate is valid.

Arguments:
1. nblocks (numeric, required)

Result:
{
"priority" : x.x, (numeric) estimated priority
"blocks" : n (numeric) block number where estimate was found
}

A negative value is returned if not enough transactions and blocks
have been observed to make an estimate for any number of blocks.
However if the mempool reject fee is set it will return 1e9 * MAX_MONEY.

Example:
> emercoin-cli estimatesmartpriority 6
```
<b>signmessagewithprivkey "privkey" "message"</b>
```
Sign a message with the private key of an address

Arguments:
1. "privkey" (string, required) The private key to sign the message with.
2. "message" (string, required) The message to create a signature of.

Result:
"signature" (string) The signature of the message encoded in base 64

Examples:

Create the signature
> emercoin-cli signmessagewithprivkey "privkey" "my message"

Verify the signature
> emercoin-cli verifymessage "1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" "signature" "my message"

As json rpc
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "signmessagewithprivkey", "params": ["privkey", "my message"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>validateaddress "emercoinaddress"</b>
```
Return information about the given emercoin address.

Arguments:
1. "emercoinaddress" (string, required) The emercoin address to validate

Result:
{
"isvalid" : true|false, (boolean) If the address is valid or not. If not, this is the only property returned.
"address" : "address", (string) The emercoin address validated
"scriptPubKey" : "hex", (string) The hex encoded scriptPubKey generated by the address
"ismine" : true|false, (boolean) If the address is yours or not
"iswatchonly" : true|false, (boolean) If the address is watchonly
"isscript" : true|false, (boolean) If the key is a script
"pubkey" : "publickeyhex", (string) The hex value of the raw public key
"iscompressed" : true|false, (boolean) If the address is compressed
"account" : "account" (string) DEPRECATED. The account associated with the address, "" is the default account
"timestamp" : timestamp, (number, optional) The creation time of the key if available in seconds since epoch (Jan 1 1970 GMT)
"hdkeypath" : "keypath" (string, optional) The HD keypath if the key is HD and available
"hdmasterkeyid" : "<hash160>" (string, optional) The Hash160 of the HD master pubkey
}

Examples:
> emercoin-cli validateaddress "1PSSGeFHDnKNxiEyFrD1wcEaHr9hrQDDWc"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "validateaddress", "params": ["1PSSGeFHDnKNxiEyFrD1wcEaHr9hrQDDWc"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>verifymessage "address" "signature" "message"</b>
```
Verify a signed message

Arguments:
1. "address" (string, required) The emercoin address to use for the signature.
2. "signature" (string, required) The signature provided by the signer in base 64 encoding (see signmessage).
3. "message" (string, required) The message that was signed.

Result:
true|false (boolean) If the signature is verified or not.

Examples:

Unlock the wallet for 30 seconds
> emercoin-cli walletpassphrase "mypassphrase" 30

Create the signature
> emercoin-cli signmessage "1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" "my message"

Verify the signature
> emercoin-cli verifymessage "1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" "signature" "my message"

As json rpc
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "verifymessage", "params": ["1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX", "signature", "my message"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```

<b>== Wallet ==</br>
abandontransaction "txid"</b>
```
Mark in-wallet transaction <txid> as abandoned
This will mark this transaction and all its in-wallet descendants as abandoned which will allow
for their inputs to be respent. It can be used to replace "stuck" or evicted transactions.
It only works on transactions which are not included in a block and are not currently in the mempool.
It has no effect on transactions which are already conflicted or abandoned.

Arguments:
1. "txid" (string, required) The transaction id

Result:

Examples:
> emercoin-cli abandontransaction "1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "abandontransaction", "params": ["1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
addmultisigaddress nrequired &#91;"key",...&#93; ( "account" )
```
Add a nrequired-to-sign multisignature address to the wallet.
Each key is a Emercoin address or hex-encoded public key.
If 'account' is specified (DEPRECATED), assign address to that account.

Arguments:
1. nrequired (numeric, required) The number of required signatures out of the n keys or addresses.
2. "keys" (string, required) A json array of emercoin addresses or hex-encoded public keys
[
"address" (string) emercoin address or hex-encoded public key
...,
]
3. "account" (string, optional) DEPRECATED. An account to assign the addresses to.

Result:
"address" (string) A emercoin address associated with the keys.

Examples:

Add a multisig address from 2 addresses
> emercoin-cli addmultisigaddress 2 "[\"16sSauSf5pF2UkUwvKGq4qjNRzBZYqgEL5\",\"171sgjn4YtPu27adkKGrdDwzRTxnRkBfKV\"]"

As json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "addmultisigaddress", "params": [2, "[\"16sSauSf5pF2UkUwvKGq4qjNRzBZYqgEL5\",\"171sgjn4YtPu27adkKGrdDwzRTxnRkBfKV\"]"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>addwitnessaddress "address"</b>
```
Add a witness address for a script (with pubkey or redeemscript known).
It returns the witness script.

Arguments:
1. "address" (string, required) An address known to the wallet

Result:
"witnessaddress", (string) The value of the new address (P2SH of witness script).
}
```
<b>backupwallet "destination"</b>
```
Safely copies current wallet file to destination, which can be a directory or a path with filename.

Arguments:
1. "destination" (string) The destination directory or file

Examples:
> emercoin-cli backupwallet "backup.dat"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "backupwallet", "params": ["backup.dat"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>bumpfee "txid" ( options )</b>
```
Bumps the fee of an opt-in-RBF transaction T, replacing it with a new transaction B.
An opt-in RBF transaction with the given txid must be in the wallet.
The command will pay the additional fee by decreasing (or perhaps removing) its change output.
If the change output is not big enough to cover the increased fee, the command will currently fail
instead of adding new inputs to compensate. (A future implementation could improve this.)
The command will fail if the wallet or mempool contains a transaction that spends one of T's outputs.
By default, the new fee will be calculated automatically using estimatefee.
The user can specify a confirmation target for estimatefee.
Alternatively, the user can specify totalFee, or use RPC setpaytxfee to set a higher fee rate.
At a minimum, the new fee rate must be high enough to pay an additional new relay fee (incrementalfee
returned by getnetworkinfo) to enter the node's mempool.

Arguments:
1. txid (string, required) The txid to be bumped
2. options (object, optional)
{
"confTarget" (numeric, optional) Confirmation target (in blocks)
"totalFee" (numeric, optional) Total fee (NOT feerate) to pay, in satoshis.
In rare cases, the actual fee paid might be slightly higher than the specified
totalFee if the tx change output has to be removed because it is too close to
the dust threshold.
"replaceable" (boolean, optional, default true) Whether the new transaction should still be
marked bip-125 replaceable. If true, the sequence numbers in the transaction will
be left unchanged from the original. If false, any input sequence numbers in the
original transaction that were less than 0xfffffffe will be increased to 0xfffffffe
so the new transaction will not be explicitly bip-125 replaceable (though it may
still be replacable in practice, for example if it has unconfirmed ancestors which
are replaceable).
}

Result:
{
"txid": "value", (string) The id of the new transaction
"origfee": n, (numeric) Fee of the replaced transaction
"fee": n, (numeric) Fee of the new transaction
"errors": [ str... ] (json array of strings) Errors encountered during processing (may be empty)
}

Examples:

Bump the fee, get the new transaction's txid
> emercoin-cli bumpfee <txid>
```
<b>dumpprivkey "address"</b>
```
Reveals the private key corresponding to 'address'.
Then the importprivkey can be used with this output

Arguments:
1. "address" (string, required) The emercoin address for the private key

Result:
"key" (string) The private key

Examples:
> emercoin-cli dumpprivkey "myaddress"
> emercoin-cli importprivkey "mykey"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "dumpprivkey", "params": ["myaddress"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>dumpwallet "filename"</b>
```
Dumps all wallet keys in a human-readable format.

Arguments:
1. "filename" (string, required) The filename

Examples:
> emercoin-cli dumpwallet "test"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "dumpwallet", "params": ["test"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>encryptwallet "passphrase"</b>
```
Encrypts the wallet with 'passphrase'. This is for first time encryption.
After this, any calls that interact with private keys such as sending or signing
will require the passphrase to be set prior the making these calls.
Use the walletpassphrase call for this, and then walletlock call.
If the wallet is already encrypted, use the walletpassphrasechange call.
Note that this will shutdown the server.

Arguments:
1. "passphrase" (string) The pass phrase to encrypt the wallet with. It must be at least 1 character, but should be long.

Examples:

Encrypt you wallet
> emercoin-cli encryptwallet "my pass phrase"

Now set the passphrase to use the wallet, such as for signing or sending emercoin
> emercoin-cli walletpassphrase "my pass phrase"

Now we can so something like sign
> emercoin-cli signmessage "address" "test message"

Now lock the wallet again by removing the passphrase
> emercoin-cli walletlock

As a json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "encryptwallet", "params": ["my pass phrase"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>getaccount "address"</b>
```
DEPRECATED. Returns the account associated with the given address.

Arguments:
1. "address" (string, required) The emercoin address for account lookup.

Result:
"accountname" (string) the account address

Examples:
> emercoin-cli getaccount "1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaccount", "params": ["1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>getaccountaddress "account"</b>
```
DEPRECATED. Returns the current Emercoin address for receiving payments to this account.

Arguments:
1. "account" (string, required) The account name for the address. It can also be set to the empty string "" to represent the default account. The account does not need to exist, it will be created and a new address created if there is no account by the given name.

Result:
"address" (string) The account emercoin address

Examples:
> emercoin-cli getaccountaddress
> emercoin-cli getaccountaddress ""
> emercoin-cli getaccountaddress "myaccount"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaccountaddress", "params": ["myaccount"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>getaddressesbyaccount "account"</b>
```
DEPRECATED. Returns the list of addresses for the given account.

Arguments:
1. "account" (string, required) The account name.

Result:
[ (json array of string)
"address" (string) a emercoin address associated with the given account
,...
]

Examples:
> emercoin-cli getaddressesbyaccount "tabby"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddressesbyaccount", "params": ["tabby"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>getbalance ( "account" minconf include_watchonly )</b>
```
If account is not specified, returns the server's total available balance.
If account is specified (DEPRECATED), returns the balance in the account.
Note that the account "" is not the same as leaving the parameter out.
The server total may be different to the balance in the default "" account.

Arguments:
1. "account" (string, optional) DEPRECATED. The account string may be given as a
specific account name to find the balance associated with wallet keys in
a named account, or as the empty string ("") to find the balance
associated with wallet keys not in any named account, or as "*" to find
the balance associated with all wallet keys regardless of account.
When this option is specified, it calculates the balance in a different
way than when it is not specified, and which can count spends twice when
there are conflicting pending transactions (such as those created by
the bumpfee command), temporarily resulting in low or even negative
balances. In general, account balance calculation is not considered
reliable and has resulted in confusing outcomes, so it is recommended to
avoid passing this argument.
2. minconf (numeric, optional, default=1) Only include transactions confirmed at least this many times.
3. include_watchonly (bool, optional, default=false) Also include balance in watch-only addresses (see 'importaddress')

Result:
amount (numeric) The total amount in EMC received for this account.

Examples:

The total amount in the wallet
> emercoin-cli getbalance

The total amount in the wallet at least 5 blocks confirmed
> emercoin-cli getbalance "*" 6

As a json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getbalance", "params": ["*", 6] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
getnewaddress ( "account" )
```
Returns a new Emercoin address for receiving payments.
If 'account' is specified (DEPRECATED), it is added to the address book
so payments received with the address will be credited to 'account'.

Arguments:
1. "account" (string, optional) DEPRECATED. The account name for the address to be linked to. If not provided, the default account "" is used. It can also be set to the empty string "" to represent the default account. The account does not need to exist, it will be created if there is no account by the given name.

Result:
"address" (string) The new emercoin address

Examples:
> emercoin-cli getnewaddress
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getnewaddress", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>getrawchangeaddress</b>
```
Returns a new Emercoin address, for receiving change.
This is for use with raw transactions, NOT normal use.

Result:
"address" (string) The address

Examples:
> emercoin-cli getrawchangeaddress
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getrawchangeaddress", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>getreceivedbyaccount "account" ( minconf )</b>
```
DEPRECATED. Returns the total amount received by addresses with <account> in transactions with at least [minconf] confirmations.

Arguments:
1. "account" (string, required) The selected account, may be the default account using "".
2. minconf (numeric, optional, default=1) Only include transactions confirmed at least this many times.

Result:
amount (numeric) The total amount in EMC received for this account.

Examples:

Amount received by the default account with at least 1 confirmation
> emercoin-cli getreceivedbyaccount ""

Amount received at the tabby account including unconfirmed amounts with zero confirmations
> emercoin-cli getreceivedbyaccount "tabby" 0

The amount with at least 6 confirmation, very safe
> emercoin-cli getreceivedbyaccount "tabby" 6

As a json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getreceivedbyaccount", "params": ["tabby", 6] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>getreceivedbyaddress "address" ( minconf )</b>
```
Returns the total amount received by the given address in transactions with at least minconf confirmations.

Arguments:
1. "address" (string, required) The emercoin address for transactions.
2. minconf (numeric, optional, default=1) Only include transactions confirmed at least this many times.

Result:
amount (numeric) The total amount in EMC received at this address.

Examples:

The amount from transactions with at least 1 confirmation
> emercoin-cli getreceivedbyaddress "1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX"

The amount including unconfirmed transactions, zero confirmations
> emercoin-cli getreceivedbyaddress "1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" 0

The amount with at least 6 confirmation, very safe
> emercoin-cli getreceivedbyaddress "1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" 6

As a json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getreceivedbyaddress", "params": ["1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX", 6] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>gettransaction "txid" ( include_watchonly )</b>
```
Get detailed information about in-wallet transaction <txid>

Arguments:
1. "txid" (string, required) The transaction id
2. "include_watchonly" (bool, optional, default=false) Whether to include watch-only addresses in balance calculation and details[]

Result:
{
"amount" : x.xxx, (numeric) The transaction amount in EMC
"fee": x.xxx, (numeric) The amount of the fee in EMC. This is negative and only available for the
'send' category of transactions.
"confirmations" : n, (numeric) The number of confirmations
"blockhash" : "hash", (string) The block hash
"blockindex" : xx, (numeric) The index of the transaction in the block that includes it
"blocktime" : ttt, (numeric) The time in seconds since epoch (1 Jan 1970 GMT)
"txid" : "transactionid", (string) The transaction id.
"time" : ttt, (numeric) The transaction time in seconds since epoch (1 Jan 1970 GMT)
"timereceived" : ttt, (numeric) The time received in seconds since epoch (1 Jan 1970 GMT)
"bip125-replaceable": "yes|no|unknown", (string) Whether this transaction could be replaced due to BIP125 (replace-by-fee);
may be unknown for unconfirmed transactions not in the mempool
"details" : [
{
"account" : "accountname", (string) DEPRECATED. The account name involved in the transaction, can be "" for the default account.
"address" : "address", (string) The emercoin address involved in the transaction
"category" : "send|receive", (string) The category, either 'send' or 'receive'
"amount" : x.xxx, (numeric) The amount in EMC
"label" : "label", (string) A comment for the address/transaction, if any
"vout" : n, (numeric) the vout value
"fee": x.xxx, (numeric) The amount of the fee in EMC. This is negative and only available for the
'send' category of transactions.
"abandoned": xxx (bool) 'true' if the transaction has been abandoned (inputs are respendable). Only available for the
'send' category of transactions.
}
,...
],
"hex" : "data" (string) Raw data for transaction
}

Examples:
> emercoin-cli gettransaction "1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d"
> emercoin-cli gettransaction "1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d" true
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "gettransaction", "params": ["1075db55d416d3ca199f55b6084e2115b9345e16c5cf302fc80e9d5fbf5d48d"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>getunconfirmedbalance</b>
```
Returns the server's total unconfirmed balance
```
<b>getwalletinfo</b>
```
Returns an object containing various wallet state info.

Result:
{
"walletversion": xxxxx, (numeric) the wallet version
"balance": xxxxxxx, (numeric) the total confirmed balance of the wallet in EMC
"unconfirmed_balance": xxx, (numeric) the total unconfirmed balance of the wallet in EMC
"immature_balance": xxxxxx, (numeric) the total immature balance of the wallet in EMC
"txcount": xxxxxxx, (numeric) the total number of transactions in the wallet
"keypoololdest": xxxxxx, (numeric) the timestamp (seconds since Unix epoch) of the oldest pre-generated key in the key pool
"keypoolsize": xxxx, (numeric) how many new keys are pre-generated
"unlocked_until": ttt, (numeric) the timestamp in seconds since epoch (midnight Jan 1 1970 GMT) that the wallet is unlocked for transfers, or 0 if the wallet is locked
"paytxfee": x.xxxx, (numeric) the transaction fee configuration, set in EMC/kB
"hdmasterkeyid": "<hash160>" (string) the Hash160 of the HD master pubkey
}

Examples:
> emercoin-cli getwalletinfo
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getwalletinfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>importaddress "address" ( "label" rescan p2sh )</b>
```
Adds a script (in hex) or address that can be watched as if it were in your wallet but cannot be used to spend.

Arguments:
1. "script" (string, required) The hex-encoded script (or address)
2. "label" (string, optional, default="") An optional label
3. rescan (boolean, optional, default=true) Rescan the wallet for transactions
4. p2sh (boolean, optional, default=false) Add the P2SH version of the script as well

Note: This call can take minutes to complete if rescan is true.
If you have the full public key, you should call importpubkey instead of this.

Note: If you import a non-standard raw script in hex form, outputs sending to it will be treated
as change, and not show up in many RPCs.

Examples:

Import a script with rescan
> emercoin-cli importaddress "myscript"

Import using a label without rescan
> emercoin-cli importaddress "myscript" "testing" false

As a JSON-RPC call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importaddress", "params": ["myscript", "testing", false] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>importmulti "requests" "options"</b>
```
Import addresses/scripts (with private or public keys, redeem script (P2SH)), rescanning all addresses in one-shot-only (rescan can be disabled via options).

Arguments:
1. requests (array, required) Data to be imported
[ (array of json objects)
{
"scriptPubKey": "<script>" | { "address":"<address>" }, (string / json, required) Type of scriptPubKey (string for script, json for address)
"timestamp": timestamp | "now" , (integer / string, required) Creation time of the key in seconds since epoch (Jan 1 1970 GMT),
or the string "now" to substitute the current synced blockchain time. The timestamp of the oldest
key will determine how far back blockchain rescans need to begin for missing wallet transactions.
"now" can be specified to bypass scanning, for keys which are known to never have been used, and
0 can be specified to scan the entire blockchain. Blocks up to 2 hours before the earliest key
creation time of all keys being imported by the importmulti call will be scanned.
"redeemscript": "<script>" , (string, optional) Allowed only if the scriptPubKey is a P2SH address or a P2SH scriptPubKey
"pubkeys": ["<pubKey>", ... ] , (array, optional) Array of strings giving pubkeys that must occur in the output or redeemscript
"keys": ["<key>", ... ] , (array, optional) Array of strings giving private keys whose corresponding public keys must occur in the output or redeemscript
"internal": <true> , (boolean, optional, default: false) Stating whether matching outputs should be be treated as not incoming payments
"watchonly": <true> , (boolean, optional, default: false) Stating whether matching outputs should be considered watched even when they're not spendable, only allowed if keys are empty
"label": <label> , (string, optional, default: '') Label to assign to the address (aka account name, for now), only allowed with internal=false
}
,...
]
2. options (json, optional)
{
"rescan": <false>, (boolean, optional, default: true) Stating if should rescan the blockchain after all imports
}

Examples:
> emercoin-cli importmulti '[{ "scriptPubKey": { "address": "<my address>" }, "timestamp":1455191478 }, { "scriptPubKey": { "address": "<my 2nd address>" }, "label": "example 2", "timestamp": 1455191480 }]'
> emercoin-cli importmulti '[{ "scriptPubKey": { "address": "<my address>" }, "timestamp":1455191478 }]' '{ "rescan": false}'

Response is an array with the same size as the input that has the execution result :
[{ "success": true } , { "success": false, "error": { "code": -1, "message": "Internal Server Error"} }, ... ]
```
<b>importprivkey "emercoinprivkey" ( "label" ) ( rescan )</b>
```
Adds a private key (as returned by dumpprivkey) to your wallet.

Arguments:
1. "emercoinprivkey" (string, required) The private key (see dumpprivkey)
2. "label" (string, optional, default="") An optional label
3. rescan (boolean, optional, default=true) Rescan the wallet for transactions

Note: This call can take minutes to complete if rescan is true.

Examples:

Dump a private key
> emercoin-cli dumpprivkey "myaddress"

Import the private key with rescan
> emercoin-cli importprivkey "mykey"

Import using a label and without rescan
> emercoin-cli importprivkey "mykey" "testing" false

Import using default blank label and without rescan
> emercoin-cli importprivkey "mykey" "" false

As a JSON-RPC call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importprivkey", "params": ["mykey", "testing", false] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>importprunedfunds</b>
```
Imports funds without rescan. Corresponding address or script must previously be included in wallet. Aimed towards pruned wallets. The end-user is responsible to import additional transactions that subsequently spend the imported outputs or rescan after the point in the blockchain the transaction is included.

Arguments:
1. "rawtransaction" (string, required) A raw transaction in hex funding an already-existing address in wallet
2. "txoutproof" (string, required) The hex output from gettxoutproof that contains the transaction
```
<b>importpubkey "pubkey" ( "label" rescan )</b>
```
Adds a public key (in hex) that can be watched as if it were in your wallet but cannot be used to spend.

Arguments:
1. "pubkey" (string, required) The hex-encoded public key
2. "label" (string, optional, default="") An optional label
3. rescan (boolean, optional, default=true) Rescan the wallet for transactions

Note: This call can take minutes to complete if rescan is true.

Examples:

Import a public key with rescan
> emercoin-cli importpubkey "mypubkey"

Import using a label without rescan
> emercoin-cli importpubkey "mypubkey" "testing" false

As a JSON-RPC call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importpubkey", "params": ["mypubkey", "testing", false] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>importwallet "filename"</b>
```
Imports keys from a wallet dump file (see dumpwallet).

Arguments:
1. "filename" (string, required) The wallet file

Examples:

Dump the wallet
> emercoin-cli dumpwallet "test"

Import the wallet
> emercoin-cli importwallet "test"

Import using the json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "importwallet", "params": ["test"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>keypoolrefill ( newsize )</b>
```
Fills the keypool.

Arguments
1. newsize (numeric, optional, default=100) The new keypool size

Examples:
> emercoin-cli keypoolrefill
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "keypoolrefill", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>listaccounts ( minconf include_watchonly)</b>
```
DEPRECATED. Returns Object that has account names as keys, account balances as values.

Arguments:
1. minconf (numeric, optional, default=1) Only include transactions with at least this many confirmations
2. include_watchonly (bool, optional, default=false) Include balances in watch-only addresses (see 'importaddress')

Result:
{ (json object where keys are account names, and values are numeric balances
"account": x.xxx, (numeric) The property name is the account name, and the value is the total balance for the account.
...
}

Examples:

List account balances where there at least 1 confirmation
> emercoin-cli listaccounts

List account balances including zero confirmation transactions
> emercoin-cli listaccounts 0

List account balances for 6 or more confirmations
> emercoin-cli listaccounts 6

As json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listaccounts", "params": [6] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>listaddressgroupings</b>
```
Lists groups of addresses which have had their common ownership
made public by common use as inputs or as the resulting change
in past transactions

Result:
[
[
[
"address", (string) The emercoin address
amount, (numeric) The amount in EMC
"account" (string, optional) DEPRECATED. The account
]
,...
]
,...
]

Examples:
> emercoin-cli listaddressgroupings
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listaddressgroupings", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>listlockunspent</b>
```
Returns list of temporarily unspendable outputs.
See the lockunspent call to lock and unlock transactions for spending.

Result:
[
{
"txid" : "transactionid", (string) The transaction id locked
"vout" : n (numeric) The vout value
}
,...
]

Examples:

List the unspent transactions
> emercoin-cli listunspent

Lock an unspent transaction
> emercoin-cli lockunspent false "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"

List the locked transactions
> emercoin-cli listlockunspent

Unlock the transaction again
> emercoin-cli lockunspent true "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"

As a json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listlockunspent", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>listreceivedbyaccount ( minconf include_empty include_watchonly)</b>
```
DEPRECATED. List balances by account.

Arguments:
1. minconf (numeric, optional, default=1) The minimum number of confirmations before payments are included.
2. include_empty (bool, optional, default=false) Whether to include accounts that haven't received any payments.
3. include_watchonly (bool, optional, default=false) Whether to include watch-only addresses (see 'importaddress').

Result:
[
{
"involvesWatchonly" : true, (bool) Only returned if imported addresses were involved in transaction
"account" : "accountname", (string) The account name of the receiving account
"amount" : x.xxx, (numeric) The total amount received by addresses with this account
"confirmations" : n, (numeric) The number of confirmations of the most recent transaction included
"label" : "label" (string) A comment for the address/transaction, if any
}
,...
]

Examples:
> emercoin-cli listreceivedbyaccount
> emercoin-cli listreceivedbyaccount 6 true
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listreceivedbyaccount", "params": [6, true, true] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>listreceivedbyaddress ( minconf include_empty include_watchonly)</b>
```
List balances by receiving address.

Arguments:
1. minconf (numeric, optional, default=1) The minimum number of confirmations before payments are included.
2. include_empty (bool, optional, default=false) Whether to include addresses that haven't received any payments.
3. include_watchonly (bool, optional, default=false) Whether to include watch-only addresses (see 'importaddress').

Result:
[
{
"involvesWatchonly" : true, (bool) Only returned if imported addresses were involved in transaction
"address" : "receivingaddress", (string) The receiving address
"account" : "accountname", (string) DEPRECATED. The account of the receiving address. The default account is "".
"amount" : x.xxx, (numeric) The total amount in EMC received by the address
"confirmations" : n, (numeric) The number of confirmations of the most recent transaction included
"label" : "label", (string) A comment for the address/transaction, if any
"txids": [
n, (numeric) The ids of transactions received with the address
...
]
}
,...
]

Examples:
> emercoin-cli listreceivedbyaddress
> emercoin-cli listreceivedbyaddress 6 true
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listreceivedbyaddress", "params": [6, true, true] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>listsinceblock ( "blockhash" target_confirmations include_watchonly)</b>
```
Get all transactions in blocks since block [blockhash], or all transactions if omitted

Arguments:
1. "blockhash" (string, optional) The block hash to list transactions since
2. target_confirmations: (numeric, optional) The confirmations required, must be 1 or more
3. include_watchonly: (bool, optional, default=false) Include transactions to watch-only addresses (see 'importaddress')
Result:
{
"transactions": [
"account":"accountname", (string) DEPRECATED. The account name associated with the transaction. Will be "" for the default account.
"address":"address", (string) The emercoin address of the transaction. Not present for move transactions (category = move).
"category":"send|receive", (string) The transaction category. 'send' has negative amounts, 'receive' has positive amounts.
"amount": x.xxx, (numeric) The amount in EMC. This is negative for the 'send' category, and for the 'move' category for moves
outbound. It is positive for the 'receive' category, and for the 'move' category for inbound funds.
"vout" : n, (numeric) the vout value
"fee": x.xxx, (numeric) The amount of the fee in EMC. This is negative and only available for the 'send' category of transactions.
"confirmations": n, (numeric) The number of confirmations for the transaction. Available for 'send' and 'receive' category of transactions.
When it's < 0, it means the transaction conflicted that many blocks ago.
"blockhash": "hashvalue", (string) The block hash containing the transaction. Available for 'send' and 'receive' category of transactions.
"blockindex": n, (numeric) The index of the transaction in the block that includes it. Available for 'send' and 'receive' category of transactions.
"blocktime": xxx, (numeric) The block time in seconds since epoch (1 Jan 1970 GMT).
"txid": "transactionid", (string) The transaction id. Available for 'send' and 'receive' category of transactions.
"time": xxx, (numeric) The transaction time in seconds since epoch (Jan 1 1970 GMT).
"timereceived": xxx, (numeric) The time received in seconds since epoch (Jan 1 1970 GMT). Available for 'send' and 'receive' category of transactions.
"bip125-replaceable": "yes|no|unknown", (string) Whether this transaction could be replaced due to BIP125 (replace-by-fee);
may be unknown for unconfirmed transactions not in the mempool
"abandoned": xxx, (bool) 'true' if the transaction has been abandoned (inputs are respendable). Only available for the 'send' category of transactions.
"comment": "...", (string) If a comment is associated with the transaction.
"label" : "label" (string) A comment for the address/transaction, if any
"to": "...", (string) If a comment to is associated with the transaction.
],
"lastblock": "lastblockhash" (string) The hash of the last block
}

Examples:
> emercoin-cli listsinceblock
> emercoin-cli listsinceblock "000000000000000bacf66f7497b7dc45ef753ee9a7d38571037cdb1a57f663ad" 6
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listsinceblock", "params": ["000000000000000bacf66f7497b7dc45ef753ee9a7d38571037cdb1a57f663ad", 6] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>listtransactions ( "account" count skip include_watchonly)</b>
```
Returns up to 'count' most recent transactions skipping the first 'from' transactions for account 'account'.

Arguments:
1. "account" (string, optional) DEPRECATED. The account name. Should be "*".
2. count (numeric, optional, default=10) The number of transactions to return
3. skip (numeric, optional, default=0) The number of transactions to skip
4. include_watchonly (bool, optional, default=false) Include transactions to watch-only addresses (see 'importaddress')

Result:
[
{
"account":"accountname", (string) DEPRECATED. The account name associated with the transaction.
It will be "" for the default account.
"address":"address", (string) The emercoin address of the transaction. Not present for
move transactions (category = move).
"category":"send|receive|move", (string) The transaction category. 'move' is a local (off blockchain)
transaction between accounts, and not associated with an address,
transaction id or block. 'send' and 'receive' transactions are
associated with an address, transaction id and block details
"amount": x.xxx, (numeric) The amount in EMC. This is negative for the 'send' category, and for the
'move' category for moves outbound. It is positive for the 'receive' category,
and for the 'move' category for inbound funds.
"label": "label", (string) A comment for the address/transaction, if any
"vout": n, (numeric) the vout value
"fee": x.xxx, (numeric) The amount of the fee in EMC. This is negative and only available for the
'send' category of transactions.
"confirmations": n, (numeric) The number of confirmations for the transaction. Available for 'send' and
'receive' category of transactions. Negative confirmations indicate the
transaction conflicts with the block chain
"trusted": xxx, (bool) Whether we consider the outputs of this unconfirmed transaction safe to spend.
"blockhash": "hashvalue", (string) The block hash containing the transaction. Available for 'send' and 'receive'
category of transactions.
"blockindex": n, (numeric) The index of the transaction in the block that includes it. Available for 'send' and 'receive'
category of transactions.
"blocktime": xxx, (numeric) The block time in seconds since epoch (1 Jan 1970 GMT).
"txid": "transactionid", (string) The transaction id. Available for 'send' and 'receive' category of transactions.
"time": xxx, (numeric) The transaction time in seconds since epoch (midnight Jan 1 1970 GMT).
"timereceived": xxx, (numeric) The time received in seconds since epoch (midnight Jan 1 1970 GMT). Available
for 'send' and 'receive' category of transactions.
"comment": "...", (string) If a comment is associated with the transaction.
"otheraccount": "accountname", (string) DEPRECATED. For the 'move' category of transactions, the account the funds came
from (for receiving funds, positive amounts), or went to (for sending funds,
negative amounts).
"bip125-replaceable": "yes|no|unknown", (string) Whether this transaction could be replaced due to BIP125 (replace-by-fee);
may be unknown for unconfirmed transactions not in the mempool
"abandoned": xxx (bool) 'true' if the transaction has been abandoned (inputs are respendable). Only available for the
'send' category of transactions.
}
]

Examples:

List the most recent 10 transactions in the systems
> emercoin-cli listtransactions

List transactions 100 to 120
> emercoin-cli listtransactions "*" 20 100

As a json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listtransactions", "params": ["*", 20, 100] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>listunspent ( minconf maxconf &#91;"addresses",...&#93; &#91;include_unsafe&#93; )</b>
```
Returns array of unspent transaction outputs
with between minconf and maxconf (inclusive) confirmations.
Optionally filter to only include txouts paid to specified addresses.

Arguments:
1. minconf (numeric, optional, default=1) The minimum confirmations to filter
2. maxconf (numeric, optional, default=9999999) The maximum confirmations to filter
3. "addresses" (string) A json array of emercoin addresses to filter
[
"address" (string) emercoin address
,...
]
4. include_unsafe (bool, optional, default=true) Include outputs that are not safe to spend
because they come from unconfirmed untrusted transactions or unconfirmed
replacement transactions (cases where we are less sure that a conflicting
transaction won't be mined).

Result
[ (array of json object)
{
"txid" : "txid", (string) the transaction id
"vout" : n, (numeric) the vout value
"address" : "address", (string) the emercoin address
"account" : "account", (string) DEPRECATED. The associated account, or "" for the default account
"scriptPubKey" : "key", (string) the script key
"amount" : x.xxx, (numeric) the transaction output amount in EMC
"confirmations" : n, (numeric) The number of confirmations
"redeemScript" : n (string) The redeemScript if scriptPubKey is P2SH
"spendable" : xxx, (bool) Whether we have the private keys to spend this output
"solvable" : xxx (bool) Whether we know how to spend this output, ignoring the lack of keys
}
,...
]

Examples
> emercoin-cli listunspent
> emercoin-cli listunspent 6 9999999 "[\"1PGFqEzfmQch1gKD3ra4k18PNj3tTUUSqg\",\"1LtvqCaApEdUGFkpKMM4MstjcaL4dKg8SP\"]"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "listunspent", "params": [6, 9999999 "[\"1PGFqEzfmQch1gKD3ra4k18PNj3tTUUSqg\",\"1LtvqCaApEdUGFkpKMM4MstjcaL4dKg8SP\"]"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>lockunspent unlock (&#91;{"txid":"txid","vout":n},...&#93;)</b>
```
Updates list of temporarily unspendable outputs.
Temporarily lock (unlock=false) or unlock (unlock=true) specified transaction outputs.
If no transaction outputs are specified when unlocking then all current locked transaction outputs are unlocked.
A locked transaction output will not be chosen by automatic coin selection, when spending emercoins.
Locks are stored in memory only. Nodes start with zero locked outputs, and the locked output list
is always cleared (by virtue of process exit) when a node stops or fails.
Also see the listunspent call

Arguments:
1. unlock (boolean, required) Whether to unlock (true) or lock (false) the specified transactions
2. "transactions" (string, optional) A json array of objects. Each object the txid (string) vout (numeric)
[ (json array of json objects)
{
"txid":"id", (string) The transaction id
"vout": n (numeric) The output number
}
,...
]

Result:
true|false (boolean) Whether the command was successful or not

Examples:

List the unspent transactions
> emercoin-cli listunspent

Lock an unspent transaction
> emercoin-cli lockunspent false "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"

List the locked transactions
> emercoin-cli listlockunspent

Unlock the transaction again
> emercoin-cli lockunspent true "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"

As a json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "lockunspent", "params": [false, "[{\"txid\":\"a08e6907dbbd3d809776dbfc5d82e371b764ed838b5655e72f463568df1aadf0\",\"vout\":1}]"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
makekeypair &#91;prefix&#93;
```
Make a public/private key pair.
[prefix] is optional preferred prefix for the public key.
```
<b>move "fromaccount" "toaccount" amount ( minconf "comment" )</b>
```
DEPRECATED. Move a specified amount from one account in your wallet to another.

Arguments:
1. "fromaccount" (string, required) The name of the account to move funds from. May be the default account using "".
2. "toaccount" (string, required) The name of the account to move funds to. May be the default account using "".
3. amount (numeric) Quantity of EMC to move between accounts.
4. (dummy) (numeric, optional) Ignored. Remains for backward compatibility.
5. "comment" (string, optional) An optional comment, stored in the wallet only.

Result:
true|false (boolean) true if successful.

Examples:

Move 0.01 EMC from the default account to the account named tabby
> emercoin-cli move "" "tabby" 0.01

Move 0.01 EMC timotei to akiko with a comment and funds have 6 confirmations
> emercoin-cli move "timotei" "akiko" 0.01 6 "happy birthday!"

As a json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "move", "params": ["timotei", "akiko", 0.01, 6, "happy birthday!"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>name_delete &lt;name&gt;</b>
```
Delete a name if you own it. Others may do name_new after this command.
```
<b>name_list &#91;name&#93; &#91;valuetype&#93;</b>
```
list my own names.

Arguments:
1. name (string, required) Restrict output to specific name.
2. valuetype (string, optional) If "hex" or "base64" is specified then it will print value in corresponding format instead of string.
```
<b>name_new &lt;name&gt; &lt;value&gt; &lt;days&gt; &#91;toaddress&#93; &#91;valuetype&#93;</b>
```
Creates new key->value pair which expires after specified number of days.
Cost is square root of (1% of last PoW + 1% per year of last PoW).
Arguments:
1. name (string, required) Name to create.
2. value (string, required) Value to write.
3. days (number, required) How many days this name will be active (1 day~=175 blocks).
4. toaddress (string, optional) Address of recipient. Empty string = transaction to yourself.
5. valuetype (string, optional) Interpretation of value string. Can be "hex", "base64" or filepath.
not specified or empty - Write value as a unicode string.
"hex" or "base64" - Decode value string as a binary data in hex or base64 string format.
otherwise - Decode value string as a filepath from which to read the data.
```
<b>name_update &lt;name&gt; &lt;value&gt; &lt;days&gt; &#91;toaddress&#93; &#91;valuetype&#93;</b>
```
Update name value, add days to expiration time and possibly transfer a name to diffrent address.

Arguments:
1. name (string, required) Name to update.
2. value (string, required) Value to write. Empty string = use previous value.
3. days (number, required) How many days to add to this name (1 day~=175 blocks).
4. toaddress (string, optional) Address of recipient. Empty string = transaction to yourself.
5. valuetype (string, optional) Interpretation of value string. Can be "hex", "base64" or filepath.
not specified or empty - Write value as a unicode string.
"hex" or "base64" - Decode value string as a binary data in hex or base64 string format.
otherwise - Decode value string as a filepath from which to read the data.
```
<b>removeprunedfunds "txid"</b>
```
Deletes the specified transaction from the wallet. Meant for use with pruned wallets and as a companion to importprunedfunds. This will effect wallet balances.

Arguments:
1. "txid" (string, required) The hex-encoded id of the transaction you are deleting

Examples:
> emercoin-cli removeprunedfunds "a8d0c0184dde994a09ec054286f1ce581bebf46446a512166eae7628734ea0a5"

As a JSON-RPC call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "removprunedfunds", "params": ["a8d0c0184dde994a09ec054286f1ce581bebf46446a512166eae7628734ea0a5"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>reservebalance &#91;&lt;reserve&gt; &#91;amount&#93;&#93;</b>
```
<reserve> is true or false to turn balance reserve on or off.
<amount> is a real and rounded to cent.
Set reserve amount not participating in network protection.
If no parameters provided current setting is printed.
```
<b>sendfrom "fromaccount" "toaddress" amount ( minconf "comment" "comment_to" )</b>
```
DEPRECATED (use sendtoaddress). Sent an amount from an account to a emercoin address.

Arguments:
1. "fromaccount" (string, required) The name of the account to send funds from. May be the default account using "".
Specifying an account does not influence coin selection, but it does associate the newly created
transaction with the account, so the account's balance computation and transaction history can reflect
the spend.
2. "toaddress" (string, required) The emercoin address to send funds to.
3. amount (numeric or string, required) The amount in EMC (transaction fee is added on top).
4. minconf (numeric, optional, default=1) Only use funds with at least this many confirmations.
5. "comment" (string, optional) A comment used to store what the transaction is for.
This is not part of the transaction, just kept in your wallet.
6. "comment_to" (string, optional) An optional comment to store the name of the person or organization
to which you're sending the transaction. This is not part of the transaction,
it is just kept in your wallet.

Result:
"txid" (string) The transaction id.

Examples:

Send 0.01 EMC from the default account to the address, must have at least 1 confirmation
> emercoin-cli sendfrom "" "1M72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd" 0.01

Send 0.01 from the tabby account to the given address, funds must have at least 6 confirmations
> emercoin-cli sendfrom "tabby" "1M72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd" 0.01 6 "donation" "seans outpost"

As a json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendfrom", "params": ["tabby", "1M72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd", 0.01, 6, "donation", "seans outpost"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>sendmany "fromaccount" {"address":amount,...} ( minconf "comment" &#91;"address",...&#93; )</b>
```
Send multiple times. Amounts are double-precision floating point numbers.

Arguments:
1. "fromaccount" (string, required) DEPRECATED. The account to send the funds from. Should be "" for the default account
2. "amounts" (string, required) A json object with addresses and amounts
{
"address":amount (numeric or string) The emercoin address is the key, the numeric amount (can be string) in EMC is the value
,...
}
3. minconf (numeric, optional, default=1) Only use the balance confirmed at least this many times.
4. "comment" (string, optional) A comment
5. subtractfeefrom (array, optional) A json array with addresses.
The fee will be equally deducted from the amount of each selected address.
Those recipients will receive less emercoins than you enter in their corresponding amount field.
If no addresses are specified here, the sender pays the fee.
[
"address" (string) Subtract fee from this address
,...
]

Result:
"txid" (string) The transaction id for the send. Only 1 transaction is created regardless of
the number of addresses.

Examples:

Send two amounts to two different addresses:
> emercoin-cli sendmany "" "{\"1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX\":0.01,\"1353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz\":0.02}"

Send two amounts to two different addresses setting the confirmation and comment:
> emercoin-cli sendmany "" "{\"1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX\":0.01,\"1353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz\":0.02}" 6 "testing"

Send two amounts to two different addresses, subtract fee from amount:
> emercoin-cli sendmany "" "{\"1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX\":0.01,\"1353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz\":0.02}" 1 "" "[\"1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX\",\"1353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz\"]"

As a json rpc call
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendmany", "params": ["", "{\"1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX\":0.01,\"1353tsE8YMTA4EuV7dgUXGjNFf9KpVvKHz\":0.02}", 6, "testing"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>sendtoaddress "address" amount ( "comment" "comment_to" subtractfeefromamount )</b>
```
Send an amount to a given address.

Arguments:
1. "address" (string, required) The emercoin address to send to.
2. "amount" (numeric or string, required) The amount in EMC to send. eg 0.1
3. "comment" (string, optional) A comment used to store what the transaction is for.
This is not part of the transaction, just kept in your wallet.
4. "comment_to" (string, optional) A comment to store the name of the person or organization
to which you're sending the transaction. This is not part of the
transaction, just kept in your wallet.
5. subtractfeefromamount (boolean, optional, default=false) The fee will be deducted from the amount being sent.
The recipient will receive less emercoins than you enter in the amount field.

Result:
"txid" (string) The transaction id.

Examples:
> emercoin-cli sendtoaddress "1M72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd" 0.1
> emercoin-cli sendtoaddress "1M72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd" 0.1 "donation" "seans outpost"
> emercoin-cli sendtoaddress "1M72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd" 0.1 "" "" true
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "sendtoaddress", "params": ["1M72Sfpbz1BPpXFHz9m3CdqATR44Jvaydd", 0.1, "donation", "seans outpost"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>sendtoname &ltname&gt; &ltamount&gt; &#91;comment&#93; &#91;comment-to&#93;</b>
```
<amount> is a real and is rounded to the nearest 0.01
```
<b>setaccount "address" "account"</b>
```
DEPRECATED. Sets the account associated with the given address.

Arguments:
1. "address" (string, required) The emercoin address to be associated with an account.
2. "account" (string, required) The account to assign the address to.

Examples:
> emercoin-cli setaccount "1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" "tabby"
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "setaccount", "params": ["1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX", "tabby"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>settxfee amount</b>
```
Set the transaction fee per kB. Overwrites the paytxfee parameter.

Arguments:
1. amount (numeric or string, required) The transaction fee in EMC/kB

Result
true|false (boolean) Returns true if successful

Examples:
> emercoin-cli settxfee 0.00001
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "settxfee", "params": [0.00001] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
```
<b>signmessage "address" "message"</b>
```
Sign a message with the private key of an address

Arguments:
1. "address" (string, required) The emercoin address to use for the private key.
2. "message" (string, required) The message to create a signature of.

Result:
"signature" (string) The signature of the message encoded in base 64

Examples:

Unlock the wallet for 30 seconds
> emercoin-cli walletpassphrase "mypassphrase" 30

Create the signature
> emercoin-cli signmessage "1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" "my message"

Verify the signature
> emercoin-cli verifymessage "1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX" "signature" "my message"

As json rpc
> curl --user myusername --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "signmessage", "params": ["1D1ZrZNe3JUo7ZycKEYQQiQAWd9y54F4XX", "my message"] }' -H 'content-type: text/plain;' http://127.0.0.1:8332/
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

