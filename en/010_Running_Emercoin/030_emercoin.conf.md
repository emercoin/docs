# emercoin.conf

In addition to providing arguments on the command-line during program launch, all Emercoin's command-line arguments may be specified in the `emercoin.conf` configuration file instead. Arguments given on the command-line override values set in the configuration file. As with Bitcoin, the configuration file is a list of _name=value_ pairs, one per line, with optional comments starting with the _#_ character.

The `emercoin.conf` configuration file is not always automatically created (depending on how you installed Emercoin); you can create it using your favorite plain-text editor. By default, Emercoin (or emercoind) will look for a file named `emercoin.conf` in the emercoin [data directory](https://en.bitcoin.it/wiki/Data\_directory), but both the data directory and the configuration file path may be changed using the `-datadir` and `-conf` command-line arguments.

The default location of emercoin.conf depends on your operating system:

Operating System|configuration directory
----------------|---------------
Windows XP				|`C:\Documents and Settings\<username>\Application Data\Emercoin\emercoin.conf`
Windows Vista, 7, 10	|`C:\Users\<username>\AppData\Roaming\Emercoin\emercoin.conf`, (or in the same directory as your emercoin-qt.exe)
Linux                	|`/home/<username>/.emercoin/emercoin.conf`
Mac OSX                	|`/Users/<username>/Library/Application Support/Emercoin/emercoin.conf`

_Note: When installing [EmerWEB](../Install_Software/Core_Wallets/EmerWEB_wallet), the location is `/var/lib/emc/.emercoin/emercoin.conf`._

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


