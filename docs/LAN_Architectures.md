# 52. LAN ARCHITECTURES

- You have studied various NETWORK technologies: ROUTING, SWITCHING, STP, ETHERCHANNEL, OSPF, FHRPs, SWITCH SECURITY FEATURES, etc.
    - Now, let’s look at some BASIC NETWORK DESIGN / ARCHITECTURE
- There are standard “BEST PRACTICES” for NETWORK DESIGN
    - However there are a few UNIVERSAL “CORRECT ANSWERS”
    - The answer to MOST general questions about NETWORK DESIGN is “IT DEPENDS”
- In the early stages of your NETWORKING career, you probably won’t be asked to DESIGN NETWORKS yourself
- However, to understand the NETWORKS you will be CONFIGURING and TROUBLESHOOTING, it’s important to know some BASICS of NETWORK DESIGN

---

COMMON TERMINOLOGIES

- STAR
    - When several DEVICES all connect to ONE CENTRAL DEVICE, we can draw them in a “STAR” shape like below, so this is often called a “STAR TOPOLOGY”

![image](https://github.com/psaumur/CCNA/assets/106411237/8aeb545d-3cc0-44bf-a01e-b7e5d47deaf2)

- FULL MESH
    - When each DEVICE is connected to each OTHER DEVICE

![image](https://github.com/psaumur/CCNA/assets/106411237/cb2d12af-cf17-4ffe-a637-148014d20753)

- PARTIAL MESH
    - When SOME DEVICES are connected to each other but not ALL

![image](https://github.com/psaumur/CCNA/assets/106411237/01ed7fe5-317b-45c7-8baa-0cc74e502433)

---

2-TIER AND 3-TIER LAN ARCHITECTURE

- The TWO-TIER LAN DESIGN consists of TWO Hierarchical Layers:
    - ACCESS LAYER
    - DISTRIBUTION LAYER
- Also called a “COLLAPSED CORE” DESIGN because it omits a layer that is found in the THREE TIER DESIGN : THE CORE LAYER
- ACCESS LAYER
    - The LAYER that END HOSTS connect to (PCs, Printers, Cameras, etc)
    - Typically, ACCESS LAYER SWITCHES have lots of PORTS for END HOSTS to connect to
    - QoS MARKING is typically done here
    - Security Services like PORT SECURITY, DAI, etc are typically performed here
    - SWITCHPORTS might be PoE-Enabled for Wireless APs, IP Phones, etc.
- DISTRIBUTION LAYER
    - Aggregates connections from the ACCESS LAYER SWITCHES
    - Typically is the border between LAYER 2 and LAYER 3
    - Connects to services such as Internet, WAN, etc
    - Sometimes called AGGREGATION LAYER

![image](https://github.com/psaumur/CCNA/assets/106411237/4592f4d8-5550-4428-923c-c805d2ca476f)

![image](https://github.com/psaumur/CCNA/assets/106411237/4fa26aec-536a-4ad8-8f39-e94dacc4cb3c)

![image](https://github.com/psaumur/CCNA/assets/106411237/72018e4f-113e-4921-8dc4-05079c590ee1)

![image](https://github.com/psaumur/CCNA/assets/106411237/c8326214-80e0-4702-a1c3-6dd2fbafb6e9)

---

THREE-TIER CAMPUS LAN DESIGN

- In large NETWORKS with many DISTRIBUTION LAYER SWITCHES (for example in separate buildings), the number of connections required between DISTRIBUTION LAYER SWITCHES grows rapidly

![image](https://github.com/psaumur/CCNA/assets/106411237/8b94c8e9-813b-40e0-bcd1-b27d73da31e8)

- To help SCALE large LAN NETWORKS, you can add a CORE LAYER.

** Cisco recommends adding a CORE LAYER if there are more than THREE DISTRIBUTION LAYERS in a single location

![image](https://github.com/psaumur/CCNA/assets/106411237/d5c1a677-38ff-425f-b91a-65a8fa37c377)

- The THREE-TIER LAN DESIGN consists of THREE HIERARCHICAL LAYERS:
    - ACCESS LAYER
    - DISTRIBUTION LAYER
    - CORE LAYER

- CORE LAYER:
    - Connects DISTRIBUTION LAYERS together in large LAN NETWORKS
    - The focus is SPEED (”FAST TRANSPORT”)
    - CPU-INTENSIVE OPERATIONS, such as SECURITY, QoS Markings / Classification, etc. should be avoided at this LAYER
    - Connections are all LAYER 3. NO SPANNING-TREE!
    - Should maintain connectivity throughout the LAN even if DEVICES FAIL
    
![image](https://github.com/psaumur/CCNA/assets/106411237/633cee0a-8952-4b27-91a3-8653bb8e353c)
    

---

SPINE-LEAF ARCHITECTURE (DATA CENTER)

- CISCO ACI ARCHITECTURE (Application Centric Infrastructure) uses this architecture
- DATA CENTERS are dedicated spaces / buildings used to STORE COMPUTER SYSTEMS such as SERVERS and NETWORK DEVICES
- Traditional DATA CENTER designs used a THREE-TIER ARCHITECTURE (ACCESS-DISTRIBUTION-CORE) like we just covered
- This worked well when most TRAFFIC in the DATA CENTER was NORTH-SOUTH

![image](https://github.com/psaumur/CCNA/assets/106411237/7e2ff784-d16f-4606-a186-c73223bf5582)

- With the precedence of VIRTUAL SERVERS, applications are often deployed in a DISTRIBUTED manner (across multiple physical SERVERS) which increases the amount of EAST-WEST TRAFFIC in the DATA CENTER
- The traditional THREE-TIER ARCHITECTURE led to bottlenecks in the BANDWIDTH as well as VARIABILITY in the SERVER-TO-SERVER latency depending on the PATH the TRAFFIC takes
- To SOLVE this, SPINE-LEAF ARCHITECTURE (also called CLOS ARCHITECTURE) has become prominent in DATA CENTERS

RULES FOR SPINE-LEAF ARCHITECTURE

- Every LEAF SWITCH is connected to every SPINE SWITCH
- Every SPINE SWITCH is connected to every LEAF SWITCH
- LEAF SWITCHES do NOT connect to other LEAF SWITCHES
- SPINE SWITCHES do NOT connect to other SPINE SWITCHES
- END HOSTS (Servers, etc) ONLY connect to LEAF SWITCHES

![image](https://github.com/psaumur/CCNA/assets/106411237/73cbe190-f589-4307-8ce4-e3de8af2f1d5)

- The PATH taken by TRAFFIC is randomly chosen to balance the TRAFFIC LOAD among the SPINE SWITCHES
- Each SERVER is separated by the same number of “HOPS” (except those connected to the same LEAF) providing CONSISTENT LATENCY for EAST-WEST TRAFFIC

---

SOHO (SMALL OFFICE / HOME OFFICE)

- SMALL OFFICE / HOME OFFICE (SOHO) refers to the office of a small company, or a small home office with few DEVICES
    - Doesn’t have to be an actual home “office”; if your home has a NETWORK connected to the INTERNET it is considered a SOHO NETWORK

- SOHO NETWORKS don’t have complex needs, so all NETWORKING functions are typically provided by a SINGLE DEVICE, often called a “HOME ROUTER” or “WIRELESS ROUTER”
- The one DEVICE can serve as a:
    - ROUTER
    - SWITCH
    - FIREWALL
    - WIRELESS ACCESS POINT
    - MODEM

![image](https://github.com/psaumur/CCNA/assets/106411237/c9edf179-f333-4fec-9e95-ee291b5eb84c)

![image](https://github.com/psaumur/CCNA/assets/106411237/7d606552-8939-41c1-ad85-13face1d27f5)
