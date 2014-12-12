# Known Issues
The following list contains known issues on our current platform. The issues will be addressed in future platform updates.

### Creating volume from an image fails when the volume is sized smaller than disk size of the image. 
#### Description
When creating a volume from an image (or a snapshot of an instance) the Dashboard will suggest a size for the volume based on the listed size of the image.
However as the image size doesn't reflect the actual amount of space required to unpack the image into a volume, accepting this suggested volume size will result in the creation of the volume failing. 
#### Workaround
- Manually adjust the volume size to a suitable value.
The minimum size for images provided by Cloudlynx is:
- Debian-7-64bit-2014.7.13: 10GB
- CentOS-6.5-64Bit-2014.07.04: 10GB
- Fedora-20-64Bit-2014.07.04: 10GB
- Ubuntu-12.04-64Bit-2014.07.04: 10GB
For snapshots of instances, the minimum size is the ephemeral disk size of the instance from which the snapshot was created.

- - -

### The resize function for instances doesn't work.  
#### Description
The resize function is intended to allow the flavour of a running instance to be changed with minimum disruption to the running of the instance. At present this function doesn't work in the Cloudlynx IaaS.
#### Workaround
Instead of resizing an existing instance, create a new instance of desired flavour and configure it to replace the existing instance. Once the new instance is running, terminate the original instance. 