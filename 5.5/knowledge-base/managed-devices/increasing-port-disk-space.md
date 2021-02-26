<!-- 5.5.3 -->
<!-- Description: This document contains instructions for increasing disk space usage for managed device ports. -->

# Overview

**New for 5.5.3:** If you are running into disk space issues while pulling operating systems on all 38 ports of your Uplogix 5000, you can now take advantage of some unallocated hard drive space and gain more storage for your managed devices. 

# Enable Large File System

To allocate more disk space to managed ports, add a system property name *_enable_large_file_system* and set its value to *true*.

## From the Local Manager

Use the **config system properties** command to add the property.

```
[admin@UplogixLM]# config system properties   
[config properties]# _enable_large_file_system true
[config properties]# exit

[admin@UplogixLM]# show system properties
_enable_large_file_system true
```

You will need to **restart** the LM before the property will take effect.

## From the Control Center

<div class='ucc' />Inventory > Local Manager Summary >Â Properties > Edit</div>

Navigate to the LM's summary page and click the *Edit* button the Properties box. 

Use the *Add Property* form to add the property.

**Name: ** _enable_large_file_system

**Value:** true

Once the property is added, allow a heartbeat to complete, and then issue a restart of the LM.

# Verifying

The default allocation for Uplogix 500/5000s is 20GB. You can verify this with the **show directory** command.

```
[admin@UplogixLM]# show directory
port1/1: 0 bytes in 0 files.
port1/2: 0 bytes in 0 files.
port1/3: 0 bytes in 0 files.
port1/4: 0 bytes in 0 files.
port1/5: 0 bytes in 0 files.
port1/6: 0 bytes in 0 files.
port2/1: 0 bytes in 0 files.
port2/2: 0 bytes in 0 files.
port2/3: 0 bytes in 0 files.
port2/4: 0 bytes in 0 files.
port2/5: 0 bytes in 0 files.
port2/6: 0 bytes in 0 files.
port2/7: 0 bytes in 0 files.
port2/8: 0 bytes in 0 files.
  20.0 GB free (100%)
```

After adding the property and restarting, run the command a second time to verify the additional space.

```
[super@UplogixLM]# show directory
port1/1: 0 bytes in 0 files.
port1/2: 0 bytes in 0 files.
port1/3: 0 bytes in 0 files.
port1/4: 0 bytes in 0 files.
port1/5: 0 bytes in 0 files.
port1/6: 0 bytes in 0 files.
port2/1: 0 bytes in 0 files.
port2/2: 0 bytes in 0 files.
port2/3: 0 bytes in 0 files.
port2/4: 0 bytes in 0 files.
port2/5: 0 bytes in 0 files.
port2/6: 0 bytes in 0 files.
port2/7: 0 bytes in 0 files.
port2/8: 0 bytes in 0 files.
  26.0 GB free (100%)
```

<div class='info' />The Local Manager should gain a minimum of 6 GB hard drive space. In some cases, it may automatically allocate more.</div>

# Disable Large File System

To disable the large file system feature, simply delete the property and restart the LM. If the amount of data currently written to disk exceeds the limit, no further files will be written until the cumulative disk space usage is reduced.