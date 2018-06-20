<div class="boxOverflow">
<img src="/images/NVS_logo.png" alt="NVS logo" width="256">
</div>

# The Emercoin NVS

Emercoin provides a service for storing **name-&gt;value** pairs in its blockchain (Name-Value Storage, or NVS). The initial concept was inherited from the <a target="_blank" rel="nofollow" href="http://namecoin.info">NameCoin</a> cryptocurrency yet while NameCoin is mostly focused on supporting decentralized domain zone **\*.bit** in their extension, Emercoin provides a universal, extensible service to store and maintain **name-&gt;value** pairs without imposing a narrow specialization.

Of course, Emercoin supports distributed <a target="_blank" rel="nofollow" href="http://en.wikipedia.org/wiki/Alternative_DNS_root">alternative DNS service</a> too, and each Emercoin wallet contains a built-in simple DNS server, supporting the standard <a target="_blank" rel="nofollow" href="https://www.ietf.org/rfc/rfc1034.txt">RFC1034</a> UDP DNS protocol.

NVS overview
------------
Emercoin stores data in the blockchain by a set of **name-&gt;value**
pairs:

-   **name** - label for the stored data, up to a length of 512 bytes.
-   **value** - the data itself, up to a length of 20\*1024 (20kb).

Emercoin allocates up to 20kB for **value**, enough to fit public keys
for most modern cryptographic applications. We consider a cryptocurrency
blockchain to be an extremely reliable place to publish and maintain
public keys for many cryptographic applications such as SSH/SSL
certificates. Like regular payment transactions, NVS pairs stored in the
blockchain also get confirmations during block generation, and are
virtually immune to being altered in a <a target="_blank" rel="nofollow" href="http://en.wikipedia.org/wiki/Man-in-the-middle_attack">Man-In-the-Middle attack</a>.

Since the blockchain is a trusted data store protected from unauthorized
modification it is a great foundation for the deployment of
cryptographic Public Key Infrastructure
(<a target="_blank" rel="nofollow" href="http://en.wikipedia.org/wiki/Public_key_infrastructure">PKI</a>), Digital
Proof-of-Ownership (DPO), immutable recordkeeping, timestamps, and other
distributed services.

The Emercoin blockchain will accept NVS pairs without any restrictions
to the data format of either the name or value. However, for
standardization purposes we recommend the following format for names:

	<service_abbreviation>:<unique_key>

For example:

    dns:emercoin.com

Each NVS pair has its owner. Each owner is specified by the Emercoin
payment address stored together with the pair. Only the owner of the
payment address is able to modify or delete the pair, or transfer
ownership to another address. When a new pair is created, a new payment
address for the pair is created in the local wallet.

You can manage NVS entries either through the Emercoin <a target="_blank" rel="nofollow" href="https://emercoin.com/benefits#download">wallet GUI</a>, or via the
[emercoin-cli](/en/running-emercoin/command-line.md).

Service abbreviations
--------------
While you are free to create your own services using Emercoin's NVS, we
recommend using the following supported service abbreviations:

  Service abbreviation  | Service description                                                    | Associated Emercoin Service
  ----------------------|------------------------------------------------------------------------|-----------------------------------
  dns                   | DNS record                                                             |  [EmerDNS](/en/blockchain-services/emerdns/emerdns-introduction.md)
  ssh                   | SSH public key                                                         |  [EmerSSH](/en/blockchain-services/emerssh.md)
  gpg                   | GNU PGP public key|
  kx                    | <a target="_blank" rel="nofollow" href="http://tools.ietf.org/html/rfc2230">[RFC2230</a>]() public key|
  ssl                   | SSL Certificate                                                        |  [EmerSSL](/en/blockchain-services/emerssl/emerssl-introduction.md)
  bls                   | BLS digital signature public key
  tts                   | <a target="_blank" rel="nofollow" href="http://en.wikipedia.org/wiki/Trusted_timestamping">Trusted Timestamp</a>  | EmcTTS
  lnx                   | Advertising Link Exchanger                                              | [EmerLNX](/en/blockchain-services/emerlnx.md)
  dpo                   | Digital Proof-of-Ownership                                              | [EmerDPO](/en/blockchain-services/emerdpo/emerdpo-introduction.md)
  magnet                | BitTorrent magnet links                                                 | [EmerMAGNET](/en/blockchain-services/emermagnet.md)
  swift                 | Bank's branch info for SWIFT transfers
  enum                  | <a target="_blank" rel="nofollow" href="http://www.voip-info.org/wiki/view/ENUM">ENUM telephone record</a>     | [ENUMER](/en/blockchain-services/enumer.md)

Managing NVS entries with the GUI
-------------

<div class="boxOverflow">
	<img src="/images/NVS_UI.jpg" alt="Emercoin's 'Manage Names' tab." width="756">
</div>
<br>

The "Manage Names" tab includes the following elements:

-   **name:** If this NVS entry will be used with a particular [service
    abbreviation](#page_service-abbreviations) (dns:, ssl:,
    ssh:, etc) then characters allowed by the appropriate service prefix
    should be used. e.g.

<!-- -->

    dns:example.coin

-   **days:** How many days to register the name (between 1 and 9999).
    Upon expiration, the name can be taken by another user.

<!-- -->

-   **Operation type:**
    -   **NAME\_NEW** - create a new name.
    -   **NAME\_UPDATE** - update values, change owner, or extend
        the registration.
    -   **NAME\_DELETE** - delete a name.

<!-- -->

-   **value:** To be filled with the content to be associated with
    the name. The percentage indicator shows how much of the 20kb
    maximum space is used. This field can contain ANY type of data,
    although conventions should be observed when the name-value pair is
    to be used by a particular service. e.g.

<!-- -->

    A=192.168.0.123|TXT=example website

-   **Import:** This button allows you to choose any file (not more than
    20kb), to be inserted in the **value** field.

<!-- -->

-   **new address:** To enter the EMC-address you wish to transfer the
    name to. Applicable only for the **NAME\_UPDATE** operation.

<!-- -->

-   **Submit:** This button confirms the operation and submits the data
    to the Emercoin blockchain.

<!-- -->

-   **Names in your wallet:** This table displays a list of your names.
    Yellow fields indicate the name is pending or when less than a month
    remains before expiry. Red fields indicate expired names.

<!-- -->

-   **Filters:**
    -   **Owned by me** - displays only names owned by the wallet.
    -   **Owned by others** - displays names transferred to others.
    -   **Expired** - displays expired names previously owned by
        the wallet.

Managing NVS entries with the command line
----------------------------------

Below is the list of
[Emercoin API](/en/emercoin-api.md) commands for
managing NVS entries. Parameters in square brackets [ ] are optional.

	name_new <name> <value> <days> [toaddress]

Create an NVS pair and publish it into the blockchain.
- `days` : initial lease time in days.

---

	name_update <name> <value> <days> [toaddress]

Update the value for an existing name.
- `days` : adds lease days.
- `toaddress` : transfer name ownership to another Emercoin address.

---

    name_delete <name>

Delete an NVS pair from the blockchain.

---
    
    name_show <name>

Retrieve an NVS pair and transaction info for specified `name`:

---

    name_list [<name>]
   
List all matching NVS pairs belonging to the current wallet and those that were owned in the past. If `name` is not specified, then it lists all names:

---

    name_scan [start-name] [max-returned]

List NVS pairs existing in the blockchain, returning `max-returned` entries (default 500):
- `start-name` : An integer. Skip this number of names. This is useful to download the list in chunks.

---

    sendtoname <name> <amount> [comment] [comment-to]

Send an EMC payment to the address associated with the specified <name>. For instance, send a donation to the owner of a EmerDNS address of a website you visit:
- `amount` : EMC amount, rounded to the nearest 0.01.
- `comment` and `comment-to` : will be stored in the local wallet, not in the blockchain.

---

	name_filter [regexp] [maxage=0] [from=0] [nb=0] 

Scan and filter names.
- `regexp` : apply `regexp` on names, empty means all names.
- `maxage` : look in last `maxage` blocks.
- `from` : show results from number `from`.
- `nb` : show `nb` results, 0 means all.
- `stat` : show some stats instead of results.

---

    name_history <name>

Look up the current and all past data history for the given name:

---

*Note: The above list is simplified. Detailed help for each API command is available in the Emercoin software itself.* 

NVS Storage Fees
-----------
The price of inserting data into the blockchain is computed by the
formula:

    p = sqrt(0.01 * R * y) + s / 128

Where:

-   R = Current Proof-of-work reward, in cents (EMc).
-   y = Lease time, in years. Available by 1 day fractions.
-   s = key value size, in bytes. Division is integer, so for entries,
    less than 128 bytes, this price part is zero.
-   The cost of creating a new name is equal to the cost of a 1
    year lease.

For example, on Sep 30 2014 the PoW reward was 140EMC, or 14000EMC cents
(EMc).

So if you wanted to lease a name (length 100 bytes) for 1 year, you
would have paid **0.17EMC**:

    p = sqrt(0.01 * 14000 * (1[create new name] + 1[one year lease])) + (floor)(100 / 128) = 17EMc = 0.17EMC

All fees are "burnt" and become unrecoverable (transaction output is
less than input).

NVS name as a payment alias
----------------
It is possible to send EMC currency directly to a name, without
knowing the address.

To create a name alias for payment address, just create an NVS pair with
a specified unique name and any value. We recommend entering a text
description as the value.

All payments made to that name will be sent to the appropriate payment
address, to which the name is registered. e.g:

    emc name_new "folding@home" "Donation to support participants of folding@home project from Stanford University" 365

