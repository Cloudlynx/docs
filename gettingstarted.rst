Getting Started
===============

Introduction
------------

Welcome to the Cloudlynx cloud! This document is designed to help cloud administrators and system operators get started with the cloud environment. It can also act as a reference for daily operations.

The document covers the following topics:

* Compute instance (how to set up, launch and manage instances)
* Storage options (Block and object storage)
* Introduction to APIs and CLI
* Introduction to orchestration (automate the cloud infrastructure)

Before using the Cloudlynx cloud environment, we recommend reading this document to familiarise yourself with the system.

Additional training courses and course material are available on the Cloudlynx website: https://www.cloudlynx.ch

**Note:** This document assumes you have an active Cloudlynx account.

Cloudlynx Dashboard
-------------------

The Cloudlynx dashboard serves as the starting point when accessing the Cloudlynx graphical user interface (GUI). It provides an overview of the current cloud resources being used, as well as listing the cloud services offered by Cloudlynx.

Log in to the Cloudlynx Dashboard
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To log in to the Cloudlynx dashboard, use the link provided in the welcome email or use the login link on the Cloudlynx webpage. The login credentials are provided during the registration process.

.. image:: _static/gettingstarted/fig1.png
   :alt: Log In window

**Note:** The registration process is not covered in this document. For more information, please visit https://www.cloudlynx.ch/en/registration.

**Note:** In the case of a forgotten password, please go to the account management site https://preview.cloudlynx.ch/account.

Overview of the Cloudlynx Dashboard
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

After successfully logging in to the Cloudlynx dashboard, you will be directed to the **Overview** page.
The **Overview** page provides an overview of the cloud resources: applied limits, currently used cloud resources, as well as providing the possibility to query cloud usage from the past.

The Cloudlynx dashboard is split into 3 sections:

* The side bar (left part of the screen)
* The content pane (middle part of the screen)
* The title bar (top part of the screen)

.. image:: _static/gettingstarted/fig2.png
   :alt: Dashboard Overview

**Note:** Directions given in this document will use the definitions above.

The Side Bar
""""""""""""
The left section of the Cloudlynx dashboard is called the side bar. Here, you will find a list of the cloud services that Cloudlynx provides as well as your current project.

The side bar has the following menu structure:

**Manage Compute**

* Overview:	provides an overview of the current resource usage
* Instances: create, launch and manage instances
* Volumes: create, attach and manage persistent block storage
* Images & Snapshots: create, upload and manage images and snapshots
* Access & Security: configure security of and access to instances 

**Manage Network**

* Network Topology: provides a graphical overview of the network setup
* Networks: create and configure virtual networks, subnets, gateways, IP allocations
* Routers: create, configure and connect routers to virtual networks

**Object Store**

* Containers: create, upload and manage persistent object storage
	
**Orchestration**

* Stacks: execute automatic deployment of a whole cloud setup (including compute, block storage, object storage, network etc.)


**Note:** The Red Hat tab forwards you to the Red Hat Customer Portal. This feature should not be used, as it will be removed in future updates. A Red Hat account or subscription is required for accessing this section.

The Content Pane
""""""""""""""""

This section displays the main content. The shown content will vary depending on the topic selected from the side bar.
On the **Overview** page you are able to query current and past cloud usage, as well as export the results. This can be done by selecting a **From:** and **To:** date and pressing **Submit**. The results are then displayed.

**Note:** The Date format needs to be YYYY-MM-DD.

.. image:: _static/gettingstarted/fig3.png
   :alt: Select a period of time to query its usage

A usage summary report can be exported into CSV format. Click on the **Download CSV Summary** button to generate the file.

.. image:: _static/gettingstarted/fig4.png
   :alt: Download CSV Summary
   
The Title Bar
"""""""""""""

The title bar can be found at the top of the page and is always displayed independent of any selected topic.

* Logged in as: indicates which user account is currently logged in 
* Settings: change language, time zone, items per page shown and password
* Help: opens the official documentation of OpenStack
* Sign Out: log out of the current session

Change Password
"""""""""""""""
A password change should not be done via the **Settings** link in the title bar. Instead please go to the account management site https://preview.cloudlynx.ch/account. Log in with your credentials, click on the user icon in the upper right hand corner and select **Change Password**. 

.. image:: _static/gettingstarted/fig5.png
   :alt: Change Password

Key Management
--------------

SSH keypairs are used to access instances securely without specifying a password each time. A keypair can be used for multiple instances that belong to the same project.

**Note:** To access a Linux-based instance for the first time, it must be accessed using an SSH keypair. This applies to the Linux images provided by Cloudlynx only.

Create a New Keypair
^^^^^^^^^^^^^^^^^^^^

There are three possibilities how to create keypairs. It can be done either directly on the Cloudlynx dashboard by using a third party tool such as the open source tool PuTTYgen on a Windows client, or by using the CLI SSH commands of a Linux client.

On the Dashboard
""""""""""""""""

1. Select the **Access & Security** tab under the Manage Compute section in the sidebar.
2. Click on the **Keypairs** tab. All available keypairs for that project are listed. The list is empty by default until somebody creates or imports a keypair.
3. Click on the **Create Keypair** button.
4. Specify a name for the key. For example “Mills_Evan_Keypair”
5. Click on the **Create Keypair** button in the dialogue window.
6. The private key is available for download (the web browser may prompt you with download options). Cloudlynx will only store the public key in the project.
7. The keypair now appears on the list of available keypairs under **Access & Security > Keypairs**.

**Note:** The private key has been generated in the browser and there is no copy of the private key in the cloud nor is there a recovery option. The only existing copy is the one you have saved (the .pem file). Treat it like any other private key you may have and make sure not to lose it. 

.. image:: _static/gettingstarted/fig6.png
   :alt: Create Keypair

With a Key Generator on a Local Windows Client
""""""""""""""""""""""""""""""""""""""""""""""

1. Get a key generator. We use the free open source tool **PuTTYgen** as an example (www.putty.org).
2. Start **PuTTYgen** and click on the **Generate** button and follow the instructions.
3. Optionally, you can change the comment under **Key comment** for easier identification of the key. For extra protection you may also add a phrase under **Key passphrase**.
4. For more security, change the field **Number of bits in a generated key** from 2048 to 4096.
5. Click on the **Save private key** button and it will be saved as a .ppk file.
6. Click on the **Save public key** button to save it in a file for further usage.
7. To import the keypair to the dashboard, copy the text from the field **Public key for pasting into OpenSSH authorized keys file** to your clipboard.
8. Continue with section Import an Existing Keypair.

.. image:: _static/gettingstarted/fig7.png
   :alt: PuTTY Key Generator

On a Local Linux Client
"""""""""""""""""""""""

To create a keypair on a Linux client, follow the steps below:

1. Open a **Terminal**.
2. Enter the **ssh-keygen** command to start the SSH key creation. Replace the variables in the examples below with your variables::

    $ ssh-keygen -b 4096 -t rsa -C Keypair_for_Cloud_Company_Instances 
    Generating public/private rsa keypair.

**Note:** Recommended options to be used when creating the SSH key are (they are case sensitive):

* -b (set the bitrate of the key) 4096 for RSA and 1024 for DSA
* -t (set the type of the key) RSA or DSA
* -C (add a comment to the key) information to identify the key

3. Enter the **keyname**.::

    Enter file in which to save the key (/filepath/.ssh/id_rsa): keyname

4. Enter the **passphrase** for the key (this is optional but is more secure).::
	
    Enter a passphrase (empty for no passphrase): passphrase
    Enter the same passphrase again: passphrase

5. The SSH key is being generated and will placed both private and public key into your .ssh file.::

    Your identification has been saved in Cloud_Instance.
    Your public key has been saved in Cloud_Instance.pub.
    The key fingerprint is:
    40:fc:bd:cd:4f:c0:bf:e5:e6:89:47:c8:9a:54:2c:9e Keypair_for_Cloud_Company_Instances
    The key's randomart image is:
    +--[ RSA 4096]----+
    |     ..          |
    |     ..          |
    |      .. . ..    |
    |       .. ..oo   |
    |        S .+=o.  |
    |          .Eooo..|
    |          . oo.+ |
    |            o +.+|
    |             ..+.|
    +-----------------+
    $

6. Add the SSH key to the ssh-agent using the ssh-add command.::

    $ ssh-add /filepath/privatekeyname

Import an Existing Keypair
^^^^^^^^^^^^^^^^^^^^^^^^^^

A keypair can be generated with an external tool that creates OpenSSH formatted keys (see section 3.1 Create a New Keypair). Any type of an OpenSSH key is accepted.

1. Select the **Access & Security** tab on the side bar under the **Manage Compute** section.
2. Click on the **Keypairs** tab. 
3. Click on the **Import Keypair** button.
4. In the **Keypair Name** field, specify a name for identification purposes. 
5. Copy and paste the content of the public key into the **Public Key** field.
6. Click on the **Import Keypair** button to finish.

**Note:** The private key is never seen by the cloud system and is only ever held by the customer. This option is the most secure one.

**Note:** An error message may occur if the format of the key is not OpenSSH.

Translate non-OpenSSH key to OpenSSH
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Download and open **PuTTYgen**. 
2. Click on the **Load** button.
3. Choose the private key file. In Windows environment, change the filter to **All Files (*.*)** if the file is not displayed.
4. Once the key is open, the text in the field **Public key for pasting into OpenSSH authorized keys file** can now be copied and used for the import dialogue on the dashboard.

Delete a Keypair
^^^^^^^^^^^^^^^^

**Warning:** Instances may not be accessible anymore if the public key is deleted.

1. Select the **Access & Security** tab on the side bar under the **Manage Compute** section.
2. Click on the **Keypairs** tab. All available keypairs for that project are listed.
3. Click on the checkbox on the left of the keypair to be deleted.
4. Click on the **Delete Keypair** button.

**Note:** This action cannot be undone.

**Note:** This will delete the public key on the system. The private key is not affected.

Create and Manage a Network
---------------------------

Cloudlynx provides a scalable, pluggable and API-driven system for managing network connectivity and IP addresses. It allows users to create their own networks and control the traffic. 

Create a Network
^^^^^^^^^^^^^^^^

1. Select the **Networks** sub-menu item under the **Manage Network** section on the side bar.
2. Click on the **Create Network** button.

.. image:: _static/gettingstarted/fig8.png
   :alt: Networks
   
3. The dialogue window which appears consists of the tabs **Network**, **Subnet** and **Subnet Detail**. 

.. image:: _static/gettingstarted/fig9.png
   :alt: Create Network – Network tab

4. Specify a name to identify the network in the **Network Name** field.
5. **Admin State** field – checked by default. If check box is empty, it means the network is down and will not forward packets.
6. Click on the **Subnet** tab.
7. Uncheck the **Create Subnet** checkbox if a subnet is not specified when the network is created.
8. Click on the **Create** button in the dialogue window.
9. The network is created.
10. The network now appears in the list of networks under **Manage Network > Networks**

**Note:** A subnet must be specified to be able to launch an instance (see chapter 5 Create and Manage a Subnet)

Edit a Network
^^^^^^^^^^^^^^

1. Select the **Networks** tab on the side bar under the **Manage Network** section.
2. Click on the **Edit Network** button on the network that needs to be edited.
3. Editable fields are **Network Name** and **Admin State**.
4. Click on the **Save Changes** button to save changes.

.. image:: _static/gettingstarted/fig10.png
   :alt: Edit Network

Delete a Network
^^^^^^^^^^^^^^^^

1. Select the **Networks** tab on the side bar under the **Manage Network** section.
2. Mark the checkboxes of the networks to delete.
3. Click on the **Delete Networks** button.

.. image:: _static/gettingstarted/fig11.png
   :alt: Delete Networks

**Warning:** Make sure that there are no instances attached to the network you want to delete.

Create and Manage a Subnet
--------------------------

Create a Subnet
^^^^^^^^^^^^^^^

1. Select the **Networks** sub-menu item under the **Manage Network** section.
2. Click on the **Network name** from the list of all **Networks** for which subnet needs to be defined.
3. Click on the **Create Subnet** button. 
4. Specify a name for the subnet.
5. Specify the IP address for the subnet (e.g. 192.168.0.0/24).
6. Select **IP version**: IPv4 or IPv6 (IPv6 currently not applicable).
7. Specify a **Gateway IP** address. This parameter is optional. If this field is left blank, the system will automatically take the first address of the defined subnet IP range (e.g. 192.168.0.1).
8. **Disable Gateway** checkbox – select this check box in order to disable the gateway. 

.. image:: _static/gettingstarted/fig12.png
   :alt: Create Subnet

**Note:** A subnet represents an IP address block that can be used to assign IP addresses to virtual instances. Each subnet must have a Classless Inter-Domain Routing (CIDR) address and must be associated to a network. IP addresses can be either selected from the whole subnet CIDR or from allocation pools that can be specified by the user.

**Note:** A subnet can also optionally have a gateway, a list of DNS name servers, and host routes. This information is pushed to instances whose interfaces are associated with the subnet. 

9. Go to the **Subnet Detail** tab in order to define additional attributes for the subnet (all optional).
10. Mark the **Enable DHCP** checkbox to enable DHCP.
11. Specify IP address allocation pools.
12. Specify a name for the DNS Server. 
13. Specify the IP address of the host routes.
14. Click on the **Create** button to finish the creation of the additional attributes for the subnet.

.. image:: _static/gettingstarted/fig13.png
   :alt: Create Subnet Detail
   
Edit a Subnet
^^^^^^^^^^^^^

1. Select **Network Topology** on the side bar under the **Manage Network** section. 
2. Click on the name of the network to get the **Network Detail** page.
3. Details about the network, subnets and ports of the selected network are displayed.
4. Click on the **Edit Subnet** button.
5. The **Update Subnet** dialogue box opens. 
6. Under the **Subnet** tab the editable fields are: **Subnet Name** and **Gateway IP** (optional).

.. image:: _static/gettingstarted/fig14.png
   :alt: Update Subnet
   

7. Under the **Subnet Detail** tab the editable fields are:

  * **Enable DHCP** – Select this checkbox to enable DHCP.
  * **DNS Name Servers** – Update the name of the DNS server.
  * **Host Routes** – Update the IP address of the host routes.

8. Click on the **Update** button to save any changes.

.. image:: _static/gettingstarted/fig15.png
   :alt: Update Subnet, Subnet Detail

Delete a Subnet
^^^^^^^^^^^^^^^

1. Select **Network Topology** on the left side bar under the **Manage Network** section. 
2. Click on the name of the network to get the **Network Detail** page.
3. Details about the network, subnets and ports of the selected network are displayed.
4. Under the section **Subnets**, mark the subnets that need to be deleted.
5. Click on the **Delete Subnets** button.
6. Confirm the deletion of subnets by clicking on the **Delete Subnets** button.

**Note:** This action cannot be undone.

.. image:: _static/gettingstarted/fig16.png
   :alt: Delete a Subnet
   
Create and Manage a Router
--------------------------

A router is needed to establish a connection between subnets or to connect a subnet to the public network so that the instances can be reached over the internet.

Create a Router
^^^^^^^^^^^^^^^

1. Select the **Routers** tab on the side bar under the **Manage Network** section.
2. Click on the **Create Router** button. 
3. In the **Create Router** dialogue box, specify a name for the router.
4. Click on the **Create Router** button. The new router is now displayed in the **Routers** tab.

.. image:: _static/gettingstarted/fig17.png
   :alt: Create Router

Set a Gateway
^^^^^^^^^^^^^

1. Select the **Routers** tab on the side bar under the **Manage Network** section.
2. Click on the **Set Gateway** button for the router you want to set a gateway for.
3. In the **External Network** field, specify the network to which the router will connect (this is normally the public network, which is a connection to the Internet).
4. Click on the **Set Gateway** button.

.. image:: _static/gettingstarted/fig18.png
   :alt: Set Gateway

Connect a Private Network to a Router
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Select the **Routers** tab on the side bar under the **Manage Network** section. 
2. Click on the name of the router.
3. On the **Router Details** page, click on the **Add Interface** button.
4. In the **Add Interface** dialogue box, select a subnet from the **Subnet** dropdown list.
7. Enter the router interface **IP address** for the selected subnet. 
8. Click on the **Add Interface** button to finish.

**Note:** If the IP address value is not set, either the default gateway IP address or the first host IP address in the subnet is used by default. 

.. image:: _static/gettingstarted/fig19.png
   :alt: Add Interface
   
Delete a Router
^^^^^^^^^^^^^^^

1. Select the **Routers** tab on the side bar under the **Manage Network** section.
2. Mark the checkboxes of the routers that need to be deleted.
3. Click on the **Delete Routers** button.
4. Confirm the action by clicking on the **Delete Routers** button. 

**Note:** This action cannot be undone. 

.. image:: _static/gettingstarted/fig20.png
   :alt: Delete Routers

