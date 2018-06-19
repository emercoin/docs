<div class="boxOverflow">
<img src="/images/EmerDPO_1.png" alt="EmerDPO" width="256">
</div>

# The EMC Antifake programme

Functioning on the Emercoin platform, **EMC
Antifake** is an anti-counterfeit and product tagging system that uses
Emercoin's [EmerDPO](/en/blockchain-services/emerdpo/emerdpo-introduction.md) blockchain technology.

**EMC Antifake** allows manufacturers to create a unique ID or "digital
passport" for each and every product unit that comes off their
production line. These *"digital passports"* are stored by the
manufacturer in Emercoin's [secure
blockchain](/en/introduction/security-principles.md), thus allowing the
manufacturer and their customers to verify the authenticity of every
product.

Counterfeiting damages brand reputation and creates cautious customers
which hurts sales. **EMC Antifake** solves the counterfeiting problem
for manufacturers, while the non-replicable *"digital passport"* provides
a valuable bridge between customer and product.

The *"digital passport"*:

-   can be used by manufacturers to record all events occurring during
    the lifetime of the product e.g. manufacture, sale, resale, service,
    repair, etc.
-   provides a technologically enhanced customer experience that
    guarantees security allowing confident purchase decisions while also
    deterring against theft.
-   allows for better communication from customers, increasing the
    customer's sense of individual connection with the brand
    and product.
-   allows for better communication to customers e.g. offering loyalty
    bonuses or other incentives like discounts, extended warranties,
    etc, helping the brand better understand their customers.

Thanks to the tools provided by the Emercoin team, all that is
(minimally) required from a product manufacturer is to apply specialized
tags or labels to their products. Optionally, the manufacturer can
install a specific security program for analysis of sales data, though
this isn’t required and may be done after deployment.

The **EMC Antifake** technology is available to try now - and it won’t
cost anything. **EMC Antifake** is in the pilot stage and the Emercoin
team are ready to provide introductions to the technology and assist
with the tools necessary for successful product integration and launch.

How does it work in a practical sense?
------------

<div class="boxOverflow">
<img src="/images/EmerDPO_2.jpg" alt="EmerDPO_2.jpg">
</div>

**For products still at the factory (or distributor’s storage)**, QR
codes in the form of a label or tag are applied to each package. Each
individual product gets its own unique tag, containing a unique serial
number given to it by the manufacturer. A second code – the "purchase
code" – exists inside the packaging of the product, or on the inside of
a two-layered tag (see image).

**In the store, the customer scans the code** with their smartphone.
There is no specialized app required (almost all smartphones have a QR
code scanner app built-in or <a target="_blank" rel="nofollow" href="https://www.google.com/search?q=qr+code+app">easily available</a>).

**For a genuine, unsold product**, a page will be displayed providing
information about the product and the manufacturer, confirming that the
product has not been purchased before, and that it is authentic.

After a customer buys the product, the other code can be accessed
(inside the product packaging or by tearing off the top layer of the
two-layered tag). When the second code is scanned, another page will
open, on which the code undergoes cryptographic verification, and if the
product is authentic (because the code is authentic), **the customer
will be able to register their purchase.**

Upon registration the customer may have the ability to create an account
or interact with the manufacturer of the product in other ways (for
instance, to leave comments), and can also take ownership with a record
in the blockchain.

Optionally, the manufacturer may ask the customer to answer a survey, or
to fill out their profile, motivating them to do so in various ways
(extended warranty, cashback bonus, service opportunity, future
discounts, etc). **The digital passport allows the manufacturer to
verify the authenticity of the customer.**

Attackers who try to forge goods can not make valid serial numbers tied
to the manufacturer without having the cryptographic keys that the
manufacturer possesses.

If an attacker manufactures fake tags with nonexistent codes, they will
not be recognized by the system, and customers will be warned when
trying to verify the code.

If an attacker purchases a product and copies the tag multiple times
onto their own products, the system will know that the product has
already been purchased and after the first purchase of any forged
product will warn all subsequent potential customers. On top of that,
the product initially purchased by the attacker can be marked
"unauthorized", which may help, among other things, to identify the
criminal.

**Only the holder of the manufacturer's private cryptographic key can
produce valid labels capable of passing verification.** It is important
to note that due to the nature of <a target="_blank" rel="nofollow" href="https://en.wikipedia.org/wiki/Public-key_cryptography">public-key cryptography</a>,
even the software developers and verification websites cannot create
fake labels that would pass verification tests. In practice, there may
be a single existing private key kept secret by the CEO of the
manufacturing company (though we strongly recommend keeping backup
copies in reserve) and without that key, no one can make a label that
will pass the test!

Also note that, cryptographic tokens ("coins", "crypto-currencies") are
not used in the verification process, so the **EMC Antifake**
authentication technology itself cannot be subject to any
crypto-currency related regulations that may otherwise apply.

Example scenarios
-----------------

### You (manufacturer) would like us to create a series of test tags for you

If you are a manufacturer who would like our help to trial EMC Antifake
during its pilot stage then please <a href="http://emercoin.com/contacts">contact the Emercoin team</a> today. During the pilot we may be
willing to take on all of the work, to produce several dozen labels for
you and provide the required cryptographic keys, all free of charge
within the timeframe of a few days. **All you'll need to do is apply the
labels to your products.**

### You (manufacturer) would like to learn how to implement EMC Antifake yourself

There are several possible workflows to accomplish this - whether you do
everything yourself (in this case you don't need to contact us at all -
just download the software, configure verification servers if you don't
want to use ours, create keys and serial numbers), or in the simplest
case (when you only create keys and serial numbers using the opensource
utility that we can provide you, and leave the rest of the work for us
to undertake), the most time-consuming operation will be applying the
labels to your products.

### You're a customer in a store

<div class="boxOverflow">
<img src="/images/EmerDPO_3.jpg" alt="EmerDPO_3.jpg">
</div>

Using your smartphone (no specialized app required) you scan the tag on
a product.

If the code is valid then a web page opens (similar to
<a target="_blank" rel="nofollow" href="https://emcDPO.info/key/DEMO-1030">this</a>) displaying information about
the manufacturer and that particular product, and informing you that the
product is genuine and for sale. In that case, if you like the product
you can go ahead and buy it with an added sense of security!

However, if the code is invalid, there will either be no page, or a page
with an error message. In the case that an attacker copied a tag from an
original product and reproduced it, you will receive a warning message
that the product has already been purchased (similar to
<a target="_blank" rel="nofollow" href="https://EmcDPO.info/key/DEMO-1001">this</a>).

### After buying a genuine product

<div class="boxOverflow">
<img src="/images/EmerDPO_4.jpg" alt="EmerDPO_4.jpg">
</div>

After purchase, you reveal the "purchase code" by tearing off the outer
layer of the two-layer tag (see picture) or as otherwise placed inside
the packaging of the product by the manufacturer. Scanning this code
opens a web page that will allow you to register the purchase, create a
user account, receive incentives or bonuses from the manufacturer, or
even transfer ownership of the product to another person.

After your purchase has been recorded, you can log in using the details
that were provided to you during registration, to manage your purchase.
Scanning either code again will result in a page declaring that the
product has already been purchased.

The manufacturer may create loyalty programs in which customers can
optionally choose to participate. These could include surveys (which may
provide additional incentives), improved terms of service, discounts,
etc. Thanks to the "digital passport", it will be easy to prove that you
purchased a genuine product.

When you first register a purchase, your purchase record (or "digital
passport" for the product) is controlled by the issuer, but they may
allow you to request its transfer to your Emercoin address to store it
yourself. Blockchain technology makes this possible, and after the
transfer of the record, no one (not the issuer, or even the Supreme
Court) will be able to take away your control (possession) of this
record - unless you yourself wish to transfer it to another person.

### Somebody stole your item

That is bad news. The good news is, that as long as the serial number is
inscribed somewhere on the product - anyone knowing about the EMC
Antifake system can potentially report the theft of the item or report
its recovery, an unwary thief may be more likely to be caught, and the
police will find it much easier to find you and return your stolen
property. And in the best of cases, the use of EMC Antifake may even
deter the thief from stealing the item in the first place.

EMC Antifake is by no means an absolute defense against theft. However,
it provides real mechanisms to reduce its risk and improves chances of
item recovery.

### You (the manufacturer) wish to receive more feedback from customers

EMC Antifake ensures that manufacturers are interacting only with
genuine customers thanks to the "digital passport" verifying customer's
purchases. This allows you to speak directly to your customers and
motivate them (perhaps with additional incentives) to participate in
surveys, provide information about themselves, etc.

Some methods of motivation have already been suggested – including
discounts, special services, extended warranties and much more.

Because all records exist on the Emercoin blockchain, you can even
motivate the customer by transferring rewards directly to the record's
associated payment address on the Emercoin blockchain! In this case, the
manufacturer does not have to know anything about the customer, and the
system will continue to function even in the case that the record of
ownership is transferred to another person! In essence, you have in your
hands an "eternal reliable phone" connection with the customer that owns
your product – just don’t forget to motivate them to answer!

How much does this cost?
------------------------

The cost of entering one name in the Emercoin
blockchain using [Emercoin NVS](/en/blockchain-services/emernvs.md), is
approximately 0.2 EMC (US\$0.04 as of the beginning of 2017). The cost
of printing a tag depends heavily on the volume and the size of the
label and can come at about 5-10 cents even for smaller volumes. For
large volumes, these figures will of course be significantly lower.
**When compared to the cost to produce an average product, the cost
becomes nearly invisible.** Ongoing costs for the operation of the
system are practically nil for any significant volume.

More info
---------

1.  See the following article on medium: <a target="_blank" rel="nofollow" href="https://medium.com/@emer.tech/how-to-protect-your-products-against-counterfeiting-using-blockchain-78b4f5096324">How to protect your products against counterfeiting using Blockchain</a>.
2.  Please <a href="http://emercoin.com/contact">contact the Emercoin team</a> if
    you would like to join our pilot program.
3.  You can also visit <a target="_blank" rel="nofollow" href="https://EmcDPO.info">EmerDPO.info</a>

Todo
----

-   Integrate the instructions from the <a target="_blank" rel="nofollow" href="https://medium.com/@emer.tech/how-to-protect-your-products-against-counterfeiting-using-blockchain-78b4f5096324">medium article</a> into the article above.


