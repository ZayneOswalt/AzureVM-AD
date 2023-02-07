<p align="center">
<img src="https://jumpcloud.com/wp-content/uploads/2016/07/AD1.png" alt="osTicket logo"/>
</p>

<h1>On-premises Active Directory Deployment in the Cloud (Azure)</h1>
This tutorial outlines the implementation of Microsoft Active Directory.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Microsoft Active Directory Domain Services
- Powershell

<h2>Operating Systems Used </h2>

- Windows Datacenter 2022
- Windows 10</b> (21H2)

<h2>Deployment and Configuration Steps</h2>

- Setup Resources in Microsoft Azure
- Ensure a secure connection between the DC and Client
- Install Active Directory
- Create organizational units in Active Directory
- Join Client to your domain
- Configure Remote desktop to non-administrative users

<h2>Microsoft Azure Resource Steps</h2>
<p>
Navigate to portal.azure.com and search for Virtual machines.
</p>
<p>
<img src="https://i.imgur.com/E6VDlGR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Create two virtual machines and make "DC-1" first and then "Client-1", select Windows Server 2022 Datacenter for the image of "DC-1" and Windows 10 Pro for "Client-1", give both a size with 2 vCPUs, and create a username and password to use to connect to your VMs. Head over to the "Networking" tab and make sure "Client-1" is on the same vnet as "DC-1".
</p>
<p>
<img src="https://i.imgur.com/qriRnFK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Navigate back to "Virtual machines" and copy the IP address of "DC-1".
</p>
<p>
<img src="https://i.imgur.com/qH56ioW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Search "Remote Desktop Connection" in your search bar and open it. Select "Show options", paste the IP you copied from "DC-1" and type the username you set for it, click "Connect". A window will pop up asking for the password, hit enter and another window will pop up, just click "Yes."
</p>
<p>
<img src="https://i.imgur.com/U5vi1SZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<h1>Inside the Virtual Machine of DC-1</h1>

<p>
Open up "Windows Defender Firewall" and look for "ICMP Echo Request". Enable both rules to ensure a secure connection between the machines you've created.
<p>
<img src="https://i.imgur.com/RRrJd9p.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<h1>Inside the Virtual Machine of Client-1</h1>

<p>
Locate the Private IP under the properties of "DC-1". Log in to "Client-1", open up the command prompt and ping the Private IP. If followed correctly, it should go through.
</p>
<p>
<img src="https://i.imgur.com/l8am8wr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<h1>Back Inside the Virtual Machine of DC-1</h1>

<p>
Navigate back to the virtual machine "DC-1", bring up the Server Manager. If not already open, open the start menu and search it. Click "Add roles and features", and go through the installer. Once you get to "Server Roles", check the box beside "Active Directory Domain Services" and finish the installer.
</p>
<p>
<img src="https://i.imgur.com/zG16QBV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
You still have to promote "DC-1" to a Domain Controller. Click the flag with a yellow warning sign and click "Promote this server to a domain controller".
</p>
<p>
<img src="https://i.imgur.com/jHJee1y.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
The computer will restart and disconnect. Log into the virtual machine with "< domain name >/< username >" then enter the password and hit enter.
</p>
<br />
  
<p>
Open the Server manager, click "Tools", then click "Active Directory Users and Computers"
<p>
<p>
<img src="https://i.imgur.com/hSi9f3x.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Right-click on your domain name to create a couple new organizational units. One named "EMPLOYEES" and the other named "ADMINS".
</p>
<p>
<img src="https://i.imgur.com/pnjPRLE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
  
<p>
Create a new user in "EMPLOYEES", and assign them to the "Domain Admins" group.
</p>
<p>
<img src="https://i.imgur.com/S6tn9hv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
  
<p>
Log out of "DC-1" and log back in with the new user with admin permission.
</p>
  
<h1>Joining Client-1 to the Domain With Azure</h1>

<p>
Head back to Microsoft Azure virtual machines, click "Client-1", click "Networking", then click "Client-192".
<p>
<p>
<img src="https://i.imgur.com/fDAzj4x.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br /> 
  
<p>
Click "DNS Servers", click "Custom", and paste the Private IP of "DC-1". Save, then restart "Client-1" through Azure.
</p>
<p>
<img src="https://i.imgur.com/D6Aqdgl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br /> 
  
<p>
Log into "Client-1" as the original admin user (the one you created with the VM). Search "Settings" and open it, click "About", click "Rename this PC (advanced)". A window will pop up, click "Change...", click "Domain" and enter your domain. Another window will pop up, log in with a user that has admin privileges.
</p>
<p>
<img src="https://i.imgur.com/kHpYsn6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
  
<p>
Log into "DC-1" and navigate to "Active Directory Users and Computers" in the Server Manager. Click "Computers" to see if "Client-1" appears. Create a new organizational unit named "Clients" and drag "Client-1" into it.
</p>
<p>
<img src="https://i.imgur.com/3EmViVb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h1>Configuring Remote Desktop for Non-administrator Users</h1>
  
<p>
Log into "DC-1" and navigate to "Settings". Click "Remote Desktop", click "Select users that can remotely access this PC". Click "Add...". Add "Domain Users" and click "Ok".
</p>
<p>
<img src="https://i.imgur.com/3EmViVb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Any user who is in your domain may now connect to the virtual machine.
</p>
