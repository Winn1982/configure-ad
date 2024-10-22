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

![image](https://github.com/user-attachments/assets/b62cec29-9d47-4554-ac3a-1443e29faf5f)

I installed Active Directory Domain Services on our Windows 2022 Server and am in now in the process of setting it up as a domain controller named "mydomain.com"

![image](https://github.com/user-attachments/assets/898e491e-b728-4042-9add-f2ff9652700e)

I then made the "Active Directory VM" a domain controller and will now begin creating organizational units.

![image](https://github.com/user-attachments/assets/7d5b0fa2-fdd2-4b05-8883-3112493ccbd4)

In Active Directory, I created two organizational units one is _EMPLOYEES and the other is _ADMINS.

![image](https://github.com/user-attachments/assets/cc10f512-85e1-433a-b93d-b0c5c2482f35)

I then went into the _ADMINS folder that I created and created a user named Jane Doe; her username is jane_admin.

![image](https://github.com/user-attachments/assets/5c882efe-9a5f-4106-8fc1-0fa1619931bb)
 
I added "Jane Doe" to the domain admins security group so she would have administrative rights. 

![image](https://github.com/user-attachments/assets/86208927-6557-4e86-9a80-70a3bc4fef84)

We logged back into the Azeruser virtual machine and are going to connect it to the domain controller. First, we right click on the start menu and go to system. Next, we click Rename this PC (advanced) and under Computer Name we click Change. Then click domain and enter mydomain.com as the domain name to use. 

![image](https://github.com/user-attachments/assets/e6b41e98-60c8-482a-afa8-78b0423d20a3)

Since we already changed Azeruser Virtual Machine to use the Active Directory Virtual Machines private IP Address, it is able to locate the domain controller for mydomain.com and therefore this window will pop-up.

![image](https://github.com/user-attachments/assets/af4d2c68-1816-4ffd-a64f-97c8729cf404)

I entered mydomain.com\jane_admin and the password and we see that we have successfully joined "Azeruser" to the "Active Directory Virtual Machine" domain controller. Once we restart Azeruser it will be a part of the domain controller. 

![image](https://github.com/user-attachments/assets/da411397-a359-4f07-854b-4e47ea59f90f)

I then logged into the domain controller and verified that Azeruser is a part of the Active Directory Users and Computers.

![image](https://github.com/user-attachments/assets/0245832c-6aa8-41bc-bc27-43d3cacc5458)

I then created and organizational unit name _CLIENTS and moved Azeruser into it. 

![image](https://github.com/user-attachments/assets/c625ad2b-a5bb-405d-b3f0-d94a2869e23b)

I then logged in to the domain controller as jane_admin and allowed domain users to have access to the domain controller. I right-clicked the start menu and went to the system menu and then clicked remote desktop. Once in remote desktop I clicked on select users that can remotely access this pc. I searched for domain users and added them accordingly. 

![image](https://github.com/user-attachments/assets/0feef233-a1a4-4d36-9d97-84278b108d1d)

I then logged in Powershell ISE as an administrator and the lab used a pre-made code through SQL that created 10,000 randomly named users for our Active Directory _EMPLOYEES folder. 

![image](https://github.com/user-attachments/assets/d7b54eef-6d3f-4718-ad35-1cc5da242a48)

I checked in Active Directory _EMPLOYEES folder to ensure that the users were created.
