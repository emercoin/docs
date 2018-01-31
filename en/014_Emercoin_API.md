<div style="overflow:hidden;"><img style="float:left;" src="Gui-debug-console.png" alt="The debug console in the emercoin-qt GUI" width="512"></div>

# Emercoin API

As with [Bitcoin](https://en.bitcoin.it/wiki/Running_Bitcoin), Application programming interface (API) is available via:

-   the "debug console" in Emercoin Core GUI](../Install_Software/Emercoin_Core/GUI_wallet).
-   [JSONRPC](https://en.bitcoin.it/wiki/API_reference_%28JSON-RPC%29), per settings in your <b>emercoin.conf</b>.
-   Directly on the command line interface (emercoin-cli).

API commands
------------

The API allows you or applications to query the blockchain and send transactions, etc. For example, to check on your EMC balance and status of the blockchain you type: 

	$ emc getinfo
	
Or to get a list of all possible commands:	

	$ emc help

The following API commands are accurate as of Emercoin Core version <b>v0.6.2.0</b>:

```text
== Blockchain ==
getbestblockhash
getblock "hash" ( verbose )
getblockchaininfo
getblockcount
getblockhash index
getchaintips
getdifficulty
getmempoolinfo
getrawmempool ( verbose )
gettxlistfor <from block> <to block> <address> [type=0] [verbose=0]
gettxout "txid" n ( includemempool )
gettxoutsetinfo
name_filter [regexp] [maxage=0] [from=0] [nb=0] [stat] [valuetype]
name_history <name> [fullhistory] [valuetype]
name_mempool [valuetype]
name_scan [start-name] [max-returned] [max-value-length=-1] [valuetype]
name_show <name> [valuetype] [filepath]
verifychain ( checklevel numblocks )

== Control ==
getinfo
help ( "command" )
reservebalance [<reserve> [amount]]
stop

== Generating ==
getgenerate
gethashespersec
setgenerate generate ( genproclimit )

== Mining ==
getauxblock [<hash> <auxpow>]
getblocktemplate ( "jsonrequestobject" )
getmininginfo
getnetworkhashps ( blocks height )
prioritisetransaction <txid> <priority delta> <fee delta>
submitblock "hexdata" ( "jsonparametersobject" )

== Network ==
addnode "node" "add|remove|onetry"
getaddednodeinfo dns ( "node" )
getcheckpoint
getconnectioncount
getnettotals
getnetworkinfo
getpeerinfo
ping

== Rawtransactions ==
createrawtransaction [{"txid":"id","vout":n},...] {"address":amount,...}
decoderawtransaction "hexstring"
decodescript "hex"
getrawtransaction "txid" ( verbose )
sendrawtransaction "hexstring" ( allowhighfees )
signrawtransaction "hexstring" ( [{"txid":"id","vout":n,"scriptPubKey":"hex","redeemScript":"hex"},...] ["privatekey1",...] sighashtype )

== Util ==
createmultisig nrequired ["key",...]
estimatefee nblocks
estimatepriority nblocks
validateaddress "emercoinaddress"
verifymessage "emercoinaddress" "signature" "message"

== Wallet ==
addmultisigaddress nrequired ["key",...] ( "account" )
backupwallet "destination"
dumpprivkey "emercoinaddress"
dumpwallet "filename"
encryptwallet "passphrase"
getaccount "emercoinaddress"
getaccountaddress "account"
getaddressesbyaccount "account"
getbalance ( "account" minconf includeWatchonly )
getnewaddress ( "account" )
getrawchangeaddress
getreceivedbyaccount "account" ( minconf )
getreceivedbyaddress "emercoinaddress" ( minconf )
gettransaction "txid" ( includeWatchonly )
getunconfirmedbalance
getwalletinfo
importaddress "address" ( "label" rescan )
importprivkey "emercoinprivkey" ( "label" rescan )
importwallet "filename"
keypoolrefill ( newsize )
listaccounts ( minconf includeWatchonly)
listaddressgroupings
listlockunspent
listreceivedbyaccount ( minconf includeempty includeWatchonly)
listreceivedbyaddress ( minconf includeempty includeWatchonly)
listsinceblock ( "blockhash" target-confirmations includeWatchonly)
listtransactions ( "account" count from includeWatchonly)
listunspent ( minconf maxconf  ["address",...] )
lockunspent unlock [{"txid":"txid","vout":n},...]
makekeypair [prefix]
move "fromaccount" "toaccount" amount ( minconf "comment" )
name_delete <name>
name_list [name] [valuetype]
name_new <name> <value> <days> [toaddress] [valuetype]
name_update <name> <value> <days> [toaddress] [valuetype]
dumpprivkey "emercoinprivkey"
sendfrom "fromaccount" "toemercoinaddress" amount ( minconf "comment" "comment-to" )
sendmany "fromaccount" {"address":amount,...} ( minconf "comment" )
sendtoaddress "emercoinaddress" amount ( "comment" "comment-to" )
sendtoname <name> <amount> [comment] [comment-to]
setaccount "emercoinaddress" "account"
settxfee amount
signmessage "emercoinaddress" "message"
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
