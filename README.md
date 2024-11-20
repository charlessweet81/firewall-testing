<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Configuring Firewalls via Network Security Groups (NSGs)</h1>
Testing Network Security Groups (NSGs) and firewalls is essential for verifying access controls, identifying vulnerabilities, and ensuring compliance with regulatory standards. This process helps optimize network performance, enhances incident response readiness, and confirms that changes do not inadvertently disrupt legitimate traffic or introduce new security risks. <br/><br/>

In this tutorial, we will test network security group traffic with a firewall. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop (Microsoft Remote Desktop)
- Various Command-Line Tools (via Powershell)
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1: Create an Azure Virtual Machine Windows 10, 4 vCPUs
- Step 2: Log into the VM with Remote Desktop
- Step 2: Open Wireshark and start packet capture
- Step 3: Within Wireshark, filter for ICMP traffic only
- Step 4: Setup a constant ping from the first device (Windows) to the second device (Linux) via Powershell
- Step 5: Configure firewall of second device's network security group settings' inbound rules


<h2>Actions and Observations</h2>


<p>
<h3>Step 1: Create an Azure Virtual Machine Windows 10, 4 vCPUs </h3> 
</p>
<p>
<img src="https://i.imgur.com/7E93uXW.png" height="80%" width="80%" alt="Log into Remote Desktop"/>
</p>

<p>
<h3> Step 2: Log into the VM with Remote Desktop </h3>
</p>

<p>
<img src="https://i.imgur.com/dlnWxf3.png" height="80%" width="80%" alt="Filter for ICMP"/>
</p>

<br />

<p>
<h3>Step 3: Retrieve the private IP address of VM.</h3> 

</p>

<p>
<img src="https://i.imgur.com/5IRiRtj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


<p>
<img src="https://i.imgur.com/zDWAbPa.png" height="80%" width="80%" alt="Ping the Linux virtual machine using Powershell"/>
</p>
<p>
Step 4: Ping the second VM from Powershell using 'ping IP -t' to create a nonstop ping. 

</p>

<p>
<img src="https://i.imgur.com/V6M9ruH.png" height="80%" width="80%" alt="Ping the Linux virtual machine using Powershell"/>
</p>
<p>
Step 5: Go to the second VM (in this case the Linux server) in Azure, and update the network security group settings' inbound rules. <br/> <br/> 

Add a new rule with the following: Source is 'any', Source Port Ranges is '*', Destination is 'any', Service is 'custom' and Destination Port Ranges is '*'. The protocol is 'ICMPv4', the Action is 'Deny' and the Priority is 290 (so that it gets executed before any other rule). Click continue. 
</p>

<p>
<img src="https://i.imgur.com/nSAIQLH.png" height="80%" width="80%" alt="Powershell showing timed out status"/>
</p>

<p>Once the changes have made their way through the system, the firewall comes into effect. We can see the firewall is working because Powershell shows a timed out status. </p>

<p>
<img src="https://i.imgur.com/NBNyWUe.png" height="80%" width="80%" alt="Wireshark showing only requests"/>
</p>

<p>Another sign the firewall is working is through Wireshark not showing replies to the requests, meaning no two-way communication between devices. </p>

<br />
