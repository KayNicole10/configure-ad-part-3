# configure-ad-part-3
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in Azure (Part Three)</h1>
This is part three of a tutorial that outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 

<h2>Deployment and Configuration Steps</h2>

- Step 1: Configure DNS Settings for Client-1 
- Step 2: Join Client-1 to Domain
- Step 3: Setup Remote Desktop for Non Administrative Users on Client-1
- Step 4: Generate 10,000 User Accounts Using Powershell ISE

<h2>Configure DNS Settings for Client-1</h2>

<p>
In this first step, I will navigate to DC-1's settings to obtain its private IP address, then navigate to Client-1's settings and select "DNS servers". Select "Custom", then enter DC-1'S private IP address in the space below.  Basically, we are choosing DC-1, the domain controller, to be the DNS server for Client-1. This is so that Client-1 will be able to recognize "mylab.com" when we eventually join it to the domain later. </p>
<p>
<img src="https://i.imgur.com/6xkStyT.png" height="80%" width="80%" alt="private IP"/>
<img src="https://i.imgur.com/M7DGp04.png" height="80%" width="80%" alt="DNS Settings"/>
<img src="https://i.imgur.com/A2NhLyc.png" height="80%" width="80%" alt="DNS server"/>
</p>
<br />

<h2>Join Client-1 to Domain</h2>

<p>
The next step is to join Client-1 to the domain (mylab.com). I navigate to "Settings" ---> "Rename this PC (advanced)" ---> Select "Change" ---> Type "Client-1" for computer name ---> Select "Domain", and type "mylab.com". 
</p>

<p>
<img src="https://i.imgur.com/zZJfFBF.png" height="80%" width="80%" alt="Rename this PC (advanced)"/>
<img src="https://i.imgur.com/cuXyok7.png" height="80%" width="80%" alt="computer name"/>
<img src="https://i.imgur.com/mNTQqEe.png" height="80%" width="80%" alt="domain"/>
</p>

<p>
The computer needs permission from the administrator to perform this action. So I use the login credentials from the admin account I created earlier, jane_admin. The PC will restart after this. Now the admin account, jane_admin, can log into Client-1 and any other computer that would be joined to the domain. 
</p>

<p>
<img src="https://i.imgur.com/vGh0fRk.png" height="80%" width="80%" alt="permission"/>
</p>

<br />

<h2>Setup Remote Desktop for Non Administrative Users on Client-1 </h2>

<p>
<img src="https://i.imgur.com/mBUxC1q.png" height="80%" width="80%" alt="Setup"/>
</p>
<p>
In Client-1, go to remote desktop settings, and under "User accounts", select "Select users that can remotely access this PC". 
</p>

<p>
Type "Domain Users", "Check Names", and "OK". 
</p>

<p>
<img src="https://i.imgur.com/1RpuFdU.png" height="80%" width="80%" alt="Domain Users"/>
<img src="https://i.imgur.com/i72i9n3.png" height="80%" width="80%" alt="Access"/>
<img src="https://i.imgur.com/RXBdb6w.png" height="80%" width="80%" alt="OK"/>
</p>

<h2>Generate 10,000 User Accounts Using Powershell ISE </h2>

<p>
<img src="https://i.imgur.com/pFJR5UK.png" height="80%" width="80%" alt="Powershell ISE"/>
</p>

<p>
Open Powershell ISE, then copy the code below. This is what I'll use to generate 10,000 user random accounts with the same password in Active Directory. 
</p>

<p>
<img src="https://i.imgur.com/YcFQxXt.png" height="80%" width="80%" alt="script"/>
</p>

<p>
Create a new file, paste the contents, then select the green arrow at the top to "run" the script. 
</p>

<p>
<img src="https://i.imgur.com/nWKAWxn.png" height="80%" width="80%" alt="new file"/>
<img src="https://i.imgur.com/S4CrtIF.png" height="80%" width="80%" alt="run"/>
</p>

<p>
I'll then observe the accounts being generated. They are actively populating in the "_EMPLOYEES" OU. 
</p>

<p>
<img src="https://i.imgur.com/KwIxBCC.png" height="80%" width="80%" alt="observe"/>
<img src="https://i.imgur.com/9msgDsH.png" height="80%" width="80%" alt="populating"/>
</p>

<p>
Next, I'll choose a random user account and try to login to Client-1 using the name and password that was given to me in the script (password1). 
</p>

<p>
<img src="https://i.imgur.com/C8wdVKD.png" height="80%" width="80%" alt="account"/>
</p>

<p>
The login is successful. Even though we've never used this user to login to this computer before, we were able to do so as long as it's a member of the domain. 
</p>

<p>
<img src="https://i.imgur.com/LEVAdUp.png" height="80%" width="80%" alt="login"/>
</p>

<p>
A new folder is created for every new user that logs on Client-1. 
</p>

<p>
<img src="https://i.imgur.com/8T9fWkE.png" height="80%" width="80%" alt="folder"/>
</p>

<br />
