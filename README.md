<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
This tutorial covers observing network traffic flows to and from Azure Virtual Machines via Wireshark, alongside experimenting with Network Security Group configurations. <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Command-Line Tools
- Network Protocols
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic


<h2>Actions and Observations</h2>


We'll start by creating a resource group to house both of our virtual machines. After setting up the resource group, we’ll proceed to create the first virtual machine, which will be a Windows 10 VM. Select the newly created resource group, and name this VM as "VM1." Choose Windows 10 Pro, version 22H, as the operating system. For specifications, ensure that the VM has at least 2 vCPUs and 16 GB of memory. Set up a username and password, and leave the inbound port rules at their default settings.

<p>
<img src="https://imgur.com/WgPD275.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  

<p>
<img src="https://imgur.com/X6ZMTJG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
Following this step, continue clicking "Next" until you reach the networking page, where a virtual network and subnet should be automatically created.
  

<p>
<img src="https://imgur.com/XzdSPoR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
Select "Review and Create" to complete the creation of the VM.

Now that the first VM is ready, we’ll create a second one using Ubuntu Server 20.04 LTS. The process will be the same as before, but this time, select "password" instead of the SSH public key option.
  
<p>
<img src="https://imgur.com/0KT3Fmb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
<p>
<img src="https://imgur.com/pyxsHfF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
Continue selecting "Next" until you reach the networking page once more.
  
The networking configuration should default to the virtual network and subnet previously created for VM1.
  
<p>
<img src="https://imgur.com/3fQXRcw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
Select "Review and Create" to finalize the setup of the second VM.
 
With both virtual machines now active, connect to the Windows 10 VM using the Remote Desktop Connection app. After connecting, open a browser and download and install Wireshark.
 
Wireshark is an open-source, free packet analyzer tool that helps with network troubleshooting, analysis, protocol development, and educational purposes.
 
 Launch Wireshark and set the filter to show only ICMP traffic.
 
 <p>
<img src="https://imgur.com/RrtChUe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
Obtain the private IP address of your Ubuntu VM, and then, in CMD or PowerShell on the Windows 10 VM, type ping 10.0.0.5 (or the correct IP address for your Ubuntu VM) to send the ping while capturing the traffic with Wireshark.
 
<p>
<img src="https://imgur.com/zmJzyne.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
<p>
<img src="https://imgur.com/pp4eZdK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
Open CMD or PowerShell, type ping www.google.com, and monitor the traffic in Wireshark as the ping is sent.
 
Next, initiate a continuous ping from the Windows 10 VM to the Ubuntu VM.
 
Access the Network Security Group for the Ubuntu machine and disable incoming ICMP traffic. To do this, click "Add" to create a new rule, then replicate the settings from the provided image. After creating the rule, it will appear as a new entry.
 
 <p>
<img src="https://imgur.com/r3dH3Yy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
<p>
<img src="https://imgur.com/qiSIrsX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
With incoming ICMP traffic disabled on VM2, the ping request from VM1 will now time out when you check the results.
 
Go back to the Network Security Group for your Ubuntu VM and re-enable ICMP traffic. On the Windows 10 VM, watch for ICMP traffic in Wireshark, and you should see the ping activity resume in the command line. Once it's working, stop the ping process.
 
The next step is to monitor SSH traffic.
 
 
 

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
  
  
