.. _setupoverview:

==============
Setup Overview
==============

This guide will walk you through the bare minimum steps required to setup a Rupaya MasterNode on a Linux server and to setup a Cold Wallet on a Windows or Mac computer.  This guide is intended for those that want to get the MasterNode up and running without configuring additional security measures or best practices.  For those that want to take the time to configure additional security measures and best practices, we recommend using the Advanced Setup Guide.
	
This guide assumes that you have a basic understanding of how to navigate the Linux OS for the setup of the MasterNode.  This guide also assumes that you have an understanding of either a Windows or Mac OS for the setup of the Cold Wallet. 

.. warning:: It's very common in this industry for scammers to offer "help" via remote screen sharing (TeamViewer, Skype, Zoom, WebEx, etc).  They will use nicknames like `MasterNode Helper`, `MasterNode Support`, `Cryptopia Support` and will be very nice and helpful to you. At least until they manage to run a command like `dumpprivkey`, `sendtoaddress` and your funds will be gone, adios, sayonara.  Please be aware and stay safe!	

**Hot Wallet**

	In this guide, we refer to the **Hot** wallet as the Rypaya wallet that is running on a Linux or Windows VPS.

	* The VPS runs the MasterNode server.  
	* The VPS requires a public IP address statically configured on it.  
	* The Hot wallet provides services to the blockchain network, for which it's rewarded with coins.
	* It's referred to as **Hot** because it's connected to and running on the public internet 24/7, directly accessible on the peer-to-peer port (TCP **9050**).  
	* Because this wallet is always running, it is much more vulnerable to attack than a **Cold** wallet.  This is why is is highly recommended to use a Cold wallet to receive the MasterNode rewards. 

**Cold Wallet**

	On the other side, the **Cold** wallet, running on Windows, OSX, or Linux, holds the RUPX collateral (**20000** RUPX). 
 
	* The Cold wallet is used to both enable the MasterNode server and to collect the rewards for its' services.
	* The Cold wallet is normally run at home, behind a firewall, on a Windows, OSX or Linux computer.  
	* After the MasterNode is enabled, the Cold wallet can even be run without direct connectivity from the internet, making it a more secure wallet. 
	* Once the MasterNode is enabled and verified as working, the Cold wallet can then be closed and the MasterNode rewards will still show up the next time the wallet is started and synced.

.. _dont_do_this_at_home:

Running a MasterNode on a home computer is a bad idea
-----------------------------------------------------

Some people, including me at some point, want to save a few bucks and run a MasterNode at home on a retired PC or Laptop collecting dust. Good idea?  **NO**

Here's why:

* The purpose of a MasterNode is to be a highly available system that is always reachable, has low network latency, and high bandwidth. These are rarely found in the average home.

* Static IP addresses are also harder to get for residential users or they cost extra money.

* You could loose important MasterNode rewards if your node loses connectivity due to an Internet outage.

* Running old PCs and Laptops at home also costs energy, creates noise and they can be a fire risk when running 24/7.

* Your IP address can be traced back to your home, therefore it is unsafe. This gives potential thieves and hackers a target.


**Recommendation:** Get a $5 a month Linux VPS from a provider such as Digital Ocean, Vultr, or AWS and save yourself from the possible loss of revinue when your home Internet or computer goes down.