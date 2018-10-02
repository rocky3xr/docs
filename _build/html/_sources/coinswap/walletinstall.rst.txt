.. _walletinstall:
.. _Video: https://www.youtube.com/watch?v=0TU044CYfl4/
.. _Windows_64bit: https://github.com/rupaya-project/rupx/releases/download/v5.0.25/rupayaqt-windows-64bit.zip
.. _Windows_x86: https://github.com/rupaya-project/rupx/releases/download/v5.0.25/rupayaqt-windows-32bit.zip
.. _Linxu_64bit: https://github.com/rupaya-project/rupx/releases/download/v5.0.25/rupayaqt-linux-64bit.tar.gz

.. _installnewwallet:

====================================
Install the New Rupaya Core 5 Wallet
====================================

These instructions are intended for those that are installing the new Rupaya Core 5 wallet on your personal Windows or Mac computer.

.. warning:: Do not install the new wallet on the computer that contains the Rupaya wallet that is holding your existing coins.  You will need to either install the new wallet on a different computer or move your coins to a different computers' wallet, prior to installing the new wallet.  This is to prevent any chance that the new wallet will overwrite your current wallet and cause you to lose your coins.

1. Be sure that your existing wallet.dat and private keys are backed up from the old wallet.  We strongly recommend backing up your wallet.dat and private keys prior to starting this process.

	For more instructions, watch this Video_ from a fellow Rupayan, David Coen, on how to export your private keys:
	
2. Delete the old Rupaya directory, if the computer contains the old Rupaya wallet::

	* Mac: ~/Library/Application Support/Rupayacore
	* Windows: ~\AppData\Roaming\Rupaya

.. warning:: Do not delete the current wallet directory if the existing wallet still has coins in it.  You should be doing this install on a computer that does not currently have a Rupaya wallet that contains coins.
	
3. Open the following URL in a web browser to download the appropriate wallet version for your system:

	* https://github.com/rupaya-project/rupx/releases
	
4. Once downloaded, unzip the files and move the Rupaya-cli and Rupaya-qt files onto the desktop.  

	* If prompted, confirm that you want to replace the existing file(s).

5.Double click the Rupaya-qt file to install the new wallet.

	* If you are prompted to use a data directory then select the radio button next to **Use the default data directory** and click **OK**
	* Accept any pop ups asking to confirm if you want to continue with the installation
	* When prompted, select **Use the default data directory** and click **OK**
	* If prompted by security or antivirus software, click **Allow Always**
	* The new wallet should now open and begin to synchronize with the network

NOTE: If the wallet is not synchronizing, then add the following line into the rupaya.conf configuration file **(Tools > Open Wallet Configuration File)**::
 
	addnode=seeds.rupx.io
	
NOTE: The file should be blank by default.  **Be sure to restart the wallet every time you update the configuration file.**
	
Documenting Your New Wallet Address
===================================

Now that the new Rupaya Core 5 wallet is installed, you need to document your new wallet address to prepare for the coin swap with the Swap Bot.

1. Open the new Rupaya Core wallet.

2. Click on **File** and select **Receiving addresses**.

3. Select the wallet address that is labeled **no label** and click **Copy**.

	* You can name the wallet with a description such as "New Wallet" by right clicking it and selecting "Edit".

4. Save this wallet address somewhere for safe keeping as you will be using it later in the process to convert your coins with the Swap Bot.  

	
Updating the Wallet Default Settings
====================================

Now that the new wallet is installed, let's take care of updating some very important default wallet settings.  These steps are especially critical if you plan to setup a MasterNode.

Enable Coin Control
^^^^^^^^^^^^^^^^^^^

This feature will allow you to control your wallet inputs, to verify that all coins are consolidated into a single input, to choose which inputs you send coins from, and to optimize staking.

1. Open the Rupaya Wallet and click on **Settings**
2. Select **Options**
3. Click on the **Wallet** tab
4. Click the check-box that says **Enable coin control features**

Disable zRUPX Automint
^^^^^^^^^^^^^^^^^^^^^^

This feature will disable the auto minting of RUPX into zRUPX.

1. Open the Rupaya Wallet and click on **Settings**
2. Select **Options**
3. Click on the **Main** tab
4. Uncheck the check-box that says **Enable zRUPX Automint**
5. Click **OK** to close the wallet options.

	**NOTE: THIS IS A CRITICAL STEP FOR THOSE THAT PLAN TO RUN A MASTERNODE**

**Once completed, you can proceed to the next step to perform the coin swap with the Swap Bot.**