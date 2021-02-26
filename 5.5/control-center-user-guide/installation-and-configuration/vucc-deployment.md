# Overview
This document contains instructions for deploying a Virtual Machine version of the Uplogix Control Center on a compatible VMWare server.

These instructions are applicable for both the production Virtual Control Center and the non-production, Evaluation Virtual Control Center.

# Requirements
* Virtual Control Center OVA file (download from uplogix.com/support/account)
* VMWare host running ESX/ESXi version 6.0 or higher (Virtual Machine Version 11)
* Two IP addresses on the same network with subnet mask and gateway
* 825 GB of storage space on SAS/SSD drive (SATA spinning drives are not recommended)
* 8 GB memory
* 8 CPU cores

# Recommended / Default Resource Allocation

|STORAGE | MEMORY | CPUs |
|-|-|-|
|825 GB (Thin provisioned)	| 8 GB	| 8 Cores|

> Due to the nature of VM environments, some resource allocations can be adjusted for smaller deployments. See [Advanced Resource Tuning](#advanced-resource-tuning) for more information.

# ESXi Version

To deploy the Virtual Control Center, choose your version of ESXi below.

* Deploying a Virtual Control Center to ESXi 7 (coming soon)
* [Deploying a Virtual Control Center to ESXi 6.7 or Earlier](https://uplogix.com/docs/control-center-user-guide/advanced-features/deploying-vucc-to-esxi6X)

# Advanced Resource Tuning
The default resource allocation has been thoroughly tested to support deployments up to 2,000 Local Managers. Smaller deployments will use fewer resources, so VM administrators may elect to set lower limits for storage, memory, and CPU.

## Estimated Resource Usage
| Deployment Size |	Storage	| Memory	| CPUs (2+ GhHz) |
| - | - | - | - |
| 1000+ |	825 GB	| 8 GB	| 8 cores| 
| 250 â€“ 999	| ~650 GB	| 8 GB	| 8 cores |
| 100 â€“ 249 	| ~550 GB	| 4 GB\*	| 4 cores |
| 1 â€“ 99	| ~450 GB	| 4 GB\*	| 2 cores |
| Evaluation vUCC	| ~65 GB	| 1 GB\* | 2 cores |

* Using less than the default 8 GB for memory requires software changes.

## Storage

The Control Center will initially use about 430 GB of space after initial deployment. The total disk space used will grow as more Local Managers are added to the deployment but will not exceed 825 GB.

The Evaluation Control Center will initially use 50 GB and can grow to a maximum of 100 GB.

SSDs are recommended for maximum performance, though SAS drives can be used in smaller (<250) deployments. SATA drives should only be used on non-production, Evaluation UCCs.

## Memory

If less than 8 GB is allocated for memory, you will need to update the Control Centerâ€™s memory configuration.

1. 	Enter **vi /etc/sysconfig/embassy.overrides**
2. 	Move the cursor over the number 8 on the line which reads **RAM=8**
3. 	Press **r**, then enter the number of gigs of RAM allocated to your VM
4. 	Type **:wq** to save the file and exit from the editor
5. 	Restart the vUCC application by entering the commands **ucc stop** and **ucc start**.

## CPUs
The number of CPUs allocated to the Control Center can be modified without any changes to software. A restart of the VM may be necessary after modifying the CPU allocation.

## Virtual Machine Version

Uplogix configures the Control Center to use VM version 11  for backwards compatibility to ESXi version 6.0 . You may optionally upgrade the VM version to match the version of ESXi in your environment. VMware recommends creating a snapshot or backup before upgrading in case there are issues post upgrade. In older versions of ESXi, you may need to use vCenter to convert the image to a newer version. In newer versions of ESXi, you can use the web client to upgrade the VM while it is powered down (**Actions > Upgrade VM Compatibility**). Uplogix has tested most of the versions from 11 to 17, which is compatible with  ESXi 7.0 

Updating the VM version will also enable you to update the Guest OS associated with the VM (**Edit > VM Options > General Options > Guest OS Version**). Any version of the Control Center after 5.4.0 uses CentOS 6 (64-bit).
Please contact Uplogix Support if you have any question about configuring the VM version or Guest OS.
