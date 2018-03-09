<div style="overflow:hidden;"><img style="float:left;" src="EmerDNS_logo.png" alt="EmerDNS logo" width="256"></div>

# EmerDNS

EmerDNS is a system for decentralized domain names supporting a full range of [DNS records](http://en.wikipedia.org/wiki/List_of_DNS_record_types). EmerDNS operates under the **"dns"** service abbreviation in the [Emercoin NVS](../Emercoin_NVS).

Because of Emercoin's secure and distributed blockchain the domain name records are completely decentralized and uncensorable and cannot be altered, revoked or suspended by any authority. Only a record's owner can modify or transfer it to another owner, and a record's owner is determined by whoever controls the private key to the associated payment address.

Only DNS record owners can manage their records: change values, lease times, or delete them or transfer ownership to another EMC address. These actions can be performed using the [Emercoin NVS](../Emercoin_NVS) in the Emercoin wallet GUI, or via the **name\_new** or **name\_update** commands in the [Emercoin API](../../Emercoin_API).

DNS records can easily be retrieved from any Emercoin wallet using the [Emercoin API](../../Emercoin_API) using JSONRPC or the command line, or by the standard [RFC1034](https://www.ietf.org/rfc/rfc1034.txt) DNS protocol that is built in to every Emercoin wallet.

Supported DNS zones
-------------------
Technically, EmerDNS can support any [DNS-zone](https://en.wikipedia.org/wiki/DNS_zone) or [TLD](https://en.wikipedia.org/wiki/TLD). However, for seamless integration into a standard DNS tree, and to prevent collisions with existing DNS-zones, we currently recommend creating EmerDNS records only in the zones: *\*.emc*, *\*.coin*, *\*.lib*, *\*.bazar*.

Current root zones supported by EmerDNS, and their intended purpose:

Zone     |Intended Purpose
-------- |---------------------------------------------------------------------
.coin    |digital currency and commerce websites
.emc     |websites associated with the Emercoin project
.lib     |from the words Library and Liberty - that is, knowledge and freedom
.bazar   |marketplace

Accessing EmerDNS zones
----------------------

There are several ways that EmerDNS domains can be reached:


### Browser extensions

Several 3rd-party browser plugins exist which allow you to easily visit EmerDNS domains:

-   [Peername.com browser
    extension](https://peername.com/browser-extension) (firefox,
    chrome, opera)
-   [Blockchain-DNS.info](https://blockchain-dns.info/) browser
    extension (firefox, chrome)
-   [friGate browser extension](https://fri-gate.org/) (firefox,
    chrome, opera)

A more updated list of browser extensions that support EmerDNS may be found [here](../../Links_&_Resources#page_EmerDNS-Browser-Plugins).

### OpenNIC
Emercoin maintains a peering agreement with the DNS provider [OpenNIC](http://opennicproject.org) which means domains registered with EmerDNS are accessible by default to all users of OpenNIC DNS servers. Emercoin domain zones are thus accessible by visiting [opennicproject.org](http://opennicproject.org) and following their [guide](http://wiki.opennicproject.org/GettingStarted) for setting your DNS resolver to OpenNIC servers.

OpenNIC is a simple and convenient method to seamlessly access all websites registered in the Emercoin blockchain, as well as all other domain zones that OpenNIC supports.

### Proxy servers

3rd-party proxy servers can provide access to EmerDNS zones:

-   [OpenNIC Proxy](http://proxy.opennicproject.org)
-   [Emerproxy.xyz](https://emerproxy.xyz)

### EmerDNS gateways

**Emergate.net** - The emergate.net gateway is an example of [DNS tree integration](#Integration_into_a_regular_DNS_tree) maintained by the Emercoin development team and provides a public gateway to EmerDNS zones. All EmerDNS domains are reachable through this gateway, provided the server hosting the domain is configured properly to receive connections from the gateway url. For example, if you have registered **emer.coin** on the Emercoin blockchain, then it can be reached by visiting: <http://emer.coin.emergate.net>

Creating and maintaining a DNS record
-------------------------------------

### Record types

Emercoin's built-in DNS server supports the following [DNS record types](http://en.wikipedia.org/wiki/List_of_DNS_record_types):

  Record abbreviation   |Service description
  --------------------- |--------------------------------------------------
  A                     |IP V4 address
  AAAA                  |IP V6 address
  NS                    |Name server record
  PTR                   |Pointer record
  CNAME                 |Canonical name record
  MX                    |Mail exchange record
  TXT                   |Free form text message
  SD                    |Subdomains ([see below](#Subdomains))

*Note: SOA, WKS, and SRV records are not directly supported by Emercoin's built-in DNS server.*

To insert a DNS record into the Emercoin blockchain, create (or update) a **name-&gt;value** pair under the **"dpo"** service abbreviation in the [Emercoin NVS](../Emercoin_NVS) as follows:

```text
"name" : "dns:<your_name_here>"
"value" : "<list of NS-records>"
```

For example:

```text
"name" : "dns:example.coin"
"value" : "A=192.168.0.123,127.0.0.1|AAAA=2607:f8b0:4004:806::1001|NS=ns1.google.com|TTL=4001"
```

In this example the domain **example.coin** is specified by:

-   two A-records (192.168.0.123 and 127.0.0.1);
-   one AAAA-record (2607:f8b0:4004:806::1001);
-   one NS-record (ns1.google.com);
-   a [TTL record](https://en.wikipedia.org/wiki/Time_to_live).

The records are separated by the default separator vertical bar or pipe
("|"). If necessary, you can redefine the separator by prefixing the
value with **\~\<new separator character\>**. For example, if you wish to
use a hash character "\#" as a separator instead of a pipe you can
assign it with "\~\#" at the start of the value as follows:

```text
"value" : "~#A=192.168.0.123,127.0.0.1#AAAA=2607:f8b0:4004:806::1001#NS=ns1.google.com#TTL=4001"
```

Note, if you use the space character " " as a separator, you will not
be able use it inside the fields. Therefore, you should select an
appropriate symbol as a separator for your records instead.

As described above, each record can contain multiple values. In the
provided example, the A-record contains two values, separated by a comma
",". You can also redefine the value separator with
**\~\<new separator character\>**. The following example demonstrates how
to redefine the separator two times: slash "/" as record separator,
and asterisk "\*" as value separators for multiple TXT-records:

```text
"value" : "~/TXT=~*This is text, Hello!*2nd text/MX=gmail.com:33,mx.microsoft.com:66/CNAME=emc.cc.st/A=192.168.0.100,127.0.0.1"
```

In the last example we've demonstrated the usage of a [MX record](https://en.wikipedia.org/wiki/MX_record). The value of MX
contains a mail exchanger reference and priority, separated by a colon ":". If priority is omitted, the default value is 1.

Also, intentionally omitted in the last example is a TTL record. The default value for TTL is 24 hours.

### Naming requirements

Domain names may be formed from the set of lowercase alphanumeric ASCII
characters (a-z, 0-9). In addition the hyphen ("-") is permitted if it
is surrounded by characters, digits or hyphens, although it is not to
start or end a name. Only lowercase letters are valid.

#### Internationalized domain names

[Internationalized domain
names](https://en.wikipedia.org/wiki/Internationalized_domain_name)
(Arabic, Chinese, Cyrillic, etc) are technically possible using
[punycode](https://en.wikipedia.org/wiki/Punycode).

For example, if we want the following internationalized domain name:

	dns:президент.emc

Then we must transcribe it using a [punycode
converter](https://www.charset.org/punycode) and register the result:

	dns:xn--d1abbgf6aiiy.emc

### Subdomains

A general challenge with distributed DNS is that anyone can allocate any
unique name, allowing someone to register a subdomain for a domain that
they do not own. To remedy this situation, EmerDNS has special ways to
manage subdomains:

-   A subdomain (SD) record in the DNS parent's NVS value, permits
    lookup and resolution of the subdomain directly within the Emercoin
    DNS subsystem e.g. **SD=www,ftp,mx**
-   A nameserver (NS) record in the DNS parent's NVS value, allows
    reference to external nameserver(s) managed by the domain owner, to
    provide authoritative lookup and resolution of the subdomain
    external to Emercoin DNS e.g. **NS=ns.example.com**

Subdomain resolution is applied in the following order, recursively to
all third-level subdomains and deeper:

1.  First, check SD record in the parent's DNS value for reference to
    the requested subdomain. If a reference for the subdomain is found
    then look up the subdomain within the Emercoin NVS subsystem.
2.  Next, check for nameserver (NS) record in the parent's DNS value. If
    found, generate reference to external nameserver.
3.  If no resolution results from SD or NS records, return as per parent
    domain (i.e. ignore subdomain prefix).

NOTE: When utilizing external nameservers, please take care with correct
name resolution in those servers, including any gateway-suffixes, e.g.
[emergate.net](http://emergate.net).

#### Example 1 - parent contains SD and NS records

	[1] dns:example.coin -> A=1.2.3.4|SD=www,gopher|NS=ns.example.com
	[2] dns:www.example.coin -> A=5.6.7.8

In this case, subdomains will resolve as follows:

-   example.coin will be resolved by record \[1\], and return A=1.2.3.4
-   www.example.coin will be approved by record \[1\], resolved by
    record \[2\] and return A=5.6.7.8
-   gopher.example.coin will be approved by record \[1\], and not
    resolved, since NVS does not contain an appropriate DNS record. This
    will return NXDOMAIN.
-   mail.example.coin will not be approved by record \[1\], but the NS
    record will generate a reference to external server ns.example.com,
    which may or may not resolve this subdomain.

Thus a single record \[1\] supports flexible hybrid resolving:

-   www is resolved by Emercoin NVS.
-   gopher is blocked.
-   all others are resolved by delegated NS=ns.example.com.

#### Example 2 - parent contains SD record only

	[1] dns:example.coin -> A=1.2.3.4|SD=www,gopher
	[2] dns:www.example.coin -> A=5.6.7.8

In this case, subdomains will resolve as follows:

-   example.coin will be resolved by record \[1\], and return A=1.2.3.4
-   www.example.coin will be approved by record \[1\], resolved by
    record \[2\] and return A=5.6.7.8
-   gopher.example.coin will be approved by record \[1\], and not
    resolved, since NVS does not contain an appropriate DNS record. This
    will return NXDOMAIN.
-   mail.example.coin will not be approved by record \[1\], and (because
    of missing NS record) prefix "mail" will be ignored and resolve the
    same as example.coin.

#### Example 3 - parent contains NS record only

	[1] dns:example.coin -> A=1.2.3.4|NS=ns.example.com
	[2] dns:www.example.coin -> A=5.6.7.8

In this case, subdomains will resolve as follows:

-   example.coin will be resolved by record \[1\], and return A=1.2.3.4
-   www.example.coin will not be approved by record \[1\], and will
    generate a reference to external server ns.example.com, which may or
    may not resolve this subdomain.
-   Record \[2\] will be ignored, and will not participate in
    DNS resolution.
-   mail.example.coin will not be approved by record \[1\], and will
    generate a reference to external server ns.example.com, which may or
    may not resolve this subdomain.

#### Example 4 - parent contains no references to subdomain

	[1] dns:example.coin -> "A=1.2.3.4"
	[2] dns:mx.example.coin -> "A=5.6.7.8"

In this case, subdomains will resolve as follows:

-   example.coin -&gt; "A=1.2.3.4"
-   mx.example.coin -&gt; "A=1.2.3.4"
-   www.example.coin -&gt; "A=1.2.3.4"
-   upload.ftp.example.coin -&gt; "A=1.2.3.4"

Because record \[1\] does not contain any SD or NS records, all
subdomains will be resolved to the "parent domain" example.coin. Record
\[2\] will be ignored, and will not participate in DNS resolution.

Integration into a regular DNS tree
-----------------------------------

First, activate the [RFC1034](https://www.ietf.org/rfc/rfc1034.txt) DNS
server in Emercoin by specifing two optional parameters in the
**emercoin.conf** config file, **EmerDNS** and **EmerDNSport**:

	EmerDNS=1 # Run DNS server. Default is 0 (don't run)
	EmerDNSport=NNN # Port for DNS, default is 5335

To integrate Emercoin DNS server into a regular DNS tree, you can use
full-service DNS or caching DNS. The standard Windows DNS-client is
unable to perform this work, so you should use an additional DNS proxy
server to do it. Below we will show some examples.

### Single PC, Acrylic DNS proxy

Running the Emercoin wallet and everything else on a single PC is the
most simple case. For this we recommend to install the lightweight
[Acrylic DNS
Proxy](http://mayakron.altervista.org/wikibase/show.php?id=AcrylicHome)
onto your PC. Acrylic will improve the performance of your PC by
resolving DNS requests with the local cache, decreasing latencies with
browsing or any other Internet activity.

For installation and initial configuration in Windows, see the [guide on
the Acrylic
website](http://mayakron.altervista.org/wikibase/show.php?id=AcrylicHome).
After installation you should configure Acrylic to integrate Emercoin
domain zones. A config file example is [available
online](http://mayakron.altervista.org/wikibase/show.php?id=AcrylicConfiguration).
To configure, you should forward all requests to EmerDNS zones (*\*.emc*,
*\*.coin*, *\*.lib*, *\*.bazar*) to the local Emercoin wallet, and all
requests to other zones to the default DNS provider. This can be
configured in the Acrylic config file as follows:

```text
; Forward to primary (default) DNS server anything but EMC-zones
PrimaryServerHostNameAffinityMask=^*.emc;^*.coin;^*.lib;^*.bazar;*
PrimaryServerAddress=DNS_of_your_provider or any public DNS, for example: 8.8.4.4
PrimaryServerPort=53

; Forward to EMC wallet requests for EMC-zones only
SecondaryServerHostNameAffinityMask=*.emc;*.coin;*.lib;*.bazar
SecondaryServerAddress=127.0.0.1
SecondaryServerPort=5335
```
*In Windows, the default path to the Acrylic config file is: C:\\Program Files (x86)\\Acrylic DNS
Proxy\\*

Alternately, you can download this
[AcrylicConfiguration.ini](http://emercoin.com/files/AcrylicConfiguration.ini)
file, pre-configured to use [OpenDNS](https://www.opendns.com/) as the
primary & secondary DNS-provider (for regular DNS-tree), and local
Emercoin wallet as the ternary provider, for domain zones *\*.emc*,
*\*.coin*, *\*.lib*, *\*.bazar*. The Emercoin team also provides a preconfigured [Acrylic
package](http://sourceforge.net/projects/emercoin/files/0.3.0/Acrylic%20%28EMC%20pre-configured%29.7z/download)
for download, already set up for Emercoin DNS.

### Single PC, BIND DNS proxy

Instead of installing a DNS proxy, you also have the option to install a
full service DNS server. Fortunately, the full DNS server "BIND" is
available for Windows, and is free. You can find many [tutorials on the
internet](https://duckduckgo.com/?q=bind+DNS+windows) that show how to
install BIND onto Windows. For example, see [this
manual](http://drupalmotion.com/article/dev-environment-install-and-configure-bind-dns-server-windows-7).

After installation you should tell BIND to forward EMC-zones to the
local Emercoin wallet by adding to the BIND configuration file
**named.conf** as follows:

```text
zone "emc" {
 type forward;
 forward only;
 forwarders {
   127.0.0.1 port 5335; // Local Emercoin wallet
 };
};
zone "coin" {
 type forward;
 forward only;
 forwarders {
   127.0.0.1 port 5335; // Local Emercoin wallet
 };
};
zone "lib" {
 type forward;
 forward only;
 forwarders {
   127.0.0.1 port 5335; // Local Emercoin wallet
 };
};
zone "bazar" {
 type forward;
 forward only;
 forwarders {
   127.0.0.1 port 5335; // Local Emercoin wallet
 };
};
```

### Local network, BIND DNS proxy

If you have a server with a static IP address in your LAN, you can
install BIND onto your server, and point your desktop PC's primary DNS
address to your BIND server. On the server you can run a headless
Emercoin wallet to which BIND will forward requests to the appropriate
zones. In this case configuration of BIND is exactly the same as above.

Also you can run the Emercoin wallet on any PC of your LAN, instead of
on the BIND server. If so, you should change the forwarding address in
the BIND configuration from 127.0.0.1 to the IP address of that PC. Of
course that PC should have a static LAN IP.

### Local network, DNSMASQ proxy

Modern routers usually contain a built-in proxy DNS in their firmware.
Usually this is
[DNSMASQ](http://www.thekelleys.org.uk/dnsmasq/doc.html). Some router
firmware like [DD-WRT](http://www.dd-wrt.com/) and
[OpenWrt](https://www.openwrt.org/) (as well as others) allow you to
configure the built-in DNS proxy (for instance, see [DD-WRT DNSMASQ
manual](http://www.dd-wrt.com/wiki/index.php/DNSMasq_-_DNS_for_your_local_network_-_HOWTO)
or [OpenWrt DNSMASQ
manual](https://wiki.openwrt.org/doc/howto/dhcp.dnsmasq)).

In this case the wallet should be run on a PC with a static LAN IP and
DNSMASQ from the router would send DNS requests to that PC. Following
are examples of the configuration lines needed to add into dnsmasq.conf.
In this example the PC running Emercoin has the LAN IP address
192.168.1.53.

```text
--server=/emc/192.168.1.53#5335
--server=/coin/192.168.1.53#5335
--server=/lib/192.168.1.53#5335
--server=/bazar/192.168.1.53#5335
```

### Public Internet, direct gateway

The ability also exists to make a public gateway from a regular DNS tree
into EmerDNS. In this case, you can lease any public domain or subdomain,
and point the NS records for this domain to a machine that is running
the Emercoin wallet with an active DNS server on port 53 (see in the
next paragraph for how to define the port). Once you do this, all
regular NS requests to that domain will be resolved by the DNS server,
and answers will be retrieved from the [Emercoin
NVS](../Emercoin_NVS) database in the Emercoin wallet.

For example, the Emercoin development team has set up the domain
**[emergate.net](http://emergate.net)** (Emercoin Gateway Network). When
you click <http://emer.coin.emergate.net>, your name request is resolved
by the Emercoin wallet, and you go directly to **emer.coin** in the
EMC-supported domain zone.

Thus, if you register any name with Emercoin DNS, the name would be
resolved by any Emercoin DNS gateway - emergate.net, or any other. And
your site **site.coin** will be available through any such gateway, by
links such as site.coin.**emergate.net**, or site.coin.**another.com**.

To configure a new domain as a public Emercoin DNS gateway, you need to
specify DNS servers as authoritative for your zone (domain). For the
domain emergate.net, we specified two Name Servers (NS), authoritative
for this domain with our domain registrar:

```
Name Server: SEED1.EMERGATE.NET
Name Server: SEED2.EMERGATE.NET
```

You can check this info using [whois](https://www.computerhope.com/unix/uwhois.htm).

On each of these nameservers runs an Emercoin wallet with an active DNS
server which serves the gateway and local zone for emergate.net. DNS
specific config parameters for the file **emercoin.conf** are as follows:

If you are only running a DNS gateway for your local computer (with
Acrylic or BIND) or for your LAN, it is enough to specify just a single
parameter in **emercoin.conf**:

```text
# enable emc dns
EmerDNS=1
```

This will activate Emercoin's DNS server and run it on default port
5335, as allowed for DNS forwarding by DNS proxies
(Acrylic, BIND, dnsmasq, etc).

To run as a public DNS gateway, you need to specify some additional
parameters:

```text
# Gateway suffix. This suffix will be ignored when a request is passed to the internal gateway.
# Requests for other domain suffixes will be ignored.
EmerDNSsuffix=.emergate.net
 
# NS Server port 53 is the default NS port and must be used if the server is public and "not forward only".
EmerDNSport=53
 
# Filter for allowed zones. Protection for "cool hackers", who try to lookup any external domains through our server
# or attack someone else by DNS amplification mechanism. Currently, only the four EMC-zones are allowed.
EmerDNSallowed=.coin|.emc|.lib|.bazar
 
# Optional path for a file that contains names in the local gateway's NS zone (like www.emergate.net).
# Must be full path. Example:
EmerDNSlocalcf=/usr/share/emercoin/EmerDNSlocal.conf
```

The local config file (**EmerDNSlocal.conf** above) contains pairs in the
format **"name=value"**. An empty name assumes "gateway as is". The
values use the same format as EmerDNS values in the blockchain. For
example, the local file for **emergate.net** is as follows:

```text
# This is local zone config
# For built-in Emercoin DNS

=A=192.241.241.153|TXT=Emercoin site
www=A=192.241.241.153|TXT=Emercoin www-site
```

Virtual webhosts (vhosts)
-------------------------

When you run [virtual hosts](https://en.wikipedia.org/wiki/Virtual_hosting), you will be required to modify your web
server's config to correctly distinguish your hostname with as many possible gateway-suffixes as you wish (or without suffix if name
resolved by LAN or locally). This is easy to do by creating a vname-alias with an asterisk "\*" as
the suffix. The following example shows the appropriate [Apache web server](https://en.wikipedia.org/wiki/Apache_HTTP_Server) config for the virtual server **exchange.emc**. Note the **ServerAlias** line:

```text
<VirtualHost *:80>
  ServerAdmin okhovayko@verizon.net
  DocumentRoot "/var/www/exchange.emc/html"
  ServerName emc.cc.st
  ServerAlias exchange.emc*
  ErrorLog  "/var/log/exchange.emc-error_log"
  CustomLog "/var/log/exchange.emc-access_log" common
  ScriptAlias /cgi-bin/ "/usr/local/libexec/cgi-bin/"
</VirtualHost>
```
