.. _disablepasswordlogins:

===========================================================
All Users - Disabling Password Logins and Root Login Access
===========================================================

These instructions are intended for all users that want to reduce the risk of brute force login attacks by disabling password logins and root login access.  These procedures will improve security to your Linux VPS by requiring the correct SSH Key to be able to login.  After completing these steps, any computer, or SSH session, that does not have the correct SSH Key installed will not be able to login to the Linux VPS, and you will no longer be able to remotely login to the Linux VPS using the root user. 

Disabling password login capabilities
-------------------------------------

* You should be logged in to the Linux VPS as the **root** user to complete the following steps:

1. The following commands will edit the SSH file **/etc/ssh/sshd_config**, will disable password login capabilities, and will then restart the **sshd** service to apply the change::

	sed -i 's/PasswordAuthentication yes/PasswordAuthentication no/g' /etc/ssh/sshd_config
	systemctl reload sshd

**Let's test it!**
	
2. Open a new Putty session to the Linux VPS by clicking the icon of two computers on the top left of the Putty application window and then select **New Session**.

3. In the **Hostname** field, type in the IP address of the Linux VPS and then click **Open**.

* Do **NOT** open the existing **rupx01** session.  We are testing to ensure username and password authentication has been successfully disabled.  To do that you need to connect to a new session that does not have the SSH key installed.

4. At the **login as:** prompt, type in **root** and hit **ENTER**.

* It should no longer allow you to login and a pop up window should appear with the following error: **Disconnected: No supported authentication methods available**

Disabling root login access
---------------------------

* You should be logged in to the Linux VPS as the root user to complete the following steps:

1. The following commands will edit the SSH file **/etc/ssh/sshd_config**, will disable root login access, and will then restart the **sshd** service to apply the change::

	sed -i 's/PermitRootLogin yes/PermitRootLogin no/g' /etc/ssh/sshd_config
	systemctl reload sshd

**Let's test it!**
	
2. Open a duplicate Putty session by clicking the icon of two computers on the top left of the Putty application window, then select **Duplicate Session**.  If saved correctly, this will open a session to the Linux VPS that already has the SSH key loaded.

3. At the **login as:** prompt, type in **root** and hit **ENTER**.  

* It should no longer allow you to login and a pop up window should appear with the following error: **Disconnected: No supported authentication methods available**

**If password authentication and root login access have been successfully disabled then you can proceed to the next section to begin the** :ref:`MasterNode Basic Setup<basicsetup>`.