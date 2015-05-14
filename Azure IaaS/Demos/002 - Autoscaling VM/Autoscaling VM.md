# Autoscaling VM

[TOC]

## Prerequisites / Setup

1. Configure three (3) VMs
	* All the **same size**
	* All part of the **same cloud service**
	* All in the **same availability set**

## From Portal

1. Open [Portal](http://portal.azure.com)
1. Click `BROWSE`
1. Click `VIRTUAL MACHINES`
1. Click on one of the three previously created VMs
1. Click `Dashboard`
1. Scroll to `autoscale status`
	* **Speaking Notes**:
		* Highlight (zoom in) on the text that says "Autoscale can save you up to **33%**"
		* Explain that Autoscale allows the Azure Fabric Controller to turn servers on and off as needed to save you money.
1. Click `CONFIGURE AUTOSCALE`
	* **Speaking Notes**:
		* Explain that there are two ways to autoscale either by a schedule or by a metric such as CPU or the number of messages in a queue.
1. Click `set up schedule times` & highlight some of the options
	* **Speaking Notes**:
		* Explain that if you know your application has traffic that follows a specific time of day or even year you can schedule your scale.
		* Or say this is for your internal dev/test environment you can have it turn off systems at night or the weekend to save on costs.
1. Close `schedule times`
1. Click `CPU`
1. Focus on `INSTANCE RANGE`
	* **Speaking Notes**:
		* Explain that you can tell Azure how to scale by setting the minimum & maximum # of instances you wish to have running at any given time.
1. Focus on `TARGET CPU`
	* **Speaking Notes**:
		* Azure will scale up when the avg CPU exceeds the maximum threshold and will scale down when it falls below the minimum confiugured threshold.
1. Focus on `SCALE UP BY`
	* **Speaking Notes**:
		* Explain that the remaining options allow you to set how quickly (or slowly) you scale up and down your number of instances.