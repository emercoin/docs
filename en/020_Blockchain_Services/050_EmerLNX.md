# EmcLNX

Introduction
------------

EMCLNX is a peer-to-peer text-based advertisement link exchange network
based on a per-click payment model. EMCLNX operates under the **"lnx"**
service abbreviation in the [Emercoin NVS](Emercoin_NVS).

> Unfortunately the EMCLNX project is temporarily frozen until it can be
> further developed.

There are 3 roles in the EMCLNX system:

-   **Buyer** : Advertises their website using the EMCLNX network. They
    pay a small amount of funds for each Visitor referred to their site
    by the EMCLNX network.

-   **Host** : Displays EMCLNX advertisements on their website. When a
    Visitor clicks an ad, the Host sends this Visitor to the Buyer's
    website and receives payment from the Buyer for this visit.

-   **Visitor** : An ordinary web-user who clicks on an advertisement on
    the Host's website and arrives at the Buyer's website.

In the EMCLNX system, a **Buyer** directly pays each **Host** for each
**Visitor**. There is no central agent to set a minimum price, allowed
words, etc, and there is no participation fee or commission. All
payments go directly from the Buyers to Hosts, without the involvement
of any intermediate agent.

An EMCLNX participant can be a **Buyer** and **Host** at the same time,
i.e. they can show advertising links on their website, and also purchase
traffic (visits) from the EMCLNX network. Hence, they can pay other
participants to attract visitors to their site, while earning money for
sending visitors to other sites.

EMCLNX runs on the Emercoin cryptocurrency and uses it in two ways:

-   It uses Emercoin ([EMC](../Introduction/The_EMC_Currency) as the payment unit for
    pay-per-click actions.
-   It uses the [Emercoin NVS](Emercoin_NVS) as distributed
    storage for advertising contracts.

Installation
------------

1.  You need to be running a php-enabled web-server with MySQL on linux.
    This is a common setup for modern websites, so we will skip
    installation instructions for this and assume you already have
    this running.

2.  You need to [install the Emercoin wallet
    daemon](../Install_Software/Core_Wallets/CLI_daemon) on your web server.

EMCLNX uses the [emercoin API](../Emercoin_API)
JSONRPC interface, so ensure you have set suitable parameters related to
RPC access in your daemon's
[emercoin.conf](../Running_Emercoin/emercoin.conf) file, namely:
**rpcuser**, **rpcpassword**, **rpcport**, and **rpcallowip**.

After starting the daemon, download and unzip the EMCLNX archive from
the [EMCLNX github
repository](https://github.com/emercoin/emclnx/releases/latest).

After unzip, there will be two subdirectories:

-   **emclnx-0.0.6/emclnx** - for website modules
-   **emclnx-0.0.6/adm** - for administrative/setup tools

Go to the **/adm** directory to perform some initial operations:

1.  Create a username and the database for EMCLNX. The file
    **emclnx\_create\_db.sql** contains the appropriate commands.
    Substitute default password 12345 with something secure.

2.  Edit the script **create\_tables.sh**, by changing default password
    12345 to the password you used above. Now run this script. This
    script will create database tables for EMCLNX.

3.  Edit the file **emclnx-config.php** and modify the following lines
    to set your password and config params for your system:

        'url'     => "http://user:password@localhost:8774";,
        'db_pass' => "12345",
        'dest_url'   => "http://www.emercoin.com/";,

    The last parameter contains the URL of your site, where **Visitors**
    will be sent. Refer to the **emclnx-config.php** file itself for
    more information and options.

4.  From your www directory, make a symbolic link to the emclnx
    directory that you unzipped earlier. This is needed so that web
    users can run php scripts located in the emclnx directory. The
    destination link must be absolute. Paths for your system can differ
    but the command should be similar to this:

        $ ln -s /home/root/emclnx-0.0.6/emclnx /var/www/emclnx

5.  In addition, you need to create a log file, and give the www user
    write access to it. To do this, run commands similar to:

        $ touch /var/log/emclnx.log
        $ chown www /var/log/emclnx.log

### Installation for Host

1. To start hosting EMCLNX advertisements, you will need to edit the file
**emclnx/emclnx-config.php**. Modify the sections **keywords, langs,
country**, and **min\_cpc**. See comments for appropriate parameters.

2. Next, you need to import advertising contracts from the Emercoin
blockchain into your local database, and assign them priorities. To do
this, just go to the emclnx **/adm** directory and run:

        $ php ./fetch_contracts.php

3. Next, go to the emclnx symlink directory, with the appropriate command,
e.g.:

        $ cd /var/www/emclnx

   and run:

        $ php ./user_page.php

If everything is OK, the program will print a link from a random
advertising contract.

The program code is simple; you should review it and then integrate it
into your website.

After integrating the code into your website, visit your site from the
internet and confirm that your page contains an EMCLNX advertisement
link. Click it... and you will earn a small amount of Emercoin!

**Don't click too quickly or often. The system can detect fraudulent
behavior, and Buyers will ban you!**

Note: It's a good idea to run **./fetch_contracts.php** daily (or even
hourly) with [crontab](https://en.wikipedia.org/wiki/Crontab), to
automatically import new contracts.

### Installation for Buyer

To use EMCLNX as a **Buyer**, you will need to deposit some
[EMC](../Introduction/The_EMC_Currency) into your emercoind wallet - the system will use
these funds to pay **Hosts** for the **Visitors** who are referred to
you.

In addition, you need to use the Emercoin
Core wallet (GUI wallet is easiest) to manage
advertisement contracts and signatures. Of course, if needed, you can
use a single wallet for all functions, but it's more practical to use
two independent wallets - one for payment, another for contract
management.

1. Generate an EMC wallet address, and deposit this address into the
**TXT** field of your domain name's [DNS
record](https://en.wikipedia.org/wiki/DNS_record), in the following
format:

        emclnx=<emc_address>

    For example, see [dig](https://en.wikipedia.org/wiki/Dig_(command))
output for domain emercoin.com:

        $ dig emercoin.com TXT | grep emclnx
        emercoin.com.       299 IN  TXT "emclnx=EasxHoQ3xs33nZZoLWDnKMRDsafF9ZdqQq"

    The domain can be a regular ICANN or [EmerDNS](./EmerDNS/EmerDNS_Introduction) domain.

    Note: It is OK if multiple Hosts or contracts use the same EMC address.

2. Select some unique name for your contract, for example:
**MyFirstContract**. You will need to check if this name is available by
using the [name\_show](../Emercoin_API) command
in the Emercoin wallet. You can do this in the GUI wallet's debug window
by entering the command:

        name_show lnx:MyFirstContract

    If you see an error message that the name was not found, then everything
is OK (the name is not taken yet).

3. Generate a signature for your contract using the EMC address you
generated above, using the
[signmessage](../Emercoin_API) command. e.g:

        signmessage EdvJ7b7zPL6gj5f8VNfX6zmVcftb35sKX2 MyFirstContract

    The wallet returns a signature, like:

        H1XLT7lj1UUIfsdUxr9uE5EZz0sCYcjBnLivrgdOeDTIQGa2D27KHwH4=

    This is the signature for your new contract. This signature is proof
that this contract came into the system from you (the domain owner), not
from a bad actor.

4. Create an advertising contract with a text editor. See the following
example contract and explanation:

    ```text
    URL=http://emercoin.com/emclnx/lnx_pay.php?
    SIGNATURE=H1XLT7lj1UUIfsdUxr9uE5EZz0sCYcjBnLivrgdOeDTIQGa2D27KHwH4=
    LANG=EN
    COUNTRY=US,EU,RU
    CPC=3.00
    KEYWORDS=emercoin|cryptocurrency mining|name-value storage
    TXT=Emercoin - Innovative cryptocurrency
    TXT=Emercoin - Innovative distributed blockchain services
    TXT=Emercoin - Distributed uncensored alternative DNS
    TXT=Emercoin - Decentralized security solutions
    TXT=Emercoin - Cryptocurrency with a strong fundamental base
    ```

    **SIGNATURE** : The contract signature (generated above). Confirms this
contract is valid for your specific domain.

    **LANG** : Contract language (must be single). If you run a multilingual
site, and need ads for many languages, generate separate contracts for
ads in each language.

    **COUNTRY** : Target
[country](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). This is an
optional field. If used, your ads will be displayed in specified
countries only. If omitted there are no country limits.

    **KEYWORDS** : Keywords that can help the host's scripts to make better
decisions about which advertiements to display. Keywords on the same
line are separated by the pipe cheracter "|" and multiple lines can be
defined.

    **CPC** : Cost Per Click. How many EMC you will pay to
the **Host** for each **Visitor** (actual amount can be less, if you
(the **Buyer**) and the **Host** have not established a good "credit
relationship" yet).

    **TXT** : These are the text strings for your actual advertisements.
Strings are randomly shown on Host's websites, shown one per exposure.
Multiple TXT lines can be defined as shown in the example.

    Save the text file where convenient. e.g. **/adm/MyFirstContract**

5. Before your installation will accept payment requests for your contract,
you will need to add it to your local ENCLNX database. To do this, run
**uplo_contract.php** in the **/adm** directory:

        $ php ./uplo_contract.php <contract> <CPC>

    For example:

        $ php ./uplo_contract.php MyFirstContract 3.00

6. Publish your EMCLNX contract into the [Emercoin
NVS](Emercoin_NVS). It is easiest to do this using the GUI
wallet, under the "Manage Names" tab.

    -   For **"name"** : enter your contract name under the **"lnx"**
        service abbreviation, e.g: **lnx:MyFirstContract**

    -   For **"value"** : copy/paste your contract from the text file you
    created above. During the paste process the wallet's GUI
    automatically converts non-ASCII symbols to UTF-8. Alternatively,
    you can use the "Import" button in the GUI. In this case, be sure
    your file is saved with US-ASCII charset, or UTF-8.

    -   For **"days:"** enter an appropriate time for your
    contract's lifespan.

    <br>Finally, click "Submit"... and wait for visitors!!!

How it works
------------

The **Buyer** creates a contract and signature, and publishes it in the
Emercoin blockchain. The contract is distributed over the EMC network.

The **Host** extracts a random contract from his local db, with call
**GetRand_href()** in the file **user_page.php**. The probability of
extracting a specific contract depends on the CPC, keywords, language
and country parameters set in the contract.

When a contract is extracted, the system generates a link to the local
program **lnx_ref.php**, with single CGI-parameter, contract name. The
format is:

    <a href='/emclnx/lnx_ref.php?MyFirstContract>advertising text here</a>

When a **Visitor** clicks this link, the program **lnx_ref.php** is
invoked with the contract name parameter. The program extracts the
contract from the local db, and parses it. It verifies the domain
signature, and if OK - it forwards the Visitor to the URL specified in
the contract. The URL must refer to **lnx_pay.php**, located on the Buyer's site. As
a CGI-parameter, **lnx_ref.php** sends an invoice in the format:

    <contract_name>:<emc_address>:<amount_for_this_click>:<total_balance>:<credit>

For example:

    https://emercoin.com/emclnx/lnx_pay.php?MyFirstContract:EasxHoQ3xs33nZZoLWDnKMRDsafF9ZdqQq:0.06:0.06:-0.06

On the **Buyer's** site, **lnx_pay.php** validates the contract, checks
the balance, invoice, etc, and if everything is OK, it pays for this
click.

Pay attention to the last value, <credit> (-0.06 in the above example).
If this value is positive, this means that the **Host** "trusts" the
**Buyer** enough not to require payment instantly.

Credit can grow during a continued relationship between a **Host** and
**Buyer**. If both behave fairly then payments will automatically become
be less frequent and the payment amount per transaction is increased
(reducing EMC transaction fees).

The system deters new **Hosts** from behaving badly. When a new **Host**
submits an invoice to the **Buyer**, they can request only \~5% of the
CPC amount. Over time, as the **Buyer's** EMCLNX installation becomes
assured of honest behavior, the maximum invoice value automatically
increases up to the contract CPC.

Context links
-------------

There is an interesting way to use context links on a CPC basis. As you
see above, **lnx_ref.php** receives a single CGI-parameter - contract
name. It doesn't matter where the link is placed. Thus, you can include
a link to your instance of the **lnx_ref.php** on a 3rd party blog,
forum signature, or another website. Any **Visitor** clicking this link,
will go to your referrer, and your referrer will charge **Buyer** for
the click value.

Bot mitigation
--------------

It is necessary to prevent web crawlers (e.g. google, bing) from
following EMCLNX links, and so hosts should take several precautions:

### robots.txt

Hosts should specify that search engines should not index the
**/emclnx** directory in their website's
[robots.txt](https://en.wikipedia.org/wiki/Robots_exclusion_standard) as
follows:

    User-agent: * Disallow: /emclnx/

### Bot trap

To help defeat bots which ignore the robots.txt, hosts should also
include a hidden link somewhere on their page, that leads to the
**robotrap.php** that is included with the EMCLNX archive. e.g:

    <font size="1%"><a href="emclnx/robotrap.php">&#21;</a></font>

The above link is not visible to humans since it contains only a
non-printable symbol, but a bot will follow it, and their IP address
will subsequently become banned by the EMCLNX system. Please, don't
click the link yourself, otherwise your IP will be banned.

FAQ
---

***Is there a website already which shows example advertisements?***

Unfortunately the EMCLNX project is frozen until it can be further
developed

<s>There is a [test page](http://emercoin.com/emclnx/user_page.php) on
emercoin.com, and [cryptor](https://cryptor.net) (see gray ad line on
top of page).</s>

***If a Buyer does not pay, what happens? Will the system prevent their
advertisements from being shown?***

Yes. There are several fraud protection measures in the code. If buyer
does not pay, the host simply does not show their ads. The buyer is
identified by their domain, so they cannot easily create new domains to
fool the system. Analogously, a "credit level" is maintained for hosts.
If a host tries to "click out" ads, then the buyer will automatically
stop paying this host.

***What is the software license for the EMCLNX php code?***

The code is, of course, open source, and can be freely used by anyone -
just like Emercoin itself.

***My site is located behind CloudFlare or another service - how do I
ensure payment requests are processed correctly?***

CloudFlare and similar services cache pages, and if a request comes to
**lnx\_pay.php**, they may return a cached value. As a result, the Buyer
does not pay for referrals, and their link will become banned by other
participants. CloudFlare provides a [solution
here](https://support.cloudFlare.com/hc/en-us/articles/200172316-How-do-I-exclude-a-specific-URL-from-CloudFlare-s-caching).
According to this solution, you can exclude certain urls from
CloudFlare's caching, and set up a rule to bypass the cache for EMCLNX
related links. e.g.

    *yourdomain.com/emclnx/*.php -> Bypass cache 

Please take steps to avoid this problem, which can occur with any kind
of server-side caching!
