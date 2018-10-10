.. _hotwalletautostart:

==============================
Enabling Hot Wallet Auto Start
==============================


This section is intended for MasterNode users that want to configure the Linux VPS to automatically start the MasterNode Hot wallet when the Linux VPS is rebooted.

1. Connect to your Linux VPS and login as **root**.  

* Be sure that you are logged in as **root** or many of the commands will not work.

2. Run the following command to create and edit the file **/etc/cron.d/resetrupaya**.  This file will be used to tell the server to restart the Hot wallet upon bootup::

	nano /etc/cron.d/resetrupaya
	
3. Copy the following text and paste it into the resetrupaya file.  This will create a cronjob that will start the Hot wallet automatically in the event that the server is rebooted::

	@reboot rupxmn sleep 5 && /usr/local/bin/rupayad

* Save and close the file by hitting **Ctrl-X**, and then type **Y** to confirm that you want to save it, and then hit **ENTER** to confirm the file name.

4. Reboot the Linux VPS to test and verify that the Hot wallet will restart upon boot::

	reboot

5. Wait a couple minutes and then reconnect your Linux VPS and login as **root**.  

* It will take a couple of minutes for the Linux VPS to reboot.

6. Run the command **ps -ef |grep rupayad** to verify the Hot wallet is running::

	ps -ef | grep rupayad
	
* You should get two lines of output, and one of the lines will have the text **/usr/local/bin/rupayad**.  
* If you only get one line of text with the output **grep --color=auto rupaya** then the wallet is not running and you will need to walk through the above steps again.

7. Run the command **rupaya-cli getblockcount** to verify that your Hot wallet is indeed running and that your block count is increasing::

	runuser -l rupxmn -c 'rupaya-cli getblockcount'
	
* The above command is using the **runuser** option because you are currently logged in a **root** and need to run the command from the **rupxmn** user.

8. Verify that your MasterNode is still showing up on the MasterNode tracker website.  The site is refreshed every 5 minutes so check it a few times just to be sure.

* http://rupx5.mn.zone/

**If the MasterNode Hot wallet automatically restarts after a reboot then you have successfully completed this section.  CONGRATULATIONS!!  The setup of your MasterNode is now fully complete!**  

**NOTE: There is no need to proceed to the next section since all of the configuration steps have been completed.** 