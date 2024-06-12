# 23. ETHERCHANNEL

WHAT IS ETHERCHANNEL?

ETHERCHANNEL allows you to GROUP multiple physical INTERFACES into a group which operates as a SINGLE LOGICAL INTERFACE - so they BEHAVE as if they are a single INTERFACE

A LAYER 2 ETHERCHANNEL is a group of SWITCH PORTS which operate as a SINGLE INTERFACE

A LAYER 3 ETHERCHANNEL is a group of ROUTED PORTS which operate as a SINGLE INTERFACE which you assign an IP ADDRESS to.

![image](https://github.com/psaumur/CCNA/assets/106411237/86cecd4a-1554-4ece-8a88-6f97e24788f1)

When the bandwidth of the INTERFACES connected to END HOSTS is greater than the bandwidth of the connection to the DISTRIBUTION SWITCH(es), this is called **OVERSUBSCRIPTION.** 

Some OVERSUBSCRIPTION is acceptable, but too much will cause congestion.

![image](https://github.com/psaumur/CCNA/assets/106411237/6ada996f-8fd4-4339-9ad7-d52e51a3553e)

- If you connect TWO SWITCHES together with multiple links, ALL except ONE will be DISABLED by SPANNING TREE PROTOCOL (Green Lights vs. Orange Lights above on ASW1)

WHY?

- If ALL of ASW1s INTERFACES were FORWARDING, LAYER 2 LOOPS would form between ASW1 and DSW1, leading to a BROADCAST STORM (Bad!)
- Other links will be unused unless the active link fails. In that case, one of the inactive link will start forwarding.

An ETHERCHANNEL (in network topology diagrams) is represented like THIS (circle around multi-connections)

![image](https://github.com/psaumur/CCNA/assets/106411237/4c2cfcf8-57f2-4907-8322-2f26cc7dc7e4)

- ETHERCHANNEL groups multiple channels together to act as a SINGLE INTERFACE
- STP will treat this GROUP as a SINGLE INTERFACE

![image](https://github.com/psaumur/CCNA/assets/106411237/a48bed14-11b4-42ba-965a-9724598d3b69)

(All INTERFACES Green!)

TRAFFIC using ETHERCHANNEL will be load-balanced among the physical INTERFACES in the group.

An algorithm is used to determine WHICH TRAFFIC will use WHICH physical INTERFACE (more details later)

Some other names for an ETHERCHANNEL are:

- PORT CHANNEL
- LAG (Link Aggregation Group)

---

HOW DOES AN ETHERCHANNEL LOAD-BALANCE?

![image](https://github.com/psaumur/CCNA/assets/106411237/bc257ff8-bf91-4744-a6cb-8f603ee9d294)

- ETHERCHANNEL load-balances based on **“flows”**
- A “flow” is a communication between TWO NODES in the NETWORK
- FRAMES in the same “flow” will be FORWARDED using the SAME physical INTERFACE
- If FRAMES in the same “flow” were FORWARDED using different physical INTERFACES, some FRAMES may arrive at the DESTINATION out of order/sequence, which can cause problems.
- You can CHANGE the INPUTS used in the INTERFACE SELECTION calculation (for “flows”)
    - INPUTS that can be used:
        - SOURCE MAC ADDRESS
        - DESTINATION MAC ADDRESS
        - SOURCE and DESTINATION MAC ADDRESS
        - SOURCE IP ADDRESS
        - DESTINATION IP ADDRESS
        - SOURCE and DESTINATION IP ADDRESS

How to see the configuration for LOAD-BALANCING method

![image](https://github.com/psaumur/CCNA/assets/106411237/571623bf-b96b-4382-ada5-f14f93ec1a6a)

How to CHANGE the LOAD-BALANCING method

![image](https://github.com/psaumur/CCNA/assets/106411237/5919f2fd-80bb-4b10-bfa0-ce403f52c710)

![image](https://github.com/psaumur/CCNA/assets/106411237/bc30e17e-716a-41cd-a57a-69a661b5d58e)

---

HOW TO CONFIGURE LAYER 2 / LAYER 3 ETHERCHANNELS

There are THREE methods of ETHERCHANNEL configuration on Cisco SWITCHES

**PAgP (Port Aggregation Protocol)**

- Cisco proprietary protocol
- Dynamically negotiates the creation/maintenance of the ETHERCHANNEL (like DTP does for trunks)

💡 **LACP (Link Aggregation Control Protocol)**
- Industry standard protocol (IEEE 802.3ad)
- Dynamically negotiates the creation/maintenance of the ETHERCHANNEL (like DTP does for trunks)


**Static EtherChannel**

- A protocol isn’t used to determine if an EtherChannel should be formed
- Interfaces are statically configured to form an EtherChannel

Up to 8 INTERFACES can be formed into a single ETHERCHANNEL (LACP allows up to 16 but only 8 will be ACTIVE, the other 8 will in STANDBY mode, waiting for an active INTERFACE to fail)

 
---

PAgP CONFIGURATION

![image](https://github.com/psaumur/CCNA/assets/106411237/d0c734e2-79ad-43ad-a50b-c17ced608021)

💡 NOTE that “auto” and “desirable” are the ONLY available modes for PAgP

![image](https://github.com/psaumur/CCNA/assets/106411237/9eabb76a-1846-48d3-abb1-bd6898a432e7)

PAgP negotiations to form an ETHERCHANNEL


💡 AWS1(config-if-range)# channel-group 1 mode desirable.
Creating a port-channel interface Port-channel1

Shows up in the interface as “Port-channel1”

![image](https://github.com/psaumur/CCNA/assets/106411237/bc0c1190-9e39-4ea2-923c-b29e03e9d40a)

The “channel-group” number has to MATCH for member INTERFACES on the same SWITCH.

It DOESN’T have to MATCH the “channel-group” number on the OTHER SWITCH!

💡 (channel-group 1 on AWS1 can form an ETHERCHANNEL with channel-group 2 on DSW1)

---

LACP CONFIGURATION

![image](https://github.com/psaumur/CCNA/assets/106411237/ba4adcf6-dec5-456f-b8d7-ab4e6b722cbf)

💡 NOTE that “active” and “passive” are the ONLY available modes for LACP

![image](https://github.com/psaumur/CCNA/assets/106411237/0a314613-d398-49f1-a4d3-1b50fb96ab7d)

LACP negotiations for form an ETHERCHANNEL

The “channel-group” number has to MATCH for member INTERFACES on the same SWITCH.

It DOESN’T have to MATCH the “channel-group” number on the OTHER SWITCH!

💡 (channel-group 1 on AWS1 can form an ETHERCHANNEL with channel-group 2 on DSW1)

---

STATIC ETHERCHANNEL CONFIGURATION

![image](https://github.com/psaumur/CCNA/assets/106411237/92db26e7-21ae-40c6-89ee-abe0197ed8ad)

💡 NOTE that “on” is the ONLY available mode for STATIC ETHERCHANNEL

ON mode only works with ON Mode

ON + desirable = DOES NOT WORK)

ON + active = DOES NOT WORK

---

HOW TO MANUALLY CONFIGURE THE NEGOTIATION PROTOCOL

![image](https://github.com/psaumur/CCNA/assets/106411237/83ef9bc8-4bd4-4dd3-b28e-83439ba96860)

TWO OPTIONS: 

- LACP Protocol
- PAgP Protocol

(Above shows a protocol mismatch error because LACP does not support “desirable” - only PAgP does)

(“channel-group 1 mode active” works because LACP supports “active”)

---

AFTER CONFIGURING THE ETHERCHANNEL MODE

CONFIGURING THE PORT INTERFACE

![image](https://github.com/psaumur/CCNA/assets/106411237/c485cdf1-f0ed-44b8-8c91-c0553bf6d82d)

“show running-config” shows “interface Port-channel1” in the configuration

![image](https://github.com/psaumur/CCNA/assets/106411237/6adda3dd-6408-445f-bb3f-61847b3920b6)

💡 NOTE the PHYSICAL INTERFACES (g0/0-g0/3) were auto-configured by the Port-channel1 configuration!

---

IMPORTANT NOTES ABOUT ETHERCHANNEL CONFIGURATION

- Member INTERFACES must have matching CONFIGURATIONS
    - Same DUPLEX (Full / Half)
    - Same SPEED
    - Same SWITCHPORT mode (Access / Trunk)
    - Same allowed VLANs / Native VLAN (for TRUNK interfaces)

- If an INTERFACE’s configurations do NOT MATCH the others, it will be EXCLUDED from the ETHERCHANNEL

---

VERIFYING STATUS OF ETHERCHANNEL

💡 “show etherchannel summary”

![image](https://github.com/psaumur/CCNA/assets/106411237/9e0edb15-2806-4d51-afc9-ad67ed465a97)

NOTE information at bottom. (”SU” means S - Layer2 + U - in use)

Protocol = What protocol the Etherchannel is using (in this case, LACP)

“Ports” = the list of interfaces in the EtherChannel (P = bundled in port-channel)

OTHER FLAGS

![image](https://github.com/psaumur/CCNA/assets/106411237/23d92ae1-9cc6-4f3a-9ddf-2ead59705c1c)

“D” = Down

![image](https://github.com/psaumur/CCNA/assets/106411237/b1b3ce70-d9a6-4bd2-be4d-976077438c85)

Changing one of the Member interfaces using “switchport mode access” has made it different than the other members so it is now appearing as “s” = suspended

Another useful command

💡 “show etherchannel port-channel”

![image](https://github.com/psaumur/CCNA/assets/106411237/61731b0c-1cc5-4a7e-b92c-d0afbea0ac2d)

💡 “show spanning-tree” will show the single EtherChannel port interface

![image](https://github.com/psaumur/CCNA/assets/106411237/df0b9cc8-0448-4bbd-aefa-62fadf2b6089)

---

LAYER 3 ETHERCHANNELS

![image](https://github.com/psaumur/CCNA/assets/106411237/c553ad64-1d8e-4a2a-a741-3102c89dc030)

HOW TO CONFIGURE A LAYER 3 ETHERCHANNEL (from a clean configuration)

![image](https://github.com/psaumur/CCNA/assets/106411237/c4520b2f-1e3b-49b8-85b1-458cdb6fc865)

💡 “show running-config”

![image](https://github.com/psaumur/CCNA/assets/106411237/8638f32d-47c3-4c64-b68e-a9e2e0070ac9)

NOTE : No SWITCHPORT and NO IP INTERFACE.

Where do we configure the IP Address?  Directly on the PORT INTERFACE !

![image](https://github.com/psaumur/CCNA/assets/106411237/3ec55a24-1de5-44a7-926c-f85500042115)

![image](https://github.com/psaumur/CCNA/assets/106411237/f99ea2a6-82fb-494a-b80d-a171732d5786)

(”RU” - “R” = Layer 3, “U” = in use)

![image](https://github.com/psaumur/CCNA/assets/106411237/acfe62c5-6908-4782-9440-1f75f842c2c9)

---

COMMANDS LEARNED IN THIS CHAPTER
```
SW(config) port-channel load-balance *mode*
```
Configures the EtherChannel load-balancing method on a SWITCH 
```
SW# show etherchannel load-balance
```
Displays information about the load-balancing settings
```
SW(config-if)# channel-group *number* mode {desirable | auto | active | passive | on}
```
Configures an interface to be PART of an EtherChannel
```
SW# show etherchannel summary
```
Displays a summary of EtherChannels on a SWITCH
```
SW# show etherchannel port-channel
```
Displays information about the virtual port-channel interfaces on a SWITCH

![image](https://github.com/psaumur/CCNA/assets/106411237/6cae87f0-0226-40cc-92ba-b839c7a5ff53)
