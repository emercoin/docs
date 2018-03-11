# The EmerDPO Serial Number Publisher

The EmerDPO Serial Number Publisher is a utility that automates the
process of placing [EmerDPO](EmerDPO_Introduction) serial numbers into the
Emercoin blockchain from a table in [CSV
format](https://en.wikipedia.org/wiki/Comma-separated_values).

Download the EmerDPO SN-Publisher from [the SN-Publisher
GitHub](https://github.com/emercoin/SN-Publisher/tree/master/Distrib).

Preparation of a CSV serial number table
----------------------------------------

1. Open a new spreadsheet (Microsoft Excel, Google Docs, Libre Office
Calc).

2. In the first box (A1) enter **"SN"**.

3. Other boxes of the first line may have any name, but if you need to
protect the content of any column with a signature, it is required to
place an **"F-"** in front of its name (for example, F-Model, F-Master).

4. In the next lines, enter the data for each serial number. See the
following image for an example:

    ![](Sn-publisher-image00.png "fig:Sn-publisher-image00.png")

5. When the table is filled in, save (export) it in .csv file format. This
table will serve as the template for the reservation and signing of
serial numbers.

Preparation of the Emercoin wallet to work with SN-Publisher
------------------------------------------------------------

1. If your [Emercoin wallet](../../Install_Software/Core_Wallets/GUI_wallet) is currently
running, exit it via the menu (File &gt; Exit).

2. Enter the wallet folder (in Windows this is: **C:\\Users\\&lt;YOUR USER
NAME&gt;\\AppData\\Roaming\\EmerCoin**) and create a configuration file
called **[emercoin.conf](../../Running_Emercoin/emercoin.conf)**. For convenience,
first create a text file called emercoin.txt, and then rename it after
editing. In the file **emercoin.conf** write the following lines:

    ```text
    server=1
    listen=1
    rpcuser=rpcemc
    rpcpassword=<random_password>
    debug=rpc
    ```

    For **rpcpassword** you should choose a strong random password. This is the RPC password and <u>not</u> your wallet encryption password.

3. Launch the wallet...

4. If your wallet is encrypted, unlock it by clicking on the lock icon in
the bottom right corner of the program and entering your wallet
password.

5. You may check the wallet’s readiness to work with the SN-Publisher utility by typing the following address in your browser:
**<http://127.0.0.1:6662>**. If the browser requests the password and login, all is fine.

6. Make sure that the Emercoin wallet contains a large enough EMC balance for all the records for your project (based on the calculation of ~0.08 EMC for each serial number).

SN Publisher preparation:
-------------------------
The SN-Publisher utility is semi-automatic. It uses your enterprise root [EmerDPO](EmerDPO_Introduction) record (for example, **dpo:Raketa**) and links all serial numbers to the EMC-address of this record. To do this, after the installation:

1. Go to the folder with the SN Publisher installation utility: **C:\\Program Files (x86)\\EmerCoin\\Emercoin DPO SN Publisher**

2. Open the file **Emercoin\_DPO\_SN\_Publisher.exe.config** in a text editor.

3. Edit the **RootDPOName** entry to match your enterprise root DPO record. e.g: `<add key="RootDPOName" value="dpo:Raketa" />`

4. After making the change, remember to save the edited file.

Publishing serial numbers into the EMC blockchain:
--------------------------------------------------
1. Launch the SN-Publisher utility.

2. In the "Wallet settings" tab, input the **rpcpassword** you entered into
the **emercoin.conf** file (see above) and click the "Check connection"
button. In case of successful connection, the utility will show the
message "Connected successfully" and your EMC wallet balance.

    ![](Sn-publisher-image02.png "fig:Sn-publisher-image02.png")

3. Go to the "Serial Numbers" tab. Press the "Browse.." button and select
the CSV file you created containing your serial numbers.

    ![](Sn-publisher-image01.png "fig:Sn-publisher-image01.png")

4. In the field "Lifetime of SN record", select the number of days, for
which your serial numbers will be reserved (by default this is 1,000
days).

5. Pressing the button "Reserve serial number records" will start the
process of publishing your serial numbers to the Emercoin blockchain.
The utility communicates with your Emercoin wallet and creates the
records automatically.

    In the process, EMC coins are spent (~0.07 EMC per record by default).
This process will take some time, proportional to the number of records.
The confirmation of all published records by the Emercoin network will
take 20–50 minutes.

6. If you have completed the operation described above and made sure that
all records were published on the blockchain, you may proceed to signing
the reserved serial names. This operation is analogous to the previous
step and will take about the same amount of time. Some coins are spent
for this operation as well (~0.01 EMC per record).

For assistance
--------------

* The SN-Publisher sourcecode is freely available on
[Github](https://github.com/emercoin/SN-Publisher), and code
contributions are welcome.

* If the EmerDPO SN-Publisher is missing any functions necessary to meet
your needs or you want to adapt it for your business please [contact the
Emercoin team](http://emercoin.com/contact).
