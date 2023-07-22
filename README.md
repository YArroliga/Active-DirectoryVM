<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- File Sharing Activity


<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create VM network using a windows server and a windows client virtual machine
- Test Network Connectivity
- Install Active Directory
- Create User and Admin accounts
- Remote Desktop as a Generic User
- Share files on the domain

<h2>Deployment and Configuration Steps</h2>

<h3>Virtual Network Deployment</h3>

<p>In Azure create a server and a Client on the Domain</p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/f85faa60-b043-428a-9a71-7cddb74eee7d)


<p>Client-1 is created using the same resources and V-net as DC-1</p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/4f00484c-0b1c-41ec-a6d4-7d00e0ab836b)


<p> DC-1's NIC IP adress is set to static</p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/b17b89d1-505f-4409-b108-0a22ed2c7c59)

<h3>Test the Network</h3>

- Client-1 pings DC-1
- Modify ICMv4
- Client-1 continously pings DC-1  

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/f92664ec-0ad0-49dc-a444-d80cab1f0473)

<p>Windows Firewall > Inbound Rules > Sort by Protocol > Enable Core Network Diagnostic</p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/ca9892d2-718e-4240-9d18-3259d052e2b4)


![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/3b503c7f-4214-400a-b1b2-c23b850c36bb)

<p> Client-1 continously pings DC-1</p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/ec75cc67-e02e-47f9-959a-675003b09879)

<h3>Install Active Directory</h3>

In DC-1 go to Server Manager > Add Roles and Features > Server Roles > Active Directory Domain Features

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/5065fe35-c34a-4482-80c7-3c930c486b88)

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/f8e65568-a788-4f64-87aa-75798a772dd1)

<p>Promote the server into a domain controller and create the domain name</p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/2d26c561-a7e2-4743-8a91-33840c58e187)

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/f6b7d601-e0b3-4976-95af-68b42ef8a16a)

<p>the server will restart and login credentials are altered to reflect the domain name</p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/3d6f670f-d478-425b-a9ca-cd99a95a6a01)


<h3>Active Directory Admin and User Accounts</h3>

In DC-1 go to Server Manager > under Tools > Active Directory Users and Computers
![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/69f9f07b-673e-4a4a-a55d-371876294daf)

<p>Create two Orginizational Unit labeled _EMPLOYEES and _ADMINS</p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/2f7cadb3-f185-4f4a-8b6e-31a8bdedb506)

<p> In the _ADMINS Organization Unit create a new Admin User </p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/9bc5d7b1-7911-4cc9-a600-f9d215b78ae2)

<p> In the Active Directory Users and Computers window right click the User's name and Add to a group. In the Text box type "Domain Admins", the check names button will auto complete.</p> 

  ![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/5d0fc6f1-b8e2-4b57-961e-e11857a50cb4)

  <p>Set the DNS server on Client-1 to be DC-1 on the Azure Portal </p>

  ![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/9d034afb-3789-4c38-9de4-917e4346411e)

<p>Restart the server from the Azure portal</p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/6236bd5b-7bbd-4856-9e80-0a28f70254a3)

<p>Remote Desktop into Client-1, right click the start menu > System > Rename this PC > set the domain name to ADlab.com </p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/dc407c9f-e721-44d9-8610-3c5a564aff9a)


<h3>Client-1 as a User using Remote Desktop</h3>

<p> Remote Desktop in using the Admin credentials created earlier</p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/43f5518e-99f9-4a06-8de3-9e37ed3af567)

<p>As Admin account System > Remote Desktop > Add "Domain Users" </p> 

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/cff0fad4-fec1-4c9e-8f9c-63994f1f8758)

<p>Create a generic user in DC-1 </p>
<p>In Active Users and Computers > right click > New > User</p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/f009b259-6111-4057-97b5-54e60fa8eed0)
![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/cef8934b-f22b-4917-a19b-92cf5ea8bed9)
<p></p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/5f0abe44-4140-4ebe-a022-aebe8f7c92b3)

<h3> File Share on the Domain</h3>

<p>On Dc-1 create four folders</p>

- read-access
- write-access
- no-access

<p>In DC-1, in the the C: Drive > New Folder </p>
  
![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/467e3f29-4ba0-4b15-8107-f20004200b1b)

<p>Set permissions for the folder</p>

<p>Folder: read-access Group: “Domain Users”, Permission: “Read”</p>
<p>Folder: write-access Group: “Domain Users”, Permissions: “Read/Write”</p>
<p>Folder: no-access Group: “Domain Admins”, “Permissions: “Read/Write”</p>

<p>Right Click the folder > Properties > Sharing >Share</p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/2182e14c-c273-4327-83eb-e8de2e10a920)

In the Share tab > type "Domain Admin" > Add > Set Permission Level to "Read/Write"

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/871f6dd8-aa23-4754-96e2-4a5d246b108c)

<p> In Client-1, log in as a user and add a file to write-access</p>
<p>In File Explorer, in the search bar type "\\DC-1" for access to the network files </p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/7d059f30-87e4-4f7f-925f-570600c2cbed)

<p>Create a new text file in the folder</p>

![image](https://github.com/YArroliga/Active-DirectoryVM/assets/139689160/60c22ba1-de4d-4438-832f-403510b55031)








