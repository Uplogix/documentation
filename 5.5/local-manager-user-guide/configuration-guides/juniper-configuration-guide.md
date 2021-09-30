<!-- 5.4 -->
The purpose of this document is to detail the installation and configuration of Uplogix Local Managers (LM) to manage and facilitate remote connectivity to a Juniper device.

#Features
Supports Juniper switches and routers running JunOS version 11 or higher with the Uplogix 500 or 5000 LM.

#Physical Connection

Connect a free serial port on the Uplogix to the Juniper's RS-232 console management port with a standard Cat-5 cable.


#Configuring the Port

To configure the Uplogix LM for connection to a Juniper device, navigate to the port that the Juniper is connected to, run the command **config init**, and follow the prompts as below (substituting your Juniper's IP address for 203.0.113.16):

> **Important**: The Uplogix advanced driver for JunOS will not work with the **root** console username. To properly configure a Juniper device you must provide a user account that automatically has a "cli" shell, as opposed to a "csh" shell that the root user has.

```
[Admin@UplogixLM (port1/4)]# config init
--- Enter New Values ---
description: EX220
make [native]: juniper
model: ex2200-24t-4g
os: JunOS
os version: 11.3R2.4
management IP: 203.0.113.16
console username: bob
console password: ********
confirm password: ********
enable username:
enable password:
Serial Bit Rate [9600]:
Serial Data Bit [8]:
Serial Parity [none]:
Serial Stop Bit [1]:
Serial Flow Control [none]:
Do you want to commit these changes? (y/n):

```

The default console settings for the Juniper Switch are 9600 bit rate, 8 serial data bit, no serial parity, serial stop bit 1, no flow control.


