Transfer Files
==============
Transfer Files to and from a Linux Instance (including attached Volume)
-----------------------------------------------------------------------

Files can be transferred to and from a Linux instance using scp and sftp. Before you do so, make sure the public key is added to the instance and port 22 is open.


File Transfers Using scp (secure remote copy)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

How to transfer files to and from an instance depends on the local operating system. 


scp Between a Local Linux and a Linux Instance  
""""""""""""""""""""""""""""""""""""""""""""""


**To transfer files from a local computer to the instance in the cloud proceed as follows**:

1) Install OpenSSH (if not already installed).

2) Add your private key to the ssh agent. 

3) Execute the following scp command in your terminal: 

	scp <source file> <username of instance>@<instance IP>:<destination file>

For <source file> substitute the path pointing to the file to be copied, and for <destination file> substitute the desired target location. The instance IP is the floating IP which is reachable over the internet.


**To transfer a file from an instance in the cloud to your local file system proceed as follows**:

1) Execute the following scp command in your terminal:

	scp <username of instance>@<instance IP>:<source file> <destination file> 

The <destination file> in this case is the file on the local computer.

.. note::
   Scp can also be used to copy files from one instance to another within the cloud.


scp Between a Local Windows Computer and a Linux Instance
""""""""""""""""""""""""""""""""""""""""""""""""""""""""" 

We recommend WinSCP to copy files from a Windows computer to a Linux instance and vice versa. You can run pageant on your local Windows computer and add the private key for easier management when also using PuTTY for SSH connection.

1) Start WinSCP and click the **New Site** button.

2) Click on the **Advanced** button on the right. A new window pops-up.

3) Click **SSH** and then **Authentication** on the left.
 
4) Activate the checkbox **Allow agent forwarding** under **Authentication parameters**.
 
5) Provide the location of the private key in the **Private key file** field (should be in the .ppk format).

6) Click on the **OK** button to close the Advanced Site Settings windows.

7) Choose SCP as the protocol in the **File protocol** dropdown menu.

8) In the **Host name** field, enter the floating IP Address of the instance the connection should be established to.

9) Fill in the user of the instance in the **User name** field.

10) Click on the **Save** button to save the settings.

11) Press the **Login** button and the connection to the instance via scp will be established. A window will appear with a graphical user interface allowing the transfer of files between the local computer and the instance.


.. note::
   In case the connection fails, please make sure Pageant is running and contains the private .ppk key.


Manage Files in the Object Storage
==================================

This section is for Windows only! For Linux we recommend to use the CLI Clients (SWIFT).

It is possible to manage Object Storage using a SWIFT/S3 browser. We are using Cyberduck in our example. Others may work as well.


1) Login to the Cloudlynx Dashboard.

2) Under the Menu **Manage Compute**, click on **Access & Security**.

3) Open the **API Access** tab.

4) Click on the button **Download EC2 Credentials**.

5) Download the zip file and open it.

6) Start **Cyberduck**.

7) Click on **Open Connection**.

8) Choose **S3 (Amazon Simple Storage Service)** from the drop down menu.

9) Fil in the **Server** field: api.preview.cloudlynx.ch

10) Open the downloaded zip file from the Dashboard, open the **ec2rc** file in notepad or another text reader.

11) Find the **EC2_ACCESS_KEY** information and copy it to the field **Access Key ID** in Cyberduck.

12) Find the **EC2_SECRET_KEY** information and copy it to the **Secret Access Key** in Cyberduck.

13) Click on the **Connect** button.

14) A message may appear that the key needs to be added to your local key store.
