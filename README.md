# Virtual Server Deployment Guide

## Overview
This document will take you through the steps to get access to the LinuxONE community cloud, deploy a virtual server and start using it in your project.    

## Steps

1. Request access to LinuxONE Community Cloud
2. First time setup
3. Deploy your LinuxONE virtual server
4. Log in to your LinuxONE virtual server

## Step 1. Request access to LinuxONE Community Cloud.
1) In a browser, go to the [LinuxONE Community Cloud website](https://developer.ibm.com/linuxone).

   ![alt text](images-deploy/dw-home.png "DeveloperWorks LinuxONE Home")

2) Click **Try Virtual Machines on the LinuxONE™ Community Cloud**.

3) Complete the required fields on the registration form.

   ![alt text](images-deploy/registration-form.png "Registration form")


4) Complete your registration by clicking **Request your trial**.

   ![alt text](images-deploy/request-your-trial.png "Submit registration form")    

5) After you will get a message confirming that your registration was received. Once registration is approved you will receive your login credentials. This process will take up to (1) business day.

   ![alt text](images-deploy/registration-review.png "Registration under review")   

5) Check your email for a registration confirmation similar to the following shown. You will need your User ID and Password from this email to sign in to the self service portal.

   ![alt text](images-deploy/welcome-email.png "Welcome email")


## First time setup

1) After activating your account, log in.

* Enter your **user ID** and the **password** created during registration.
* Click **Sign in**.

   ![alt text](images-deploy/ssp-login.png "Self-Service Portal login page")

## Deploy your LinuxONE virtual server

1) Go to the **Home** page, **Service Catalog** section and **Virtual Servers** service.

* Click **Manage Instances**.

   ![alt text](images-deploy/manage-instances.png "Manage instances")

* Click **Create**.

   ![alt text](images-deploy/create-server.png "Create server")

2) Select a virtual server type.

* If this server is for generic purpose use, select **General purpose VM**.

   ![alt text](images-deploy/create-server-type-general.png "Create server type General purpose")
* If this server is for a Hackathon event, select **Hackathon**.  A valid event code is required. 

   ![alt text](images-deploy/create-server-type-hackathon.png "Create server type Hackathon")

3) Provide details information for this instance.  Enter:

* An **Instance Name**, without any spaces or special characters. 
* An **Instance Description**. 

   ![alt text](images-deploy/create-server-instance-details.png "Create server details")

4) Select the desired Linux image.

   ![alt text](images-deploy/create-server-image.png "Create server image")

5) Select the desired Linux flavor.

   ![alt text](images-deploy/flavor.png "flavor")
   
 6) Create a new SSH key pair:     
 * Click **Create**.
 
![alt text](images-deploy/click-create.png "Click Create")

* Enter a **Key Name** for this key.
* Click **Create a new key pair**.   

![alt text](images-deploy/create-key.png "Create SSH key")


* A pop-up window will appear asking you to save **yourkey. pem** file. This is your private key.  Please save it to a secure location.  Once this operation is complete, there is no way to retrieve this key. Click **OK** to save the file. 

![alt text](images-deploy/pem-file.png "Save SSH private key")   

7) Select the SSH key to use.

   ![alt text](images-deploy/create-server-select-key.png "Create server SSH key")

8) Verify that all the information is correct and click **Create**.

   ![alt text](images-deploy/create-server-submit.png "Create server submit")

9) Watch the status of your newly deployed instance go through the following phases of start up:  *NETWORKING*, *SPAWNING*,  *ACTIVE*.  When your instance status changes to *ACTIVE*, it is ready for use.

   ![alt text](images-deploy/create-server-status.png "Create server status")

   Write down the IP address of your instance. You will need it to log in.

## Log in to your LinuxONE virtual server

### From Mac OS X or Linux using Terminal

1) Open a Terminal application.
2) Ensure that you have the SSH private key used to deploy the server. 
3) If you have not done so already, change the permission bits of this key to 600.

   ```
   chmod 600 /path/to/key/keyname.pem  
   ```
4) Use SSH to access the Linux guest.

* UserID: linux1

* `-i` lets SSH know which identity file to use access the Linux guest.

* Serveripaddress: This was written down from the *Manage Instances* page of the LinuxONE Community Cloud.

   ```
   ssh –i /path/to/key/keyname.pem linux1@serveripaddress 
   ```
### From Windows using PuTTY

1) Set up PuTTY to use the SSH key for your server.  Refer to the [Setting up PUTTY on Windows to use ssh private key](http://developer.ibm.com/linuxone/wp-content/uploads/sites/57/2016/02/PUTTY-Set-up.pdf) tutorial.

2) Log in to the linux1 user ID. 

## Important notes about your server:
1) You can use ‘sudo’ to execute commands that require root authority.

2) It could take up to 10 minutes to format and mount the /data disk.  Issue the following command to verify the /data disk is available before continuing:
   ```sh
   df -h 
   ```
   ![alt text](images-deploy/df.png "Check /data disk")

3) Firewall is enabled. Only the SSH port is open.  Modify the firewall rules with iptables if you need other ports opened. For example:
   ```sh
   iptables -I INPUT -p tcp --dport <port#> -j ACCEPT 
   ```
   If you want to make your changes permanently, issue this command:
   ```sh
   iptables-save > /etc/sysconfig/iptables 
   ```

4) You must log in with the user ‘linux1’ with your SSH private key. No modification (use of password authentication, for example) is allowed.

5) The user ‘root’ login is disabled for security reasons. No modification is allowed.

6) There is no backup for your virtual server.  It is the end user’s responsibility to back up any critical data.

