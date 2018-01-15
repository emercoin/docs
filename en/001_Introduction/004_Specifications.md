# Emercoin Specifications

Emercoin (EMC) is a
[cryptocurrency](https://en.wikipedia.org/wiki/Cryptocurrency) with
hybrid [PoS](http://en.wikipedia.org/wiki/Proof-of-stake) and
[PoW](http://en.wikipedia.org/wiki/Proof-of-work_system) mining
(merge-mined with Bitcoin). Coin generation is focused mostly on
production of coins by energy-conservative PoS as PoW difficulty
gradually increases over time.

<table>
  <tr><td>Total Supply:</td><td>Algorithmically increasing at approx. 6% per year [<a href="https://emercoin.mintr.org/stats">click here for latest stats</a>].</td></tr>
  <tr><td>Block frequency:</td><td>10 minute average.</td></tr>
  <tr><td>PoW Algorithm:</td><td><a href="https://en.wikipedia.org/wiki/SHA-2">SHA-256</a> (merge-mined with Bitcoin).</td></tr>
  <tr><td>PoW block reward:</td><td>5020 EMC, decreasing according to PoW difficulty.<br><br><code>Formula: Reward = 5020 / sqrt(sqrt(difficulty))</code></td></tr>
  <tr><td>PoS reward:</td><td>Approx. 6% pa.</td></tr>
  <tr><td>PoS stake-weight maturity:</td><td>30 days.</td></tr>
  <tr><td>Max. stake-weight:</td><td>90 days.</td></tr>
  <tr><td>Difficulty adjustment:</td><td>Recalculated each block. Adjustment gradually increases over time to favor PoS minting.</td></tr>
  <tr><td>Maturity for newly mined reward:</td><td>32 blocks until new coins can be spent.</td></tr>
  <tr><td>Base58Check encoding <a href="https://en.bitcoin.it/wiki/List_of_address_prefixes">address prefix</a>:</td><td>33</td></tr>
  <tr><td>Default p2p port:</td><td>6661</td></tr>
  <tr><td>Default RPC port:</td><td>6662</td></tr>
</table>
