# Proof-of-Stake block generation

By holding EMC in your wallet, you can assist the Emercoin network to
verify/broadcast transactions by generating new blocks with Emercoin's
[Proof-of-Stake](http://en.wikipedia.org/wiki/Proof-of-stake) (PoS)
system.

When PoS blocks are generated, the wallet that generated the block is
rewarded with additional EMC. Earnings from PoS are at the rate of
approx. 6% per year. The process of generating blocks with Proof-of-Stake is loosely referred to as *minting*.

*EMC coin age maturity is 30 days. This means, the
[UTXO](https://bitcoin.org/en/glossary/unspent-transaction-output) (Unspent Transaction Output) that
added the EMC to your balance must sit unspent for 30 days before it
becomes eligible to generate a PoS block.*

Proof-of-Stake guide
--------------------
This guide covers how to mint
[Proof-of-Stake](http://en.wikipedia.org/wiki/Proof-of-stake) (PoS)
blocks with an encrypted wallet on your own computer using the <b>Emercoin
GUI</b>. Note that it is also possible to mint
PoS blocks on a headless server with the <b>Emercoin
daemon</b> (see *walletpassphrase* command
below).

Before we begin, let's understand a few things about PoS with Emercoin:

-   EMC blocks are mined approx. every 10 minutes.
-   The chance of mining a block with PoS is related to the amount of
    EMC you hold.
-   Coins must sit unspent in the EMC address for <u>30 days</u> to
    become eligible for staking.
-   Maximum staking weight (chances of staking) is reached after <u>90
    days</u>.
-   To have the chance to mine a block with PoS, the wallet must be
    unlocked for minting, as described below.
-   Staking correctly will generate approx. 6% interest p.a. The PoS
    reward for minting a block is based on coin age.

Follow these steps to mine PoS blocks using the GUI:

1. **Encrypt your wallet:**

    To encrypt your wallet, choose 'Encrypt Wallet' from the Settings menu
and choose a strong password that you won't forget.

    ![](Pos1.png "fig:Pos1.png")

    After your wallet is encrypted, a locked padlock icon appears at the
bottom of the window.

    ![](Pos2.png "fig:Pos2.png")

2. **Unlock your wallet in Mint-only mode:**

    Click the padlock icon at the bottom of the window, check the 'Mint only
mode' checkbox and enter your password.

    ![](Pos3.png "fig:Pos3.png")

    When the wallet is unlocked, the padlock icon at the bottom of the
window will appear unlocked.

    ![](Pos4.png "fig:Pos4.png")

    While the wallet is in 'Mint only mode', you can safely leave it open
without anyone being able to send funds out.

3. **Leave your wallet unlocked and running in Mint-only mode:**

    Coins only have a chance to stake while your wallet is open, and they
sit untouched in the EMC address for 30 days.

    If you mint a PoS block, you will see your 'Stake' balance change for 32
blocks until the PoS transaction confirms.

    ![](Pos5.png "fig:Pos5.png")

4. When coins have staked successfully, you will see new transaction and
new coins added to your balance.

    ![](Pos6.png "fig:Pos6.png")

### How often to run the client for staking?

You could unlock your wallet for minting for a few days each month,
however in practice it's unlikely all your transaction
[UTXO](https://bitcoin.org/en/glossary/unspent-transaction-output)'s are
ready to stake at the same time. Therefore in the long term it is more
pratical to leave the wallet running 24/7 to increase your chances of
minting PoS blocks and to support the Emercoin network.

### Checking your PoS statistics

-   There is PoS calculator provided at
    <https://emercoin.mintr.org/poscal>.

-   Additional statistics particular to your EMC address are also
    available:

    -   Visit the Emercoin blockchain explorer at
        <https://emercoin.mintr.org> and search for your EMC address(es)
        that are currently staking.
    -   Run the staking calculator tool for your EMC address on <https://emercoin.mintr.org> (press the purple "leaf" icon and you will
        see the results on your minting %, coin age, and several other variables).

### Preventing your wallet from staking

While coins are staking they will not be accessible to spend. If you
need to prevent an amount of EMC from staking, simply set
**reservebalance** in your wallet's
[emercoin.conf](../Running_Emercoin/emercoin.conf) file. e.g:

    reservebalance=1000

To prevent your wallet from staking at all, simply set
**reservebalance** to be greater than your total EMC balance.

### Minting using the headless daemon

If using the command line daemon instead of the GUI then you can unlock
your wallet for minting using the
**walletpassphrase** command:

    walletpassphrase "passphrase" timeout [mintonly]

e.g. to unlock for minting for 604800 seconds (1 week):

    $ emc walletpassphrase yourlongrandompassphrase 604800 true

### Troubleshooting tips

-   Check your expected PoS rewards at
    <https://emercoin.mintr.org/poscal>
-   Check your minting statistics for your EMC address (see above).
-   Ensure the EMC
    [UTXO](https://bitcoin.org/en/glossary/unspent-transaction-output)
    has been left unspent in your wallet for at least 30 days.
-   Ensure you have not set **reservebalance** in your wallet's
    [emercoin.conf](../Running_Emercoin/emercoin.conf) file.
-   See
    <https://www.reddit.com/r/EmerCoin/comments/6xsmfw/pos_minting_question/>

More info
---------

1.  See the following article on medium: [Money makes money: How to earn
    Emercoin by taking advantage of the PoS
    algorithm](https://medium.com/@emer.tech/money-makes-money-e23087c6dc7d?source=rss-d2f48d13ac49------2).

