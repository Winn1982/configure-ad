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
- Windows 10 (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create a Windows 2022 Server virtual machine
- Create a Windows 10 virtual machine
- Install and Configure Active Directory
- Create "users" with Powershell

<h2>Deployment and Configuration Steps</h2>

![image](https://github.com/user-attachments/assets/b4103fc3-8e16-4893-a1d4-f60ceaddd615)

I created a Windows Server 2022 and I named it "Active Directory VM" I am going into its virtual network settings and I am switching the NIC's private IP Address to static which will be 10.1.0.6.
</p>
<br />

![image](https://github.com/user-attachments/assets/4bb6dcc9-4e80-4a9c-936e-f0abbc07029a)

I then used Remote Desktop to log into the Windows Server 2022 virtual machine and disabled the Windows firewall to test the connectivity. 
</p>
<br />

![image](https://github.com/user-attachments/assets/5e0235fb-4a06-4afa-9ea7-39063a4cf2a0)

I then set "Azeruser" virtual machine's DNS settings to the Windows Server 2022's private IP address (10.1.0.6) so that they are on the same network and the Windows Server 2022 will act as a domain controller. 
</p>
<br />

![image](https://github.com/user-attachments/assets/11903d9a-03f3-4473-8a12-60d55b9ed485)

I then logged into the Windows 10 Pro virtual machine and sent a ping via Powershell to the "domain controller's" private IP address, which showed me that it was a successful ping and there is connectivity. 

![image](https://github.com/user-attachments/assets/3a30c221-d1a6-4a6e-8569-c8199a90e25a)

From Powershell I ran ipconfig /all and the output for the DNS settings should show DC-1’s private IP Address and I confirmed this with what Powershell showed me.


 
