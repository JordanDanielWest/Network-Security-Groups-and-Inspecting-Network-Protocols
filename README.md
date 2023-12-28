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

- Log into Ubuntu-VM via Remote Desktop
- 


<p>

</p>
<br />
