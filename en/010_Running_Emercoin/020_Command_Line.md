# Command-line arguments

Options can be set when launching emercoin via the command-line, or specified in [emercoin.conf](emercoin.conf).

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
