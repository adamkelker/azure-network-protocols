<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
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

1.) Let's begin by creating a resource group in Microsoft Azure to accommodate both virtual machines. Once the resource group is set up, we'll proceed to create the first virtual machine, which will be a Windows 10 Virtual Machine. Follow these steps:

- Start by creating a resource group to house both virtual machines.
- Once the resource group is ready, proceed to create the first virtual machine.
- The first virtual machine will be named "VM1." When prompted to choose the operating system, select "Windows 10 Pro, version 22H."
- For the virtual machine's specifications, opt for a minimum of 2 VCPUs and 16 GB of memory.
- During setup, choose a username and password as per your preference.
- Ensure that the inbound port rules remain set to their default configurations.


<p>
<img src="https://imgur.com/WgPD275.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  

<p>
<img src="https://imgur.com/X6ZMTJG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
2.) Once we complete the previous step, proceed by clicking "Next" continuously until we reach the networking page. At this stage, the system will automatically generate a virtual network and subnet on our behalf. 
  

<p>
<img src="https://imgur.com/XzdSPoR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
  Click review and create our VM.

Having successfully created our first VM, we'll now proceed to create the second VM. This time, we'll be setting up an Ubuntu Server 20.04 LTS machine. The process will be similar to creating the first machine, but with one change: we'll switch from using an SSH public key to a password for authentication. Follow these steps to create the second VM:

Begin by initiating the VM creation process as before.
Select "Ubuntu Server 20.04 LTS" as the operating system for the second virtual machine.
It will be the same process as creating our first machine but instead we are going to switch the SSH public key to password instead of the SSH public key.
By following these steps, we'll have our second VM set up and ready to use.
    
<p>
<img src="https://imgur.com/0KT3Fmb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
<p>
<img src="https://imgur.com/pyxsHfF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
 We get to the next step by clicking "Next" repeatedly until we reach the networking page again. At this stage, the networking settings will automatically provide us with the virtual network from VM1, along with the associated subnet.
  
<p>
<img src="https://imgur.com/3fQXRcw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
 Click review and create, and it will create our second VM.
 
 2.)With both virtual machines now operational, next we will connect to the Windows 10 VM using the remote desktop connection app. Once we are connected, we'll open our web browser and proceed to download and install Wireshark.

"Wireshark is a free and open-source packet analyzer. It is used for network troubleshooting, analysis, software and communications protocol development, and education."

Open Wireshark and filter to display only ICMP traffic.
 
 <p>
<img src="https://imgur.com/RrtChUe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
 4.) We are going to want to retrieve the private IP address of our Ubuntu VM and then attempt to ping it from within our Windows 10 VM using wireshark. To ping the private IP address of the Ubuntu machine open CMD or Powershell on the Windows machine and type: ping 10.0.0.5 or whatever the private IP address is for your Ubuntu machine.

 Now we are going to retrieve the private IP address of our Ubuntu VM, then attempt to ping it from our Windows 10 VM using wireshark.

To initiate the ping, open either CMD or PowerShell on the Windows machine and type: ping 10.0.0.5.
By executing this command, we will be attempting to ping the Ubuntu VM from the Windows 10 VM, and Wireshark will capture the network traffic for analysis.
 
<p>
<img src="https://imgur.com/zmJzyne.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
<p>
<img src="https://imgur.com/pp4eZdK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
 In either CMD or Powershell ping www.google.com and observe the traffic in wireshark.
 
5.) Next we are going to initiate a continuous ping from our Windows 10 VM to our Ubuntu VM.
 
6.) Open the Network Security Group of our Ubuntu machine and disable incoming (inbound) ICMP traffic. We disable incoming ICMP traffic by clicking "Add" new rule and copying everything exactly from the picture. Once that is done we can create the rule and it will create automatically and show up as a new rule.
 
 <p>
<img src="https://imgur.com/r3dH3Yy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
<p>
<img src="https://imgur.com/qiSIrsX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
 
 Now that we have disabled incoming ICMP traffic from VM2 if we go back to VM1 you can see the ping request is timing out. 
 
 7.) Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
Stop the ping activity
 
 8.) The next thing we are going to do is Observe SSH Traffic.
