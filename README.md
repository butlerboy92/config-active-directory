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

<strong>Client-1 failing ping to DC-1</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/GElhj1N.jpg" height="80%" width="80%" alt="Client-1 failing ping to DC-1"/>
</p>

<br />
<br />
<strong>Enabling pings in DC-1</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/ABVH4Tl.jpg" height="80%" width="80%" alt="Enablinging Ping in DC-1"/>
</p>

<br />
<br />
<strong>Checking Client-1 for response from DC-1</strong>
<br />
<br />
<p>
<img src="https://i.imgur.com/95PwvPd.jpg" height="80%" width="80%" alt="Response from DC-1"/>
</p>
