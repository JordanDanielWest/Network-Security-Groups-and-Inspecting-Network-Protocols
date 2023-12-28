<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Windows VM & Ubuntu VM
- Install Wireshark
- Observe Protocols within Wireshark

<h2>Actions and Observations</h2>

<h3>Create Virtual Machines</h3>

- Create Virtual Machine
- Virtual Machine Name: Windows-VM
- Region: West US 3
- Image: Windows 10 Pro
- Size: 2 vcpus, 16 GiB memory
- Username: labuser
- Password: VirtualMachine!
- Check box "I confirm I have an elligible Windows 10/11 license with multi-tenant hosting rights."
- Wait for New resource group & v-net to deploy
- Create Vitual Machine
- Resource Group: Windows-_group (use resource group created when Windows-VM was created)
- Virtual Machine Name: Ubuntu-VM
- Region: West US 3
- Image: Ubuntu Server 20.04 LTS
- Size: 2 vcpus, 16 GiB memory
- Authentication type: Password
- Username: labuser
- Password: VirtualMachine!
- Next
- Next
- Virtual Network: Windows-VM-vnet (use vnet created when Windows-VM was created)
- Review + Create
- Create

<h3>Observe ICMP Traffic</h3>

- Connect to Windows-VM with Remote Desktop
- Download & Install Wireshark https://www.wireshark.org/
- Open Wireshark
- Select Ethernet
- Select Blue Fin to start receiving packets

![image](https://github.com/JordanDanielWest/Network-Security-Groups-and-Inspecting-Network-Protocols/assets/96628562/c0663802-7e1a-4cb6-bc9c-ffbc559fead4)

- Filter traffic by "icmp"

![image](https://github.com/JordanDanielWest/Network-Security-Groups-and-Inspecting-Network-Protocols/assets/96628562/76cd6191-30ad-4baa-b6df-78008cea4263)

- Ping Ubuntu-VM private IP Address from Windows-VM Command Line (10.0.0.5)
- Observe Ping Requests in Wireshark

![image](https://github.com/JordanDanielWest/Network-Security-Groups-and-Inspecting-Network-Protocols/assets/96628562/972f409f-ab68-45a5-aa1c-e8d13a74c567)

- Open Command Line and ping www.google.com
- Observe results in wireshark

![image](https://github.com/JordanDanielWest/Network-Security-Groups-and-Inspecting-Network-Protocols/assets/96628562/1aa4347f-c797-4438-a788-6b318c051335)

- Initiate perpetual ping from Windows-VM to Ubuntu-VM (ping -t 10.0.0.5)
- Open Network Security Group for Ubuntu-VM and disable inbound (ICMP) traffic

![image](https://github.com/JordanDanielWest/Network-Security-Groups-and-Inspecting-Network-Protocols/assets/96628562/ae6de9a0-3dbb-4e9f-a07f-7a909260d79e)

- Select "Create Port Rule"
- Inbound rule
- Protocol: ICMP
- Action: Deny
- Priority: 200
- Add

![image](https://github.com/JordanDanielWest/Network-Security-Groups-and-Inspecting-Network-Protocols/assets/96628562/32e6da60-c318-4971-ac6e-3ef889c20e09)

- Observe Changes in Wireshark

![image](https://github.com/JordanDanielWest/Network-Security-Groups-and-Inspecting-Network-Protocols/assets/96628562/9b94bf85-7cdb-432e-beb3-6fcf17e014cb)

- Re-enable ICMP traffic In Ubuntu Network Security Group (delete the rule)
- Observe changes

![image](https://github.com/JordanDanielWest/Network-Security-Groups-and-Inspecting-Network-Protocols/assets/96628562/1a5b592b-fb68-4e5b-ab79-70d1a5130c20)

<h3>Observe SSH Traffic</h3>

- Filter for SSH in Wireshark
- In Windows-VM Powershell into Ubuntu-VM
- Open Powershell
- ssh labuser@10.0.0.5 (ssh "username"@"private ip address")
- yes
- Password: VirtualMachine!
- Input Linux commands (pwd, uname, etc) and observe Wireshark SSH traffic
- exit

<h3>Observe DHCP Traffic</h3>

- Filter for DHCP
- Command Line ipconfig /renew

![image](https://github.com/JordanDanielWest/Network-Security-Groups-and-Inspecting-Network-Protocols/assets/96628562/75c4b8a2-dbe9-43ce-a4db-7644e0866694)

<h3>Observe DNS Traffic</h3>

- Filter by DNS
- Command Line nslookup www.google.com
- Observe traffic in Wireshark

<h3>Observe RDP Traffic</h3>

- Filter "tcp.port == 3389"
- Observe
- Done

<p>

</p>
<br />
