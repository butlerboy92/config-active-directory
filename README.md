<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure and ensure connectivity
- Install Active Directory
- Create accounts and join client to domain
- Setup remote desktop for non-admin users
- Create a bunch of accounts (using a script)

<h2>Deployment and Configuration Steps</h2>

<strong>Step 1:</strong> Setup Resources in Azure and ensure connectivity
<br />
<br />

<p>
Create two Virtual Machines in Azure, one named DC-1 (Server) and the other Client-1 (Win10)
<br />
<br />
Make sure you remember the username and password you create
</p>
<br />
<br />
<strong>✪ DC-1 VM</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/ToGULuK.jpg" height="80%" width="80%" alt="Creating DC-1 Virtual Machine"/>
</p>

<br />
<br />

<strong>✪ Client-1 VM</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/mcddAXN.jpg" height="80%" width="80%" alt="Creating Client-1 Virtual Machine"/>
</p>

<br />
<br />
<p>
Now we want to set DC-1 private IP address to be static so it doesn't change. (in Azure) Virtual Machines ⇒ DC-1 ⇒ Networking ⇒ (Next to Networking Interface click dc-***) ⇒ IP Configurations ⇒ Click the private ip address with dynamic ⇒ Switch it to static then click save
</p>
<br />
<br />
<strong>✪ Networking Interface w/ dc-***</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/QyDyni9.jpg" height="80%" width="80%" alt="Networking Interface Location"/>
</p>

<br />
<br />
<strong>✪ Swapping to Static</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/CGG1hVz.jpg" height="80%" width="80%" alt="Swapped IP to static"/>
</p>

<br />
<br />

<strong>Step 1.2:</strong> Ensure Connectivity with Client and Domain
<br />
<br />

<p>
Login to Client-1 remotely and ping DC-1 ip address with ping -t (so it constantly keeps pinging)
<br />
<br />
Login to DC-1 remotely and in the search bar on the task bar search <strong>wf.msc</strong> and continue
<br />
<br />
Sort by Protocol to find ICMPv4 and then enable both ICMP Echo requests and then check back on Client-1 for a response
</p>
<br />
<br />

<strong>✪ Client-1 failing ping to DC-1</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/GElhj1N.jpg" height="80%" width="80%" alt="Client-1 failing ping to DC-1"/>
</p>

<br />
<br />
<strong>✪ Enabling pings in DC-1</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/ABVH4Tl.jpg" height="80%" width="80%" alt="Enablinging Ping in DC-1"/>
</p>

<br />
<br />
<strong>✪ Checking Client-1 for response from DC-1</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/95PwvPd.jpg" height="80%" width="80%" alt="Response from DC-1"/>
</p>

<br />
<br />

<strong> Step 2:</strong> Install Active Directory
<br />
<br />
<p>
Login to DC-1 and install Active Directory
<br />
<br />
Make sure Server Manager is opened and then click Add roles and features then you want to click 'Next' till you get to Server roles and make sure Active Directory Domain Service is clicked. Then click 'Next' until you get to install.
<br />
<br />
Once installed go to the flag with a yellow exclimation mark and click Promote this server to a domain controller
<br />
<br />
In the radio selector select new root and name your domain (whatever).com and then 'Next' and just make the password whatever (it wont be used) then 'Next' through until you get to install and install AD and let it set up. It will need to restart so just reconnect after but you will have to use a different account called (nameofyourdomain)\(username) and then same password as the one you created during VM setup. Example:( mydomain.com\labuser1 ).
</p>

<br />
<br />
<strong>✪ Installing Active Directory</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/2xskjNc.jpg" height="80%" width="80%" alt="Installing Active Directory"/>
</p>

<br />
<br />
<strong>✪ Making into a Domain Controller</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/VkMTMnF.jpg" height="80%" width="80%" alt="Making into a Domain Controller"/>
</p>

<br />
<br />
<strong>✪ Reconnecting DC-1 as domain controller with full quailified domain name</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/IwOYVdR.jpg" height="80%" width="80%" alt="Making into a Domain Controller"/>
</p>

<br />
<br />


<strong> Step 3:</strong> Create Admin and Normal User in Active Directory
<br />
<br />
<p>
Start by creating a few organizational units in Active Directory
<br />
<br />
Click 'Tools' and then click 'Active Directory Users and Computers' and right click 'mydomain.com' ⇒ New ⇒ Organizational Units
<br />
Create _EMPLOYEES and _ADMINS
<br />
<br />
Then in _ADMINS right click and create 'New' ⇒ 'User' name it whatever then right click your user and go to Properties >> Member of >> Add >> Domain Admins 
<br />
<br />
OK and Apply to finish. Then logout of DC-1 and reconnect as mydomain.com\jane_admin
  and use this as your admin from now on.
</p>

<br />
<br />
<strong>✪ Creating _EMPLOYEES and _ADMINS</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/dyKLGfD.jpg" height="80%" width="80%" alt="Creation of _EMPLOYEES and _ADMINS"/>
</p>

<br />
<br />
<strong>✪ Creating a user in _ADMINS</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/EZZGgnf.jpg" height="80%" width="80%" alt="Creation of user in _ADMINS"/>
</p>

<br />
<br />
<strong>✪ Making user in _ADMINS an Admin</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/v0PyInY.jpg" height="80%" width="80%" alt="Making user into an Admin"/>
</p>

<br />
<br />
<strong>✪ Reconnecting into DC-1 as new admin</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/HftVymZ.jpg" height="80%" width="80%" alt="Reconnecting to DC-1 as new Admin"/>
</p>
