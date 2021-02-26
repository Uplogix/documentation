In this example we will copy an OS file from the Uplogix file directory to a Cisco ASA Firewall.


Navigate to the port the device is connected to and temrinal in.
```
[admin@Uplogix (port2/4)]# terminal 

Press ~[ENTER] to exit. 


Connecting ...


Retrieving running-config from device ...
Complete. running-config pulled. 
running-config saved to archive as current.

Console session started.  Press ~[ENTER] to exit.
CISCO-FIREWALL# 
```  

                                                                                                                                                                                
Enable the interactive SCP server by typing **~g** (the Uplogix escape character tilde with the letter g).

```                                                                                                                                                                                                
Enable SFTP/SCP server? (y/n) [y]:                                
SFTP/SCP enabled as port2_4:bWZo3N94RBjTJYl                      
Host 198.51.100.1 or 203.0.113.248                         
Disable the SFTP/SCP server? (y/n) [n]:                                          
CISCO-FIREWALL#                                                

```                                                                                                                                                                               
Enter the device's SCP (or SFTP) commands on the device. In this example we use the dedicated IP address as the host.

```                                                                                                                                         
CISCO-FIREWALL# copy scp: flash:
                                    
Address or name of remote host []? 198.51.100.1
                                                 
Source username []? port2_4

```                                 
For Source filename, the syntax is **/port/category/version/filename** with and underscore (_) in the port name. See [The Uplogix File System](https://uplogix.com/docs/local-manager-user-guide/configuring-managed-devices/uplogix-file-system "The Uplogix File System") for more info on the different files for managed devices. 

                                                                                                                               
```                                                                                                         
Source filename []? /port2_4/os/candidate/asa991-lfbff-k8.SPA

Destination filename [asa991-lfbff-k8.SPA]?                                                
 
Accessing scp://port2_4@198.51.100.1//port2_4/os/candidate/asa991-lfbff-k8.SPA...
Password:
```                                                                                                          
Enter the password that was randomly generated when the SCP server was started (in this example 'bWZo3N94RBjTJYl').

```
Password: ***************
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
Done!
Computed Hash   SHA2: 57df44b741f933b426c26d36c0e67aa6
                      0d9d7d49e8ecccf638eb05aab6dbd082
                      82388c17025f70df40463cd534337392
                      4174dd644248a2277eb9374045550fe5  
                                                    
Embedded Hash   SHA2: 57df44b741f933b426c26d36c0e67aa6
                      0d9d7d49e8ecccf638eb05aab6dbd082
                      82388c17025f70df40463cd534337392
                      4174dd644248a2277eb9374045550fe5
 

Digital signature successfully validated
Writing file disk0:/asa991-lfbff-k8.SPA...                                            
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!!!!!!!!!!!!!!!!!!!!!!
109776224 bytes copied in 1068.860 secs (102786 bytes/sec)
```



### To copy a file from the network device to the Local Manager, reverse the commands:
```
CISCO_FIREWALL# copy flash: scp: 
 
Source filename []? asa951-lfbff-k8.spa

Address or name of remote host []? 198.51.100.1
  
Destination username []? port2_4  
  
Destination filename [asa951-lfbff-k8.spa]? //port2_4/os/named/asa951-lfbff-k8
                                                                                                                                                                                                
Password: *************** 
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
```                                                      
