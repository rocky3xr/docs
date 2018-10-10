.. _walletinstall:
.. _Video: https://www.youtube.com/watch?v=0TU044CYfl4/

.. _installnewwallet:

====================================
Install the New Rupaya Core 5 Wallet
====================================

These instructions are intended for those that are installing the new Rupaya Core 5 wallet on your personal Windows or Mac computer.

Requirements:
--------------
	* Windows 7 or higher, Mac OS, or Linux
	* Outgoing internet access to sync the blockchain and enable the MasterNode remotely

Install the Rupaya Core Wallet
------------------------------

1. Open the following URL in a web browser to download the appropriate wallet version for your system:

	* https://github.com/rupaya-project/rupx/releases

.. warning:: Do not install the new wallet on the computer that contains an existing Rupaya wallet that is currently holding RUPX coins.  You will need to either install the new wallet on a different computer or move your coins to a different computers' wallet, prior to installing the new wallet.  This is to prevent any chance that the new wallet will overwrite your current wallet and cause you to lose your coins.

2. Be sure that your existing wallet.dat and private keys are backed up from the old wallet.  We strongly recommend backing up your wallet.dat and private keys prior to starting this process.

	For more instructions, watch this Video_ from a fellow Rupayan, David Coen, on how to export your private keys:

3. Rename the old Rupaya directory to something like **rupaya4**. This will prevent the new wallet install from conflicting with any of the existing data.  This is only required if the computer contains the old Rupaya wallet:

	* Mac: ~/Library/Application Support/Rupaya
	* Windows: ~/AppData/Roaming/Rupaya

* NOTE: If you are confident that you no longer need this old data then you can just delete the old rupaya directory instead of renaming it.

.. warning:: Do not delete the current wallet directory if the existing wallet still has coins in it.  You should be doing this install on a computer that does not currently have a Rupaya wallet that contains coins.
	
4. Unzip the wallet files and move the Rupaya-cli and Rupaya-qt files onto the Desktop or Application folder.  

	* If prompted, confirm that you want to replace the existing file(s).

5.Double click the Rupaya-qt file to open and install the new wallet.

	* If you are prompted to use a data directory then select the radio button next to **Use the default data directory** and click **OK**
	* Accept any pop ups asking to confirm if you want to continue with the installation
	* When prompted, select **Use the default data directory** and click **OK**
	* If prompted by security or antivirus software, click **Allow Always**
	* The new wallet should now open and begin to synchronize with the network

Documenting Your New Wallet Address
-----------------------------------

Now that the new Rupaya Core 5 wallet is installed, you need to document your new wallet address to prepare for the coin swap with the Swap Bot.

1. Open the new Rupaya Core wallet.

2. Click on **File** and select **Receiving addresses**.

3. Select the wallet address that is labeled **no label** and click **Copy**.

	* You can name the wallet with a description such as **New Wallet** by right clicking it and selecting "Edit".

4. Save this wallet address somewhere for safe keeping as you will be using it later in the process to convert your coins with the Swap Bot.  

	
Updating the Wallet Default Settings
------------------------------------

Now that the new wallet is installed, let's take care of updating some very important default wallet settings.  These steps are especially critical if you plan to setup a MasterNode.

Enable Coin Control
-------------------

This feature will allow you to control your wallet inputs, to verify that all coins are consolidated into a single input, to choose which inputs you send coins from, and to optimize staking.

1. Open the Rupaya Wallet and click on **Settings**
2. Select **Options**
3. Click on the **Wallet** tab
4. Click the check-box that says **Enable coin control features**

Disable zRUPX Automint
----------------------

This feature will disable the auto minting of RUPX into zRUPX.

1. Open the Rupaya Wallet and click on **Settings**
2. Select **Options**
3. Click on the **Main** tab
4. Uncheck the check-box that says **Enable zRUPX Automint**
5. Click **OK** to close the wallet options.

	**NOTE: THIS IS A CRITICAL STEP FOR THOSE THAT PLAN TO RUN A MASTERNODE**

**Once completed, you can proceed to the next step to perform the coin swap with the Swap Bot.**