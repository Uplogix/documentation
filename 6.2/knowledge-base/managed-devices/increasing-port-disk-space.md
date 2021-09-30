# Overview

**New for 5.5.3:** If you are running into disk space issues while pulling operating systems on high density Local Managers, you can now take advantage of some unallocated hard drive space and gain more storage for your managed devices. 

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
port1/1: 5.6 MB in 15 files.
port1/2: 0 bytes in 0 files.
port1/3: 0 bytes in 0 files.
port1/4: 0 bytes in 0 files.
port1/5: 0 bytes in 0 files.
port1/6: 0 bytes in 0 files.
port1/7: 0 bytes in 0 files.
port1/8: 0 bytes in 0 files.
port3/1: 0 bytes in 0 files.
port3/2: 0 bytes in 0 files.
port3/3: 0 bytes in 0 files.
port3/4: 0 bytes in 0 files.
port3/5: 0 bytes in 0 files.
port3/6: 0 bytes in 0 files.
port3/7: 0 bytes in 0 files.
port3/8: 0 bytes in 0 files.
port4/1: 0 bytes in 0 files.
port4/2: 0 bytes in 0 files.
port4/3: 0 bytes in 0 files.
port4/4: 0 bytes in 0 files.
port4/5: 0 bytes in 0 files.
port4/6: 0 bytes in 0 files.
port4/7: 0 bytes in 0 files.
port4/8: 0 bytes in 0 files.
port4/9: 0 bytes in 0 files.
port4/10: 0 bytes in 0 files.
port4/11: 0 bytes in 0 files.
port4/12: 0 bytes in 0 files.
port4/13: 0 bytes in 0 files.
port4/14: 0 bytes in 0 files.
port4/15: 0 bytes in 0 files.
port4/16: 0 bytes in 0 files.
port5/1: 0 bytes in 0 files.
  20.0 GB free (99%)
```

After adding the property and restarting, run the command a second time to verify the additional space.

```
[admin@UplogixLM]# show directory
port1/1: 5.6 MB in 15 files.
port1/2: 0 bytes in 0 files.
port1/3: 0 bytes in 0 files.
port1/4: 0 bytes in 0 files.
port1/5: 0 bytes in 0 files.
port1/6: 0 bytes in 0 files.
port1/7: 0 bytes in 0 files.
port1/8: 0 bytes in 0 files.
port3/1: 0 bytes in 0 files.
port3/2: 0 bytes in 0 files.
port3/3: 0 bytes in 0 files.
port3/4: 0 bytes in 0 files.
port3/5: 0 bytes in 0 files.
port3/6: 0 bytes in 0 files.
port3/7: 0 bytes in 0 files.
port3/8: 0 bytes in 0 files.
port4/1: 0 bytes in 0 files.
port4/2: 0 bytes in 0 files.
port4/3: 0 bytes in 0 files.
port4/4: 0 bytes in 0 files.
port4/5: 0 bytes in 0 files.
port4/6: 0 bytes in 0 files.
port4/7: 0 bytes in 0 files.
port4/8: 0 bytes in 0 files.
port4/9: 0 bytes in 0 files.
port4/10: 0 bytes in 0 files.
port4/11: 0 bytes in 0 files.
port4/12: 0 bytes in 0 files.
port4/13: 0 bytes in 0 files.
port4/14: 0 bytes in 0 files.
port4/15: 0 bytes in 0 files.
port4/16: 0 bytes in 0 files.
port5/1: 0 bytes in 0 files.
  199.1 GB free (99%)
```

<div class='info' />The Local Manager should gain a minimum of 6 GB hard drive space. In some cases, it may automatically allocate more.</div>

# Disable Large File System

To disable the large file system feature, simply delete the property and restart the LM. If the amount of data currently written to disk exceeds the limit, no further files will be written until the cumulative disk space usage is reduced.