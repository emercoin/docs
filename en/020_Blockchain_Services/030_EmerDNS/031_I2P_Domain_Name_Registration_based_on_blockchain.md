# I2P Domain Name Registration with EmerDNS

Traditionally, [I2P](https://en.wikipedia.org/wiki/I2P) does not have a single domain name system. There are
several independent registrars with their own rules. Although among some
registrars there is peering, in creating a I2P website, it will still
require separate registration, and lists of hosts with different
registrars may vary greatly. In the beginning of creating I2P this situation was acceptable, and any
centralized structure was considered a single point of denial. But today, a
suitable structure already exists: Blockchain.

In the heart of the cryptocurrency [Emercoin](http://emercoin.com) is a
special version of blockchain having additional functionality that is -
recording and storing arbitrary pairs of the **name-&gt;value** pairs, [Name /
Value Storage - NVS](../Emercoin_NVS). This technology is already applied to various blockchain services, in
particular, in decentralized, uncensorable DNS zones for .lib, .emc,
.coin, .bazar, and DNS server built right into emercoin wallet.

Now we offer this technology to maintain a domain name register for I2P.

How it works.
-------------

To register a, I2P domain name put a pair inside the blockchain:

    name = i2p: myhost.i2p, value = <I2P local destination>

Local destination are has in the **Local dectination(L):** field on the [eepsite i2ptunnel configuration page](http://127.0.0.1:7657/i2ptunnel/edit.jsp?tunnel=3).

For system support there is a special registrar site - <http://emercoin.i2p>, aka <http://o6aga5qbgi555rulkuerbjzmmibupcpywownhuokl7b5s3ktmbsa.b32.i2p/>,[аddress helper](http://o6aga5qbgi555rulkuerbjzmmibupcpywownhuokl7b5s3ktmbsa.b32.i2p/?i2paddresshelper=K8DkHBpCSfsylTOZtlZ2NI9lA0cqT97YF7CJ4Zvnwp-aXmSOmumcMonr7IvXatZkg63LCNnnYBf5cJ1-23Lb2uMD3eg8VckPVbOvhYVHJnQ-p1McGOywfDE0C~5RzVI8OA36YGtiXM2JFOic3Beh8~pWHIHF1bFHkwUnuY-sVNYghDijDloKbHgqhhZmgDTV-5D46zRuqXQoma2EoK-ZALitI3PxRuJCRB9bQLK2y7iETeqjulnKsBytNsGgrl7dOiK8GXcMA7HFxcgF7qNq-2fFhLmvP6DNxdQfToQ2RNKMLfxjl7Us7jWDpYJTcNADwbJX5pzusJHhiK7aVUi1TI8efdNkeP95A7QKpi1qcBJrfT3jDYKJSKuK6MNqzYk9HbRKLRmxTzMJpdhOJWMhIsASGkTJfJFwAgZ~XDGYoQtuvQqbVokeCcczuGpL7I~0G7zt401YXaOQ6XzUTy88PWsCdLBM~RJjkCHvYgG9Od-wiBLKDy7V7kYgR1vR96liBQAEAAcAAA==)

[Link](http://o6aga5qbgi555rulkuerbjzmmibupcpywownhuokl7b5s3ktmbsa.b32.i2p/hosts.txt) for address book subscriptions settings. You may add this link to file **.i2p/addressbook/subscriptions.txt** or in the "Subscriptions" on the "Address Book" in the Web console of the router.

### emercoin.i2p has standard functionality of the I2P registrar.

-   You can download the subscription - generated from blockchain **hosts.txt**
-   You can find a host manually, through a search box.

Significantly, the registrar does not have any secret data, all is taken from blockchain and anyone can build a website registrar with a new design, additional functionality, etc. The hosts base will still be derived from the Emercoin blockchain.

What it gives.
--------------

-   One domain name space.
-   Uncensorable registration.
-   The ability to transfer the domain to another person (it was
    previously impossible to do so, traditional registrars do not allow
    to change the key).

Backup of existing domains I2P and transfering to the current owners.
---------------------------------------------------------------------

You can not just start using an empty blockchain for the registration.
The I2P network has a lot of existing websites, and cybersquatters could
capture their names and fake websites would have appeared.

In order to avoid this, there is a special procedure for transferring of
existing names into the hands of their respective owners. Names,
existing in I2P on *11/05/2016* collected from major registrars, have been
registered by the Emercoin team to protect them from cybersquatters. Now
everything is ready for transferring these names to their owners.
Absolutely free.

If you have a website in the I2P network, go to <http://emercoin.i2p> and enter the name of your website into the search box.

You should see a similar inscription:

```
Domain rus.i2p is protected from cyber squatters!
If you are domain owner, you can take ownership of this domain by placing special file emertransfer.txt
into the root of yout site to initiate domain transfer. See transfer manual.
```

This means that everything is fine. You can take a control of the domain
account right now.

-   [Download](https://sourceforge.net/projects/emercoin/files/) and
    install the Emercoin Core Wallet. There are versions for Linux
    and Windows, GUI and daemon – whatever is more comfortable.
-   Generate an address in your wallet (let's assume for this explanation that your address
    is **EMRMAYQUNDArzVKZX7WLyzRvVpD98qEjGQ**).
-   Sign the <u>new</u> address your host name (e.g. let's assume it is **fs.i2p**)
    -   In the GUI client console (menu "Help" - "Debug window" -
        "Console") type:

            signmessage EMRMAYQUNDArzVKZX7WLyzRvVpD98qEjGQ fs.i2p

    -   In the case you are using the command-line daemon:

            emercoind signmessage EMRMAYQUNDArzVKZX7WLyzRvVpD98qEjGQ fs.i2p

    -   You will get back a signature, e.g: **H19woLpZPERqGiGkEK2J3QwMzSCcJIRZQftTTTzwHT9ACQwoOjpC8GrGegA5TF78Ny0kI3JGFyHwRnjamqY / 9rk =**
    
    -   Create a **emertransfer.txt** file in the root of your website, and write down the following lines:

            I2P fs.i2p
            EMC EMRMAYQUNDArzVKZX7WLyzRvVpD98qEjGQ
            SIG H19woLpZPERqGiGkEK2J3QwMzSCcJIRZQftTTTzwHT9ACQwoOjpC8GrGegA5TF78Ny0kI3JGFyHwRnjamqY / 9rk =

    -   In a while our robot will check the signature. If it converges, it will give the domain name to the specified address.

That's it!

*Warning: The EMC address above is written only for example. You must use your own emercoin address, generated in your wallet.*

How to register a new name
--------------------------

For example, your I2P site named **example.i2p**.

-   It is needed to
    [download](https://sourceforge.net/projects/emercoin/files/) and run
    the Emercoin Wallet.
-   Your wallet must contain a small amount of EMC from somewhere (e. g. 0.3 EMC).
    For example, you may buy this on many cryptocurrency marketpaces or
    in the cryptocurency exchanges.
-   Create new name in the emercoin's blockchain:
    -   In the Emercoin-QT:
        -   Open [eepsite i2ptunnel configuration
            page](http://127.0.0.1:7657/i2ptunnel/edit.jsp?tunnel=3)
        -   Check the content of the field "Website name" -- should
            be "example.i2p".
        -   Copy the hash of site - content of the field "Local
            destination(L):" - to clipboard.
        -   Open the main window of the Emercoin-QT (EmerCoin Client).
        -   Click "Manage names".
        -   Write "i2p:example.i2p" into field "name:" (this is name of
            your i2p site prefixed with "i2p:").
        -   Write 3652 into field "days:" (or write here another period
            of address reservation).
        -   Paste hash of site to field "value (0%):".
        -   Click "name\_new".
    -   In the emercoind:
        -   Open [eepsite i2ptunnel configuration
            page](http://127.0.0.1:7657/i2ptunnel/edit.jsp?tunnel=3)
        -   Check the content of the field "Website name" -- should
            be "example.i2p".
        -   Copy the hash of site - content of the field "Local
            destination(L):" - to clipboard.
        -   Open the console of the command processor (bash in the
            GNU/Linux, CMD in the Windows)
        -   Type **emercoind name_new "i2p:example.i2p"**, paste site hash from clipboard, type 3652 and then press **enter**:

            ```text
            emercoind name_new "i2p:example.i2p" <site_hash_from_clipboard> 3652
            ```
            

-   The action "name\_new" will generated transaction, where amount of
    0.2~0.3 EMC will be used for registration the name
    "i2p:example.i2p" with specified address.
-   Some time later your transaction will be confirmed and the name of
    the site "example.i2p" will be registered for you for 10 years
    (3652 days).

