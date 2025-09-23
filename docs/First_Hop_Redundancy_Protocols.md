# 29. FIRST HOP REDUNDANCY PROTOCOLS

THE PURPOSE OF FHRPS

 
![image](https://github.com/psaumur/CCNA/assets/106411237/32c286ce-e042-4cda-9067-c232a210ec81)

What happens when the configured DEFAULT GATEWAY for network HOSTS goes down ?

What happens to the routed traffic?

How can we route our traffic to the functional GATEWAY at R2 (.253) ? 

This is what the FIRST HOP REDUNDANCY PROTOCOL is designed to fix

---

FIRST HOP REDUNDANCY PROTOCOL (FHRP)

- Computer networking protocol
- Designed to PROTECT the DEFAULT GATEWAY used on a SUBNET by allowing TWO or MORE ROUTERS to provide BACKUP for that ADDRESS
- In the event of a FAILURE of the ACTIVE ROUTER, the BACKUP ROUTER will take over the ADDRESS (usually within seconds)

---

HOW DOES FHRP WORK?

- TWO (or more) ROUTERS share a VIP (A Virtual IP ADDRESS)
- THIS VIP is used by HOSTS as the DEFAULY GATEWAY IP
- The ROUTERS communicate with each other by sending “Hello” messages
- One ROUTER becomes the ACTIVE ROUTER, the other(s) STANDBY
- When a HOST sends traffic to an ADDRESS outside of the NETWORK, it sends an ARP REQUEST (Broadcast Flood) to the VIP to find out it’s MAC ADDRESS
    - Spanning Tree prevents BROADCAST STORM due to Broadcast Flood
- The ACTIVE ROUTER sends the ARP REPLY back (it’s VIRTUAL MAC ADDRESS) to the HOST
- The HOST now sends traffic OUTSIDE of the NETWORK with:
    - Source IP (HOST IP)
    - Destination IP (External IP ADDRESS)
    - Source MAC (HOST MAC ADDRESS)
    - Destination MAC (GATEWAY VIP MAC ADDRESS)

![image](https://github.com/psaumur/CCNA/assets/106411237/2a1c5df8-d4fa-44fa-b850-a8fd6bb69388)

IF R1 goes down, R2 will switch from STANDY to ACTIVE after not receiving “Hello” messages from R1

![image](https://github.com/psaumur/CCNA/assets/106411237/5e54ee53-09bd-42a7-b89e-69892590913d)

The HOST ARP TABLE doesn’t need to change since the MAC ADDRESS of the VIP is already known and traffic flows externally via R2

R2 DOES need to update the SWITCHES with a GRATUITOUS ARP

- GRATUITOUS ARP is an ARP REPLY sent without being REQUESTED (no ARP REQUEST received)
- GRATUITOUS ARP uses BROADCAST (FFFF.FFFF.FFFF) - Normal ARP REPLY is Unicast

![image](https://github.com/psaumur/CCNA/assets/106411237/6a47dc71-544e-4e33-99cd-b6a8db90f56f)

![image](https://github.com/psaumur/CCNA/assets/106411237/6f36cdf9-d002-48d6-ae5b-6fb899431b46)

What happens is R1 comes back ONLINE again?

It becomes a STANDBY ROUTER

R2 remains the ACTIVE ROUTER

<aside>
💡 FPRPs are “non-preemptive”. The current ACTIVE ROUTER will not automatically give up its role, even if the former ACTIVE ROUTER returns.

*** You CAN change this setting to make R1 ‘preempt’ R2 and take back it’s ACTIVE role, automatically ***

</aside>

---

HSRP (HOT STANDBY ROUTER PROTOCOL)

- **Cisco proprietary**
- An ACTIVE and STANDBY ROUTER are elected
- There are TWO VERSIONS :
    - version 1
    - version 2 : *adds IPv6 support* and increases # of *groups* that can be configured

- Multicast IPv4 ADDRESSES :
    - **v1** : 224.0.0.2
    - **v2** : 224.0.0.102

- VIRTUAL MAC ADDRESSES :
    - **v1** : 0000.0c07.acXX (XX = HSRP GROUP NUMBER)
    - **v2** : 0000.0c9f.fXXX (XXX = HSRP GROUP NUMBER)

- In a situation with MULTIPLE SUBNETS / VLANS, you can configure a DIFFERENT ACTIVE ROUTER in EACH SUBNET / VLAN to LOAD BALANCE

![image](https://github.com/psaumur/CCNA/assets/106411237/a5795fa0-d57b-4037-8945-a39da7fb2d15)

---

VRRP (VIRTUAL ROUTER REDUNDANCY PROTOCOL)

- Open Standard
- A MASTER and BACKUP ROUTER are elected

- Multicast IPv4 ADDRESSES :
    - 224.0.0.18

- VIRTUAL MAC ADDRESSES :
    - 0000.5e00.01XX (XX = VRRP GROUP NUMBER)
        - for GROUP NUMBERS > 99, you need to convert the number to HEX
        - Example: 200 = “c8” in Hex so the MAC would be 0000.5e00.01c8

- In a situation with MULTIPLE SUBNETS / VLANS, you can configure a DIFFERENT MASTER ROUTER in EACH SUBNET / VLAN to LOAD BALANCE

![image](https://github.com/psaumur/CCNA/assets/106411237/4bd45dbc-fc51-4c45-818e-5274530accde)

---

GLBP (GATEWAY LOAD BALANCING PROTOCOL)

- Cisco Proprietary
- LOAD BALANCES among MULTIPLE ROUTERS within a SINGLE SUBNET
- An AVG (Active Virtual Gateway) is elected
- Up to FOUR AVFs (Active Virtual Forwarders) are assigned BY the AVG (the AVG can be an AVF, too)
- Each AVF acts as the DEFAULT GATEWAY for a portion of the HOSTS in the SUBNET

- Multicast IPv4 ADDRESSES :
    - 224.0.0.102

- VIRTUAL MAC ADDRESSES :
    - 0007.b400.XXYY (XX = GLBP GROUP NUMBER, YY = AVF NUMBER)

---

MEMORIZE THIS CHART and the differences between the FHRPs

![image](https://github.com/psaumur/CCNA/assets/106411237/a5b5ee87-4c92-4b3e-9b98-3d0c09a1732d)

---

BASIC HSRP CONFIGURATION

R1s configuration

![image](https://github.com/psaumur/CCNA/assets/106411237/028b13d4-b258-4551-96ae-068adb931356)

NOTE : group number has to match ALL ROUTERS being configured in a given SUBNET

![image](https://github.com/psaumur/CCNA/assets/106411237/d2e5eb5f-d105-4788-a869-d9e65f53eca7)

R2’s configuration

![image](https://github.com/psaumur/CCNA/assets/106411237/65b999f6-eed8-45c3-89fe-bff749f40f11)

NOTE : HSRP versions are not cross-compatible. All ROUTERS must use the same HSRP Version

Output of the “show standby” command

![image](https://github.com/psaumur/CCNA/assets/106411237/99107301-2619-4454-b104-8aed3780924d)
