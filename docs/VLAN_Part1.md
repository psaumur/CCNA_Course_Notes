# 16. VLANS : PART 1

WHAT IS A LAN ? 

- A LAN is a single BROADCAST DOMAIN, including all devices in that broadcast domain.

BROADCAST DOMAINS

- A BROADCAST DOMAIN is the group of devices which will receive a BROADCAST FRAME (Destination MAC : FFFF.FFFF.FFFF) sent by any one of the members.

Image of LAN with FOUR BROADCAST DOMAINS (192.168.1.0 / 24)

![image](https://github.com/psaumur/CCNA/assets/106411237/de712483-e881-41f5-9525-576216186498)


Performance :

Lots of unnecessary BROADCAST traffic can reduce network performance.

![image](https://github.com/psaumur/CCNA/assets/106411237/a807fdc5-27b9-4735-8b8d-51bdc0c91a8c)


BROADCAST FRAME flooding all our subnets with unnecessary traffic.

![image](https://github.com/psaumur/CCNA/assets/106411237/fcd03904-a193-4423-8940-09be1df1bd2c)


Security :

Even within the same office, you want to limit who has access to what. You can apply security policies on a ROUTER / FIREWALL. Because this is one LAN, PC’s can reach each other directly, without traffic passing through the router. So, even if you configure security policies, they won’t have any effect.

![image](https://github.com/psaumur/CCNA/assets/106411237/7bd562fc-7dff-4692-81d7-c026b007df8f)

---

WHAT IS A VLAN ? 

VLANS:

- logically separate end-hosts at LAYER 2
- are configured on Layer 2 SWITCHES on a per-interface basis.
- any END HOST connected to that interface is part of that VLAN

---

PURPOSE OF VLANs:

Network Performance :

- Reduce unnecessary BROADCAST traffic, which helps prevent network congestion, and improve network performance

Network Security :

- Limiting BROADCAST and unknown UNICAST traffic, also improves network security, since messages won’t be received by devices outside of the VLAN

![image](https://github.com/psaumur/CCNA/assets/106411237/fae2f1ed-ffc3-4d91-adf7-16a67c2dc5aa)


SWITCHES do not forward traffic directly between HOSTS in different VLANS

![image](https://github.com/psaumur/CCNA/assets/106411237/2e5834e9-9096-46eb-bb96-ba8459338107)


![image](https://github.com/psaumur/CCNA/assets/106411237/3046f727-fad4-421e-85ef-63a73e109f83)


Sending Packets to another VLAN (Routed through R1)

![image](https://github.com/psaumur/CCNA/assets/106411237/7090ef6d-ce8c-454f-b80d-f6dfd82745c8)


![image](https://github.com/psaumur/CCNA/assets/106411237/b7237602-5b46-4c31-bd75-2e50e0fb1017)

---

HOW TO CONFIGURE VLANS ON CISCO SWITCHES

#show vlan brief

![image](https://github.com/psaumur/CCNA/assets/106411237/13ce8382-6aea-484e-9580-d91c98189522)


Shows which VLANS that exist on the SWITCH and what INTERFACES are in each VLAN

VLANs 1 (DEFAULT), 1002-1005 exist by default and **cannot be deleted (5 VLANs)**

---

HOW TO ASSIGN INTERFACES TO A VLAN

![image](https://github.com/psaumur/CCNA/assets/106411237/ed31145d-7949-4c68-b88a-97716beaf074)


1) Use the “interface range” command to select all the interfaces at once

2) Use the “switchport mode access” command to set the interface as an ACCESS PORT

---

WHAT IS AN ACCESS PORT?

- An ACCESS PORT is a SWITCHPORT which belongs to a single VLAN, and usually connects to end hosts like PCs.

SWITCHPORTS which carry multiple VLANs are called “TRUNK PORTS” (more info on TRUNK in next chapter)

3) Use the “switchport access” command to assign a VLAN to a PORT

![image](https://github.com/psaumur/CCNA/assets/106411237/b1bdb937-3707-496f-bc49-445df354d16b)


Use “#vlan <#>” to enter **Configuration Mode** for a given VLAN (this can also create a VLAN)

Use “#name <name>” to configure a NAME for your VLAN

To check your VLAN configuration, use “#show vlan brief”

![image](https://github.com/psaumur/CCNA/assets/106411237/2f7d26d8-9b2a-43a3-b213-fec4f984a309)


Testing VLAN 10

Pinging from PC1 using 255.255.255.255 (FFFF:FFFF:FFFF) floods broadcast packets to R1 and VLAN10 hosts only

![image](https://github.com/psaumur/CCNA/assets/106411237/5c64e485-f492-4436-9c1d-3a1ab20fbe05)
