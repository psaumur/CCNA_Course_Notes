# 51. DYNAMIC ARP INSPECTION

WHAT IS DYNAMIC ARP INSPECTION (DAI) ?

ARP REVIEW

- ARP is used to learn the MAC ADDRESS of another DEVICE with a known IP ADDRESS
    - For example, a PC will use ARP to learn the MAC ADDRESS of its DEFAULT GATEWAY to communicate with external NETWORKS
- Typically, it is a TWO MESSAGE EXCHANGE :  ARP REQUEST and ARP REPLY

GRATUITOUS ARP

- A GRATUITOUS ARP MESSAGE is an ARP REPLY that is sent without receiving an ARP REQUEST
- It is SENT to the BROADCAST MAC ADDRESS
- It allows other DEVICES to learn the MAC ADDRESS of the sending DEVICE without having to send ARP REQUESTS.
- Some DEVICES automatically send GARP MESSAGES when an INTERFACE is enabled, IP ADDRESS is changed, MAC address is changed, etc.

DYNAMIC ARP INSPECTION

- DAI is a SECURITY FEATURE of SWITCHES that is used to filter ARP MESSAGES received on  *UNTRUSTED PORTS*
- DAI only filters ARP MESSAGES. Non-ARP MESSAGES are NOT affected
- All PORTS are *UNTRUSTED*, by DEFAULT
    - Typically, all PORTS connected to other NETWORK DEVICES (SWITCHES, ROUTERS) should be configured as TRUSTED, while INTERFACES connected to END HOSTS should remain UNTRUSTED

![image](https://github.com/psaumur/CCNA/assets/106411237/02da32ef-654c-4755-abcd-ea8230df4029)

![image](https://github.com/psaumur/CCNA/assets/106411237/29744383-746e-47be-8220-ba1a641a7a11)

![image](https://github.com/psaumur/CCNA/assets/106411237/6848c2b5-e866-4023-9ad9-c18f63aa6bb5)

---

ARP POISONING (MAN IN THE MIDDLE)

- Similar to DHCP POISONING, ARP POISONING involved an ATTACKER manipulating TARGET’S ARP TABLES so TRAFFIC is sent to the ATTACKER
- To do this, the ATTACKER can send GRATUITOUS ARP MESSAGES using another DEVICE’S IP ADDRESS
- Other DEVICES in the NETWORK will receive the GARP and update their ARP TABLES, causing them to send TRAFFIC to the ATTACKER instead of the legitimate DESTINATION

![image](https://github.com/psaumur/CCNA/assets/106411237/aae80c8f-2673-4c04-a206-9b646f5c1f08)

DYNAMIC ARP INSPECTION OPERATIONS

- DAI inspects the SENDER MAC and SENDER IP fields of ARP MESSAGES received on UNTRUSTED PORTS and checks that there is a matching entry in the DHCP SNOOPING BINDING TABLE
    - If there is a MATCH, the ARP MESSAGE is FORWARDED
    - If there is NO MATCH, the ARP MESSAGE is DISCARDED

![image](https://github.com/psaumur/CCNA/assets/106411237/060f3d3a-b2fd-46a1-8b3c-7a6839985c87)

- DAI doesn’t inspect messages received on TRUSTED PORTS. They are FORWARDED as normal.

- ARP ACLs can be manually configured to map IP ADDRESSES / MAC ADDRESSES for DAI to check
    - Useful for HOSTS that don’t use DHCP
    
- DAI can be configured to perform more in-depth checks also - but these are optional

- Like DHCP SNOOPING, DAI also supports RATE-LIMITING to prevent ATTACKERS from overwhelming the SWITCH with ARP MESSAGES
    - DHCP SNOOPING and DAI both require work from the SWITCH’S CPU
    - Even if the ATTACKER’S messages are BLOCKED, they can OVERLOAD the SWITCH CPU with ARP MESSAGES

---

DYNAMIC ARP INSPECTION CONFIGURATION

![image](https://github.com/psaumur/CCNA/assets/106411237/4a91bd7b-626a-4d64-b69a-308d65bbdda4)

![image](https://github.com/psaumur/CCNA/assets/106411237/774765fa-4918-4cd9-bb64-57130968c359)

Command : `show ip arp inspection interfaces`

![image](https://github.com/psaumur/CCNA/assets/106411237/e64a568e-e5c6-442b-98f7-4fe829ff7519)

DAI RATE LIMITING

![image](https://github.com/psaumur/CCNA/assets/106411237/6400e059-2c8c-4369-827d-7774fddd57eb)

DAI OPTIONAL CHECKS

![image](https://github.com/psaumur/CCNA/assets/106411237/0e6b780a-16ef-466a-bfd3-8dd2cdace4ad)

![image](https://github.com/psaumur/CCNA/assets/106411237/1f109b81-9c9b-4acd-9557-0b652ba29b8d)

![image](https://github.com/psaumur/CCNA/assets/106411237/dd78740a-4f41-43aa-8ed2-3fa574acc0f9)

ARP ACLs (Beyond Scope of CCNA)

CREATE AN ARP ACL FOR SRV1

![image](https://github.com/psaumur/CCNA/assets/106411237/cf121a75-45b2-4e2d-a35f-320e3f5491fa)

AFTER APPLYING IT TO SWITCH 2, SRV1 is able to send ARP REQUEST to R1

![image](https://github.com/psaumur/CCNA/assets/106411237/582feed0-1915-4f59-b3b9-9db37854c6e1)

Command: `show ip arp inspection`

Shows a summary of the DAI configuration and statistics

![image](https://github.com/psaumur/CCNA/assets/106411237/684e694a-5b0a-4f85-b135-b288a8c4c6ec)

---

COMMAND REVIEW

![image](https://github.com/psaumur/CCNA/assets/106411237/4cb7dc28-b09d-4a98-8d43-aca2cdf6180b)
