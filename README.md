# Enterprise-Network-Expansion

In this project, I demonstrate how to:

- Integrate a new switch block into an existing enterprise network using Cisco Packet Tracer, simulating
real-world brownfield network expansion
- Configure VLANs, trunks, Layer 3 routing, SVIs, EtherChannel, and first-hop redundancy protocols to support
resilient network growth
- Apply the access-distribution-core design model to optimize performance, scalability, and manageability in a
multi-layer enterprise environment

This project will be split into 7 parts, with a new part being uploaded each week until 5/25/25. Each section will focus on a different phase of the enterprise network upgrade to keep things organized and easy to follow.

Credit: Rick Graziani, professor at University of California - Santa Cruz and Curriculum Engineering Team Member at Cisco, created the idea for this lab that uses Packet Tracer. My project shown here is a write up that demostrates my knowledge of the lab, with my own adjustments in its implementation.

<h2>Technologies Used</h2>

- <a href="https://www.netacad.com/cisco-packet-tracer"> Cisco Packet Tracer<a/> (version 8.2.2)

<h2>What is Cisco Packet Tracer?</h2>

<a href="https://www.netacad.com/cisco-packet-tracer"> Cisco Packet Tracer<a/> is a comprehensive, widely used, and free network simulation software tool. It enables users to design, configure, and troubleshoot network topologies without the need for physical hardware. Cisco Packet Tracer offers realistic simulation and visualization for modern computer networks, making it ideal for simulating both greenfield and brownfield computer network environments. Feel free to check out their <a href="https://www.netacad.com/cisco-packet-tracer"> website<a/> for more information about Cisco Packet Tracer and its capabilities.

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

Afterwards, the connection will look like this:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%201%20-%2010.png">

Now I'll configure the rest of the connections according to this table:

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

Now that the IP addressing is complete, we need to configure Service Set Identifiers (SSIDs) on the access points so that the wireless laptops can connect. Let's set Access Point0's display name and SSID to "Guest-0" and Access Point1's display name and SSID to "Guest-1":

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

For part 2, we will be focusing on configuring VLANs and trunks in our new switch block. To do this, we will be configuring both multi-layer switches and the access switches.

<h2>Basic CLI Configuration for the Switches</h2>

First, let's change the display names on the switches to make the topology more clear. Click on the display name for each switch and set it to match the screenshot below:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%202%20-%201.png">
Note: I disabled the device model names by going to <code>Options -> Preferences -> Show Device Model Labels</code><br><br>

Now, let's use the command line interface (CLI) to set up each switch with security and access settings. This is essential to begin the process of setting up VLANs. On each individual switch (both distribution and access switches) we can use the commands shown below to set up their settings. Be sure to change the hostname field to match the display name of the switch:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%202%20-%202.png">
Note: The passwords I chose are very insecure, as I chose them for simplicity. They should not be used outside of a contained lab setting.

Let's dive into what each of those commands does:
- <code>enable</code> - This enables privileged exec mode, giving more control over the switch.
- <code>conf t</code> - Short for configure terminal, which allows you to configure the switch settings.
- <code>hostname Distribution-1</code> - This changes the switches hostname to Distribution-1.
- <code>no ip domain-lookup</code> - Disables DNS lookups so that mistyped commands aren't read as hostnames.
- <code>enable secret class</code> - Sets the password "class" for privileged exec mode.
- <code>username admin secret sshadmin</code> - Creates a user account with credentials admin, sshadmin.
- <code>ip domain-name SSh-KEY.com</code> - This allows us to generate SSH keys.
- <code>crypto key generate rsa general-keys modulus 1024</code> - Creates a 1024-bit RSA key pair.
- <code>line con 0</code> - This puts us into configuration mode.
- <code>exec-timeout 0 0</code> - Disables the idle timeout, allowing the session to be open indefinitely.
- <code>logging synchronous</code> - This makes it so that system messages won't interrupt console command input.
- <code>password cisco</code> - Sets the password for console access to "cisco".
- <code>login</code> - Enables password authentication to access the console.
- <code>line vty 0 15</code> - Opens configuration mode for virtual terminal (VTY) lines. This is used for remote access.
- <code>login local</code> - Sets up the VTY lines to use the local username and password for authentication.
- <code>transport input ssh</code> - Sets remote access to only use SSH.
- <code>copy running-config startup-config</code> - This saves the current configuration to persist after a reboot.

After completing this process for all of the switches, we can start to add the VLANs.

<h2>Configuring the VLANs</h2>

By default, all ports are on the same VLAN, VLAN 1. This is the default VLAN, as you can see below on the access switch:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%202%20-%203.png">

Each department in our network will get their own VLAN, and we will set these up for each switch.

<div align ="center">

VLAN ID | Name | 10.vlan.0.0/16
|:---:|:-------------:|:------:|
| 1 | Default | N/A |
| 10 | Engineering | 10.10.1.0/24 |
| 20 | QA - Engineering | 10.20.1.0/24 |
| 30 | Sales | 10.30.2.0/24 |
| 40 | Marketing | 10.40.2.0/24 |
| 101 | Voice-1 | 10.101.0.0/16 |
| 102 | Voice-2 | 10.102.0.0/16 |
| 121 | Guest-1 | 10.121.0.0/16 |
| 122 | Guest-2 | 10.122.0.0/16 |
| 180 | Management | 10.180.0.0/16 |
| 254 | Native | 10.254.0.0/16 |
| 255 | Parking-Lot | 10.255.0.0/16 |

</div>

We can enter the following commands on each switch to set up these VLANs:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%202%20-%204.png">
Don't forget to run <code>copy run start</code> to save the config!<br><br>
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%202%20-%205.png">

Let's take a look at what these commands do:
- <code>vlan &lt;vlan ID&gt;</code> - This puts us into the configuration mode for a specific VLAN ID. Note that even without this command, a VLAN will still be created if an interface is configured to be a member of that VLAN ID.
- <code>name &lt;name&gt;</code> - This names the VLAN.

<h2>Setting Up the Access Ports</h2>

So now we have made the VLANs, but the ports for each switch are all still on the native VLAN. We want to configure access ports to particular VLANs, which we then use to connect the switch to an end device on that VLAN.

We can do this with the following commands for each switch (make sure you are in "configure terminal" mode:

<h4>Access-1-1:</h4>
<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 10</code><br><code>exit</code>

<h4>Access-1-2:</h4>
<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 20</code><br><code>exit</code>

<h4>Access-1-3:</h4>
<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 10</code><br><code>exit</code>

<code>interface FastEthernet0/6</code><br><code>switchport mode access</code><br><code>switchport access vlan 20</code><br><code>exit</code>

Since this switch is connected to the phone, we will receive an error that VLAN 10 has not been configured for voice traffic. We can fix this by using the following commands:

<code>interface FastEthernet0/5</code><br><code>switchport voice vlan 101</code><br><code>mls qos trust cos</code><br><code>exit</code>

<h4>Access-1-4:</h4>
<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 121</code><br><code>exit</code>

<code>interface FastEthernet0/6</code><br><code>switchport mode access</code><br><code>switchport access vlan 20</code><br><code>exit</code>

<h4>Access-2-1:</h4>
<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 30</code><br><code>exit</code>

<h4>Access-2-2:</h4>
<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 40</code><br><code>exit</code>

<h4>Access-2-3:</h4>
<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 30</code><br><code>exit</code>

<code>interface FastEthernet0/6</code><br><code>switchport mode access</code><br><code>switchport access vlan 40</code><br><code>exit</code>

<h4>Access-2-4:</h4>
<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 122</code><br><code>exit</code>

<code>interface FastEthernet0/6</code><br><code>switchport mode access</code><br><code>switchport access vlan 30</code><br><code>exit</code>

Here's what each command is doing:
- <code>interface FastEthernet0/5</code> - Enters configuration mode for the FastEthernet0/5 interface.
- <code>switchport mode access</code> - This configures the port as an access port, which means that it will only carry the traffic for a single VLAN.
- <code>switchport access vlan 10</code> - This assigns the port to VLAN 10.

As you can see, the Fa0/5 port was assigned to VLAN 10 on Access-1-1.

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%202%20-%206.png">

<h2>Establishing Trunks</h2>

We use trunk links to carry multiple VLANs on a single interface, using tags to identify the VLANs. By using trunks, we greatly reduce the amount of physical interfaces we need in order to distribute VLANs across the network.

We can do this with the following commands for each switch (make sure you are in "configure terminal" mode:

Note: You may initially get errors due to native VLAN mismatches, but this will be resolved once all of the trunk links are configured.

<h4>Distribution-1:</h4>
<code>interface range GigabitEthernet1/0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<h4>Distribution-2:</h4>
<code>interface range GigabitEthernet1/0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<h4>Access-1-1:</h4>
<code>interface GigabitEthernet0/1</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<h4>Access-1-2:</h4>
<code>interface GigabitEthernet0/1</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<h4>Access-1-3:</h4>
<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<h4>Access-1-4:</h4>
<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<h4>Access-2-1:</h4>
<code>interface GigabitEthernet0/1</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<h4>Access-2-2:</h4>
<code>interface GigabitEthernet0/1</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<h4>Access-2-3:</h4>
<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<h4>Access-2-4:</h4>
<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code><br><br>

Let's break down what these commands do:
- <code>interface range GigabitEthernet1/0/1-2</code> - This enters the configuration mode for the interfaces in this range.
- <code>shutdown</code> - This disables the chosen interfaces, which is good practice when making significant changes.
- <code>switchport mode trunk</code> - This configures the interface to be a trunk port.
- <code>switchport trunk native vlan 254</code> - This sets VLAN 254 to be the native VLAN.
- <code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code> - This configures the trunk link to carry only the specified VLANs.
- <code>switchport nonegotiate</code> - This disables Dynamic Trunking Protocol (DTP), which means that both ends of the link have to be configured.
- <code>no shutdown</code> - This re-enables the disabled interfaces.
- <code>exit</code> - This takes us out of interface configuration mode and puts us back into global configuration mode.

<h2>Verifying Pings</h2>

Let's make sure that the network is still connected properly by sending pings between devices.

Ping from PC0 to PC1:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%202%20-%207.png">

Ping from PC2 to PC3:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%202%20-%208.png">

Now that we have verified that the connections work properly, we can review our network topology and move on to Part 3!

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%202%20-%209.png">

<h1>Part 3: SVIs</h1>

In this part of the project, we will now be configuring SVIs. An Switched Virtual Interface, or SVI, allows for remote management on switches. It does this by assigning an IP address to a VLAN on the switch, which allows us to now access that virtual interface remotely, and therefore remotely manage the switch.

We will be configuring SVIs for both of the layer 3 distribution switches.

<h2>Clarifying the Topology</h2>

Before we get to configuring the SVIs, let's first add more description to our links so that we can easily tell the difference between each kind of link:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%203%20-%201.png">

<h2>Configuring the SVIs</h2>

Now let's begin the process of configuring the SVIs. On the Distribution-1 switch, login and type <code>configure terminal</code>. Then input the following commands and verify that both SVIs are up:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%203%20-%202.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%203%20-%203.png">

Let's also enable ip routing on this switch:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%203%20-%204.png">

Now that we have configured the switch to route between the VLANs, devices on VLANs 10 and 20 should be able to reach each other. Let's test this with a ping:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%203%20-%205.png">

The ping succeeded (after the first ping timed out due to an ARP Request), meaning that the devices are able to communicate with each other.

Now repeat all of the same configuration steps on the Distribution-2 switch, except changing the ip addresses for the corresponding VLANs:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%203%20-%206.png">

We can do a similar ping test as well:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion-and-VLAN-Implementation/blob/main/assets/Part%203%20-%207.png">

And that's it! We configured SVIs for both layer 3 switches and now they can support inter-VLAN routing. During the next part of this project, we will be adding a link between the distribution switches to allow them to communicate with each other.

<h1>Part 4: Routed Ports and Static Routing (Coming 5/8/25)</h1>

In this part of the lab, we will be connecting the two distribution switches, and configure routed ports and static routing on them.

<h2>Connecting the Switches</h2>

Similar to earlier in the project, we can connect the switches physically using a copper crossover cable. Let's connect them on the G1/0/23 interface:

_insert image_

<h2>Methodology</h2>

Since we will be configuring the link between the switches as a separate Layer 3 network, we will need to use a routed port. This physical interface will be set up to work like a port on a router. This means that no VLANs are associated with it, and that it will also need an IP address.

Why not just use a trunk link?

This is a good question, as we could connect the VLANs together by using a layer 2 trunk link between the switches. However, choosing this option would mean that there would not be as much redundancy and scalability. For example, we would have to use Spanning Tree Protocol, blocking redundant paths while also limiting the total number of layer 2 switches we can have in a row. On the other hand, using a layer 3 link would reduce the risk of loops while also providing scalability as the network can grow larger.

So why would we ever use layer 2 switches if it would always be advantageous to use a layer 3 switch, which has more capabilities?

Money and ease of use. Layer 3 switches have more functionality, so naturally they cost more. Also, for a simple network, you may not need the additional functionality that a layer 3 switch provides, making layer 2 switches a more logical choice.

<h2>Configuring Routed Ports</h2>

Now let's get into how to configure the routed ports. Most layer 3 ports are configured as layer 2 by default. We will need to change them to work as layer 3 ports, which can be done with the <code>no switchport</code> command. The rest of the commands used to configure the interface are similar to how we configured the VLANs.

This is the process for configuring both of the distribution switches.

_insert image_
_insert image_

We can double check to make sure that switchport is disabled on the switches, as shown below:

_insert image_
_insert image_

With this, we have made it possible for Distribution-1 to communicate with Distribution-2. However, we have not defined routes to allow each of these switches to communicate with the other switch's VLANs. We will do this through static routing.

<h2>Static Routing for Remote Networks</h2>

An alternative to static routing is using a dynamic routing protocol. This is useful for when the network grows larger and it is hard to keep track of everything manually. We will configure dynamic routing later, and for now we will configure the routes statically to verify connectivity:

_insert image_
_insert image_

Now let's see if PC2 can communicate with PC7 (VLAN 20 to VLAN 40):

_insert image_
_insert image_

And it worked! Now our switches can not only provide routing between the VLANs directly connected to it, but they can also provide routing to reach the other VLANs via the new link.

Lastly, let's add labels to the topology to indicate the SVIs and the new link:

_insert image_

Great, and that's all for this section! In the next part of the project, we will take a look at EtherChannel and Spanning Tree Protocol.

<h1>Part 5: EtherChannel and Examining STP (Coming 5/18/25)</h1>

<h1>Part 6: Connecting to the Core (Coming 5/25/25)</h1>

<h1>Part 7: DHCP (Coming 6/1/25)</h1>


