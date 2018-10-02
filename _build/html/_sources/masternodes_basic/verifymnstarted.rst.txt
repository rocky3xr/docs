.. _verifymnstarted:
.. _find.rupx.io: https://find.rupx.io/masternodes

=============================
Verify the MasterNode Started
=============================

1. Login to the Linux VPS console via Putty or Terminal.

2. Run the following command to verify that the output **"CActiveFundamentalnode::EnableHotColdFundamentalNode() - Enabled! You may shut down the cold daemon."** is showing up in your debug log.  This is a very useful command to run immediately after starting the MN::
	
	cat ~/.rupaya/debug.log | grep HotCold
	
* **NOTE: Output from this command will only show up if your MasterNode started properly**

3. Run the following command to verify the status of the MasterNode::

	rupaya-cli masternode status

* If you see status **Not capable masternode: Hot node, waiting for remote activation**, you need to wait a bit longer for the blockchain to reach consensus. It's common to take 30 to 90 minutes before activation can be done.

* If you see status **MasterNode successfully started** as well as the **HotCold** output from the first command then you've done it, congratulations!! Go hug someone now :)
	
* It will take a few hours until the first rewards start coming in.  The time before the first payout will increase as more MasterNodes come online. 


4. Check the MasterNode tracker website find.rupx.io_ to see that your MasterNode(s) are showing up on the site.  You will need to search by your MasterNode wallet address to locate it on the website.  The site is refreshed every 5 minutes so don't be surprised if it takes up to 5 minutes to show up on the website.

Congratulations! The setup process is complete and your MasterNode is fully operational!