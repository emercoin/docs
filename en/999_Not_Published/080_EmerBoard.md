EmerBoard is a simple "proof-of-concept" decentralized messageboard
using the [Emercoin NVS](Emercoin_NVS).

Records can be viewed at <https://explorer.emercoin.com/emerboard> or in
the Emercoin blockchain itself.

Format for **name-&gt;value** pairs is as follows:

    "name" : "<channel>:<type>:<unique_name>"
    "value" : "<comment>" 

For example, to issue a new Emerboard message with the **name\_new**
command in the [emercoin-cli](../Intro/Running_Emercoin#emercoin-cli):

    emc name_new "ads:info:mintr" "The Emercoin Blockchain Explorer: https://explorer.emercoin.com" 7
