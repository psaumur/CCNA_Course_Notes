# 22. RAPID SPANNING TREE PROTOCOL

*COMPARISON OF STP VERSIONS (Standard vs. Cisco)*

![image](https://github.com/psaumur/CCNA/assets/106411237/ca5ff85c-842e-4ed3-9b6a-f9d6ed546a78)


We are only concerned with 802.1w for MOST use cases.

MSTP (802.1s) is more useful for VERY LARGE networks.

WHAT IS RAPID PER-VLAN SPANNING TREE PLUS?

> RSTP is not a time-based spanning tree algorithm like 802.1D. Therefore, RSTP offers an improvment over teh 30 seconds or more 802.1D takes to move a link to forwarding. The heart of the protocol is a new bridge-bridge handshake mechanism, which allows ports to move directly to forwarding

---

SIMILARITIES BETWEEN STP AND RSTP:

- RSTP serves the same purpose as STP, blocking specific PORTS to prevent LAYER 2 LOOPS.
- RSTP elects a ROOT BRIDGE with the same rules as STP
- RSTP elects ROOT PORTS with the same rules as STP
- RSTP elects DESIGNATED PORTS with the same rules as STP

---

DIFFERENCES BETWEEN STP AND RSTP:

**PORT COSTS**

![image](https://github.com/psaumur/CCNA/assets/106411237/b250c6da-2579-4576-8e93-5a8f8e66d873)


(STUDY AND MEMORIZE PORT COSTS OF STP AND RSTP)

RSTP PORT STATES

![image](https://github.com/psaumur/CCNA/assets/106411237/054d5037-a60e-478e-986b-6f43825a0d1a)

- If a PORT has been ADMINISTRATIVELY DISABLED (”shutdown” command) = DISCARDING STATE
- If a PORT is ENABLED but BLOCKING traffic to prevent LAYER 2 LOOPS = DISCARDING STATE

---

RSTP ROLES

- The ROOT PORT role remains unchanged in RSTP
    - The PORT that is closest to the ROOT BRIDGE becomes the ROOT PORT for the SWITCH
    - The ROOT BRIDGE is the only SWITCH that doesn’t have a ROOT PORT
- The DESIGNATED PORT role remains unchanged in RSTP
    - The PORT on a segment (Collision Domain) that sends the best BPDU is that segment’s DESIGNATED PORT (only one per segment!)
- The NON-DESIGNATED PORT role is split into TWO separate roles in RSTP:
    - The ALTERNATE PORT role
    - The BACKUP PORT role

**RSTP : ALTERNATE PORT ROLE**

- The RSTP ALTERNATE PORT ROLE is a DISCARDING PORT that receives a superior BPDU from another SWITCH
- This is the same as what you’ve learned about BLOCKING PORTS in classic STP

![image](https://github.com/psaumur/CCNA/assets/106411237/7d81e70c-3b31-4448-9d45-9aadb738c74d)

- An ALTERNATE PORT (labelled “A” above) functions as a backup to the ROOT PORT
- If the ROOT PORT fails, the SWITCH can immediately move it’s best alternate port to FORWARDING

![image](https://github.com/psaumur/CCNA/assets/106411237/41f3be85-6225-4749-83b4-f76952c5756a)

💡 This immediate move to FORWARDING STATE functions like a classic STP optional feature called **UplinkFast.** Because it is built into RSTP, you do not need to activate UplinkFast when using RSTP/Rapid PVST+

One more STP optional feature that was built into RSTP is **BackboneFast**

![image](https://github.com/psaumur/CCNA/assets/106411237/c4cea7b7-599f-4ec8-b9d3-a5acba71a5f5)

- **BackboneFast** allows SW3 to expire the MAX AGE TIMERS on it’s INTERFACE and rapidly FORWARD the superior BPDUs to SW2
- This FUNCTIONALITY is built into RSTP, so it does not need to be configured.

UPLINKFAST and BACKBONE FAST (SUMMARY)

💡 **UplinkFast** and **BackboneFast** are two optional features in Classic STP. They must be configured to operate on the SWITCH (not necessary to know for the CCNA)

- Both features are built into RSTP, so you do NOT have to configure them. They operate, by DEFAULT
- You do NOT need to have a detailed understanding of them for the CCNA. Know their names and their BASIC purpose (to help BLOCKING / DISCARDING PORTS rapidly move to FORWARDING)

---

**RSTP : BACKUP PORT ROLE**

- The RSTP BACKUP PORT role is a DISCARDING PORT that receives a superior BPDU from another INTERFACE on the same SWITCH
- This only happens when TWO INTERFACES are connected to the SAME COLLISION DOMAIN (via a HUB)
- Hubs are NOT used in modern networks, so you will probably NOT encounter an RSTP BACKUP PORT
- Hubs are NOT used in modern networks, so you will probably NOT encounter an RSTP BACKUP PORT.
- Functions as a BACKUP for a DESIGNATED PORT

💡 The INTERFACE with the LOWERS PORT ID will be selected as the DESIGNATED PORT, and the other will be the BACKUP port.

![image](https://github.com/psaumur/CCNA/assets/106411237/61aefc04-b3a9-484a-bbfa-1efe792c73c7)

WHICH Switch will be ROOT BRIDGE?
What about the OTHER ports ?

![image](https://github.com/psaumur/CCNA/assets/106411237/be4d404d-829d-41ab-ba39-34e918ed7ea9)

![image](https://github.com/psaumur/CCNA/assets/106411237/b5dec396-d5fc-486b-9110-5dcc2c4dc4aa)

![image](https://github.com/psaumur/CCNA/assets/106411237/1930a17b-6c74-4756-b89d-4148008f586b)

💡 RAPID STP *is* compatible with CLASSIC STP.
💡 The INTERFACE(S) on the RAPID STP-enabled SWITCH connected to the CLASSIC STP-enabled SWITCH will operate in CLASSIC STP MODE (Timers, BLOCKING >>> LISTENING >>> LEARNING >>> FORWARDING, etc.)

---

RAPID STP BPDU

CLASSIC RSTP (LEFT) vs RAPID STP BPDU (RIGHT)

![image](https://github.com/psaumur/CCNA/assets/106411237/2d2deb45-3f81-4c60-b9fa-0f6c3fe7c060)


💡 NOTE:

Classic STP BPDU has a “Protocol Version Identifier: Spanning Tree (0)

BPDU Type: Configuration (0x00)

BPDU flags: 0x00

RAPID STP BPDU has a “Protocol Version Identifier: Spanning Tree (2)

BPDU Type: Configuration (0x02)

BPDU flags: 0x3c


In CLASSIC STP, only the ROOT BRIDGE originated BPDUs, and other SWITCHES just FORWARDED the BPDUs they received. 

In RAPID STP, ALL SWITCHES originate and send their own BPDUs from their DESIGNATED PORTS

---

RAPID SPANNING TREE PROTOCOL

- ALL SWITCHES running RAPID STP send their own BPDUs every “hello” time (2 Seconds)
- SWITCHES “age” the BPDU information much more quickly
    - In CLASSIC STP, a SWITCH waits 10 “hello” intervals (20 seconds)
    - In RAPID STP, a SWITCH considers a neighbour lost if it misses 3 BPDUs (6 seconds). It will then “flush” ALL MAC ADDRESSES learned on that interface

![image](https://github.com/psaumur/CCNA/assets/106411237/c03d2645-42d8-4d95-b486-999e82ac12a8)

---

RSTP LINK TYPES

![image](https://github.com/psaumur/CCNA/assets/106411237/e837a271-ad13-4d6a-a800-434a0eff2576)

```
<E> = EDGE

<P> = POINT-TO-POINT

<S> = SHARED
```

RSTP distinguishes between THREE different “link types” : **EDGE**, **POINT-TO-POINT**, and **SHARED**

EDGE PORTS

- Connected to END HOSTS
- Because there is NO RISK of creating a LOOP, they can move straight to the FORWARDING STATE without the negotiation process!
- They function like a CLASSIC STP PORT with PORTFAST ENABLED

💡 SW1(config-if)# spanning-tree portfast

---

POINT-TO-POINT PORTS

- Connect directly to another SWITCH
- They function in FULL-DUPLEX
- You don’t need to configure the INTERFACE as POINT-TO-POINT (it should be detected)

💡 SW1(config-if)# spanning-tree link-type point-to-point

---

SHARED PORTS

- Connect to another SWITCH (or SWITCHES) via a HUB
- They function in HALF-DUPLEX
- You don’t need to configure the INTERFACE as SHARED (it should be detected)

💡 SW1(config-if)# spanning-tree link-type shared

---

QUIZ:

![image](https://github.com/psaumur/CCNA/assets/106411237/a7314f6f-55f0-4e62-bd24-b311b090afe8)

SW1 :

- **ROOT BRIDGE**
- G0/0 - 0/3= DESIGNATED

SW2 : 

- G0/0 = ROOT PORT
- G0/1 = DESIGNATED PORT
- G0/2 = BACKUP PORT
- G0/3 = DESIGNATED PORT

SW3 :

- G0/0 = DESIGNATED PORT
- G0/1 = ALTERNATE PORT
- G0/2 = ROOT PORT
- G0/3 = DESIGNATED PORT

SW4:

- G0/0 = ROOT
- G0/1 = ALTERNATE PORT
- G0/2 = DESIGNATED PORT

Connection between SW1 G0/0 and SW2 G0/0 = POINT-TO-POINT

Connection between SW3 G0/0 and SW4 G0/0 = POINT-TO-POINT

Connection between SW1 G0/1 and G0/2 to SW3 G0/1 and G0/2 = POINT-TO-POINT

Connections to all the END HOSTS = EDGE 

Connection from SW4 to HUB = SHARED

Connections from SW2 to HUB = SHARED

ANSWER

![image](https://github.com/psaumur/CCNA/assets/106411237/b76eb7be-897a-4617-990e-f399ceaea5f2)
