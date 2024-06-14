# 2. INTERFACES AND CABLES

SWITCHES provide many PORTS for connectivity (usually 24)

These PORTS tend to be RJ-45 (Registered Jack) ports.

---

WHAT IS ETHERNET?

- Ethernet is a collection of network protocols/standards.

Why do we need network protocols and standards?

- provide common communication standards over networks.
- provide common hardware standards to allow connectivity between devices.



Connections between devices operates at a set speed.

These speeds are measured in "bits per second" (bps)

A bit is a value of "0" or "1".
A byte is 8 bits (0s and 1s)

| Size | # of Bits |
| --- | --- |
| 1 kilobit (Kb) |  1,000 |
| 1 megabit (Mb) | 1,000,000 |
| 1 gigabit (Gb) | 1,000,000,000 |
| 1 terabit (Tb) | 1,000,000,000,000  |

Ethernet standards are:

- Defined in the IEEE 802.3 standard in 1983
- IEEE = Institute of Electrical and Electronics Engineers

ETHERNET STANDARDS (COPPER)

| Speed | Common Name | Standard | Cable Type | Max Transmission Distance |
| --- | --- | --- | --- | --- |
| 10 Mbps | Ethernet | 802.3i | 10BASE-T | 100m Max |
| 100 Mbps | Fast Ethernet | 802.3u | 100BASE-T | 100m Max |
| 1 Gbps | Gigabit Ethernet | 802.3ab | 1000BASE-T | 100m Max |
| 10 Gbps | 10 Gigabit Ethernet | 802.3an | 10GBASE-T | 100m Max |

BASE = refers to Baseband Signaling

T = Twisted Pair 

Most Ethernet uses copper cables.

UTP or Unshielded Twisted Pair
(no metallic shield)
Twist protects against EMI (Electromagnetic Interference)

Most use 8 wires (4 pairs) however ...

10/100BASE-T = 2 pairs (4 wires)

![image](https://github.com/psaumur/CCNA/assets/106411237/00b27997-a78a-4e81-a878-7f8ab7e3279e)


---

How do devices communicate via their connections?

Each ethernet cable has a RJ-45 plug with 8 pins on the ends.

![image](https://github.com/psaumur/CCNA/assets/106411237/323930c9-3387-4bf9-aae1-f61db0fd9c04)


- PCs Transmit(TX) data on Pins #1-2
- Switches Receive(RX) data on Pins #1-2
- PCs Receive(RC) data on Pins #3,6
- Switches Transmit(TX) data on Pins #3,6

This allows Full-Duplex transmission of data.

---

What if a Router / Switch connect?

![image](https://github.com/psaumur/CCNA/assets/106411237/907259d9-1837-4d53-8f45-a42934fb66f2)


- Routers Transmit(TX) data on Pins #1-2
- Routers Receive(RX) data on Pins #3,6
- Switches Transmit(TX) data on Pins #3,6
- Switches Receive(RX) data on Pins #1-2

Routers and PCs connect the same way with Switches.

The cable used to connect is called a "Straight-Through" cable.

---

What if we want to connect similar devices to each other?

We CANNOT use a "Straight-Through" cable.
We MUST use a "Crossover" cable.

This cable swaps the pins on one end to allow connection to work.

![image](https://github.com/psaumur/CCNA/assets/106411237/d98646ad-366f-4e96-8c6f-f6b5f32f9bdc)


PIN#1 -----> PIN#3
PIN#2 -----> PIN#6

PIN#3 -----> PIN#1
PIN#6 -----> PIN#2

---

| DEVICE TYPE | TRANSMIT (TX) PINS | RECEIVE (RX) PINS |
| --- | --- | --- |
| ROUTER | 1 and 2 | 3 and 6 |
| FIREWALL | 1 and 2 | 3 and 6 |
| PC | 1 and 2 | 3 and 6 |
| SWITCH | 3 and 6 | 1 and 2 |

---

Most modern equipment now has AUTO MDI-X which **automatically detects** which pins their neighbour is transmitting on and adjust the pins they receive data on.

1000BASE-T/10GBASE-T = 4 pairs (8 wires)

Each wire pair is **bidirectional** so can transmit/receive much faster than 10/100BASE-T.

![image](https://github.com/psaumur/CCNA/assets/106411237/763c841a-d7b5-4e87-8500-b54d623af620)


---

Fiber-Optic Connections:

- Defined in the IEEE 802.3ae standard

SFP Transceiver (Small Form-Factor Pluggable) allows fiber-optic cables to connect to switches/routers.

- Have separate cables to transmit / receive.

4 parts to a fiber-optic cable.

![image](https://github.com/psaumur/CCNA/assets/106411237/70b81cde-265f-413b-815b-3e7184ea0586)


There are TWO types of fiberoptic cable.

Single-Mode:

![image](https://github.com/psaumur/CCNA/assets/106411237/d9a4b633-44c2-491d-92e4-329dd3b9074b)


- Narrower than multimode
- Lighter enters at a single angle (mode) from a laser-based transmitter.
- Allows longer cables than both UTP and multimode fiber.
- More expensive than multimode fiber (due to more expensive laser-based SFP transmitters)

Multimode:

![image](https://github.com/psaumur/CCNA/assets/106411237/e73ec4d0-9aa1-4a75-848c-3af70e770dce)


- Core is wider than Single-mode
- Allows multiple angles (modes) of light waves to enter core
- Allows longer cables than UTP but shorter than single-mode
- Cheaper than single-mode fiber (due to cheaper LED-based SFP transmitter)

---

Fiber Optic Standards:

| Speed | Standard | Connection Speed | Mode Support | Max Transmission Distance |
| --- | --- | --- | --- | --- |
| 1000BASE-LX | 802.3z | 1 Gbps | Multimode / Single | 550 meters (Multi)  / 5km (Single) |
| 10GBASE-SR | 802.3ae | 10 Gbps | Multimode | 400 meters |
| 10GBASE-LR | 802.3ae | 10 Gbps | Single | 10 kilometers |
| 10GBASE-ER | 802.3ae | 10 Gbps | Single | 30 kilometers |

---

UTP vs Fiber-Optic Cabling:

UTP are:

- Lower cost than fiber-optic.
- Shorter maximum distance than fiber-optic (~100m).
- Can be vulnerable to EMI (Electromagnetic Interference).
- RJ45 ports used with UTP are cheaper than SFP ports.
- Emit (leak) a faint signal outside of cable, which can be copied (security risk).

Fiber-Optic:

- Higher cost than UTP.
- Longer maximum distance than UTP.
- No vulnerability to EMI.
- SFP ports are more expensive than RJ45 ports (single-mode is more expensive than multimode).
- Does not emit any signal outside of the cable (no security risk).
