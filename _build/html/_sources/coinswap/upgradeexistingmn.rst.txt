.. _upgradeexistingmn:

=============================================
Upgrade an Existing MasterNode VPS Hot Wallet
=============================================

These instructions are intended for those that are already running a MasterNode and want to upgrade an existing VPS with the new Rupaya Core 5 wallet.

.. warning::  We created this process for those of you that want to continue to use the same VPS.  However, there is some minor risk involved as you may need to reboot the VPS during this process.  If you are running MasterNodes from other coins on this same VPS then those MasterNodes may be impacted by the VPS reboots.  To prevent the possible impact to the other MasterNodes you are running on this VPS, we suggest doing a fresh install, on a new VPS.

1. Login to the VPS provider website and update the external firewall ports to allow TCP port 9050 from all sources instead of port 9020.  You can edit the existing rule and change the port from 9020 to 9050.   

	* **NOTE: This is not necessary for Virmach VPS users since they do not provide an external firewall.**
	
2. Use Putty (PC) or Terminal (MAC) to login to the Linux VPS that is running the Rupaya Hot Wallet.  

3. Login as the user that you used to install the wallet.  Below are some of the possible usernames you may have used, depending on which installation guide you followed:

	* root (github)
	* rupxmn (http://rupx.center/mnode)
	* rupx01 (GoodTimes setup guide)

	Note: These instructions will assume that you used root as the default user since most MasterNodes were setup using the github instructions.  If you used a different username then just update the provided commands with your username rather than root.

4. Stop the current wallet daemon with the following command::

	rupaya-cli stop

5. Display the contents of your existing rupaya.conf file::

	cat ~/.rupaya/rupaya.conf

6. Copy the contents of the rupaya.conf file and paste it into a text editor so you can easily update the necessary fields.

7. In the text editor, change port 9020 to the new port 9050.  The port can be found at the end of the following line::

	externalip=

8. Save the text file to be sure you don't lose any of the data during the process.

9. Back on the VPS, delete the existing rupayad daemon from the **/usr/local/bin** directory::

	sudo rm /usr/local/bin/rupayad
	sudo rm /usr/local/bin/rupaya-cli
	sudo rm /usr/local/bin/rupaya-qt

10. Delete the existing ~/.rupaya folders::

	sudo rm -rf ~/.rupaya

11. Update the internal firewall to allow TCP port 9050 and to block 9020::

	sudo ufw allow 9050/tcp
	sudo ufw deny 9020/tcp

12. Download the new wallet and extract it to the **/usr/local/bin** directory::

	wget https://github.com/rupaya-project/rupx/releases/download/v5.0.25/rupayaqt-linux-64bit.tar.gz
	sudo tar xvzf rupayaqt-linux-64bit.tar.gz -C /usr/local/bin/

13. Install the new wallet by running the **rupayad** command::

	rupayad -daemon

14. Generate a new MasterNode Private Key (aka GenKey)::

	rupaya-cli masternode genkey

15. Copy the outputted GenKey and paste it in the text editor, overwriting the old GenKey, with the new one you just copied, on the line **masternodeprivkey=**

16. Edit the new rupaya.conf file::

	nano ~/.rupayacore/rupaya.conf

17. Copy the contents from the text editor, that you copied from the old rupaya.conf file, and paste all of the lines into the new rupaya.conf file.

18. Close the file and save it by hitting **Ctrl-X**, and then type **Y** to confirm that you want to save it, and then hit **ENTER** to confirm the file name.

19. Stop and restart the wallet deamon::

	rupaya-cli stop && sleep 60 && rupayad -daemon

* NOTE: If you get the error "error: couldn't connect to server" then you may need to kill the process manually or reboot the VPS.

**Your new VPS setup is now complete.  Please proceed to the next step to set up the Cold Wallet on your computer.**
