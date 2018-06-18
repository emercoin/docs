# EmcMAGNET

EmcMAGNET is the storage of <a target="_blank" rel="nofollow" href="http://www.makeuseof.com/tag/bittorrent-magnets-work-technology-explained/">BitTorrent magnet links</a>
under the **"magnet"** service abbreviation in the [Emercoin NVS](/en/blockchain-services/emernvs.md).

Magnet links should use the following **name-&gt;value** format:

    "name" : "magnet:Emercoin 0.3.2 for Linux - packed as tar.gz, original file from emercoin.com"
    "value" : "magnet:?xt=urn:btih:dff183bcac72a628fcac88ac1c85c239b806fd5e&dn=emercoin-0.3.2-linux.tar.gz"

A list of all magnet links can be retrieved using the following command
with the [Emercoin API](/en/emercoin-api.md):

    $ emc name_filter ^magnet:
