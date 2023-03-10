<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Microsoft Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
- MacOS

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1 - Create a Domain Controller on Microsoft Azure. When logging into the Azure Portal you'll first create a Virtual Machine (Windows Server 2022). Be sure to take note of the resource group and VNET. 
- Step 2 - Create your next VM. We'll assign this under the same VNET & resource group that we established in the previous step. This will act as the client that we'll be connecting later on with Active Directory. Once the VM is running, it is criticial to confirm they are both using the same VNET.
- Step 3 - Log into the Domain Controller through Mircrosoft Remote Desktop. After login, open server manager and click the 'Add Roles and Features' tab. From here install 'Active Directory Domain Services' and setup a new Forest. For this example we'll name it mydomaindotcom (but it can be anything).
- Step 4 - Once installation is complete you will be asked to restart the computer and upon restart Active Directory will be ready to go. See photos below.

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/Zh7MIP2.jpg)"  height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Here in the azure portal we see the client VM we setup. On the left of the page we see "Networking" where we can view the VNET and verify it's identical to our Domain Controllers VNET. In the center of the page we see the Microsoft Remote Desktop app where we will be using to access both VM's via 'Public IP Address', VM Name, and password.
</p>
<br />

<p>
<img src="https://i.imgur.com/j6jX25h.jpeg)" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
When first logging into your Domain Controllers VM, open up the 'Server Manager' application. This is where we'll install Active Directory. Be sure to check the box that is labeled "Active Directory Domain Services" and setup a new 'Forest'. Once completed Active Directory will be ready to run as soon as you restart the VM.
</p>
<br />

<p>
<img src="https://i.imgur.com/rqvuhur.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After restarting the DC VM and logging in click on the Windows icon and search Active Directory to verify it was a succesful installation. I ran a script to generate thousands of users. This is where we'll utilize the "Client" VM. From the Azure Portal, set the "Client" VM's DNS settings to the DC VM's private IP address and restart the "Client" VM. Next after logging back into the VM join it into the domain, "mydomaindotcom". Once it has successfully joined it will restart. Since this VM is now apart of the network it will be able to log into any of the random users that we create and able to access the files on the server as long as it has the right permissions. The photo below shows me logging into a user I created in Active Directory.

<img src="https://i.imgur.com/ofNsVlz.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
