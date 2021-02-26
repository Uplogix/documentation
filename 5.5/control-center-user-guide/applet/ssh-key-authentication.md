<!-- 5.4 -->

<div class='ucc' />SSH Applet -> Preferences -> Private Key</div>

# Overview 

The Control Center provides the capability to open SSH connections to Local Managers and managed devices via the SSH Applet using SSH keys in lieu of prompting for a username and password.

> Providing public keys to authenticate overrides TACACS/RADIUS authentication for that user.

# Arguments

* **Authorized Keys** - The SSH public key stored in the user profile in the Control Center. This key is synchronized to Local Managers with user information.
* **SSH Private Key File** - The path to the SSH private key file on the userâ€™s workstation. This path is stored in a cookie in the userâ€™s browser.

# Generate SSH Key Pair on Client Workstation (if one has not been previously created)

This example walks through the process of configuring SSH Applet SSH key authentication for user *ajones*. 

If the client workstation (i.e., the workstation that will launch the CLI applet to connect to the Local Manager or managed devices) is running Linux, Unix, or Mac OSX (or is running Windows with a Linux-like environment application like Cygwin), issue the following command in a terminal window to generate the key pair: **ssh-keygen â€“t rsa**.

```
/Users/admin > ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/ajones/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/ajones/.ssh/id_rsa.
Your public key has been saved in /Users/ajones/.ssh/id_rsa.pub.
The key fingerprint is:
53:6d:4d:bd:5e:45:15:e1:16:45:ad:67:b9:1b:ed:d9 ajones
```

If the Local Manager is running in FIPS mode, then an â€œrsaâ€ key must be generated with at least 2048 bits â€“ here is the command to generate this key pair:  **ssh-keygen â€“t rsa â€“b 2048**.

If the client workstation is running a Windows operating system, the free puTTYgen tool can be downloaded and used to generate SSH key pairs. An example of this puTTYgen tool is shown below:

![](http://uplogix.com/support/docs/img/cc-user-guide/image167.png)
 
After installing and running the puTTYgen tool, perform the following:

1.	In the Parameters section, choose *SSH-2 RSA*, leave the default number of bits set to *2048* and click the **Generate** button.
2.	Move the mouse in the small screen as instructed by the tool during key generation in order to add randomness to the key pair being generated.
3.	Enter a key comment to identify the key pair. This is useful when using several SSH key pairs.
4.	Do not enter a *Key passphrase* â€“ leave it blank.
5.	Click **Save private key** to save your private key.  Give the key a filename and confirm that it should have a blank passphrase.  Also, note the filename and path, as the location for this private key will be configured in a subsequent step.
6.	Copy the text from the box under "*Public key for pasting into OpenSSH authorized_keys file*" and paste to a text file for use in the "**Add Public SSH key to User in Control Center**" section.

# Add Public SSH key to User in Control Center

The contents of the SSH public key text file should be provided to a Control Center admin if the user does not have privileges to edit their user profile.  Next, the user or Control Center admin should log in to the web interface, navigate to the Administration-Users page and then click on the user to be provisioned with the SSH public key.  In the example below, the SSH public key for user ajones is pasted into the Authorized Keys text box. Be sure to click *Save* after pasting the SSH public key.

![](http://uplogix.com/support/docs/img/cc-user-guide/image168.png)
 
# Set SSH Private Key Location in Browser

Log into the Control Center, navigate to a Local Manager, and click on a SSH applet button.

Upon launching applet, you may be prompted to confirm that you trust the Control Center certificate and to allow the SSH applet access to your workstation â€“ you must trust the certificate and allow the applet access to your workstation in order to continue.

Once the applet finishes initializing, click the *Edit* menu selection at the top of the screen and then click *Preferences*. Select the *Private Key** tab as shown below.

![](http://uplogix.com/support/docs/img/ucc5.2/Applet_SSH_KEY-1.jpg)

Next, click *Browse* on the popup menu, browse to and select the private key file, then click *Open* to set the path as shown below. Finally, click *Save* to save the path to the private key in an Uplogix cookie in the browser. Close the applet window.

![](http://uplogix.com/support/docs/img/ucc5.2/Applet_SSH_KEY-2.jpg)

This completes configuration for user ajones â€“ ajonesâ€™ public key is stored in the Control Center and the path to the private key is stored as a cookie in ajones' browser.
â€ƒ
# Usage

Once the private key has been configured as specified above, the SSH Applet failover feature is configured and active. To use the SSH Applet to access the console port of a managed device, connect to the web interface of the Control Center and navigate to the Inventory page. Select an Uplogix device from the Inventory tree to bring up its Summary page. Launch the Control Center applet by clicking on the *SSH* button. The applet should establish and authenticate the SSH session without the user having to enter a password.