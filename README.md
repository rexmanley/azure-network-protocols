# azure-network-protocols<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Resource Groups
- Virtual Network and Subnet
- Two Virtual Machines
- Examine traffic between machines

<h2>Actions and Observations</h2>


Part 1
https://portal.azure.com/
(Create our Virtual Machines)
![image](https://github.com/user-attachments/assets/bacd6825-c406-4ae3-8d59-891a2dde0cbd)

Create a Resource Group
![image](https://github.com/user-attachments/assets/93169622-0806-4c91-9709-4ed51fb5e39b)

Create a Windows 10 Virtual Machine (VM)
![image](https://github.com/user-attachments/assets/b8c04563-7cb0-419e-b60a-7e1beb4ee510)

While creating the VM, select the previously created Resource Group
![image](https://github.com/user-attachments/assets/d86cc1ae-cbc7-404c-ad66-78f9529141bd)
![image](https://github.com/user-attachments/assets/d1eb80ec-dfcf-4866-99ff-3e32b0aa4347)

While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet

![image](https://github.com/user-attachments/assets/65925304-c498-4f62-93f1-7374f784879b)

Create a Linux (Ubuntu) VM
While creating the VM, select the previously created Resource Group and Virtual Network—the Virtual Network MUST BE THE SAME.
Authentication type: Username/Password
![image](https://github.com/user-attachments/assets/debdfe8c-c6e5-4a67-ada1-a7ad25413abe)
![image](https://github.com/user-attachments/assets/61a4602e-a24a-43a7-9436-a8ca4709215a)

Ensure both VMs are in the same Virtual Network / Subnet



Part 2
https://portal.azure.com/
(Observe ICMP Traffic)

If using Mac, install Microsoft Remote Desktop
Use Remote Desktop to connect to your Windows 10 Virtual Machine
![image](https://github.com/user-attachments/assets/8e2bf87e-d48c-45db-9afa-207ad2f30b54)

Within your Windows 10 Virtual Machine, Install Wireshark
![image](https://github.com/user-attachments/assets/55b93481-7c93-4d52-8286-ee7e9d898b97)

Open Wireshark and start packet capture (click Ethernet)
![image](https://github.com/user-attachments/assets/26c2006b-cf74-4a90-8071-86c699373668)

Within Wireshark, filter for ICMP traffic only
![image](https://github.com/user-attachments/assets/f1fb1027-6144-4af3-bece-62e0460cddfe)

Retrieve the private IP address of the Ubuntu VM (linux-vm) and attempt to ping it from within the Windows 10 VM
![image](https://github.com/user-attachments/assets/e26d5b3d-123f-4627-b01a-901a543de2d8)
Observe ping requests and replies within WireShark
From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
![image](https://github.com/user-attachments/assets/d96b01bd-d474-476a-abb2-f78c1c1f1048)


Part 3
(Configuring a Firewall [Network Security Group])
Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic

![image](https://github.com/user-attachments/assets/889d578d-96cd-4fe6-a51b-4a0c546af3e0)

Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
![image](https://github.com/user-attachments/assets/ec47c6dc-665c-4988-a670-818c0bb72428)


Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
![image](https://github.com/user-attachments/assets/b061218c-64a9-4e18-b2a4-db76bb594fc6)

Stop the ping activity (ctrl-c in powershell)
![image](https://github.com/user-attachments/assets/ffbeab9c-c51d-4539-b82b-f03ec3935392)

(Observe SSH Traffic)
Log back into the windows-vm
Back in Wireshark, start a packet capture up
![image](https://github.com/user-attachments/assets/21d84c37-1426-4ed5-98f9-18da031ca43d)

Filter for SSH traffic only
![image](https://github.com/user-attachments/assets/3ac3bf00-ab35-4493-85af-81bdbb31ab5f)

From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
Open PowerShell, and type: ssh labuser@<private IP address>
![image](https://github.com/user-attachments/assets/3d8b8584-877d-46af-af65-61c084100a9b)

Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
![image](https://github.com/user-attachments/assets/eeef61a2-aa59-49b9-b515-de4ad474885e)

Exit the SSH connection by typing ‘exit’ and pressing [Enter]
![image](https://github.com/user-attachments/assets/9fd43b16-9133-40ed-a15b-ff84fad8e0a6)



