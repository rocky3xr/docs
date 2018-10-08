.. _Putty: https://putty.org/
.. |br| raw:: html

   <br />

.. _basicsetup:
   
========================
VPS and Hot wallet Setup
========================

This server and wallet will run 24/7 and provides services to the network via TCP port **9050** for which it will be rewarded with coins. It will run with an empty wallet reducing the risk of losing the funds in the event of an attack.

**Order and setup a Linux VPS**
	
1. :ref:`Identify a VPS provider and order a Linux Ubuntu 16.04 server<identifyvps>`
2. :ref:`Login to the VPS provider website and configure the external firewall to allow SSH port 22 and the Rupaya Wallet port 9050<externalfirewall>`
3. :ref:`Login to the VPS via SSH<loginviassh>`
4. :ref:`Configure a virtual swap space on the VPS to avoid running out of memory<swapspace>`
5. :ref:`Configure the VPS internal firewall to allow SSH port 22 and the Rupaya Wallet port 9050<allowssh>`
	
**Create a New User and Login as rupxmn**

1. :ref:`Create a new user named rupxmn<createnewuserbasic>`
2. :ref:`Grant root access to the new user rupxmn<grantrootaccessbasic>`
3. :ref:`Login as the new user rupxmn<loginasnewuserbasic>`

**Download and Configure the Rupaya Hot wallet**
	
1. :ref:`Install the Rupaya Hot wallet on the VPS<downloadwallet>`
2. :ref:`Start the Hot wallet service<startservice>`
3. :ref:`Generate the MasterNode private key (aka GenKey)<generategenkey>`
4. :ref:`Copy and save the MasterNode private key<savegenkey>`
5. :ref:`Stop the Hot wallet with the rupaya-cli stop command<stophotwallet>`
6. :ref:`Edit the Hot wallet configuration file (~/.rupayacore/rupaya.conf)<editconfig>`
7. :ref:`Copy the rupaya.conf template and update the configuration data accordingly<copyconfig>`
8. :ref:`Paste the updated template into the rupaya.conf configuration file<pastetemplate>`
9. :ref:`Save and exit the file by typing CTRL+X and hit Y + ENTER to save your changes<saveconfig>`
10. :ref:`Restart the Hot wallet with the rupayad -daemon command<starthotwallet>`
	
**Verify the Hot wallet is synchronizing with the blockchain**
	
1. :ref:`Run the rupaya-cli getinfo command to make sure that you see active connections<getinfo>`
2. :ref:`Run the rupaya-cli getblockcount command every few mins until you see the blocks increasing<blockcount>`

Order and setup a Linux VPS
---------------------------
	
.. _identifyvps:

1. Identify a VPS provider and order a Linux Ubuntu 16.04 server.  Order the VPS server from a provider like DigitalOcean, Vultr, Linode, Amazon AWS, etc.  It's important not to run the VPS at home because of the risk of network instability that could cause loss of connectivity to the server.

	**VPS Requirements**
	
	* Linux 64 bit, (e.g. Ubuntu 16.04)
	* Dedicated Public IP Address
	* Recommended at least 1GB of RAM and 20GB of disk space
	* Basic Linux skills
	
	|br|	
	You can get servers like this for $5 a month and can run 3 to 4 MasterNode wallets, from different coins, if the monthly cost is a concern.

.. _externalfirewall:

2. Login to the VPS provider website and configure the external firewall to allow SSH port 22 and the Rupaya Wallet port 9050
	
.. _loginviassh:
	
3. Login to the VPS, via SSH, as the **root** user.

	For Windows users, Putty_ is a very good SSH client that you can use to connect to a remote Linux server.
	If you are running a VPS from Vultr, or a similar provider, then you need to use an SSH client, such as Putty_, if you want to have copy and paste functionality. Otherwise you will have to type them all out manually!

.. _swapspace:
	
4. Configure a virtual swap space on the VPS to avoid running out of memory::

	fallocate -l 3000M /mnt/3000MB.swap
	dd if=/dev/zero of=/mnt/3000MB.swap bs=1024 count=3072000
	mkswap /mnt/3000MB.swap
	swapon /mnt/3000MB.swap
	chmod 600 /mnt/3000MB.swap
	echo '/mnt/3000MB.swap  none  swap  sw 0  0' >> /etc/fstab
	
.. _allowssh:

5. Configure the VPS internal firewall to allow SSH port 22 and the Rupaya Wallet port 9050::

	ufw allow 22/tcp	
	ufw limit 22/tcp	
	ufw allow 9050/tcp 	
	ufw logging on
	ufw --force enable

.. _createnewuserbasic:
	
Create a New User and Login as rupxmn
-------------------------------------

**OPTIONAL STEP:** The following steps (1 - 3) are optional.  These steps are strongly recommended for those that want to implement security best practices.  These steps are recommended so that the Hot wallet is not installed under the root user account.

	* In these steps you will create a new user named **rupxmn**, set a password, grant that user root access, and login as the new user.
	* All advanced Rupaya setup guides will assume that you used **rupxmn** as your user.
	* For those of you that want to continue to use **root** as your user instead of **rupxmn**, you can skip ahead to the next section :ref:`Download and Configure the Rupaya Hot Wallet<hotwalletinstallbasic>`.

1. Create a new user named **rupxmn** and assign a password to the new user::

	useradd -m -s /bin/bash rupxmn
	passwd rupxmn

**Type in a new password, as you are prompted, two times.  Be sure to save this password somewhere safe, as you will need it to manage the VPS Hot wallet.**

.. _grantrootaccessbasic:

2. Grant root access to the new user rupxmn::

	usermod -aG sudo rupxmn

.. _loginasnewuserbasic:
	
3. Login as the new user rupxmn::

	sudo login rupxmn

.. _hotwalletinstallbasic:
	
Download and Configure the Rupaya Hot wallet
--------------------------------------------

.. _downloadwallet:

1. Install the Rupaya Hot wallet on the VPS.  Download and unpack the Rupaya wallet binaries by running the following commands::

	wget https://github.com/rupaya-project/rupx/releases/download/v5.0.25/rupayaqt-linux-64bit.tar.gz
	sudo tar xvzf rupayaqt-linux-64bit.tar.gz -C /usr/local/bin/
	
.. _startservice:
	
2. Start the Hot wallet service.  When the service starts, it will create the initial data directory(`/root/.rupayacore/`)::

	rupayad -daemon
	
.. _generategenkey:

3. Generate the MasterNode private key (aka GenKey).  Wait a few seconds after starting the wallet service and then run this command to generate the masternode private key::

	rupaya-cli masternode genkey

.. _savegenkey:

4. Copy and save the MasterNode private key from the previous command to be used later in the process.  The value returned should look similar to the below example:

	* 87LBTcfgkepEddWNFrJcut76rFp9wQG6rgbqPhqHWGvy13A9hJK

.. _stophotwallet:

5. Stop the Hot wallet with the **rupaya-cli stop** command::

	rupaya-cli stop
	
.. _editconfig:
	
6. Edit the MasterNode Hot wallet configuration file (~/.rupayacore/rupaya.conf)::

	nano ~/.rupayacore/rupaya.conf

.. _copyconfig:
	
7. Copy the rupaya.conf template and update the variables manually.  All variables that need to be updated manually are identified with the **<>** symbols around them::
	
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
	
* You can right click in Putty to paste the template into the configuration file.
* Update the variable after **rpcpassword=** with a 40 character RPC rpcpassword.
* You will need to generate the rpcpassword yourself.
* Use the **ifconfig** command to find out your Linux VPS IP address.  It is normally the address listed after the **eth0** interface. 
* Save your Linux VPS IP address as we are going to use this IP again in the Cold wallet setup
* Update the variable after **externalip=** with your Linux VPS IP 
* Update the variable after **masternodeaddr=** with your Linux VPS IP 
* Update the variable after **masternodeprivkey=** with your MasterNode private key (GenKey) 

.. _pastetemplate:

8. Paste the updated template into the **rupaya.conf** configuration file on the Linux VPS.

* This is a real example of what the configuration file should look like when you are done updating the variables.
* The IP address (`199.247.10.25` in this example) will be different for you::
	
	rpcuser=rupxuser 
	rpcpassword=someSUPERsecurePASSWORD3746375620 
	rpcport=7050 
	rpcallowip=127.0.0.1 
	rpcconnect=127.0.0.1 
	rpcbind=127.0.0.1 
	maxconnections=512 
	listen=1 
	daemon=1 
	masternode=1 
	externalip=199.247.10.25:9050 
	masternodeaddr=199.247.10.25
	masternodeprivkey=87LBTcfgkepEddWNFrJcut76rFp9wQG6rgbqPhqHWGvy13A9hJK 
	
.. _saveconfig:

9. Save and exit the file by typing **CTRL+X** and hit **Y** + **ENTER** to save your changes.

.. _starthotwallet:

10. Restart the Hot wallet with the **rupayad -daemon** command::

	rupayad -daemon
	
Verify the Hot wallet is synchronizing with the blockchain
----------------------------------------------------------

.. _getinfo:

1. Run the **rupaya-cli getinfo** command to make sure that you see active connections::
	
	rupaya-cli getinfo
	
.. _blockcount:

2. Run the **rupaya-cli getblockcount** command every few mins until you see the blocks increasing::
	
	rupaya-cli getblockcount

* NOTE: If your block count is **NOT** increasing then you will need to stop the daemon with the **rupaya-cli stop** command and then reindex with the **rupayad -reindex** command. 
	
**If your block count is indeed increasing, then you can proceed to the next step to setup the Cold wallet.**