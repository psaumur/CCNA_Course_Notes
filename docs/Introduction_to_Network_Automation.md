# 59. INTRODUCTION TO NETWORK AUTOMATION

WHY NETWORK AUTOMATION

- Previous versions of the CCNA focused on the traditional model of managing / controlling networks
- The current version focuses on the traditional model as well, but CCNA candidates are expected to have a basic understanding of various topics related to network automation
- In the traditional model, engineers manage devices one at a time by connecting to their CLI via SSH

---

DOWNSIDES OF CONFIGURING DEVICES ONE-BY-ONE

- Typos and other small mistakes are common
- It is time-consuming and very inefficient in large-scale networks
- It is difficult to ensure that all devices ADHERE to the organization’s STANDARD CONFIGURATION

---

BENEFITS OF NETWORK AUTOMATION

- Human Error (Typos, etc) is reduced
- Networks become much more scalable and implemented in a fraction of the time
    - New deployments
    - Network-wide changes
    - Troubleshooting
- Network-wide policy compliance can be assured
    - Standard configurations
    - Software versioning

- The improved efficiency of network operations reduces the OP-EX (operating expenses) of the network. Each task requires fewer man-hours

```
There are various tools / methods that can be used to automate tasks in the network

- SDN (Software-Defined Networking)
- Ansible
- Puppet
- Python scripts
- etc…
```

---

LOGICAL “PLANES” OF NETWORK FUNCTIONS

**What does a ROUTER do?**

- It forwards messages between networks by examining information in the Layer 3 header
- It uses a routing protocol like OSPF to share route information with other routers and build a routing table
- It uses ARP to build an ARP table, mapping IP Addresses to MAC Addresses
- It uses Syslog to keep logs of events that occur
- and MUCH more…

**What does a SWITCH do?**

- It forwards messages within a LAN by examining information in the Layer 2 header
- It uses STP to ensure there are no Layer 2 loops in the network
- It builds a MAC address table by examining the Source MAC address of frames
- It uses Syslog to keep logs of events that occur
- It allows a user to connect to it via SSH and manage it

---

The various functions of network devices can be logically divided up (categorized) into *PLANES*

```
- DATA PLANE
- CONTROL PLANE
- MANAGEMENT PLANE
```


- The operations of the MANAGEMENT PLANE and the CONTROL PLANE are usually managed by the CPU
- However, this is not desirable for DATA PLANE operations because CPU processing is slow (relatively speaking)
- Instead, a specialized hardware ASIC (Application-Specific Integrated Circuit) is used.
    - ASICs are chips built for a specific purpose
- Using a SWITCH, as an example:
    - When a FRAME is received, the ASIC (not the CPU) is responsible for the switching logic
    - The MAC Address table is stored in a kind of memory called TCAM (Ternary Content-Addressable Memory)
        - Another common name for the MAC Address table is CAM TABLE
    - The ASIC feeds the DESTINATION MAC address of the FRAME into the TCAM which returns the matching MAC Address table entry
    - The FRAME is then forwarded out of the appropriate DEVICE
- Modern ROUTERS also use a similar hardware DATA PLANE: An ASIC designed for forwarding logic, and tables store in TCAM

---

A SIMPLE SUMMARY:

>- When a DEVICE receives CONTROL / MANAGEMENT traffic (destined for itself), it will be processed in the CPU
>- When a DEVICE receives DATA traffic which should pass through the DEVICE, it is processed by the ASIC for maximum speed

---

DATA PLANE

- All tasks involved in forwarding USER  DATA / TRAFFIC from one INTERFACE to another are part of the DATA PLANE
- A ROUTER receives a message, looks for the most specific matching ROUTER in its ROUTING TABLE, and forwards it out of the appropriate INTERFACE to the next hop
    - It also de-encapsulates the original LAYER 2 header, and re-encapsulates with a new header destined for the next hop’s MAC address
- A SWITCH receives a message, looks at the DESTINATION MAC Address, and forwards it out of the appropriate INTERFACE (or FLOODS it)
    - This includes functions like adding / removing 802.1q VLAN tags
- NAT (changing the SRC / DST addresses before forwarding) is part of the DATA PLANE
- Deciding to forward / discard messages due to ACL’s, port-security, etc. is part of the DATA PLANE
- The DATA PLANE is also called the ‘FORWARDING PLANE’

![image](https://github.com/psaumur/CCNA/assets/106411237/6a72186b-2956-45f6-8643-801caa2cb28e)

---

CONTROL PLANE

- How does a DEVICE’s DATA PLANE make its forwarding decisions?
    - ROUTING TABLE
    - MAC ADDRESS table
    - ARP table
    - STP
    - etc…
    
- Functions that build THESE tables (and other functions that influence the DATA PLANE) are part of the CONTROL PLANE

- The CONTROL PLANE *controls* what the DATA PLANE does, for example by building the ROUTER’s ROUTING TABLE

- The CONTROL PLANE performs *overhead* work
    - OSPF itself doesn’t forward user data packets, but it informs the DATA PLANE about HOW packets should be forwarded
    - STP itself isn’t directly involved in the process of forwarding FRAMES, but it informs the DATA PLANE about which INTERFACES should and shouldn’t be used to forward FRAMES
    - ARP messages aren’t user data but they are used to build an ARP TABLE which is used in the process of forwarding data

![image](https://github.com/psaumur/CCNA/assets/106411237/4c21b082-5d6e-4388-94c5-bebf33b50c8d)

---

MANAGEMENT PLANE

- Like the CONTROL PLANE, the MANAGEMENT PLANE performs overhead work
    - However, the MANAGEMENT PLANE doesn’t directly affect the forwarding of messages in the DATA PLANE
- The MANAGMENT PLANE consists of PROTOCOLS that are used to manage devices
    - SSH / TELNET : Used to connect to the CLI of a DEVICE to configure / manage it
    - SYSLOG : Used to keep logs of events that occur on the device
    - SNMP : Used to monitor the operations of the device
    - NTP : Used to maintain accurate time on the device

![image](https://github.com/psaumur/CCNA/assets/106411237/3cfffa40-f4cb-4042-8778-139605c2eb26)

---

SOFTWARE-DEFINED NETWORKING (SDN)

- SOFTWARE-DEFINED NETWORKING (SDN) is an approach to networking that centralizes the CONTROL PLANE into an application called a *CONTROLLER*
- SDN is also called SOFTWARE-DEFINED-ARCHITECTURE (SDA) or CONTROLLER-BASED NETWORKING
- Traditional CONTROL PLANES use a distributed architecture
    - For example:
        - Each ROUTER in the NETWORK runs OSPF and the ROUTERS share routing information and then calculate their preferred routes to each destination
- An SDN CONTROLLER centralized CONTROL PLANE functions like calculation routes
    - That is just an example and how much of the CONTROL PLANE is centralized varies greatly
- The CONTROLLER can interact programmatically with the NETWORK DEVICE using APIs (Application Programming Interface)

![image](https://github.com/psaumur/CCNA/assets/106411237/05c4c5d9-5ba4-480c-9c13-72fa1f7937db)

---

SOUTHBOUND INTERFACE (SBI)

- The SBI is used for communications between the CONTROLLER and the NETWORK DEVICES it controls
- It typically consists of a COMMUNICATION PROTOCOL and API (Application Programming Interface)

- APIs facilitate data exchanges between programs
    - DATA is exchanged between the CONTROLLER and the NETWORK DEVICES
    - An API on the NETWORK DEVICES allows the CONTROLLER to access information on the DEVICES, control their DATA PLANE TABLES, etc.
- Some examples of SBIs :
    - OpenFlow
    - Cisco OpFlex
    - Cisco OnePK (Open Network Environment Platform Kit)
    - NETCONF

---

 NORTHBOUND INTERFACE (NBI)

- Using the SBI, the CONTROLLER communicates with the managed DEVICES and gathers information about them:
    - The DEVICES in the NETWORK
    - The TOPOLOGY (how the DEVICES are connected together)
    - The available INTERFACES on each DEVICE
    - Their CONFIGURATIONS
- The NORTHBOUND INTERFACE (NBI) is what allows us to:
    - Interact with the CONTROLLER
    - Access the DATA it gathers about the NETWORK
    - Program the NETWORK
    - Make changes to the NETWORK via the SBI

- A REST API (Representational State Transfer) is used on the controller as an interface for APPS to interact with it
- OSGi (Java Open Services Gateway Initiative) - Java based NBI API

- DATA is sent in a structured (*serialized*) format such as JSON or XML
    - This makes it easier for programs to use the DATA

![image](https://github.com/psaumur/CCNA/assets/106411237/d980626f-f731-46a4-ba14-72c3d21f2fd3)

---

AUTOMATION IN TRADITIONAL NETWORKS VS SDN

- Networking tasks can be automated in traditional NETWORK architectures too:
    - SCRIPTS can be written (ie: using Python) to push commands to many DEVICES at once
    - Python with good use of REGULAR EXPRESSIONS can parse through “show” commands to gather information about network devices
    
- However, the robust and centralized DATA collected by SDN CONTROLLERS greatly facilitates these functions
    - The CONTROLLER collects information about all DEVICES in the NETWORK
    - NORTHBOUND APIs allow APPS to access information in a format that is easy for programs to understand (ie: JSON and XML)
    - The centralized DATA facilitates network-wide analytics
- SDN Tools can provide the benefits of automation without the requirement of third-party scripts and apps.
    - You don’t need expertise in automation to make use of SDN Tools
    - However, APIs allow third-party applications to interact with the CONTROLLER, which can be very powerful


>💡 Although SDN and automation aren’t the same thing, the SDN architecture greatly facilitates the automation of various tasks in the network via the SDN CONTROLLER and APIs
