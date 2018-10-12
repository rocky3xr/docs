.. _Putty: https://putty.org/
.. _adv-vpsandhotwallet:
.. |br| raw:: html

   <br />
   
========================
VPS and Hot wallet Setup
========================

These instructions are intended for advanced users that are setting up a MasterNode Hot wallet on a Linux VPS and don't want to waste time with all those pesky details and explanations.

Order and setup a Linux VPS
---------------------------
	
.. _identifyvps_vpsandhotwallet:

1. Identify a VPS provider and order a Linux Ubuntu 16.04 server.

	**Recommended VPS Providers:**
	
	* `Digital Ocean <https://m.do.co/c/95a89fb0b62d>`_
	* `Vultr <https://www.vultr.com/?ref=7318338>`_
	* `Linode <https://www.linode.com/>`_
	* `Amazon Web Services (AWS) <https://aws.amazon.com/>`_

	|br|
	**VPS Requirements**
	
	* Linux - Ubuntu 16.04 - 64 Bit OS
	* 1GB of RAM
	* 20GB of disk space
	* Dedicated Public IP Address 
	
2. Login to the VPS provider website and configure the external firewall to allow SSH port 22 and the Rupaya Wallet TCP port 9050.
	
3. Login to the VPS, via SSH, as the **root** user.

4. Install Linux updates::

	apt install make
	apt install aptitude -y
	apt-get update -y
	apt-get upgrade -y

5. Install fail2ban and create modifiable configs for fail2ban and its jail settings.   Run these commands **one at a time** to install basic ssh protection with fail2ban::

	apt-get install fail2ban -y
	cp /etc/fail2ban/fail2ban.conf /etc/fail2ban/fail2ban.local
	cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local

6. Install tzdata.  Run the following command to install the application that will allow you to select your clock timezone::

	apt install tzdata

7. Set your time zone.  Run the following command to set your preferred time zone::

	dpkg-reconfigure tzdata

8. Configure a virtual swap space on the VPS to avoid running out of memory::

	fallocate -l 3000M /mnt/3000MB.swap
	dd if=/dev/zero of=/mnt/3000MB.swap bs=1024 count=3072000
	mkswap /mnt/3000MB.swap
	swapon /mnt/3000MB.swap
	chmod 600 /mnt/3000MB.swap
	echo '/mnt/3000MB.swap  none  swap  sw 0  0' >> /etc/fstab

9. Configure the VPS internal firewall to allow SSH port 22 and the Rupaya Wallet port 9050::

	ufw allow 22/tcp	
	ufw limit 22/tcp	
	ufw allow 9050/tcp 	
	ufw logging on
	ufw --force enable
	
Create a New User and Login as rupxmn
-------------------------------------

1. Create a new user named **rupxmn** and assign a password to the new user::

	useradd -m -s /bin/bash rupxmn
	passwd rupxmn

2. Grant root access to the new user rupxmn::

	usermod -aG sudo rupxmn

3. Login as the new user rupxmn::

	login rupxmn
	
Download and Configure the Rupaya Hot wallet
--------------------------------------------

1. Install the Rupaya Hot wallet on the VPS::

	wget https://github.com/rupaya-project/rupx/releases/download/v5.0.25/rupayaqt-linux-64bit.tar.gz
	sudo tar xvzf rupayaqt-linux-64bit.tar.gz -C /usr/local/bin/
	
2. Start the Hot wallet::

	rupayad -daemon

3. Generate the MasterNode private key (aka GenKey)::

	rupaya-cli masternode genkey

4. Copy and save the MasterNode private key (GenKey) from the previous command to be used later in the process:

5. Stop the Hot wallet with the **rupaya-cli stop** command::

	rupaya-cli stop
	
6. Copy the rupaya.conf template, paste it into a text editor, and update the variables manually::
	
	rpcuser=rupayarpc 
	rpcpassword=<alphanumeric_rpc_password> 
	rpcport=7050 
	rpcallowip=127.0.0.1 
	rpcconnect=127.0.0.1 
	rpcbind=127.0.0.1 
	maxconnections=512 
	listen=1 
	daemon=1
	masternode=1
	externalip=<public_mn_ip_address_here>:9050 
	masternodeaddr=<public_mn_ip_address_here> 
	masternodeprivkey=<your_masternode_genkey_output> 
	
7. Edit the MasterNode Hot wallet configuration file **~/.rupayacore/rupaya.conf**::

	nano ~/.rupayacore/rupaya.conf

8. Paste the updated template into the **rupaya.conf** configuration file on the Linux VPS.

9. Save and exit the file by typing **CTRL+X** and hit **Y** + **ENTER** to save your changes.

10. Restart the Hot wallet with the **rupayad -daemon** command::

	rupayad -daemon
	
Verify the Hot wallet is synchronizing with the blockchain
----------------------------------------------------------

1. Run the **rupaya-cli getinfo** command to make sure that you see active connections::
	
	rupaya-cli getinfo
	
2. Run the **rupaya-cli getblockcount** command every few mins until you see the blocks increasing::
	
	rupaya-cli getblockcount

* NOTE: If your block count is **NOT** increasing then you will need to stop the Hot wallet with the **rupaya-cli stop** command and then reindex with the **rupayad -reindex** command. 
* **NOTE: If you did the reindex and you continue to have issues with establishing connections then check that the VPS provider external firewall is setup correctly to allow TCP port 9050 from anywhere.  If that is not setup correctly then you will not be able to proceed beyond this step.**
	
**If your block count is indeed increasing, then you can proceed to the next step to setup the Cold wallet.**