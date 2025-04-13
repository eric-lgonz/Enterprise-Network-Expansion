# Enterprise-Network-Expansion-and-VLAN-Implementation

In this project, I will demonstrate how to:

- Integrate a new switch block into an existing enterprise network using Cisco Packet Tracer, simulating
real-world brownfield network expansion
- Configure VLANs, trunks, Layer 3 routing, SVIs, EtherChannel, and first-hop redundancy protocols to support
resilient network growth
- Apply the access-distribution-core design model to optimize performance, scalability, and manageability in a
multi-layer enterprise environment

This project will be split into 6 parts, with each section focusing on a different phase of the enterprise network upgrade to keep things organized and easy to follow.

<h2>Technologies Used</h2>

- <a href="https://www.netacad.com/cisco-packet-tracer"> Cisco Packet Tracer<a/> (version 8.2.2)

<h2>What is Cisco Packet Tracer?</h2>

<a href="https://www.netacad.com/cisco-packet-tracer"> Cisco Packet Tracer<a/> is a comprehensive, widely used, and free network simulation software tool. It enables users to design, configure, and troubleshoot network topologies without the need for physical hardware. Cisco packet tracer offers realistic simulation and visualization for modern computer networks, making it ideal for simulating both greenfield and brownfield computer network environments. Feel free to check out their <a href="https://www.netacad.com/cisco-packet-tracer"> website<a/> for more information about Cisco Packet Tracer and its capabilities.

<h1>Part 1: Basic Ethernet and IP Networking</h1>

In this section, we will be starting off with the existing network topology below and will be adding the two LANs highlighted in blue.

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%201.png">

Let's start by setting up the devices, configuring their cabling and IP addressing. Then we can make sure the connections work by pinging the devices.

<h2>Device Setup</h2>

Some of the devices need their power supply to be set up before connecting them, such as the multilayer switches and the IP phone. We can connect each multilayer switch to power by clicking on the device, and then dragging the AC power adapter to them:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%202.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%203.png">

We can do the same for the IP phone:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%204.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%205.png">

<h2>Cabling</h2>

Now let's connect all the devices together with cables, except for the laptops, those will have a wireless connection. I will be using copper straight-through cables for connections between different kinds of devices (pc to switch), and copper cross-over cables for similar devices (switch to switch). To demonstrate how to connect the cables, here's how to set up the connection between PC0 and Switch0:

First click the connections icon on the bottom (the lightning bolt), and select on the type of cable you want to use:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%206.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%207.png">

Then bring the cable to your starting device, choose the port to connect it on, and then do the same for the device with the other end of the cable:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%208.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%209.png">

Afterwords, the connection will look like this:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2010.png">

Now I'll configuring the rest of the connections according to this table:

<div align ="center">

From Device | From Port | Cable Type | To Device | To Port
|:---:|:-------------:|:-----------------------:|:-------:|:-----:|
| **PCs** |
| PC0 | Fast Ethernet | Copper Straight-Through | Switch0 | Fa0/5 |
| PC1 | Fast Ethernet | Copper Straight-Through | IP Phone0 | PC |
| PC2 | Fast Ethernet | Copper Straight-Through | Switch1 | Fa0/6 |
| PC3 | Fast Ethernet | Copper Straight-Through | Switch3 | Fa0/3 |
| PC4 | Fast Ethernet | Copper Straight-Through | Switch2 | Fa0/5 |
| PC5 | Fast Ethernet | Copper Straight-Through | Switch4 | Fa0/5 |
| PC6 | Fast Ethernet | Copper Straight-Through | Switch5 | Fa0/5 |
| PC7 | Fast Ethernet | Copper Straight-Through | Switch5 | Fa0/6 |
| PC8 | Fast Ethernet | Copper Straight-Through | Switch7 | Fa0/6 |
| PC9 | Fast Ethernet | Copper Straight-Through | Switch6 | Fa0/5 |
| **IP Phone and Access Points** |
| IP Phone0 | Switch | Copper Straight-Through | Switch1 | Fa0/5 |
| Access Point0 | Port0 | Copper Straight-Through | Switch3 | Fa0/5 |
| Access Point1 | Port0 | Copper Straight-Through | Switch7 | Fa0/5 |
| **Multilayer Switch to Access Switch** |
| MLS0 | G1/0/1 | Copper Cross-Over | Switch0 | G0/1 |
| MLS0 | G1/0/2 | Copper Cross-Over | Switch2 | G0/1 |
| MLS1 | G1/0/1 | Copper Cross-Over | Switch4 | G0/1 |
| MLS1 | G1/0/2 | Copper Cross-Over | Switch6 | G0/1 |
| **Access Switch to Access Switch** |
| Switch0 | Fa0/1 | Copper Cross-Over | Switch1 | Fa0/1 |
| Switch0 | Fa0/2 | Copper Cross-Over | Switch1 | Fa0/2 |
| Switch2 | Fa0/1 | Copper Cross-Over | Switch3 | Fa0/1 |
| Switch2 | Fa0/2 | Copper Cross-Over | Switch3 | Fa0/2 |
| Switch4 | Fa0/1 | Copper Cross-Over | Switch5 | Fa0/1 |
| Switch4 | Fa0/2 | Copper Cross-Over | Switch5 | Fa0/2 |
| Switch6 | Fa0/1 | Copper Cross-Over | Switch7 | Fa0/1 |
| Switch6 | Fa0/2 | Copper Cross-Over | Switch7 | Fa0/2 |

</div>

After all of the cabling, this is what the topology looks like:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2011.png">

<h2>IP Addressing</h2>

For the IP addressing, we can manually configure each device. Normally, this would be automated using DHCP, which I will demonstrate in a later part of this project for the IP Phone. But for now, this is how to configure the default gateway and DNS server for an end device:

First click on the device, then go to the config tab. From there, click on settings, which is where you can manually configure the IP address settings:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2012.png">

Now I'll configure the rest of the IPv4 address settings according to this table:

<div align ="center">

Device | IPv4 Address | IPv4 Network | Default Gateway | DNS Server
|:---:|:-------------:|:-----------------------:|:-------:|:-----:|
| **Left-side of the topology** |
| PC0 | 10.10.1.100/24 | 10.10.1.0/24 | 10.10.1.1 | 10.2.1.10 |
| PC1 | 10.10.1.101/24 | 10.10.1.0/24 | 10.10.1.1 | 10.2.1.10 |
| PC2 | 10.20.1.100/24 | 10.20.1.0/24 | 10.20.1.1 | 10.2.1.10 |
| PC3 | 10.20.1.101/24 | 10.20.1.0/24 | 10.20.1.1 | 10.2.1.10 |
| PC4 | 10.20.1.102/24 | 10.20.1.0/24 | 10.20.1.1 | 10.2.1.10 |
| **Right-side of the topology** |
| PC5 | 10.30.2.100/24 | 10.30.2.0/24 | 10.30.2.1 | 10.2.1.10 |
| PC6 | 10.30.2.101/24 | 10.30.2.0/24 | 10.30.2.1 | 10.2.1.10 |
| PC7 | 10.40.2.100/24 | 10.40.2.0/24 | 10.40.2.1 | 10.2.1.10 |
| PC8 | 10.30.2.102/24 | 10.30.2.0/24 | 10.30.2.1 | 10.2.1.10 |
| PC9 | 10.40.2.102/24 | 10.40.2.0/24 | 10.40.2.1 | 10.2.1.10 |
| **IP Phone and Laptops** |
| IP Phone0 | 10.10.1.x/24 DHCP | N/A | N/A | N/A |
| Laptop0 | 10.121.0.100 | 10.121.0.0/24 | 10.121.0.1 | 10.2.1.10 |
| Laptop1 | 10.122.0.100 | 10.122.0.0/24 | 10.122.0.1 | 10.2.1.10 |

</div>

Now that the IP addressing is complete, we need to configure Service Set Identifiers (SSIDs) on the access points so that the wireless laptops can connect. Let'c set Access Point0's display name and SSID to "Guest-0" and Access Point1's display name and SSID to "Guest-1":

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2013.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2014.png">

For the laptops, we are going to connect them to the network wirelessly. To do that, they need to have a wireless network interface card (NIC) instead of their wired NIC. We can do this by powering off each laptop, removing the wired NIC, installing the wireless NIC, and then powering back on the laptop:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2015.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2016.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2017.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2018.png">

Once that is done for both laptops, we can set the corresponding SSID in config tab under the wireless interface. This will allow the laptops to "associate" with their respective access points:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2019.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2020.png">

Lastly, we can now configure all of the IPv4 address settings for the laptops, using the same method we did for the other end devices:

<div align ="center">

Device | IPv4 Address | IPv4 Network | Default Gateway | DNS Server
|:---:|:-------------:|:-----------------------:|:-------:|:-----:|
| Laptop0 | 10.121.0.100/24 | 10.121.0.0/24 | 10.121.0.1 | 10.2.1.10 |
| Laptop1 | 10.122.0.100/24 | 10.122.0.0/24 | 10.122.0.1 | 10.2.1.10 |

</div>

<h2>Verifying Connections</h2>

We can make sure everything was configured properly by testing if devices in the same network can ping each other.

Let's do a ping from PC2 to PC3, which should work because they are on the same network. We can do this by clicking on PC2, navigating to the Desktop tab, and clicking on Command Prompt. Then we can enter <code>ping 10.20.1.101</code>:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2021.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2022.png">

Now let's do a ping between devices on different networks. For example, PC0 should not be able to ping PC3:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2023.png">

Now that we have verified that the devices are configured properly, that wraps up Part 1 of this project. Let's take a look at our new network topology:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2024.png">

<h1>Part 2: VLANs and Trunks</h1>


