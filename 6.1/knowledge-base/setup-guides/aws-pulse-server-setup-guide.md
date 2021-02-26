# Overview
The Uplogix Local Manager's Pulse feature allows you to specify a network endpoint to act as an indicator of good network connectivity. While most customers use the Uplogix Control Center as an endpoint, any system capable of running the [echo service](https://en.wikipedia.org/wiki/Echo_Protocol) can be used as a target. This document describes the process for setting up a Pulse server (echo service) using Amazon Web Services (AWS).

# Requirements
* AWS Account - log into or create an account at [aws.amazon.com](https://aws.amazon.com)
* Network path from Local Manager to Pulse Server (routing, firewalls, etc.)

# Creating the EC2 Instance

Navigate to the AWS Management Console.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image001.png)

Click on **Launch a virtual machine**.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image003.png)

Select **Amazon Linux 2 AMI (HVM), SSD Volume Type**.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image005.png)

Select *Free tier eligible* or larger size depending on the number of Local Managers in your deployment.

Click **Next: Configure Instance Details**.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image007.png)

Select *Enable* under **Auto-assign Public IP**.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image009.png)

![](https://uplogix.com/support/docs/img/aws-pulse-server/image011.png)

> **Note:** If you shut down and restart your EC2 instance, there is a possibility that the public IP address may change. To maintain your IP address, use an elastic IP address (see [Assigning an Elastic IP Address](https://uplogix.com/docs/knowledge-base/setup-guides#assigning-an-elastic-ip-to-ec2-instance)), which can be allocated after the instance is created. At the time of this writing, one free elastic IP is allowed per instance.

Click on **Configure Security Group**.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image013.png)

By default, SSH is added as part of the allowed access. Select *My IP* under **Source** to restrict SSH access to your WAN IP. Other addresses can be added as necessary.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image015.png)

Click **Add Rule**. 

![](https://uplogix.com/support/docs/img/aws-pulse-server/image017.png)

Choose *Custom TCP Port* as **Type**, *7* as **Port Range**, your WAN IP address as **Source**, and *Echo Service* as **Description**.

Add as many addresses as necessary to cover the source IP addresses from all of your Local Managers. You can also specify *Anywhere* as the **Source** to allow all incoming connections to port 7.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image019.png)

Click **Review and Launch**.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image021.png)

Review your selections and click **Launch**.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image023.png)

You will be presented with the following screen.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image025.png)

Select *Create a new key pair*. This will allow secure communication between your SSH client and the AWS server.

Name your key pair and then download it to your computer.

<div class='warning' />You will not be able to download the key pair again.</div>

* How to install .pem file to putty: [click here](https://aws.amazon.com/premiumsupport/knowledge-center/convert-pem-file-into-ppk/)
* How to install .pem file to SecureCRT: [click here](https://s2-forums.vandyke.com/showthread.php?t=12755)

Click **Launch Instances** to launch the EC2 server.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image027.png)

You will be presented with the following screen. Click **View Instances** to access the newly created EC2 server. It may take a few minutes for the instance to become available.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image029.png)

The next screen will list your EC2 instance as well as its Public IPv4 address.

![](https://uplogix.com/support/docs/img/aws-pulse-server/aws_instances.jpg)

# Configuring Echo Service

Using your SSH client, connect to the server using its public IP address and the username **ec2-user**. There is no password as authentication is handled by the SSH certificates configured earlier.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image031.png)

Become root by running the **sudo su -** command.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image033.png)

Install xinetd by running the **yum install xinetd** command. Enter **y** when asked *Is this ok**.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image035.png)

![](https://uplogix.com/support/docs/img/aws-pulse-server/image037.png)

Wait for installation of xinetd to complete.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image039.png)

Use vi to edit **/etc/xinetd.d/echo-stream** to configure and enable the echo service.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image041.png)

Change the **disable** option to *no* and save the file.

1. Press *i* to enter insert mode
2. Use arrow keys to move cursor to **disable** line
3. Use backspace to delete *yes*
4. Type *no*
5. Press ESC
6. Type *:wq* and press Enter

![](https://uplogix.com/support/docs/img/aws-pulse-server/image043.png)

Start xinetd by running the **systemctl start xinetd.service** command. If the service is already running, use the **systemctl restart xinetd.service** command instead.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image045.png)

To view the status of the echo server, run the **systemctl status xinetd** command. If Local Managers are already trying to reach the Pulse server, you should see echo-stream START and EXIT messages every 30 seconds.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image047.png)

# Assigning an Elastic IP to EC2 Instance
From the AWS Management Console, click on **EC2** to access the EC2 Dashboard.

![](https://uplogix.com/support/docs/img/aws-pulse-server/aws_ec2.jpg)

In the EC2 Dashboard, click on **Elastic IP**, which is located in the left panel under the **Network & Security** section.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image049.png)

Click the **Allocate Elastic IP address** button. 

![](https://uplogix.com/support/docs/img/aws-pulse-server/image050.png)

To use an address from Amazon's pool of IPv4 addresses, accept the default configuration and click **Allocate**.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image052.png)

You new elastic IP address will be displayed on the next screen.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image054.png)

Select **Associate Elastic IP Address** from the **Actions** menu in the upper right hand corner.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image056.png)

Use the **Instance** and **Private IP address** boxes to select your EC2 instance. Click **Associate** to save your configuration.

![](https://uplogix.com/support/docs/img/aws-pulse-server/image058.png)

<div class='warning' />AWS does not charge for an Elastic IP address if it is associated with a running EC2 instance. If the EC2 instance is stopped, AWS will begin charging for the Elastic IP address.</div>

# Control Center / Local Manager Configuration

You can now proceed with configuring Local Managers to use the EC2 instance's public IP address as a Pulse server. Pulse settings can also be configured from an Inventory group on the Control Center.



