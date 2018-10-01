.. _find.rupx.io: https://find.rupx.io/masternodes

=============================
Verify the MasterNode Started
=============================

1. Login to the Linux VPS console via Putty or Terminal.

2. Run the following command to verify the status of the MasterNode::

	rupaya-cli masternode status

If you see status `Not capable masternode: Hot node, waiting for remote activation`, you need to wait a bit longer for the blockchain to reach consensus. It's common to take 30 to 90 minutes before activation can be done.

If you see status `MasterNode successfully started`, you've done it, congratulations. Go hug someone now :)
	
It will take a few hours until the first rewards start coming in.

3. Run the following command to verify that the output "CActiveFundamentalnode::EnableHotColdFundamentalNode() - Enabled! You may shut down the cold daemon." is showing up in your debug log.  This is a very useful command to run immediately after starting the MN.  Output from this command will only show up if your MN started properly::
	
	cat ~/.rupaya/debug.log | grep HotCold

4. Check the MasterNode tracker website find.rupx.io_ to see that your MasterNode(s) are showing up on the site.  You will need to search by your MasterNode wallet address to locate it on the website.

Congratulations! The setup process is now complete and your MasterNode is now fully operational!