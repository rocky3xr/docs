.. _downloadputty:

===========================================
PC Users - Download Putty and Configure SSH
===========================================

These instructions are intended for PC users that will be using Putty and SSH keys to login to the Linux VPS.  If you already have Putty installed and are able to connect to the Linux VPS using an SSH key then you can skip this process and proceed to the next section to :ref:`disable password logins and root login access<disablepasswordlogins>`.

**Download and Configure Putty**

1. :ref:`Download the Putty terminal emulator<downloadputty_downloadputty>`
2. :ref:`Move the Putty application to your Desktop<moveputty_downloadputty>`
3. :ref:`Open Putty and create a saved session for your Linux VPS<createputtysession_downloadputty>`

**Configure Putty to use an SSH Key**

1. :ref:`Import the SSH Private Key into the saved session for the Linux VPS<puttyimportprivkey_downloadputty>`
2. :ref:`In the Putty window, click Open to connect to your Linux VPS<connectwithputty_downloadputty>`
3. :ref:`Login to the Linux VPS as the root user<loginasroot_downloadputty>`

**Configure the Linux VPS to use an SSH Key**

1. :ref:`Change directory into the /root/.ssh directory or create it if necessary<changetosshdir_downloadputty>`
2. :ref:`Create and edit the file named authorized_keys<editauthorizedkeys_downloadputty>`
3. :ref:`Paste the SSH Key into the authorized_keys file on the Linux VPS<pastesshkey_downloadputty>`
4. :ref:`Verify you can now login to the Linux VPS without entering a password<loginwithoutpass_downloadputty>`

.. _downloadputty_downloadputty:

Downloading and Configuring Putty
---------------------------------

1. Download the Putty terminal emulator that matches your OS.

	* `Download Putty 64 bit <https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe>`_
	* `Download Putty 32 bit <https://the.earth.li/~sgtatham/putty/latest/w32/putty.exe>`_
	
.. _moveputty_downloadputty:

2. Move the Putty application to your Desktop.

.. _createputtysession_downloadputty:

3. Open Putty and create a saved session named **rupx01** for your Linux VPS.

	* In the **Hostname** field, type in your Linux VPS IP address
	* In the **Saved Sessions** field, type in the name **rupx01**
	* Click **Save** to save the session

.. _puttyimportprivkey_downloadputty:
	
Configure Putty to use an SSH Key
---------------------------------

1. Follow these steps to add the SSH key into the **rupx01** Putty session.

	* Click on the saved session named **rupx01** and click **Load** 
	* Expand the **SSH** Category on the left side of the window
	* Click on the **Auth** Category so that it is highlighted
	* Click on **Browse** next to the **Private key file for authentication** field
	* Browse to the folder that contains your SSH private key
	* Select the **sshprivatekey.ppk** file and click **Open**
	* Scroll back up on the left under **Category** and click on the word **Session**, at the top of the window, to bring back the session page
	* Click on **Save** to save the SSH Key to the **rupx01** session.  **NOTE: This step is very important.  Make sure that your server rupx01 is loaded in the Saved Sessions window and that you click Save.  If this step is not completed successfully, then your SSH Key will not be saved to this session and you will have to repeat these steps again**

.. _connectwithputty_downloadputty:

2. In the Putty window, click **Open** to connect to your Linux VPS.

	* Click Yes on the PuTTY Security Alert to install the security certificate

.. _loginasroot_downloadputty:

3. 	At the **login as:** prompt, type in **root** and hit **ENTER** to login to the Linux VPS as the **root** user.

	* At the **password:** prompt, paste in or type in the root password and hit **ENTER**
	* **The screen will not display your password**
	* **NOTE:** For those using Digital Ocean as your VPS provider, you will be prompted to change your **root** password.

.. _changetosshdir_downloadputty:

Configure the Linux VPS to use an SSH Key
-----------------------------------------------------------

You should be logged into the Linux VPS as the **root** user to complete the following steps:

1. Change directory into the /root/.ssh directory or create it if necessary::

	cd /root/.ssh

* NOTE: If the directory does not already exist then use this command to create it::

	mkdir /root/.ssh

.. _editauthorizedkeys_downloadputty:

2. Create and edit the file named authorized_keys with the following command::

	nano /root/.ssh/authorized_keys

.. _pastesshkey_downloadputty:

3. Paste the SSH Key into the **authorized_keys** file on the Linux VPS.  This is the key that you generated with the PuttyGen application.

* Save and close the file by hitting **Ctrl-X**, and then type **Y** to confirm that you want to save it, and then hit **ENTER** to confirm the file name.
* NOTE: Your new SSH key is now saved in the /root/.ssh/authorized_keys file.  All future logins with the root username will allow you to login without being prompted for a password.

.. _loginwithoutpass_downloadputty:

**Let's test it!**
	
4. Verify you can now login to the Linux VPS without entering a password.  

	* Duplicate the existing Putty session to the Linux VPS by clicking the icon of two computers on the top left of the Putty application window and then select **Duplicate Session**
	* At the **login as:** prompt, type in **root** and hit **ENTER** 
	* **NOTE: You should be automatically logged in to the Linux VPS without having to type in the root password**
	
.. warning::  If you are not automatically logged in without typing in a password then you likely did not save the SSH key into the putty session correctly, or you did not save the entire SSH key into the Linxu VPS file /root/.ssh/authorized_keys.  You will need to walk through the steps to save the SSH key in the Putty session and to ensure that the ENTIRE SSH key is added to the authorized_keys file on the Linux VPS before you proceed with the next section.
	
**If you are able to use Putty to login to the Linux VPS without being prompted for a password then you are done configuring your SSH keys and can proceed to the next section to disable password logins and root login access.**