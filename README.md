# Enterprise-Network-Expansion

In this project, I demonstrate how to:

- Integrate a new switch block into an existing enterprise network using Cisco Packet Tracer, simulating real-world brownfield network expansion
- Configure VLANs, trunks, Layer 3 routing, SVIs, EtherChannel, and first-hop redundancy protocols to support resilient network growth
- Apply the access-distribution-core design model to optimize performance, scalability, and manageability in a multi-layer enterprise environment

This project will be split into 8 parts, with a new part being uploaded each week until 5/18/25. Each section will focus on a different phase of the enterprise network upgrade to keep things organized and easy to follow.

Credit: Rick Graziani, professor at University of California - Santa Cruz and Curriculum Engineering Team Member at Cisco, created the idea for this lab that uses Packet Tracer. My project shown here is a write up that demostrates my knowledge of the lab, with my own adjustments in its implementation.

<h2>Technologies Used</h2>

- <a href="https://www.netacad.com/cisco-packet-tracer"> Cisco Packet Tracer<a/> (version 8.2.2)

<h2>What is Cisco Packet Tracer?</h2>

<a href="https://www.netacad.com/cisco-packet-tracer"> Cisco Packet Tracer<a/> is a comprehensive, widely used, and free network simulation software tool. It enables users to design, configure, and troubleshoot network topologies without the need for physical hardware. Cisco Packet Tracer offers realistic simulation and visualization for modern computer networks, making it ideal for simulating both greenfield and brownfield computer network environments. Feel free to check out their <a href="https://www.netacad.com/cisco-packet-tracer"> website<a/> for more information about Cisco Packet Tracer and its capabilities.

<h1>Part 1: Basic Ethernet and IP Networking</h1>

In this section, we will be starting off with the existing network topology below and will be adding the two LANs highlighted in blue.

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%201.png">

Let's start by setting up the devices, configuring their cabling and IP addressing. Then we can make sure the connections work by pinging the devices.

<h2>Device Setup</h2>

Some of the devices need their power supply to be set up before connecting them, such as the multilayer switches and the IP phone. We can connect each multilayer switch to power by clicking on the device, and then dragging the AC power adapter to them:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%202.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%203.png">

We can do the same for the IP phone:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%204.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%205.png">

<h2>Cabling</h2>

Now let's connect all the devices together with cables, except for the laptops, those will have a wireless connection. I will be using copper straight-through cables for connections between different kinds of devices (pc to switch), and copper cross-over cables for similar devices (switch to switch). To demonstrate how to connect the cables, here's how to set up the connection between PC0 and Switch0:

First click the connections icon on the bottom (the lightning bolt), and select on the type of cable you want to use:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%206.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%207.png">

Then bring the cable to your starting device, choose the port to connect it on, and then do the same for the device with the other end of the cable:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%208.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%209.png">

Afterwards, the connection will look like this:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2010.png">

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

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2011.png">

<h2>IP Addressing</h2>

For the IP addressing, we can manually configure each device. Normally, this would be automated using DHCP, which I will demonstrate in a later part of this project for the IP Phone. But for now, this is how to configure the default gateway and DNS server for an end device:

First click on the device, then go to the config tab. From there, click on settings, which is where you can manually configure the IP address settings:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2012.png">

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

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2013.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2014.png">

For the laptops, we are going to connect them to the network wirelessly. To do that, they need to have a wireless network interface card (NIC) instead of their wired NIC. We can do this by powering off each laptop, removing the wired NIC, installing the wireless NIC, and then powering back on the laptop:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2015.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2016.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2017.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2018.png">

Once that is done for both laptops, we can set the corresponding SSID in config tab under the wireless interface. This will allow the laptops to "associate" with their respective access points:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2019.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2020.png">

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

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2021.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2022.png">

Now let's do a ping between devices on different networks. For example, PC0 should not be able to ping PC3:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2023.png">

Now that we have verified that the devices are configured properly, that wraps up Part 1 of this project. Let's take a look at our new network topology:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%201%20-%2024.png">

<h1>Part 2: VLANs and Trunks</h1>

For part 2, we will be focusing on configuring VLANs and trunks in our new switch block. To do this, we will be configuring both multi-layer switches and the access switches.

<h2>Basic CLI Configuration for the Switches</h2>

First, let's change the display names on the switches to make the topology more clear. Click on the display name for each switch and set it to match the screenshot below:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%202%20-%201.png">
Note: I disabled the device model names by going to <code>Options -> Preferences -> Show Device Model Labels</code><br><br>

Now, let's use the command line interface (CLI) to set up each switch with security and access settings. This is essential to begin the process of setting up VLANs. On each individual switch (both distribution and access switches) we can use the commands shown below to set up their settings. Be sure to change the hostname field to match the display name of the switch:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%202%20-%202.png">
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

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%202%20-%203.png">

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

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%202%20-%204.png">
Don't forget to run <code>copy run start</code> to save the config!<br><br>
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%202%20-%205.png">

Let's take a look at what these commands do:
- <code>vlan &lt;vlan ID&gt;</code> - This puts us into the configuration mode for a specific VLAN ID. Note that even without this command, a VLAN will still be created if an interface is configured to be a member of that VLAN ID.
- <code>name &lt;name&gt;</code> - This names the VLAN.

<h2>Setting Up the Access Ports</h2>

So now we have made the VLANs, but the ports for each switch are all still on the native VLAN. We want to configure access ports to particular VLANs, which we then use to connect the switch to an end device on that VLAN.

We can do this with the following commands for each switch (make sure you are in "configure terminal" mode:

**Access-1-1:**

<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 10</code><br><code>exit</code>

**Access-1-2:**

<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 20</code><br><code>exit</code>

**Access-1-3:**

<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 10</code><br><code>exit</code>

<code>interface FastEthernet0/6</code><br><code>switchport mode access</code><br><code>switchport access vlan 20</code><br><code>exit</code>

Since this switch is connected to the phone, we will receive an error that VLAN 10 has not been configured for voice traffic. We can fix this by using the following commands:

<code>interface FastEthernet0/5</code><br><code>switchport voice vlan 101</code><br><code>mls qos trust cos</code><br><code>exit</code>

**Access-1-4:**

<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 121</code><br><code>exit</code>

<code>interface FastEthernet0/6</code><br><code>switchport mode access</code><br><code>switchport access vlan 20</code><br><code>exit</code>

**Access-2-1:**

<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 30</code><br><code>exit</code>

**Access-2-2:**

<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 40</code><br><code>exit</code>

**Access-2-3:**

<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 30</code><br><code>exit</code>

<code>interface FastEthernet0/6</code><br><code>switchport mode access</code><br><code>switchport access vlan 40</code><br><code>exit</code>

**Access-2-4:**

<code>interface FastEthernet0/5</code><br><code>switchport mode access</code><br><code>switchport access vlan 122</code><br><code>exit</code>

<code>interface FastEthernet0/6</code><br><code>switchport mode access</code><br><code>switchport access vlan 30</code><br><code>exit</code>

Here's what each command is doing:
- <code>interface FastEthernet0/5</code> - Enters configuration mode for the FastEthernet0/5 interface.
- <code>switchport mode access</code> - This configures the port as an access port, which means that it will only carry the traffic for a single VLAN.
- <code>switchport access vlan 10</code> - This assigns the port to VLAN 10.

As you can see, the Fa0/5 port was assigned to VLAN 10 on Access-1-1.

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%202%20-%206.png">

<h2>Establishing Trunks</h2>

We use trunk links to carry multiple VLANs on a single interface, using tags to identify the VLANs. By using trunks, we greatly reduce the amount of physical interfaces we need in order to distribute VLANs across the network.

We can do this with the following commands for each switch (make sure you are in "configure terminal" mode:

Note: You may initially get errors due to native VLAN mismatches, but this will be resolved once all of the trunk links are configured.

**Distribution-1:**

<code>interface range GigabitEthernet1/0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

**Distribution-2:**

<code>interface range GigabitEthernet1/0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

**Access-1-1:**

<code>interface GigabitEthernet0/1</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

**Access-1-2:**

<code>interface GigabitEthernet0/1</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

**Access-1-3:**

<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

**Access-1-4:**

<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

**Access-2-1:**

<code>interface GigabitEthernet0/1</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

**Access-2-2:**

<code>interface GigabitEthernet0/1</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

**Access-2-3:**

<code>interface range FastEthernet0/1-2</code><br><code>shutdown</code><br><code>switchport mode trunk</code><br><code>switchport native vlan 254</code><br><code>switchport trunk allowed vlan 1,10,20,30,40,101-102,121-122,180,254</code><br><code>switchport nonegotiate</code><br><code>no shutdown</code><br><code>exit</code>

**Access-2-4:**

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

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%202%20-%207.png">

Ping from PC2 to PC3:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%202%20-%208.png">

Now that we have verified that the connections work properly, we can review our network topology and move on to Part 3!

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%202%20-%209.png">

<h1>Part 3: SVIs</h1>

In this part of the project, we will now be configuring SVIs. An Switched Virtual Interface, or SVI, allows for remote management on switches. It does this by assigning an IP address to a VLAN on the switch, which allows us to now access that virtual interface remotely, and therefore remotely manage the switch.

We will be configuring SVIs for both of the layer 3 distribution switches.

<h2>Clarifying the Topology</h2>

Before we get to configuring the SVIs, let's first add more description to our links so that we can easily tell the difference between each kind of link:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%203%20-%201.png">

<h2>Configuring the SVIs</h2>

Now let's begin the process of configuring the SVIs. On the Distribution-1 switch, login and type <code>configure terminal</code>. Then input the following commands and verify that both SVIs are up:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%203%20-%202.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%203%20-%203.png">

Let's also enable ip routing on this switch:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%203%20-%204.png">

Now that we have configured the switch to route between the VLANs, devices on VLANs 10 and 20 should be able to reach each other. Let's test this with a ping:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%203%20-%205.png">

The ping succeeded (after the first ping timed out due to an ARP Request), meaning that the devices are able to communicate with each other.

Now repeat all of the same configuration steps on the Distribution-2 switch, except changing the ip addresses for the corresponding VLANs:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%203%20-%206.png">

We can do a similar ping test as well:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%203%20-%207.png">

And that's it! We configured SVIs for both layer 3 switches and now they can support inter-VLAN routing. During the next part of this project, we will be adding a link between the distribution switches to allow them to communicate with each other.

<h1>Part 4: Routed Ports and Static Routing</h1>

In this part of the lab, we will connect the two distribution switches, and configure routed ports and static routing on them.

<h2>Connecting the Switches</h2>

Similar to earlier in the project, we can connect the switches physically using a copper crossover cable. Let's connect them on the G1/0/23 interface:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%204%20-%201.png">

<h2>Methodology</h2>

Since we will be configuring the link between the switches as a separate Layer 3 network, we will need to use a routed port. This physical interface will be set up to work like a port on a router. This means that no VLANs are associated with it, and that it will also need an IP address.

Why not just use a trunk link?

This is a good question, as we could connect the VLANs together by using a layer 2 trunk link between the switches. However, choosing this option would mean that there would not be as much redundancy and scalability. For example, we would have to use Spanning Tree Protocol, blocking redundant paths while also limiting the total number of layer 2 switches we can have in a row. On the other hand, using a layer 3 link would reduce the risk of loops while also providing scalability as the network can grow larger.

So why would we ever use layer 2 switches if it would always be advantageous to use a layer 3 switch, which has more capabilities?

Cost and simplicity. Layer 3 switches have more functionality, so naturally they cost more. Also, for a simple network, you may not need the additional functionality that a layer 3 switch provides, making layer 2 switches a more logical choice.

<h2>Configuring Routed Ports</h2>

Now let's get into how to configure the routed ports. Most layer 3 ports are configured as layer 2 by default. We will need to change them to work as layer 3 ports, which can be done with the <code>no switchport</code> command. The rest of the commands used to configure the interface are similar to how we configured the VLANs.

This is the process for configuring both of the distribution switches.

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%204%20-%202.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%204%20-%203.png">

We can double-check to make sure that switchport is disabled on the switches, as shown below:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%204%20-%204.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%204%20-%205.png">

With this, we have made it possible for Distribution-1 to communicate with Distribution-2. However, we have not defined routes to allow each of these switches to communicate with the other switch's VLANs. We will do this through static routing.

<h2>Static Routing for Remote Networks</h2>

An alternative to static routing is using a dynamic routing protocol. This is useful for when the network grows larger and it is hard to keep track of everything manually. We will configure dynamic routing later, and for now we will configure the routes statically to verify connectivity:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%204%20-%206.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%204%20-%207.png">

Now let's see if PC2 can communicate with PC7 (VLAN 20 to VLAN 40):

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%204%20-%208.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%204%20-%209.png">

And it worked! Now our switches can not only provide routing between the VLANs directly connected to it, but they can also provide routing to reach the other VLANs via the new link.

Lastly, let's add labels to the topology to indicate the SVIs and the new link:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%204%20-%2010.png">

That wraps up this section! In the next part of the project, we will take a look at EtherChannel and how it interacts with the Spanning Tree Protocol.

<h1>Part 5: EtherChannel and Examining STP</h1>

In this part of the project, we will be configuring Link Aggregation, specifically EtherChannel. Link Aggregation is a protocol that allows for the bundling of several physical links to be combined into one logical link. This enhances redundancy and higher bandwidth, since the capacities of all links are combined. Cisco has their own version of Link Aggregation, called EtherChannel, which is what we will be using here. We will also look at how EtherChannel interacts with STP.

It is important to note that there are two primary protocols that handle Link Aggregation. There is Link Aggregation Control Protocol (LACP), which is an IEEE standard, and Port Aggregation Protocol (PAgP), which is a Cisco proprietary protocol that is similar to LACP. Both of these protocols dynamically manage the links and ensure that the links are properly configured. There is also Static Persistence, which involves configuring EtherChannel manually without using LACP or PAgP. While this is a simple approach, it can lead to many configuration problems, especially on a larger network.

<h2>Configuring Layer 2 EtherChannel</h2>

In our current configuration, Spanning Tree Protocol (STP) blocks one of the ports to prevent loops. This is represented by an amber light on the port. With EtherChannel, the bundled links will be treated as one link by STP, which means that all ports connecting switches will be in the forwarding state, and thus not have an amber light.

On all of the access switches, we can use the following commands to configure EtherChannel:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%205%20-%201.png">

Let's break down what these commands do:
- <code>port-channel load-balance src-dst-ip</code> - This sets up the load-balancing for the links on the EtherChannel. This is necessary because the switch needs a way to decide which port to use to forward a frame, so here we tell it to take the source and destination IP addresses into account.
- <code>interface range fa 0/1-2</code> - This puts us in configuration mode for this range of interfaces, allowing us to configure both Fa 0/1 and Fa 0/2 at the same time.
- <code>shutdown</code> - This shuts down the interfaces, which is essential because we don't want them to be active while we set up LACP.
- <code>channel-protocol lacp</code> - This sets up LACP and tells the switch that this is the protocol that we want to use.
- <code>channel-group 1 mode active</code> - This assigns the interfaces to channel-group 1 and allows the interface to negotiate LACP configuration with other switches.

It is important to keep in mind that before bringing each switch back online, it is important to have both connected switches be configured with the set of EtherChannel commands. Otherwise, we may run into inconsistencies and synchronization issues. With that being said, let's bring each pair of connected switches back online with the following commands:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%205%20-%202.png">

A few minutes after configuring all eight access switches, you will see all the switch lights turn green. This means that the configuration worked and all of the switch ports are in the forwarding state.

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%205%20-%203.png">

Lastly, there is one more step we need to take. We had previously configured particular VLANs to traverse the interfaces. This property is not inherited by the Port-channel1 interface, despite both of the physical interfaces being configured with them. We can remedy this by simply using the <code>switchport trunk allowed vlan</code> command:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%205%20-%204.png">

<h2>Verifying Layer 2 EtherChannel</h2>

We can verify that EtherChannel has been configured on the switch by using the <code>show etherchannel</code>, <code>show etherchannel summary</code>, <code>show etherchannel port-channel</code>, and <code>show etherchannel load-balance</code> commands:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%205%20-%205.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%205%20-%206.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%205%20-%207.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%205%20-%208.png">

<h2>Configuring Layer 3 EtherChannel</h2>

Now we will be going through a similar process for the layer 3 switches. To start, we need to add a second routed port between the distribution switches, otherwise there would be no links to aggregate.

To do this, let's first shut down both ports on the switches, as this is best practice. Then we can add another copper crossover cable between the switches on their 1/0/24 ports:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%205%20-%209.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%205%20-%2010.png">

Now we can use the following commands to configure the distribution switches:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%205%20-%2011.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%205%20-%2012.png">

We can now re-enable the interfaces by using the <code>no shutdown</code> command. In Packet Tracer, the lights may appear amber instead of green, but this is just a visual bug.

And that's all for this part of the project! In the next section, we will be connecting our switch block to the core network.

<h1>Part 6: Connecting to the Core</h1>

In this section of the project, we will be connecting our distribution switches to the core switches and give them valid IP addresses on the network. Then we will remove the static routing we previously configured and replace it with Open Shortest Path First (OSPF), a dynamic routing protocol.

<h2>Physical Connections</h2>

Let's make the following connections using copper crossover cable:
- Distribution-1's G1/0/10 to Core-3's G1/0/10 interface
- Distribution-1's G1/0/11 to Core-4's G1/0/10 interface
- Distribution-2's G1/0/10 to Core-3's G1/0/11 interface
- Distribution-2's G1/0/11 to Core-4's G1/0/11 interface

After making the connections, the topology should look like this:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%206%20-%201.png">

And you can check the interface status to ensure that they are connected:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%206%20-%202.png">

<h2>Configuring IPv4 Addressing</h2>

Now, we will configure IPv4 addressing on the distribution switches. The addressing for Core-3 and Core-4 have already been configured, so we don't have to touch those. The addresses we will use will be part of /30 networks, in an effort to conserve IP addresses. This means that the network only has four total IP addresses, with two usable ones (two are reserved for the network and broadcast addresses). The core switches have already been assigned the first usable address in the subnet, so the distribution switches will be assigned the second usable address in the subnet.

**Distribution-1:** <br>
G1/0/10 -> 10.200.100.6/30 will connect to Core-3 G 1/0/10 -> 10.200.100.5 <br>
G1/0/11 -> 10.200.100.10/30 will connect to Core-4 G 1/0/11 -> 10.200.100.9

**Distribution-2:** <br>
G1/0/10 -> 10.200.100.14/30 will connect to Core-3 G 1/0/10 -> 10.200.100.13 <br>
G1/0/11 -> 10.200.100.18/30 will connect to Core-4 G 1/0/11 -> 10.200.100.17

The commands for configuring the IP addressing are the same as what we have been using throughout this project:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%206%20-%203.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%206%20-%204.png">

We can verify the configuration by making sure that the statuses of the links are up and that they are reachable by the switch:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%206%20-%205.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%206%20-%206.png">

*Note, the first probe fails for each ping due to an ARP Request being sent out*

<h2>Removing Static Routes and Adding OSPF</h2>

We previously configured static routing so that the networks on the opposing distribution switches could reach each other. Now we will remove those static routes and configure OPSF, a dynamic routing protocol, to handle the routing for non-directly connected networks.

Let's remove the current static routes:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%206%20-%207.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%206%20-%208.png">

Now let's enable OSPF on the switches:

**Distribution-1 Config:** <br>
<code>router ospf 1</code> <br>
<code>router-id 1.0.0.0</code> <br>
<code>auto-cost reference-bandwidth 10000</code> <br>
<code>network 10.0.0.0 0.255.255.255 area 0</code> <br>
<code>exit</code> <br>
<code>interface gig 1/0/10</code> <br>
<code>ip ospf network point-to-point</code> <br>
<code>exit</code> <br>
<code>interface gig 1/0/11</code> <br>
<code>ip ospf network point-to-point</code> <br>
<code>exit</code> <br>
<code>interface gig 1/0/23</code> <br>
<code>ip ospf network point-to-point</code> <br>
<code>exit</code> <br>
<code>interface gig 1/0/24</code> <br>
<code>ip ospf network point-to-point</code> <br>
<code>exit</code> <br>
<code>end</code> <br>
<code>clear ip ospf process</code> <br>
<code>yes</code> <br>

**Distribution-2 Config:** <br>
<code>router ospf 1</code> <br>
<code>router-id 2.0.0.0</code> <br>
<code>auto-cost reference-bandwidth 10000</code> <br>
<code>network 10.0.0.0 0.255.255.255 area 0</code> <br>
<code>exit</code> <br>
<code>interface gig 1/0/10</code> <br>
<code>ip ospf network point-to-point</code> <br>
<code>exit</code> <br>
<code>interface gig 1/0/11</code> <br>
<code>ip ospf network point-to-point</code> <br>
<code>exit</code> <br>
<code>interface gig 1/0/23</code> <br>
<code>ip ospf network point-to-point</code> <br>
<code>exit</code> <br>
<code>interface gig 1/0/24</code> <br>
<code>ip ospf network point-to-point</code> <br>
<code>exit</code> <br>
<code>end</code> <br>
<code>clear ip ospf process</code> <br>
<code>yes</code> <br>

And with that configured, any PC in the topology should be able to reach each other. We can test this by doing a couple pings from PC0:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%206%20-%209.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%206%20-%2010.png">

And that's all for this section! In the next part, we will configure DHCP to provide IP addressing for our end devices.

<h1>Part 7: DHCP</h1>

In this section of the project, we will be configuring DHCP, DHCP Relay, RSTP, PortFast, and BPDU Guard. This may seem overwhelming, but I'll go through it step-by-step and explain what everything is and how it all works.

<h2>Configuring SVIs for VoIP and WLAN Networks</h2>

In order to configure the DHCP process, we first need to make sure that IP address assignment is supported for all clients in our network. We previously configured Switched Virtual Interfaces (SVIs) in a previous section, but we didn't do so for our Voice over Internet Protocol (VoIP) and Wireless Local Area Network (WLAN) devices. Setting these SVIs up enables them to be the default gateway for these devices, allowing them to connect to other devices on the enterprise network, thus enabling them to be eligible for automatic IP addressing.

Here are the commands for configuring the SVIs on the distribution switches:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%207%20-%201.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%207%20-%202.png">

<h2>Configuring the DHCP Server</h2>

Before we configure the DHCP server, let's first go over what DHCP is. DHCP stands for Dynamic Host Configuration Protocol, and it automatically assigns IP addresses to devices on a network. It also sends end devices other important data about the network, such as the IP address of the default gateway. DHCP uses a client-server model, where the clients request addressing information and the server leases it out. So to begin the process of using DHCP, let's start by configuring the server to recognize the networks in our new switch block.

Our DHCP server is the device with the IP address of 10.2.1.10/24. We can add server pools for each VLAN. These server pools will define network parameters for the end devices, such as the default gateway, DNS server, and the assignable IP addresses for the network. Click on the 10.2.1.10/24 device, and then go to the <code>Services</code> tab and select <code>DHCP</code>. There is an existing server pool automatically created by Packet Tracer which cannot be edited, so let's put that one in the parking-lot VLAN:

<code>Default Gateway</code> to <code>0.0.0.0</code><br>
<code>DNS Server</code> to <code>0.0.0.0</code><br>
<code>Start IP Address</code> to <code>10.255.0.0</code><br>
<code>Maximum Number of Users</code> to <code>0</code><br>
<code>Save</code>

Now let's add the other server pools:

Pool Name | Default Gateway | DNS Server | Start Address | Subnet Mask | Max Users |
|:-------:|:---------------:|:----------:|:-------------:|:-----------:|:---------:|
| serverPool | 0.0.0.0 | 0.0.0.0 | 10.10.0.150 | 255.255.255.0 | 100 |
| serverPool-VLAN10 | 10.10.1.1 | 10.2.1.10 | 10.10.1.150 | 255.255.255.0 | 100 |
| serverPool-VLAN20 | 10.20.1.1 | 10.2.1.10 | 10.20.1.150 | 255.255.255.0 | 100 |
| serverPool-VLAN30 | 10.30.2.1 | 10.2.1.10 | 10.30.2.150 | 255.255.255.0 | 100 |
| serverPool-VLAN40 | 10.40.2.1 | 10.2.1.10 | 10.40.2.150 | 255.255.255.0 | 100 |
| serverPool-VLAN50 | 10.50.3.1 | 10.2.1.10 | 10.50.3.150 | 255.255.255.0 | 100 |
| serverPool-VLAN60 | 10.60.3.1 | 10.2.1.10 | 10.60.3.150 | 255.255.255.0 | 100 |
| serverPool-VLAN70 | 10.70.4.1 | 10.2.1.10 | 10.70.4.150 | 255.255.255.0 | 100 |
| serverPool-VLAN80 | 10.80.4.1 | 10.2.1.10 | 10.80.4.150 | 255.255.255.0 | 100 |
| serverPool-VLAN101 | 10.101.0.1 | 10.2.1.10 | 10.101.0.150 | 255.255.255.0 | 100 |
| serverPool-VLAN102 | 10.102.0.1 | 10.2.1.10 | 10.102.0.150 | 255.255.255.0 | 100 |
| serverPool-VLAN103 | 10.103.0.1 | 10.2.1.10 | 10.103.0.150 | 255.255.255.0 | 100 |
| serverPool-VLAN104 | 10.104.0.1 | 10.2.1.10 | 10.104.0.150 | 255.255.255.0 | 100 |
| serverPool-VLAN121 | 10.121.0.1 | 10.2.1.10 | 10.121.0.150 | 255.255.255.0 | 100 |
| serverPool-VLAN122 | 10.122.0.1 | 10.2.1.10 | 10.122.0.150 | 255.255.255.0 | 100 |
| serverPool-VLAN123 | 10.123.0.1 | 10.2.1.10 | 10.123.0.150 | 255.255.255.0 | 100 |
| serverPool-VLAN124 | 10.124.0.1 | 10.2.1.10 | 10.124.0.150 | 255.255.255.0 | 100 |

After adding all of the server pools, the table should look like this:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%207%20-%203.png">

Enable the DHCP service by turning it on:

<code>Service: On</code>

Since the DHCP service is now on, let's select a few PCs to configure for DHCP addressing. I chose PC0, PC1, PC4, PC5, and PC9. We can change their configuration easily by clicking on the device, going to the config tab, navigating to FastEthernet0, and selecting DHCP under IP Configuration. Make sure to change the display name of the device so you can tell at a glance that you configured it with DHCP. For example, I renamed PC0 to 10.10.1.DHCP/24.

Notice how all of these devices were given an IP address that starts with 169.254.x.x. These are known as Automatic Private IP Addressing (APIPA) addresses. They are given to devices when they fail to obtain an IP address from a DHCP server. So why did our IP address assignment with DHCP fail? 

Our devices weren't able to get IP addresses from the DHCP server because they weren't able to connect to it. The DHCP discover messages never reached the server because the two devices are on different broadcast domains. To do this, we need to implement another DHCP technology, DHCP relay.

<h2>DHCP Relay</h2>

DHCP relay is a mechanism that allows routers to relay DHCP broadcast requests from a client on one network to a DHCP server on another network. This is done by configuring an ip helper-address, which converts the broadcast on one network into a unicast to the DHCP server. This ip helper-address is configured on the layer 3 switch or router that serves as the default gateway for the client device. We will configure this for all VLANs on Distribution-1 and Distribution-2:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%207%20-%204.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%207%20-%205.png">

After making these changes on the distribution switches, you can now receive a DHCP assigned IP address on the end devices:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%207%20-%206.png">

<h2>RSTP</h2>

Currently, our topology uses Per-VLAN Spanning Tree Plus (PVST+), which runs a separate instance of Spanning Tree Protocol (STP) for each VLAN. This works in practice, but is outdated and uses the old 802.1D standard. This standard has slower convergence times, sometimes taking up to a minute for the ports to go from blocking to forwarding. We will replace PVST+ with the newer IEEE 802.1w standard, which is Rapid Spanning Tree Protocol (RSTP). RSTP greatly reduces the convergence time after a topology change, and we will notice this difference whenever we start up Packet Tracer. Although we won't get into the details of RSTP, at a glance it introduces new port roles and gets rid of the traditional learning and listening states, allowing the ports to transition to the forwarding state more quickly.

Let's enable RSTP by configuring it on all of the distribution and access switches in the network. This includes all of the switches in both switch blocks, not just the one we added. RSTP is easy to configure, as it is just one command:

<code>spanning-tree mode rapid-pvst</code>

<h2>PortFast and BPDU Guard</h2>

Lastly, we will configure PortFast and BPDU Guard on switch ports. Without PortFast, switch ports go through the STP process. This means that during the time that STP is converging, the port is not forwarding data. This poses a problem as DHCP messages won't be able to go through. By the time STP has converged, the end device may have given up on DHCP. With PortFast, it allows the switch port to immediately begin forwarding data. But this poses another problem, what if a switch is plugged into the port and tries sending data? This could cause STP to break, which is the whole reason why STP doesn't forward data until it is done with its listening, learning, and forwarding convergence process. To protect against switches from being plugged into a port with PortFast enabled, we can also enable BPDU guard. With BPDU guard, any device that tries sending BPDUs will cause that port to immediately shut down, ensuring that STP doesn't break. Let's set up PortFast and BPDU Guard on our access switches.

For Access-1-1, 1-2, 2-1, and 2-2:

<code>interface fa 0/5</code><br>
<code>spanning-tree portfast</code><br>
<code>spanning-tree bpduguard enable</code><br>

For Access-1-3, 1-4, 2-3, and 2-4:

<code>interface range fa 0/5, fa 0/6</code><br>
<code>spanning-tree portfast</code><br>
<code>spanning-tree bpduguard enable</code><br>

Now in case any switches get plugged in on these ports, the port will immediately shut down and the network stability will be preserved.

That wraps up this section! In the final section, we will implement a First Hop Redundancy Protocol (FHRP) at the data center in our topology.

<h1>Part 8: FHRP-DC (Coming 5/18/25)</h1>

In this section of the lab, we will be configuring a First Hop Redundancy Protocol (FHRP) on the Distribution-DC-1 and Distribution-DC-2 switches. FHRP is a group of protocols that are designed to ensure network availability by keeping a backup default gateway in case the default gateway goes down. The way this works is by taking two layer 3 devices and setting up a virtual default gateway. The main router assumes the identity of the default gateway and tells the other router that it is still working. Then in case the main router goes down, the backup router assumes the identity of the virtual default gateway. The client device has no idea that the main router went down, as its packets are still being sent out like normal. Additionally, the client's ARP table remains unchanged, as it is oblivious to the fact that the default gateway is a different device.

Before we configure a FHRP, let's first enable RSTP, PortFast, and BPDU Guard on the Access-DC switch on interfaces 0/1-3, 0/10. Refer back to the previous section if you forgot how to do this.

Next, since we want to set up our virtual default gateway, let's change the IP addresses of our existing distribution switch ports. This will allow our virtual default gateway address to be the first address on the network, which is the common standard.

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%208%20-%201.png">

<h2>Configuring HSRP</h2>

The specific FHRP we are going to use is called Hot Standby Router Protocol (HSRP). This is a Cisco proprietary protocol, and it is designed to provide redundancy as FHRPs do. What we will do is assign the IP address to the port, give it a high priority for becoming the default router, and then give it preempt. Preempt just allows the router to take over as the default gateway if it were ever to come back online after temporarily being offline.

Here are the commands for configuring HSRP on both switches:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%208%20-%202.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%208%20-%203.png">

So now if we shutdown the link to the main layer 3 switch...

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%208%20-%204.png">
<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%208%20-%205.png">

...the DHCP/DNS server is still able to reach its default gateway! This demonstrates the power of FHRPs, they provide redundancy to the client without the client having to do anything on their end.

And that's it! We have now configured HSRP for the data center portion of the network. here's the final layout of our network topology:

<img src = "https://github.com/eric-lgonz/Enterprise-Network-Expansion/blob/main/assets/Part%208%20-%206.png">

<h1>Conclusion</h1>

Congratulations, you have now:

- Integrated a new switch block into an existing enterprise network using Cisco Packet Tracer, simulating real-world brownfield network expansion
- Configured VLANs, trunks, Layer 3 routing, SVIs, EtherChannel, and first-hop redundancy protocols to support resilient network growth
- Applied the access-distribution-core design model to optimize performance, scalability, and manageability in a multi-layer enterprise environment

Cisco Packet Tracer is a great network simulation tool, and I highly recommend you practice more with it if you have an interest in the field.

For more interactive and exciting projects, I recommend that you check out the other projects and walkthroughs on my <a href="https://github.com/eric-lgonz"> github page<a/>.
