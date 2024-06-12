# 5. ETHERNET LAN SWITCHING : PART 1

![image](https://github.com/psaumur/CCNA/assets/106411237/a40e81d9-c008-4fb4-8580-2eaf63003e63)

![image](https://github.com/psaumur/CCNA/assets/106411237/2db46525-98b8-4211-aeb3-efc34bd84222)


LAN's

- A LAN is a network contained in a relatively small area.
- Routers are used to connect separate LAN's

![image](https://github.com/psaumur/CCNA/assets/106411237/2a4de9d4-3408-49b9-9492-42b7eb56fe27)


An ETHERNET FRAME looks like:

![image](https://github.com/psaumur/CCNA/assets/106411237/ad579917-f9a0-4cd8-be25-351ecbfc87af)


Ethernet Trailer --- PACKET --- Ethernet Header

The Ethernet Header contains 5 Fields:

Preamble -- SFD -- Destination -- Source -- Type
7 bytes  -- 1 byte -- 6 bytes -- 6 bytes -- 2 bytes

---

PREAMBLE:

- Length: 7 bytes (56 bits)
- Alternating 1's and 0's
- 10101010 * 7x
- Allows devices to synchronize their receiver clocks

SFD : ‘Start Frame Delimiter’

- Length: 1 byte(8 bits)
- 10101011
- Marks end of the PREAMBLE and beginning of rest of frame.

---

DESTINATION AND SOURCE

- Layer 2 Address
- Indicates the devices sending / receiving the frame
- MAC = ’Media Access Control’
- = 6 byte (48-bit) address of the physical device

---

TYPE / LENGTH

- 2 bytes (16-bit) field
- A value of 1**500 or less** in this field indicates the LENGTH of the encapsulated packet (in bytes)
- A value of **1536 or greater** in this field indicates the TYPE of the encapsulated packet and length is determined via other methods.
- IPv4 = 0x0800 (hexadecimal) = 2048 in decimal
- IPv6 = 0x86DD (hexadecimal) = 34525 in decimal
- Layer 3 protocol used in the encapsulated Packet, which is almost always Internet Protocol (IP) version 4 or version 6.

---

The ETHERNET TRAILER contains:

FCS

- ‘FRAME CHECK SEQUENCE’
- 4 bytes (32 bits) in length
- Detects corrupted data by running a 'CRC' algorithm over the received data
- CRC = "Cyclic Redundancy Check"

---

Altogether the ETHERNET FRAME = 26 bytes (header + trailer)

![image](https://github.com/psaumur/CCNA/assets/106411237/c8c1a143-0675-4aa4-83bc-6031d10cc0b8)


---

MAC ADDRESS (48 bits long)

- 6-bytes (48-bits) physical address assigned to the device when it is made.
- AKA 'Burned-In Address' (BIA)
- Is globally unique
- First 3 bytes are the OUI (Organizationally Unique Identifier) which is assigned to the company making the device
- The last 3 bytes are unique to the device itself
- Written as 12 hexadecimal characters

Example:

E8:BA:70 // 11:28:74
OUI    // Unique Device ID

HEXADECIMAL

![image](https://github.com/psaumur/CCNA/assets/106411237/65a5e84a-b8db-46f5-b288-518139e99453)


INTERFACE NAMES

F0/1, F0/2, F0/3... F stands for "Fast Ethernet" or 100 Mbps interfaces.

---

MAC ADDRESS TABLE

Each Switch stores a DYNAMICALLY LEARNED MAC ADDRESS TABLE, using the SOURCE MAC ADDRESS of frames it receives.

![image](https://github.com/psaumur/CCNA/assets/106411237/582421a9-6351-48b7-bfe1-c2153520920c)


When a Switch doesn't know the DESTINATION MAC ADDRESS of a frame (UNKNOWN UNICAST FRAME), it is forced to FLOOD the frame - Forward the frame out of ALL it's interfaces, except the one it received the packet from.

When a KNOWN Unicast Frame is known (MAC Address is recognized by the entry in the MAC ADDRESS TABLE), the frame is FORWARDED like normal.

![image](https://github.com/psaumur/CCNA/assets/106411237/ff731ab3-fad2-4e10-9fa7-ce583a6a0bb2)

- Note: Dynamic MAC Addresses are removed from the MAC ADDRESS TABLE every 5 minutes of inactivity.
