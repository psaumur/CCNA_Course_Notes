# 17. VLANS : PART 2

Basic VLAN topology from PART 1

![image](https://github.com/psaumur/CCNA/assets/106411237/f6df37e0-d494-4e46-b6e8-6d2ba0cd0ff6)


What about THIS Network Topology ?

![image](https://github.com/psaumur/CCNA/assets/106411237/e6aff877-3792-469f-8955-0f3e17c6f1ed)


Notice this one has TWO Switches (SW1 and SW2) and ENGINEERING (VLAN 10) has two separate locations on the network.

---

TRUNK PORTS

- In a small network with few VLANS, it’s possible to use a separate interface for EACH VLAN when connecting SWITCHES to SWITCHES, and SWITCHES to ROUTERS

- HOWEVER, when the number of VLANS increases, this is not viable. It will result in wasted interfaces, and often ROUTERS won’t have enough INTERFACES for each VLAN

- You can use TRUNK PORTS to carry traffic from multiple VLANS over a single interface

A TRUNK PORT carrying multiple VLAN connections over single interface

![image](https://github.com/psaumur/CCNA/assets/106411237/5cb7c933-689a-499b-9f30-51fe63d8b059)


![image](https://github.com/psaumur/CCNA/assets/106411237/8ea9a799-cf0d-4b1d-9706-db002772fe6d)


How does a packet know WHICH VLAN to send traffic to over the TRUNK PORT ?

VLAN TAGS !

SWITCHES will “tag” all frames that they send over a TRUNK LINK. This allows the receiving SWITCH to know which VLAN the frame belongs to.

TRUNK PORT = “Tagged” ports

ACCESS PORT = “Untagged” ports

---

VLAN TAGGING

- There are TWO main TRUNK protocols:
    - ISL (Inter-Switch Link)
    - IEEE 802.1Q (also known as “dot1q”)

ISL is an old Cisco proprietary protocol created before industry standard IEEE 802.1Q

IEEE 802.1Q is an industry standard protocol created by the IEEE (Institute of Electrical and Electronics Engineers)

You will probably NEVER use ISL in the real world; even modern Cisco equipment doesn’t use it.

For the CCNA, you will only need to learn 802.1Q

---

ETHERNET HEADER with 802.1Q

![image](https://github.com/psaumur/CCNA/assets/106411237/00e817cd-1cac-44c5-a5f6-5459d383236d)


- The 802.1Q TAG Is inserted between the SOURCE and TYPE/LENGTH fields in the ETHERNET FRAME
- The TAG is 4 bytes (32 bits) in length
- The TAG consists of TWO main fields:
    - Tag Protocol Identifier (TPID)
    - Tag Control Information (TCI)
        - TCI consists of THREE sub-fields:

![image](https://github.com/psaumur/CCNA/assets/106411237/8e52856b-58b9-448e-a007-254973fe707e)


TPID (TAG Protocol Identifier) :

- 16 bits (2 bytes) in length
- Always set to a value of 0x8100. This indicates that the frame is 802.1Q TAG

TCI / PCP (Priority Code Point) :

- 3 bits in length
- Used for Class of Service (CoS), which prioritizes important traffic in congested networks

TCI / DEI (Drop Eligible Indicator) :

- 1 bit in length
- Used to indicated frames that can be dropped if the network is congested

TCI / VID (VLAN ID) :

- 12 bits in length
- Identifies the VLAN the frame belongs to
- 12 bits in length = 4096 total VLANS (2^12), range of 0 - 4095
- VLANs 0 and 4095 are reserved and can’t be used
- Therefore, the actual range of VLANs is 1 - 4094

NOTE : Cisco’s ISL also had a VLAN range of 1 - 4094

---

VLAN RANGES

![image](https://github.com/psaumur/CCNA/assets/106411237/1c55a830-bfdd-423a-9688-334a3dd2bfa3)


---

NATIVE VLAN

![image](https://github.com/psaumur/CCNA/assets/106411237/8b1e09a1-e9c5-410e-ad87-581b95eaca81)


![image](https://github.com/psaumur/CCNA/assets/106411237/f8145795-b3f7-4766-9507-4fba7c743a14)


![image](https://github.com/psaumur/CCNA/assets/106411237/a1811276-c043-4035-9957-800873068615)

---

TRUNK CONFIGURATION

![image](https://github.com/psaumur/CCNA/assets/106411237/d73b8f0b-2154-4e7f-8057-7c5b3f5078cc)


![image](https://github.com/psaumur/CCNA/assets/106411237/29313a87-cf16-439c-8a9e-90b518326954)

Many modern switches do not support Cisco’s ISL at all. They only support 802.1Q (dot1q)

However, SWITCHES that do support both (like the one I am using in this example) have a TRUNK encapsulation of “AUTO” by default

To MANUALLY configure the INTERFACE as a TRUNK PORT, you must first set the encapsulation to “802.1Q” or “ISL”. On SWITCHES that only support 802.1Q, this is not necessary

After you set the encapsulation type, you can then configure the interface as a TRUNK

1) Select the interface to configure

2) Use “#switchport trunk encapsulation dot1q” to set the encapsulation mode to 802.1Q

3) Use “#switchport mode trunk” to manually configure the interface to TRUNK

![image](https://github.com/psaumur/CCNA/assets/106411237/6b897fb0-14a3-4e6a-b4e8-e278a6aec08e)


Use the “#show interfaces trunk” command to confirm INTERFACES on TRUNK

![image](https://github.com/psaumur/CCNA/assets/106411237/d3e144c7-90e3-4ab0-8021-7eb4d1420282)


Commands to allow a VLAN on a given TRUNK

![image](https://github.com/psaumur/CCNA/assets/106411237/6a60f6ce-55be-4df5-a715-b871e5e461f4)


![image](https://github.com/psaumur/CCNA/assets/106411237/b39b091d-1ea9-4f72-b592-1eeb8ef25f90)


Command to change the NATIVE VLAN

![image](https://github.com/psaumur/CCNA/assets/106411237/5109becb-27dd-4c63-9c7b-74b6f55e9d5f)


![image](https://github.com/psaumur/CCNA/assets/106411237/36abc437-69cb-4c56-8a59-87479ce01a7f)


---

Setting up our TRUNKS for this Network

![image](https://github.com/psaumur/CCNA/assets/106411237/892b5322-807b-4d76-91cb-a039766794c5)


We will need to configure :

SW1 : g0/0 interface (already configure above this section)

SW2: g0/0, and g0/1 interface

SW2 g0/0

![image](https://github.com/psaumur/CCNA/assets/106411237/7b313959-b710-4bb6-a281-727ec9477c3e)


SW2 g0/1

![image](https://github.com/psaumur/CCNA/assets/106411237/c26f17c8-0ec9-4406-ab66-83adf28c8550)


What about the ROUTER, R1 ? 

---

ROUTER ON A STICK (ROAS)

![image](https://github.com/psaumur/CCNA/assets/106411237/66c4ace0-8341-4c9c-8ff5-7c171034df53)


![image](https://github.com/psaumur/CCNA/assets/106411237/b409165d-39e6-4fba-ade1-2451f7e2fa8c)


![image](https://github.com/psaumur/CCNA/assets/106411237/112a2089-5a9e-4b13-945c-6be7f188d6a8)


NOTE the Sub-Interface names (like the network diagram) of 0.10, 0.20 and 0.30

You assign them IP addresses identically like you would a regular interface (using the last usable IP address of a given VLAN subnet)

Sub-interfaces will appear with the “show ip interface brief” command

![image](https://github.com/psaumur/CCNA/assets/106411237/9b7ecbd1-c5f4-4ed0-9988-8fd17e16c9ae)


They also appear in the “show ip route” command (Route Table)

![image](https://github.com/psaumur/CCNA/assets/106411237/1e9bb3fa-5aca-4883-8aff-52a554dcfba6)


ROAS is used to route between multiple VLANs using a SINGLE interface on a ROUTER and SWITCH

The SWITCH interface is configured as a regular TRUNK

The ROUTER interface is configured using SUB-INTERFACES. You configure the VLAN tag and IP address on EACH SUB-INTERFACE

The ROUTER will behave as if frames arriving with a certain VLAN tag have arrived on the SUB-INTERFACE configured with that VLAN tag

The ROUTER will TAG frames sent out of EACH SUB-INTERFACE with the VLAN TAG configured on the SUB-INTERFACE
