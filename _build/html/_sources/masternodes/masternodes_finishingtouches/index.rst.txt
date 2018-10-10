.. meta::
   :description: Introduction to the Rupaya cryptocurrency and links to further reading
   :keywords: rupaya, rupx, masternodes, hosted, hosting, linux, setup, payment

.. _masternodes_finishingtouches:


=================
Finishing Touches
=================

.. toctree::
   :maxdepth: 1

   logrotate.rst
   hotwalletautostart.rst
	
This section is intended for MasterNode users that want to configure the following:
	
	* Automatic log rotation to prevent the log files from filling up the Linux VPS hard drive.  If you do not occassionally clean up the log files then your Linux VPS hard drive will eventually fill up and the server will crash.  Completing the steps in this section will configure your Linux VPS to automatically clean up the logs every 30 days, rather than having to do it manually.  This is a necessary step for anyone running a MasterNode.  
	
	* Automatic restart of the MasterNode Hot wallet in the event that the Linux VPS is rebooted.  This is an extremely useful feature to ensure that your MasterNode Hot wallet will start up automatically when the Linux VPS is rebooted.







