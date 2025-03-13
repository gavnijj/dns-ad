<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Building an Intuition for DNS</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Configuration Steps</h2>

- Create an A-record in the Domain Controller and ping it from the Client computer
- Create a CNAME record and observe the results from "ping" & "nslookup"

<h2>Creating A-records and CNAME records</h2>

<p>
<img src="https://i.imgur.com/36k4jLx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
When the computer tries to interact with any kind of host's name on the network whether or not its browsing to it or trying to ping it, it will first check the local DNS cache, then the local host file, and lastly the DNS server. It does this because the local DNS cache file is the fastest to check since its in memory, checking the local host file is slower, and checking the DNS server is the slowest since it is reaching out over the internet. We created a DNS A-record on the Domain Controller called "mainframe" and had it point to the Domain Controller's private IP address. Pinging mainframe will now return the Domain Controller's private IP adress
</p>
<br />

<p>
<img src="https://i.imgur.com/n6llHAV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Domain Controller if we change the IP that mainframe points to something else. It will still return the previous IP because it checks the local DNS cache frst and since mainframe already has a value stored in the local DNS cache it will return that value without checking what the new value is in the DNS server. To ping the new mainframe record we have to use the command "ipconfig /flushdns" because this will empty the cache. 
</p>
<br />

<p>
<img src="https://i.imgur.com/fwUorQq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Created a CNAME record called "search: that points to "www.google.com" in Domain Controller
</p>
<br />

<p>
<img src="https://i.imgur.com/U8FgB4d.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Pinging "search" will ping "www.google.com" and return the IP adress of google. The command "nslookup" will also return the website "www.google.com" and return Google's IP adress
</p>
<br />
