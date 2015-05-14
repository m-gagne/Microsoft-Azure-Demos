# Provisioning VM In Current Portal Demo

[TOC]

## Guide

### Gallery
1. Click `NEW`
1. Click `VIRTUAL MACHINE`
1. CLICK `FROM GALLERY`
	* **Speaking Notes**:
		* Explain that the gallery is a collection of Microsoft supported images that you can quickly and easily deploy as an Azure Virtual Machine
		* These images include Windows Server, Windows images with Visual Studio pre-installed, SQL Server, Linux distro's such as Ubuntu, Centos, Suse and more.

### Windows Server

1. Click `Windows Server 2012 R2 Datacenter`
1. Click `Next`
1. Enter a `VIRTUAL MACHINE NAME`
	* **Speaking Notes**:
		* Explain that this name must be globally unique.
1. Toggle between `BASIC` & `STANDARD`
	* **Speaking Notes**:
		* Virtual Machines are supported in both a Basic and Standard tier. The Basic tier provides an economical option for dev/test workloads, and other applications that don’t require load-balancing, auto-scaling, or memory-intensive virtual machines. The Standard tier is our recommended option for all production workloads.
1. Scroll through `SIZE`
	* **Speaking Notes**:
		* *Basic* servers support A0-A4
		* *Standard* servers support up to the G (Godzilla) class servers with 32 cores and nearly 1/2 a terabyte of ram.
1. Enter a `NEW USER NAME`
1. Enter a `PASSWORD` & confirm it.
1. Click `NEXT` (Right Arrow)
1. Either create a new `CLOUD SERVICE` or use an existing one.
	* **Speaking Notes**:
		* Explain that we will cover cloud services more shortly but it's important to understand that they act as a virtual security 'container' for related services.
		* For example, Virtual Machines in the same cloud service can be load balanced and can communicate directly to each other. 
		* Services in separate cloud services are considered un-related and can only communicate to each other by public network which is slower, introduces bandwidth charges and more.
		* You can connect cloud services together by using Virtual Networks
 1. Select a `REGION/AFFINITY GROUP/VIRTUAL NETWORK`
	* **Speaking Notes**:
 		* Explain that select a Region will tell Azure which Data Center or DC you wish your infrastructure to be deployed to
 		* Affinity Groups were once used to further tell Azure to allocate infrastructure physically closer to each other for performance and network management however this is no longer required or suggested.
 		* Select a Virtual Network to join systems together on the same vnet.
 1. Select a `STORAGE ACCOUNT`
	* **Speaking Notes**:
 		* Explain that one of the key benefits of Azure IaaS vs other providers is that ALL services are based on our triple redundant and optionally geo-redundant storage solution.
 		* Why does this matter? It means if the underlying hardware fails, your OS disk and Data disks persist and you can be back up and running in no time by simply re-attaching the disks to a new VM.
 1. Select an `AVAILABILITY SET`
	* **Speaking Notes**:
 		* Explain that Availability Sets allows Azure to understand your infrastructure better and how to handle maintenance like patching and rebooting systems.
 		* As an example if you have two VMs load-balanced together but not in separate availability sets and the host servers they are on need maintenance your entire system could be taken off line.
 		* However if they are placed in separate Availability Sets then Azure will only deal with one set at a time.
 		* This means maintenance is done to each set sequentially and only after the one is confirmed to be up and running again before moving on to the next one.
 		* [Read more](http://azure.microsoft.com/en-in/documentation/articles/virtual-machines-manage-availability/)
 1. `ENDPOINTS`
	* **Speaking Notes**:
 		* Explain that here you can add/edit/delete public endpoints.
 1. Click `NEXT`
 	* **Speaking Notes**:
 		* Explain that here you can select some additional features/applications to be added to your server.
 1. Click `OK` (checkmark)
 	* **Speaking Notes**:
 		* Explain that it will take Azure about 5-6 minutes to provision, boot and configure your virtual machine!

### Linux

1. From VM Gallery select `Ubuntu LTS` (any version)
1. Click `Next`
1. Enter a `VIRTUAL MACHINE NAME`
	* **Speaking Notes**:
		* Explain that this name must be globally unique.
1. Toggle between `BASIC` & `STANDARD`
	* **Speaking Notes**:
		* Virtual Machines are supported in both a Basic and Standard tier. The Basic tier provides an economical option for dev/test workloads, and other applications that don’t require load-balancing, auto-scaling, or memory-intensive virtual machines. The Standard tier is our recommended option for all production workloads.
1. Scroll through `SIZE`
	* **Speaking Notes**:
		* *Basic* servers support A0-A4
		* *Standard* servers support up to the G (Godzilla) class servers with 32 cores and nearly 1/2 a terabyte of ram.
1. Enter a `NEW USER NAME`
1. Upload a SSH key
	* Upload a .pem or .cer file
	* **Setup**:
		* To create a compatible SSH key yourself or for the audience, go to [http://aka.ms/azuressh](http://aka.ms/azuressh)
			* On Windows you will need to create a key using OpenSSL, download the [Windows Binaries here](http://slproweb.com/products/Win32OpenSSL.html), [direct download](http://slproweb.com/download/Win32OpenSSL_Light-1_0_2a.exe).
				* Notes on OpenSSL
					* Ignore the warning about Visual Studio 2008 redistributable
					* `openssl.exe` can be found in `c:\OpenSSL-Win32\bin`
					* You will get an error about not being able to open a config file to fix that add `-config <config file>` to the params
						* `openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout myPrivateKey.key -out myCert.pem -config c:\OpenSSL-Win32\bin\openssl.cfg`
	* **Speaking Notes**:
		* Explain that SSH keys are the best and most secure way to connect to a Linux server (vs username & password).
		
1. Click `NEXT` (Right Arrow)
1. Either create a new `CLOUD SERVICE` or use an existing one.
	* **Speaking Notes**:
		* Explain that we will cover cloud services more shortly but it's important to understand that they act as a virtual security 'container' for related services.
		* For example, Virtual Machines in the same cloud service can be load balanced and can communicate directly to each other. 
		* Services in separate cloud services are considered un-related and can only communicate to each other by public network which is slower, introduces bandwidth charges and more.
		* You can connect cloud services together by using Virtual Networks
 1. Select a `REGION/AFFINITY GROUP/VIRTUAL NETWORK`
	* **Speaking Notes**:
 		* Explain that select a Region will tell Azure which Data Center or DC you wish your infrastructure to be deployed to
 		* Affinity Groups were once used to further tell Azure to allocate infrastructure physically closer to each other for performance and network management however this is no longer required or suggested.
 		* Select a Virtual Network to join systems together on the same vnet.
 1. Select a `STORAGE ACCOUNT`
	* **Speaking Notes**:
 		* Explain that one of the key benefits of Azure IaaS vs other providers is that ALL services are based on our triple redundant and optionally geo-redundant storage solution.
 		* Why does this matter? It means if the underlying hardware fails, your OS disk and Data disks persist and you can be back up and running in no time by simply re-attaching the disks to a new VM.
 1. Select an `AVAILABILITY SET`
	* **Speaking Notes**:
 		* Explain that Availability Sets allows Azure to understand your infrastructure better and how to handle maintenance like patching and rebooting systems.
 		* As an example if you have two VMs load-balanced together but not in separate availability sets and the host servers they are on need maintenance your entire system could be taken off line.
 		* However if they are placed in separate Availability Sets then Azure will only deal with one set at a time.
 		* This means maintenance is done to each set sequentially and only after the one is confirmed to be up and running again before moving on to the next one.
 		* [Read more](http://azure.microsoft.com/en-in/documentation/articles/virtual-machines-manage-availability/)
 1. `ENDPOINTS`
	* **Speaking Notes**:
 		* Explain that here you can add/edit/delete public endpoints.
 		* By default SSH is open so you can connect and manage the system.
 1. Click `NEXT`
 	* **Speaking Notes**:
 		* Explain that here you can select some additional features/applications to be added to your server.
 1. Click `OK` (checkmark)
 	* **Speaking Notes**:
 		* Explain that it will take Azure about 5-6 minutes to provision, boot and configure your virtual machine!