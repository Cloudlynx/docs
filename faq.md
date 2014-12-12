# Customer FAQ


## Instances

### Slow Instance Traffic
Q: My Instance's traffic is much slower than it should be. What causes this? 

A: Your MTU might be configured to be over 1454. Please check your configurations and make sure MTU is set to 1454 or less. 

### Stuck Instance Snapshots
Q: I took a snapshot of an instance, but now my instance is stuck in “Image Pending Upload” and the Snapshot is stuck on “Queued”. Even deleting the snapshot image is not fixing the instance status. What can I do? 

A: One option is to delete the instance and start again. If this is not feasible for various reason, you can contact support to ask help. Cloudlynx admins are able to perform admin level commands to reset the status of the instance, which will allow you to regain control of the instance. 

### RHEL Instance Snapshots
Q: How do I make a proper snapshot from a running RHEL instance? 

A: We recommend to use RHEL images only with profiles(flavours) which have at least 1GB RAM.

When you make a snapshot you have no guarantee that this will be consistent. You must make sure that the filesystem is in a clean state, and that there is nothing going on. The best way to do this is to 
“freeze” it. Now freezing the filesystem will freeze the prompt too. However you can do the following steps.

1. Log in, and become root (sudo su - )
2. Run the following command :

	fsfreeze -f / && sleep 60 && fsfreeze -u /

This freezes the filesystem, waits 60 seconds, then unfreezes it. During these 60 seconds you just make the snapshot. If you don't do this the snapshot might be inconsistent.

### Change a Keypair
Q: What can I do if I want to change the keypair of an Instance? 

A: Take a snapshot of that instance (preferably when it is shut off) –> Launch a new instance based on the snapshot and use a different keypair.

Please note it may take several minutes until the instance is reachable over the Internet when launched from a snapshot. Start a ping in CMD to see when it is reachable.

	ping "Floating IP Address" -t

Attention: This will additionally add the new keypair but will not remove the old one. So it is possible to access the instance with both private keys (old and new). 

	
