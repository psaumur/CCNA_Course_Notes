# 33. IPv6 : PART 3

CORRECTION TO PRIOR LECTURES:

RFC Requirements for IPv6 Address Representation

- Leading 0s MUST be removed
    - This - 2001 : 0db8 : 0000 : 0001 : 0f2a : 4fff : fea3 : 00b1
    - Becomes - 2001 : db8 : 0 : 1 : f2a : 4fff : fea3 : b1
- :: MUST be used to shorten the longest string of all-0 quartets
    - If there is only ONE all-0 quartet, don’t use ‘::’
    - This - 2001 : 0000 : 0000 : 0000 : 0f2a : 0000 : 0000 : 00b1
    - Becomes - 2001 :: f2a : 0 : 0 : b1
- If there are two equal-length choices for the :: , use :: to the shorten the one on the LEFT
    - This - 2001 : 0db8 : 0000 : 0000 : 0f2a : 0000 : 0000 : 00b1
    - Becomes - 2001 : db8 :: f2a : 0 : 0 : b1
- Hexadecimal characters ‘a’, ‘b’, ‘c’, ‘d’, ‘e’, and ‘f’ MUST be written using lower-case, NOT upper case A B C D E F

---

IPv6 HEADER

![image](https://github.com/psaumur/CCNA/assets/106411237/5bba7262-60aa-4348-9b7a-55dc354f4ed3)

Length is ALWAYS 40 bytes (Fixed Header)

Version (4 bits)

- Indicates version of IP used
- Fixed value of ‘6’ (0b0110) to indicate IPv6

Traffic Class (8 bits)

- Used for QoS (Quality of Service) to indicate high-priority traffic
- Example: IP phone traffic, live video calls, etc.

Flow Label (20 bits)

- Identifies specific traffic “flows” (communication between Source and Destination)

Payload Length (16 bits)

- Indicates the LENGTH of the PAYLOAD (the encapsulation LAYER 4 SEGMENT) **in bytes**
- The length of the IPv6 header, itself, isn’t included, because it’s ALWAYS 40 bytes

Next Header (8 bits)

- Indicates the TYPE of the ‘next header’ (header of the encapsulated SEGMENT)
    - Example: TCP or UDP
- Same function as the IPv4 header’s ‘Protocol’ field

Hop Limit (8 bits)

- Value in this field decrements by 1 every time a ROUTER forwards it. If it reaches ‘0’, the PACKET is discarded (similar to IPv4 TTL field )

Source Address (128 bits)

- Packet’s SOURCE address

Destination Address (128 bits)

- Packet’s DESTINATION address

---

SOLICITED-NODE MULTICAST ADDRESS

- An IPv6 SOLICITED-NODE Multicast Address is calculated from a UNICAST ADDRESS

How to generate a SOLICITED-NODE Multicast Address

![image](https://github.com/psaumur/CCNA/assets/106411237/eef6815b-405b-485d-884d-ff08bbbf16d3)

Note the automatically joined group addresses for this IPv6 Interface

![image](https://github.com/psaumur/CCNA/assets/106411237/4f981645-7488-4f0c-8ec5-d7c1b878acba)

---

NEIGHBOR DISCOVERY PROTOCOL (NDP)

- NEIGHBOR DISCOVERY PROTOCOL (NDP) is a PROTOCOL used with IPv6
- It has various functions and one of those functions is to replace ARP, which is no longer used in IPv6
- The ARP-like function of NDP uses ICMPv6 and SOLICITED-MODE Multicast Addresses to learn the MAC ADDRESS of other HOSTS (ARP in IPv4 uses Broadcast Messages)

- TWO MESSAGES types are used:
    - 1) NEIGHBOR SOLICITATION (NS)
        - ICMPv6 Type 135
    
    - 2) NEIGHBOR ADVERTISEMENT (NA)
        - ICMPv6 Type 136

![image](https://github.com/psaumur/CCNA/assets/106411237/88b9dde5-bc94-49ce-ba4a-b38c47f4670d)

![image](https://github.com/psaumur/CCNA/assets/106411237/cc9010cb-eb67-4fcb-8c6a-7a0aa11c7057)

IPv6 NEIGHBOR TABLE

![image](https://github.com/psaumur/CCNA/assets/106411237/085bb9df-8015-4c2f-bfc8-2d6336436fe2)

- Another function of NDP allows HOSTS to automatically discover ROUTERS on the LOCAL NETWORK

- TWO MESSAGES are used for this process:
  
    - ROUTER SOLICITATION (RS)
        - ICMPv6 Type 133
        - Sent to Multicast Address `FF02::2` (All Routers)
        - Asks ALL ROUTERS on the Local Link to identify themselves
        - Sent when an INTERFACE is enabled / HOST is connected to the NETWORK
        
    - ROUTER ADVERTISEMENT (RA)
        - ICMPv6 Type 134
        - Sent to Multicast Address `FF02::1` (All Nodes)
        - The ROUTER announces its presence, as well as other information about the link
        - These messages are sent in response to RS messages
        - They are also sent periodically, even if the ROUTER hasn’t received an RS
        
    
![image](https://github.com/psaumur/CCNA/assets/106411237/f7861fda-e893-4fd1-b5c3-5deed57de2f0)
    

---

SLAAC

- Stands for **STATELESS ADDRESS AUTO-CONFIGURATION**
- HOSTS use the RS / RA messages to learn the IPv6 Prefix of the LOCAL LINK (ie: 2000:db8:: /64) and then automatically generate an IPv6 Address
- Using the `ipv6 address prefix / prefix-length eui-64` command, you need to manually enter the prefix
- Using the `ipv6 address autoconfig` command, you DON’T need to enter the prefix. The device uses NDP to learn the prefix used on the local link
- The device will use EUI-64 to generate the INTERFACE ID or it will be randomly generated (depending on the device / maker)

![image](https://github.com/psaumur/CCNA/assets/106411237/e1cc9b26-1a81-48fb-8538-77f97d456eff)

---

DUPLICATE ADDRESS DETECTION (DAD)

- One final point about NDP!
- Duplicate Address Detection (DAD) allows HOSTS to check if other devices on the Local Link are using the same IPv6 Address
- Any time an IPv6-enabled interface initializes (`no shutdown` command) or an IPv6 ADDRESS is configured on an INTERFACE (by any method: manual, SLAAC, etc.) it performs DAD
- DAD uses TWO MESSAGES you learned earlier : NS and NA
- The HOST will send an NS to its own IPv6 ADDRESS.
    - If it doesn’t get a reply, it KNOWS the ADDRESS is unique
    - If it DOES get a reply, it means ANOTHER HOST on the NETWORK is already using that ADDRESS

---

IPv6 STATIC ROUTING

- IPv6 ROUTING works the same as IPv4 ROUTING
- However, the TWO processes are separate on the ROUTER, and the TWO routing tables are separate, as well.
- IPv4 ROUTING is enabled BY DEFAULT
- IPv6 ROUTING is disabled BY DEFAULT
    - MUST BE ENABLED with the `ipv6 unicast-routing` command
- If IPv6 ROUTING is disabled, the ROUTER will be able to SEND and RECEIVE IPv6 traffic, but will not *route* IPv6 traffic (ie: will NOT FORWARD it between NETWORKS)

![image](https://github.com/psaumur/CCNA/assets/106411237/e082920f-3a76-438d-b43d-8eac968dcd55)

![image](https://github.com/psaumur/CCNA/assets/106411237/90acb6ca-2703-47d1-907f-1878490c78f6)

- A CONNECTED NETWORK ROUTE is automatically added for EACH CONNECTED NETWORK
- A LOCAL HOST ROUTE is automatically added for each ADDRESS configured on the ROUTER
- Routes for Link-Local ADDRESSES are not added to the ROUTING TABLE

![image](https://github.com/psaumur/CCNA/assets/106411237/d01849d3-c031-45a0-8e31-efd9dba61df6)

Everything is configured similar to normal static routes in IPv4

[AD] = Administrative Distance. You NEED this value in order to configure a STATIC ROUTE

DIRECTLY ATTACHED Static Route:

- Only the EXIT INTERFACE is specified
- `ipv6 route destination / prefix-length exit-interface`
- Example : `~~R1(config)# ipv6 route 2001:db8:0:3:: /64 g0/0~~`

<aside>
💡 In IPv6, you CANNOT use DIRECTLY ATTACHED Static Routes if the INTERFACE is an ETHERNET INTERFACE

</aside>

RECURSIVE Static Route:

- Only the Next-Hop is specified
- `ipv6 route destination / prefix-length next-hop`
- Example: `R1(config)# ipv6 route 2001:db8:0:3::/64 2001:db8:0:12::2`

FULLY SPECIFIED Static Route:

- Both the Exit Interface and Next Hop are specified
- `ipv6 route destination / prefix-length exit-interface next-hop`
- Example: `R1(config)# ipv6 route 2001:db8:0:3::/64 g0/0 2001:db8:0:12::2`

---

(NOTE THAT THESE ROUTES ARE ALL RECURSIVE : They specify the Next-Hop)

NETWORK ROUTE:

`R1(config)# ipv6 route 2001:db8:0::/64 2001:db8:0:12::2`

This is a route to R3/PC2 NETWORK via R2’s G0/0 INTERFACE

(We did this in Day 32’s Lab)

HOST ROUTE:

`R2(config)# ipv6 route 2001:db8:0:1::100/128 2001:db8:0:12::1`

`R2(config)# ipv6 route 2001:db8:0:3::100/128 2001:db8:0:23::2`

This is a route from R2 to PC1 and PC2 using the “next hop” ADDRESSES of R1 and R3 G0/0 INTERFACES

Note the /128 prefix. This is how SPECIFIC IPv6 ADDRESSES are written

DEFAULT ROUTE:

`R3(config)# ipv6 route ::/0 2001:db8:0:23::1`

::/0 is the IPv6 equivalent of 0.0.0.0/0 in IPv4

FLOATING STATIC ROUTES:

- Require you to increase the [AD] number HIGHER than the currently used NETWORK IGP AD value

LINK-LOCAL NEXT HOPS:

![image](https://github.com/psaumur/CCNA/assets/106411237/52cf09e2-2b37-4319-a2b9-15213524530c)

You HAVE to specify the INTERFACE name when using Link-Local Next-Hops

This is EXACTLY like a FULLY-SPECIFIED STATIC ROUTE
