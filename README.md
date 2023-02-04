<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Microsoft Azure Virtual Machine (VM) under tenant
- Install IIS (with CGI)
- Install PHP Manager and Rewrite Module
- Install and configure MySQL
- Install and configure HeidiSQL
- Install osTicket

<h2>Microsoft Azure Steps</h2>
<p>
Navigate to portal.azure.com and search for Virtual machines.
</p>
<p>
<img src="https://i.imgur.com/E6VDlGR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Click the blue drop-down menu and click "Azure Virtual Machine".
</p>
<p>
<img src="https://i.imgur.com/H3eC2M2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Name your virtual machine "vm-osTicket", select Windows 10 Pro for the image, select a size with 4 vCPUs, and create a username and password to use to connect to your VM.
</p>
<p>
<img src="https://i.imgur.com/ylZvWBy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/CQUicVo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Go back to your virtual machines and copy the IP address.
</p>
<p>
<img src="https://i.imgur.com/1a8VSCv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Search "remote desktop connection" in your search bar and open it. Select "Show options", paste the IP you copied from your virtual machine and type the username you set for it, click "Connect". A window will pop up asking for the password, hit enter and another window will pop up, just click "Yes."
</p>
<p>
<img src="https://i.imgur.com/VHeLTzI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
