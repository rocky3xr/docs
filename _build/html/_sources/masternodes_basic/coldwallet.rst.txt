.. _coldwallet:

=================
Cold Wallet Setup
=================

This is the wallet where the MasterNode collateral will have to be transferred and stored. After the setup is complete, this wallet doesn't have to run 24/7 and will be the one receiving the rewards.

1. :ref:`Install and open the Rupaya-Qt wallet on your machine<installwallet>`
2. :ref:`Create a receiving address for the MasterNode collateral funds<createmnaddress>`
3. :ref:`Send EXACTLY 20000 RUPX coins to the address you just copied<sendburncoins>`
4. :ref:`Open the debug console of the wallet in order to type a few commands<opendebugconsole>`
5. :ref:`Run **masternode outputs** command to retrieve the transaction ID of the collateral transfer<outputtxhash>`
6. :ref:`Copy and save the *txhash* and *outputidx*<copysavetxhash>`
7. :ref:`Go to *Tools -> Open MasterNode Configuration File* and add a line in the newly opened *masternode.conf* file<masternodeconf>`
8. :ref:`Restart the Cold wallet to pick up the **masternode.conf** changes<restartcoldwallet>`
9. :ref:`Open the Debug console to verify that the output from the *masternode list-conf* command`<listconf>`
10. :ref:`Go to the MasterNodes tab and check if your newly added masternode is listed<masternodetab>`
11. :ref:`Run the **startmasternode alias false MN1** command, in the Cold Wallet debug console, in order to enable the MasterNode<startmasternode>`

Requirements:
-------------
* Windows 7 or higher, Mac OS or Linux
* Outgoing internet access to sync the blockchain and enable the MasterNode remotely

Install the Rupaya Cold Wallet
------------------------------

.. _installwallet:

1. Install and open the Rupaya-Qt wallet on your machine.

 * If you have a previous Rupaya wallet installed, backup the `wallet.dat`, uninstall it then delete its original data directory.
 * Download the newest Rupaya Qt wallet from: https://github.com/rupaya-project/rupaya/releases
 * The Windows wallet needs to be extracted to a permanent location, OSX Wallet goes into `Applications`
 * Start the wallet software and ignore the unidentified developer warning
 * If you are prompted to Allow Access by the firewall, do so
 * Let the wallet sync until you see this in the bottom right corner of your Wallet 
 
 .. figure:: /img/qt-wallet-sync.png
 
 * If the wallet is not synching, add this line in the configuration file::
 
	addnode=seeds.rupx.io

The Qt wallet will open the configuration from **Tools > Open Wallet Configuration File**. 
Be sure to restart the wallet every time you update the configuration.

Create a new MN wallet address and send it the required burn coins
------------------------------------------------------------------

.. _createmnaddress:

2. Create a receiving address for the MasterNode collateral funds.

	* Go to **File -> Receiving addresses**
	* Click **New**, type in a label and press **Ok**.
	* Select the row of the newly added address and click **Copy** to store the destination address in the clipboard.

.. _sendburncoins:

3. Send EXACTLY 20000 RUPX coins to the address you just copied. Double check you've got the correct address before transferring the funds.

	After sending, you can verify the balance in the Transactions tab. This can take **a few minutes** to be confirmed by the network. Go get a glass of water. No alcoholic beverages please, we are not out of the woods yet.

.. warning::	If you are sending from an exchange, make sure you account for the withdrawal fee so that you get EXACTLY EXACTLY EXACTLY 20000 RUPX in the new wallet address. This is a common error that will cause the next step to not give you the transaction id that is needed. For example, to withdraw from `Stocks.Exchange` the correct ammount for a MasterNode, you need to specify the ammount of **20000.001** to account for the fee.

Output your MN TXhash and Outputidx and update the MasterNode configuration file
--------------------------------------------------------------------------------

.. _opendebugconsole:

4. Open the debug console of the wallet in order to type a few commands. 

	Go to **Tools -> Debug console**

.. _outputtxhash:

5. Run the `masternode outputs` command to retrieve the transaction ID of the collateral transfer::

	**masternode outputs** 
	
	You should see an output that looks like this::
   
	'"txhash" : "c19972e47d2a77d3ff23c2dbd8b2b204f9a64a46fed0608ce57cf76ba9216487",'
	'"outputidx" : 1'

.. _copysavetxhash:

6. Copy and save the `txhash` and `outputidx`.  Both the `txhash` and `outputidx` will be used in the next step. The `outputidx` will be either a `0` or `1`, both are valid values.

.. _masternodeconf:

7. Go to `Tools` -> `Open MasterNode Configuration File` and add a line in the newly opened `masternode.conf` file.  If you get prompted to choose a program, select a text editor like Notepad/TextEdit to open it.
	
These are the default directories for the Rupaya data directory where this file is stored::
	
	Mac: ~/Library/Application Support/Rupaya
	Windows: ~\AppData\Roaming\Rupayacore

Below is an example of what you need in the `masternode.conf` file, all on a single line with no carriage returns.  The file contains an example that is commented out(with a # in front). Read it if it helps. Based on the output from the `masternode outputs` command, I would add this line in::

	MN1 199.247.10.25:9050 87LBTcfgkepEddWNFrJcut76rFp9wQG6rgbqPhqHWGvy13A9hJK c19972e47d2a77d3ff23c2dbd8b2b204f9a64a46fed0608ce57cf76ba9216487 1

* **MN1** is the node's alias. 
* **199.247.10.25** is the external IP of the masternode server that will provide services to the network. 
* **87LBTcfgkepEddWNFrJcut76rFp9wQG6rgbqPhqHWGvy13A9hJK** is your masternode private key (aka GenKey) from (Part 1), the value used for `masternodeprivkey` in **/root/.rupayacore/rupaya.conf**. 
* **c19972e47d2a77d3ff23c2dbd8b2b204f9a64a46fed0608ce57cf76ba9216487** is your TXhash from `masternode outputs`. 
* **1** is your 'outputidx' (aka Index) from `masternode outputs`.

.. _restartcoldwallet:

8. Restart the Cold wallet to pick up the `masternode.conf` changes.

.. _listconf:

9. Open the Debug console (Open **Tools > Debug console**) to verify that the output from the `masternode list-conf` command matches what you entered in the `masternode.conf` file::

	masternode list-conf

.. _masternodetab:
	
10. Go to MasterNodes tab and check if your newly added masternode is listed.

	You should now see the newly added MasterNode with a status of `MISSING`.
	If you want to control multiple MasterNode Hot wallets from this Cold wallet, you will need to repeat the previous 2-7 steps. The `masternode.conf` file will contain an entry for each masternode that will be added to the network.
 

Starting the MN from the Cold Wallet
------------------------------------

.. warning:: It is very important that you let the MasterNode Hot wallet synchronize for a couple of hours prior to starting it from the Cold wallet.  If you attempt to start it before it is fully synchronized then it will fail.

.. _startmasternode:
	
11. Run the *startmasternode alias false MN1* command, in the Cold Wallet debug console, in order to enable the MasterNode::

	startmasternode alias false MN1

In the example above, the alias of my MasterNode was MN1, in your case, it might be different.
	
You can now proceed to the next step to verify that your MasterNode started correctly.