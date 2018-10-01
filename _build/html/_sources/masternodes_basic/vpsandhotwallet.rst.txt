.. _Putty: https://putty.org/
.. |br| raw:: html

   <br />
   
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
	
**Download and Configure the Rupaya Hot wallet**
	
1. :ref:`Install the Rupaya Hot wallet on the VPS<downloadwallet>`
2. :ref:`Start the Hot wallet service<startservice>`
3. :ref:`Generate the masternode private key (aka GenKey)<generategenkey>`
4. :ref:`Copy and save the MasterNode private key<savegenkey>`
5. :ref:`Edit the Hot wallet configuration file (/root/.rupayacore/rupaya.conf)<editconfig>`
6. :ref:`Copy the rupaya.conf template and update the configuration data accordingly<copyconfig>`
7. :ref:`Paste the updated template into the rupaya.conf configuration file<pastetemplate>`
8. :ref:`Save and exit the file by typing CTRL+X and hit Y + ENTER to save your changes<saveconfig>`
9. :ref:`Stop and restart the Hot wallet <stopandstart>`
	
**Verify the Hot wallet is synchronizing with the blockchain**
	
1. :ref:`Run the **rupaya-cli getinfo** command to make sure that you see active connections<getinfo>`
2. :ref:`Run the **rupaya-cli getblockcount** command every few mins until you see the blocks increasing<blockcount>`

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
	
3. Login to the VPS via SSH.

	For Windows users, Putty_ is a very good SSH client that you can use to connect to a remote Linux server.
	If you are running a VPS from Vultr or similar, you need to use an SSH client, such as Putty_, if you want to copy and paste these commands otherwise you will have to type them all out manually!

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

Download and Configure the Rupaya Hot wallet
--------------------------------------------

.. _downloadwallet:

1. Install the Rupaya Hot wallet on the VPS.  Download and unpack the Rupaya wallet binaries by running the following commands::

	wget https://s3-us-west-2.amazonaws.com/rupayax/75.1/linux-x64.tar.gz	
	sudo tar xvzf linux-x64.tar.gz -C /usr/local/bin/
	
.. _startservice:
	
2. Start the Hot wallet service.  When the service starts, it will create the initial data directory(`/root/.rupayacore/`)::

	rupayad -daemon
	
.. _generategenkey:

3. Generate the MasterNode private key (aka GenKey).  Wait a few seconds after starting the wallet service and then run this command to generate the masternode private key::

	rupaya-cli masternode genkey

.. _savegenkey:

4. Copy and save the MasterNode private key from the previous command to be used later in the process.  The value returned should look similar to the below example::

	87LBTcfgkepEddWNFrJcut76rFp9wQG6rgbqPhqHWGvy13A9hJK

.. _editconfig:
	
5. Edit the MasterNode Hot wallet configuration file (/root/.rupayacore/rupaya.conf)::

	nano /root/.rupayacore/rupaya.conf

.. _copyconfig:
	
6. Copy the rupaya.conf template and update the configuration data accordingly.  All variables that need to be updated manually are identified with the <> symbols around them::
	
	**rpcuser=rupayarpc** 
	**rpcpassword=<alphanumeric_rpc_password>** 
	**rpcport=7020** 
	**rpcallowip=127.0.0.1** 
	**rpcconnect=127.0.0.1** 
	**rpcbind=127.0.0.1** 
	**maxconnections=512** 
	**listen=1** 
	**daemon=1** 
	**externalip=<public_mn_ip_address_here>:9050** 
	**masternodeaddr=<public_mn_ip_address_here>:9050** 
	**bind=<public_mn_ip_address_here>** 
	**masternode=1** 
	**masternodeprivkey=<public_mn_ip_address_here>** 
	**addnode=rupx.seeds.mn.zone** 
	**addnode=rupx.mnseeds.com** 
	**addnode=104.248.58.227:9050** 
	**addnode=142.93.247.186:9050** 
	**addnode=104.238.146.167:9050** 
	**addnode=206.189.6.102:9050** 
	**addnode=178.128.225.48:9050** 
	**addnode=128.199.204.114:9050** 
	**addnode=139.59.80.208:9050** 
	**addnode=34.221.226.22:9050** 
	**addnode=159.89.236.115:9050** 
	**addnode=54.71.156.120:9050** 
	**addnode=45.55.32.108:9050** 
	**addnode=178.238.230.212:9050** 
	**addnode=159.65.251.235:9050** 
	**addnode=144.202.33.21:9050** 
	**addnode=207.246.116.61:9050** 
	**addnode=140.82.24.203:9050** 

	#update the variable after rpcpassword= with a 40 character RPC rpcpassword.  
	#You will need to generate the rpcpassword yourself. 
	#update the variable after externalip= with your Linux VPS IP 
	#update the variable after masternodeaddr= with your Linux VPS IP 
	#update the variable after masternodeprivkey= with your MasterNode private key (GenKey) 
	#You can right click in Putty to paste all of the above into the configuration file.

.. _pastetemplate:

7. Paste the updated template into the rupaya.conf configuration file.

.. _saveconfig:

8. Save and exit the file by typing CTRL+X and hit Y + ENTER to save your changes.

	This is a real example of what the configuration file should look like when you are done updating the variables::
	
	**rpcuser=rupxuser** 
	**rpcpassword=someSUPERsecurePASSWORD3746375620** 
	**rpcport=7020** 
	**rpcallowip=127.0.0.1** 
	**rpcconnect=127.0.0.1** 
	**rpcbind=127.0.0.1** 
	**maxconnections=512** 
	**listen=1** 
	**daemon=1** 
	**masternode=1** 
	**externalip=199.247.10.25:9050** 
	**masternodeaddr=199.247.10.25:9050** 
	**masternodeprivkey=87LBTcfgkepEddWNFrJcut76rFp9wQG6rgbqPhqHWGvy13A9hJK** 
	**addnode=rupx.seeds.mn.zone** 
	**addnode=rupx.mnseeds.com** 
	**addnode=104.248.58.227:9050** 
	**addnode=142.93.247.186:9050** 
	**addnode=104.238.146.167:9050** 
	**addnode=206.189.6.102:9050** 
	**addnode=178.128.225.48:9050** 
	**addnode=128.199.204.114:9050** 
	**addnode=139.59.80.208:9050** 
	**addnode=34.221.226.22:9050** 
	**addnode=159.89.236.115:9050** 
	**addnode=54.71.156.120:9050** 
	**addnode=45.55.32.108:9050** 
	**addnode=178.238.230.212:9050** 
	**addnode=159.65.251.235:9050** 
	**addnode=144.202.33.21:9050** 
	**addnode=207.246.116.61:9050** 
	**addnode=140.82.24.203:9050**

	The IP address (`199.247.10.25` in this example) will be different for you. Use the `ifconfig` command to find out your IP address.  It is normally the address of the `eth0` interface. Save this IP address as we are going to use this IP and port (9050) again in the Cold wallet setup. 

.. _stopandstart:

9. Stop and restart the Hot wallet.  The following commands will stop the service, wait 2 minutes, and then restart the service::

	**rupaya-cli stop && sleep 120** 
	**rupayad -daemon**
	
Verify the Hot wallet is synchronizing with the blockchain
----------------------------------------------------------

.. _getinfo:

1. Run th `rupaya-cli getinfo` command to make sure that you see active connections::
	
	rupaya-cli getinfo
	
.. _blockcount:

2. Run the `rupaya-cli getblockcount` command every few mins until you see the blocks increasing::
	
	rupaya-cli getblockcount

	
You can now proceed to the next step to setup the Cold wallet while this wallet syncs up with the network and the other MasterNodes.

