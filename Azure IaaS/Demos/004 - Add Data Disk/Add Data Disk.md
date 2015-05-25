# Add Data Disk

## Requirements

* Windows (or Linux) VM running

## Demo

1. Log into [Current Portal](https://manage.windowsazure.com)
1. Click `Virtual Machines`
1. Click on a VM
1. Click `DASHBOARD` (top nav)
1. Click `ATACH` (bottom nav)
1. Click `Attach empty disk`
1. Focus on `File Name`
	* *Speaker*:
		* Explain that you can customize the file name so for example you can call it <vm_name>-logs or <vm_name>-backups to give the drive meaning
1. Focus on `Size (GB)` & enter a size (e.g 200)
	* *Speaker*:
		* Explain that you can configure the size of the drive up to ~1TB (1023 GB)
1. Focus on `HOST CACHE PREFERENCE`
	* *Speaker*:
		* Explain that this allows you to configure caching options for the attached drive. In some case caching read/writes improves IO performance and is by default enabled on OS drives.

## Optional Demo - Initialize Disk in Windows

**Tip:** You can also have a RDP session waiting to go instead of logging in to speed up the demo.

1. Click `CONNECT` (bottom nav) to RDP to the machine
1. Log into the machine
	* **Tip:** If you are on a domain joined machine click `User another accont` and enter "\<your user name>" to log into the system account and not your domain account.
1. Type `START+X` or right-click the start menu
1. Click `Disk Management`
1. Click `OK` when prompted to *Initialize Disk*
1. Right-Click on your new Disk (likely named `Disk 2`)
1. Click `New Simple Volume`
1. Click `Next` to start the wizard
1. Click `Next` to accept the default size of the disk
1. Click `Next` to accept the default drive letter
1. Click `Next` to format as a NTFS drive
1. Click `Finish` to complete the wizard
1. Click the `Explorer` icon in the taskbard or hit `WindowsKey+E` to open the File Explorer
1. Show that the drive is now available to use

## Optional Demo - Detach Disk

1. Return to VM in Current Portal on the `DASHBOARD` screen.
1. Click `DETACH DISK`
1. Click the `OK` checkmark icon to detach the disk
	* *Speaker*:
		* Explain that you are not deleting the disk, but rather simple "detaching" it from the server. You can reattach it to the same or a different server or using a storage explorer delete the actual VHD disk.
1. Once the disk has been detached click `ATTACH` once again to show that you can easily re-attach the disk (since it wasn't deleted).