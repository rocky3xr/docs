.. _upgradeexistingmn:

.. _upgradehotwallet:

=============================================
Upgrade an Existing MasterNode VPS Hot Wallet
=============================================

These instructions are intended for those that are already running a MasterNode and want to upgrade an existing VPS with the new Rupaya Core 5 wallet.

.. warning::  We created this process for those of you that want to continue to use the same VPS.  However, there is some minor risk involved as you may need to reboot the VPS during this process.  If you are running MasterNodes from other coins on this same VPS then those MasterNodes may be impacted by the VPS reboots.  To prevent the possible impact to the other MasterNodes you are running on this VPS, we suggest doing a fresh install, on a new VPS. :ref:`Link to VPS and Hot wallet basic setup guide<basicsetup>`

1. Login to the VPS provider website and update the external firewall ports to allow TCP port 9050 from all sources instead of port 9020.  You can edit the existing rule and change the port from 9020 to 9050.   

	* **NOTE: This is not necessary for Virmach VPS users since they do not provide an external firewall.**
	
2. Use Putty (PC) or Terminal (MAC) to login to the Linux VPS that is running the Rupaya Hot wallet.  

3. Login as the user that you used to install the wallet.  Below are some of the possible usernames you may have used, depending on which installation guide you followed:

	* root (github)
	* rupxmn (http://rupx.center/mnode)
	* rupx01 (GoodTimes setup guide)

	Note: These instructions will assume that you did not use root as the default user and therefore provides the commands starting with sudo to allow the commands to run with root privileges.

4. Stop the current wallet daemon with the following command::

	rupaya-cli stop

5. Display the contents of your existing rupaya.conf file::

	cat ~/.rupaya/rupaya.conf

6. Copy the contents of the rupaya.conf file and paste it into a text editor so you can easily update the necessary fields.

7. In the text editor, update the following information to start using port 9050 instead of 9020:

	* On the line **externalip=** change port 9020 to the new port 9050

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

13. **OPTIONAL STEP:** The following steps (13A - 13C) are optional.  These steps are strongly recommended for those that want to implement security best practices.  These steps are recommended so that the Hot wallet is not installed under the root user account.

	* In these steps you will create a new user named **rupxmn**, set a password, grant that user root access, and login as the new user.
	* All advanced Rupaya setup guides will assume that you used **rupxmn** as your user.
	* For those of you that want to continue to use **root** as your user instead of **rupxmn**, you can skip ahead to step 14.
	
13A. Create a new user named **rupxmn** and assign a password to the new user::

	useradd -m -s /bin/bash rupxmn
	passwd rupxmn

**Type in a new password, as you are prompted, two times.  Be sure to save this password somewhere safe, as you will need it to manage the VPS Hot wallet.**

13B. Grant root access to the new user rupxmn::

	usermod -aG sudo rupxmn
	
13C. Login as the new user::

	sudo login rupxmn

14. Install the new wallet by running the **rupayad -daemon** command::

	rupayad -daemon

15. Generate a new MasterNode Private Key (aka GenKey)::

	rupaya-cli masternode genkey

16. Copy the outputted GenKey and paste it in the text editor, overwriting the old GenKey, with the new one you just copied, on the line **masternodeprivkey=**

17. Stop the Hot wallet with the **rupaya-cli stop** command::

	rupaya-cli stop

18. Edit the new rupaya.conf file::

	nano ~/.rupayacore/rupaya.conf

19. Copy the contents from the text editor, that you copied from the old rupaya.conf file, and paste all of the lines into the new rupaya.conf file.

20. Close the file and save it by hitting **Ctrl-X**, and then type **Y** to confirm that you want to save it, and then hit **ENTER** to confirm the file name.

21. Restart the Hot wallet with the **rupayad -deamon** command::

	rupayad -daemon
	
* NOTE: If you get the error "**error: couldn't connect to server**" then you may need to kill the process manually or reboot the VPS and then restart the wallet with the **rupayad -daemon** command.

21. Run the **ps -ef |grep rupaya** command to verify that the daemon is indeed running::

	ps -ef |grep rupaya
	
NOTE: You should get output showing that the **rupayad -daemon** is running.  If you only see one single line that contains this output "**grep --color=auto rupaya**" then the daemon is not actually running.  In this case, you may need to restart the VPS and then run the **rupayad -daemon** command to start the daemon successfully.

**Once the rupayad -daemon service is confirmed as running, the setup of your new VPS and Hot wallet is complete.  Please proceed to the next step to set up the Cold Wallet on your computer.**