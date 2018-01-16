# Running Emercoin

Linux Quickstart
----------------

The simplest way to start from scratch with the command line client,
automatically syncing blockchain and creating a wallet, is to just run
this command (without arguments) from the directory containing your
emercoind binary:

	$ ./emercoind

To run with the standard GUI interface:

	$ ./emercoin-qt

Command-line arguments
----------------------

Options can be set when launching emercoin via the command-line, or specified in [emercoin.conf](Running_Emercoin).

You can check your version for a list of available commands by invoking emercoin with the argument _"-?"_ or _"-help"_. e.g:

    $ ./emercoind -help

The following command-line arguments are available as of Emercoin Core version **v0.6.3.1**:

```text
Options:
  -?                     This help message
  -conf=<file>           Specify configuration file (default: emercoin.conf)
  -datadir=<dir>         Specify data directory
  -testnet               Use the test network
  -regtest               Enter regression test mode, which uses a special chain in which blocks can be solved instantly. This is intended for regression testing tools and app development.
  -rpcconnect=<ip>       Send commands to node running on <ip> (default: 127.0.0.1)
  -rpcport=<port>        Connect to JSON-RPC on <port> (default: 6662 or testnet: 6662)
  -rpcwait               Wait for RPC server to start
  -rpcuser=<user>        Username for JSON-RPC connections
  -rpcpassword=<pw>      Password for JSON-RPC connections

SSL options: (see the Bitcoin Wiki for SSL setup instructions)
  -rpcssl                Use OpenSSL (https) for JSON-RPC connections
```
One important argument not listed in the help is _reservebalance_:

```text
  -reservebalance=<number>  Reserves a given amount of coins in your wallet, excluding them from participating in Proof-of-Stake minting.
```
_Note: Not all commands are listed in the help at the time of writing, and you should check the help in your version, in case they have been updated. Emercoin is originally derived from the Bitcoin project, so you may find additional configuration arguments at <https://en.bitcoin.it/wiki/Running_Bitcoin></i>_

emercoin.conf
-------------

In addition to providing arguments on the command-line during program launch, all Emercoin's command-line arguments may be specified in the `emercoin.conf` configuration file instead. Arguments given on the command-line override values set in the configuration file. As with Bitcoin, the configuration file is a list of _name=value_ pairs, one per line, with optional comments starting with the _#_ character.

The `emercoin.conf` configuration file is not always automatically created (depending on how you installed Emercoin); you can create it using your favorite plain-text editor. By default, Emercoin (or emercoind) will look for a file named `emercoin.conf` in the emercoin [data directory](Running_Emercoin), but both the data directory and the configuration file path may be changed using the `-datadir` and `-conf` command-line arguments.

The default location of emercoin.conf depends on your operating system:

Operating System|configuration directory
----------------|---------------
Windows XP				|`C:\Documents and Settings\<username>\Application Data\Emercoin\emercoin.conf`
Windows Vista, 7, 10	|`C:\Users\<username>\AppData\Roaming\Emercoin\emercoin.conf`, (or in the same directory as your emercoin-qt.exe)
Linux                	|`/home/<username>/.emercoin/emercoin.conf`
Mac OSX                	|`/Users/<username>/Library/Application Support/Emercoin/emercoin.conf`

_Note: When installing [EmcWEB](../Install_Software/Emercoin_Core), the location is `/var/lib/emc/.emercoin/emercoin.conf`._

### Example emercoin.conf
```text
rpcuser=emccoinrpc
rpcpassword=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
listen=1
server=1
rpcallowip=0.0.0.0/0
rpcport=6662
maxconnections=80
gen=0
daemon=1
rpcssl=1
reservebalance=0
rpcsslcertificatechainfile=/etc/ssl/emc/emercoin.crt
rpcsslprivatekeyfile=/etc/ssl/emc/emercoin.key
rpcsslciphers=HIGH:!aNULL:!eNULL:!EXPORT:!DES:!MD5:!PSK:!RC4:!SSLv2
```
_Note: you may find additional .conf file examples at <https://en.bitcoin.it/wiki/Running_Bitcoin>_

Emercoin ports
--------------

The following ports are used by emercoin core client, so you may need to adjust your firewall accordingly:

<table>
<tr><td>P2P</td><td>6661</td></tr>
<tr><td>RPC</td><td>6662</td></tr>
<tr><td>testnet P2P</td><td>6663</td></tr>
</table>

The Emercoin test network
---------------------

<div style="overflow:hidden;"><img style="float:left;" src="../../images/EMC-testnet.png" alt="Emercoin testnet" width="256"></div>
<br>
The Emercoin testnet is a separate network used for testing upcoming
releases and new features.

-   To run in testnet mode, start the client with the
    `-testnet` argument.
-   The testnet blockchain will be stored in the `/testnet` directory.
-   If you need testnet coins, contact the Emercoin developers.

See Also
--------

-   [Data directory](https://en.bitcoin.it/wiki/Data\_directory)

