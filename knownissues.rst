Known Issues
============
The following list contains known issues on our current platform. The issues will be addressed in future platform updates.

Instances
---------

Creating a volume from an image fails when the volume is sized smaller than disk size of the image
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Description
"""""""""""
When creating a volume from an image (or a snapshot of an instance) the Dashboard will suggest a size for the volume based on the listed size of the image.

However as the image size doesn't reflect the actual amount of space required to unpack the image into a volume, accepting this suggested volume size will result in the creation of the volume failing. 

Workaround
""""""""""
Manually adjust the volume size to a suitable value.

The minimum size for all images provided by Cloudlynx is 10GB.

For snapshots of instances, the minimum size is the ephemeral disk size of the instance from which the snapshot was created.

The resize function for instances doesn't work
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Description
"""""""""""

The resize function is intended to allow the flavour of a running instance to be changed with minimum disruption to the running of the instance. At present this function doesn't work in the Cloudlynx IaaS.

Workaround
""""""""""

Instead of resizing an existing instance, create a new instance of desired flavour and configure it to replace the existing instance. Once the new instance is running, terminate the original instance. 

Networking
----------

Multiple or repeated IP addresses may be shown in the Dashboard for running instances
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Description
"""""""""""

The Dashboard will sometimes show multiple IP addresses for a single instance where only one should be shown. Usually this occurs when large numbers of identical instances are requested by the same customer simultaneously.

Only one of the shown IP addresses will be active for the instance, often this is the last one listed.
When this happens some of the requested instances may also fail to start. 

Workaround
""""""""""

Disregard the additional, incorrect IP addresses.

Request identical instances in smaller batches (e.g. 10 or 20 at a time).

The "Disassociate Floating IP" option in the Dashboard also releases the IP
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Description
"""""""""""

When using the "Disassociate Floating IP" option on the "Instances" page the floating IP assigned to the instances is also released from the customer’s account and thus no longer assigned to the customer.

Workaround
""""""""""

When disassociating a floating IP from an instance in the Dashboard, use the "disassociate" button on the "Floating IP" tab of the “Access & Security” page instead of the "Disassociate Floating IP" option on the "Instances" page.

Removing an ICMP allow rule from a security group doesn't affect floating IPs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Description
"""""""""""

If an instance has a floating IP and it's security group allows ICMP traffic, removing the rule allowing ICMP traffic doesn't stop/block ICMP traffic on the floating IP as would be expected. The effect persists until the floating IP is disassociated from the instance.

Workaround
""""""""""

Ensure that ICMP rules are configured as required in an instance’s security groups prior to associating a floating IP with that instance.

If ICMP rules needed to be removed after a floating IP has been associated, disassociating the floating IP from the instance prior to removing the rules, then re-associating the floating IP to the instance 5-10 minutes after the rules have been removed works in some cases.

Images
------

Large image uploads fail when submitted via the Dashboard
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Description
"""""""""""

When attempting to upload larger (approximately > 2GB) images via the Dashboard using the "Image File" option the upload will fail and the image will be permanently listed with a status of "Queued".

Workaround
""""""""""

Larger images can be uploaded via the Glance API or command line client or using the "Image Location" option via the Dashboard.

Image uploads via the Glance API or command line client fail when the upload takes more than 6 hours or exceeds 1TiB
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Description
"""""""""""

When attempting to upload an image from a local file on the customer’s computer the upload will fail to produce a working image in the Cloudlynx IaaS if the upload takes longer than 6 hours or is greater than 1TiB in size.

Workaround
""""""""""

These are purposeful limitations of the Cloudlynx IaaS, and as such there is no workaround.