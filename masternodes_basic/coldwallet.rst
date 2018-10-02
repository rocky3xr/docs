.. _coldwallet:
.. _Video: https://www.youtube.com/watch?v=0TU044CYfl4/

=================
Cold Wallet Setup
=================

This is the wallet where the MasterNode collateral will have to be transferred to and stored. After the setup is complete, this wallet will be the one receiving the rewards and will not have to run 24/7.

Requirements:
--------------
	* Windows 7 or higher, Mac OS, or Linux
	* Outgoing internet access to sync the blockchain and enable the MasterNode remotely

Implementation Steps
--------------------

1. :ref:`Install and open the Rupaya-Qt wallet on your machine<installwalletbasic>`
2. :ref:`Create a receiving address for the MasterNode collateral funds<createmnaddressbasic>`
3. :ref:`Send EXACTLY 20000 RUPX coins to the address you just copied<sendburncoinsbasic>`
4. :ref:`Open the debug console of the wallet in order to type a few commands<opendebugconsolebasic>`
5. :ref:`Run MasterNode outputs command to retrieve the transaction ID of the collateral transfer<outputtxhashbasic>`
6. :ref:`Copy and save the txhash and outputidx<copysavetxhashbasic>`
7. :ref:`Go to Tools -> Open MasterNode Configuration File and add a line in the newly opened masternode.conf file<masternodeconfbasic>`
8. :ref:`Restart the Cold wallet to pick up the masternode.conf changes<restartcoldwalletbasic>`
9. :ref:`Open the Debug console to verify that the output from the MasterNode list-conf command<listconfbasic>`
10. :ref:`Go to the Masternodes tab and check if your newly added MasterNode is listed<masternodetabbasic>`
11. :ref:`Run the startmasternode alias false MN1 command, in the Cold Wallet debug console, in order to enable the MasterNode<startmasternodebasic>`

.. _installwalletbasic:

Install the Rupaya Cold Wallet
------------------------------

These instructions are intended for those that are installing the new Rupaya Core 5 wallet on your personal Windows or Mac computer.

.. warning:: Do not install the new wallet on the computer that contains the Rupaya wallet that is holding your existing coins.  You will need to either install the new wallet on a different computer or move your coins to a different computers' wallet, prior to installing the new wallet.  This is to prevent any chance that the new wallet will overwrite your current wallet and cause you to lose your coins.

1A. Be sure that your existing wallet.dat and private keys are backed up from the old wallet.  We strongly recommend backing up your wallet.dat and private keys prior to starting this process.

	For more instructions, watch this Video_ from a fellow Rupayan, David Coen, on how to export your private keys:
	
1B. Delete the old Rupaya directory, if the computer contains the old Rupaya wallet::

	* Mac: ~/Library/Application Support/Rupayacore
	* Windows: ~\AppData\Roaming\Rupaya

.. warning:: Do not delete the current wallet directory if the existing wallet still has coins in it.  You should be doing this install on a computer that does not currently have a Rupaya wallet that contains coins.
	
1C. Open the following URL in a web browser to download the appropriate wallet version for your system:

	* https://github.com/rupaya-project/rupx/releases
	
1D. Once downloaded, unzip the files and move the Rupaya-cli and Rupaya-qt files onto the desktop.  

	* If prompted, confirm that you want to replace the existing file(s).

1E.Double click the Rupaya-qt file to install the new wallet.

	* If you are prompted to use a data directory then select the radio button next to **Use the default data directory** and click **OK**
	* Accept any pop ups asking to confirm if you want to continue with the installation
	* When prompted, select **Use the default data directory** and click **OK**
	* If prompted by security or antivirus software, click **Allow Always**
	* The new wallet should now open and begin to synchronize with the network

NOTE: If the wallet is not synchronizing, then add the following line into the rupaya.conf configuration file **(Tools > Open Wallet Configuration File)**::
 
	addnode=seeds.rupx.io
	
NOTE: The file should be blank by default.  **Be sure to restart the wallet every time you update the configuration file.**

Create a new MN wallet address and send it the required burn coins
------------------------------------------------------------------

.. _createmnaddressbasic:

2. Create a receiving address for the MasterNode collateral funds.

	* Go to **File -> Receiving addresses**
	* Click **New**, type in a label and press **Ok**.
	* Select the row of the newly added address and click **Copy** to store the destination address in the clipboard.
	* You can name the wallet with a description such as "**MN1**" by right clicking it and selecting "Edit".

.. _sendburncoinsbasic:

3. Send **EXACTLY 20000 RUPX** coins to the address you just copied. Double check you've got the correct address before transferring the funds.

	* After sending, you can verify the balance in the Transactions tab. This can take **a few minutes** to be confirmed by the network. Go get a glass of water. No alcoholic beverages please, we are not out of the woods yet.

.. warning::	If you are sending from an exchange, make sure you account for the withdrawal fee so that you get EXACTLY EXACTLY EXACTLY 20000 RUPX in the new wallet address. This is a common error that will cause the next step to not give you the transaction id that is needed. For example, to withdraw from `Stocks.Exchange` the correct ammount for a MasterNode, you need to specify the ammount of **20000.001** to account for the fee.

Output your MN TXhash and Outputidx and update the MasterNode configuration file
--------------------------------------------------------------------------------

.. _opendebugconsolebasic:

4. Open the debug console of the wallet in order to type a few commands. 

	Go to **Tools -> Debug console**

.. _outputtxhashbasic:

5. Run the `masternode outputs` command to retrieve the transaction ID of the collateral transfer::

	masternode outputs 
	
* You should see an output that looks like this in the Debug console:
   
	'"txhash" : "c19972e47d2a77d3ff23c2dbd8b2b204f9a64a46fed0608ce57cf76ba9216487",'
	'"outputidx" : 1'

**NOTE: If you do not get output resembling the above example then you likely do not have EXACTLY 20000 RUPX in the MN1 wallet address.  You will need to resolve this issue and ensure that ONLY and EXACTLY 20000 RUPX is in the MN1 address and that it is in a single input.**

.. _copysavetxhashbasic:

6. Copy and save the `txhash` and `outputidx`.  

	* Both the `txhash` and `outputidx` will be used in the next step. 
	* The `outputidx` will be either a `0` or `1`, both are valid values.

.. _masternodeconfbasic:

7. Go to `Tools` -> `Open masternode Configuration File` and add a line in the newly opened `masternode.conf` file.  

	* If you get prompted to choose a program, select a text editor like Notepad/TextEdit to open it.
	* These are the default directories for the Rupaya data directory where this file is stored:
	
		* Mac: ~/Library/Application Support/Rupayacore
		* Windows: ~\AppData\Roaming\Rupayacore

* Below is an example of what you need in the `masternode.conf` file, all on a single line with no carriage returns.  The file contains an example that is commented out(with a # symbol in front). Read it if it helps. Based on the output from the `masternode outputs` command, I would add this line in::

	MN1 199.247.10.25:9050 87LBTcfgkepEddWNFrJcut76rFp9wQG6rgbqPhqHWGvy13A9hJK c19972e47d2a77d3ff23c2dbd8b2b204f9a64a46fed0608ce57cf76ba9216487 1

* **MN1** is the node's alias. 
* **199.247.10.25** is the external VPS IP address of the MasterNode server. 
* **87LBTcfgkepEddWNFrJcut76rFp9wQG6rgbqPhqHWGvy13A9hJK** is your masternode private key (aka GenKey), which is the value used for `masternodeprivkey=` in **/root/.rupayacore/rupaya.conf**. 
* **c19972e47d2a77d3ff23c2dbd8b2b204f9a64a46fed0608ce57cf76ba9216487** is your TXhash from `masternode outputs`. 
* **1** is your 'outputidx' (aka Index) from `masternode outputs`.

.. _restartcoldwalletbasic:

8. Restart the Cold wallet to pick up the `masternode.conf` changes.

.. _listconfbasic:

9. Open the Debug console (Open **Tools > Debug console**) and run the command **masternode list-conf**::

	masternode list-conf

* Verify that the output matches what you entered in the `masternode.conf` file.

.. _masternodetabbasic:
	
10. Go to Masternodes tab and check if your newly added MasterNode is listed.

	* You should now see the newly added MasterNode with a status of `MISSING`.
	
* NOTE: If you want to control multiple MasterNode Hot wallets from this Cold wallet, you will need to repeat the previous steps 2-9. The `masternode.conf` file requires an entry for each MasterNode that you will be managing with this Cold wallet.
 

Starting the MasterNode from the Cold Wallet
--------------------------------------------

.. warning:: It is very important that you let the MasterNode Hot wallet synchronize for a couple of hours prior to starting it from the Cold wallet.  If you attempt to start it before it is fully synchronized then it will fail.

.. _startmasternodebasic:
	
11. Run the **startmasternode alias false MN1** command, in the Cold wallet Debug console, in order to enable the MasterNode::

	startmasternode alias false MN1

* In the example above, the alias of my MasterNode was MN1. In your case, it might be different and is based on what you entered as the first word in the masternode.conf file.
* You should get multiple lines of output.  If one of the lines of output says **"result" : successful"** then you can proceed to the next step to verify the MasterNode started correctly on the VPS Hot wallet.  If you did not get the **successful** output then there is likely an issue with the masternode.conf file that needs to be resolved first.

	
**If you received the output that shows the MasterNode started successfully then you can proceed to the next step to verify that your MasterNode started correctly from the VPS Hot wallet.**