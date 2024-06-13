# 9. SWITCH INTERFACES

![image](https://github.com/psaumur/CCNA/assets/106411237/5d0d80dc-74d1-4656-841c-fcaa2b89c760)


CISCO CLI for SWITCHES

![image](https://github.com/psaumur/CCNA/assets/106411237/e3947ef5-9100-426f-8d62-fd4ce5224351)


// enter Privileged EXEC mode

SW1>enable

// Show all interfaces of Switch 1.

SW# show ip interface brief

This will show the interfaces currently on Switch 1. It has the same information structure as Cisco Routers.

Notice the Status (Layer 2) and Protocol (Layer 1) columns are showing "up/up".

Unlike ROUTERS, SWITCHES do no DEFAULT to 'administrative down/down'(shutdown).

Unconnected devices will show as "down" and "down" (not connected to another device)

![image](https://github.com/psaumur/CCNA/assets/106411237/e0fdc339-21d9-4313-b7d8-78303a7ba1ea)


// Show the status of all interfaces on SW1

SW1#show interfaces status

This will list:

- Ports
- Name (which is description)
- Status (connection status)
- Vlan (can be used to divide up LANs) - Vlan 1 is the default.
- Duplex (can the connection send/receive at same time?) - Auto is default
- Speed (speed in bps) - Auto is default
- Type (what medium is being used, speed of interface)

---

![image](https://github.com/psaumur/CCNA/assets/106411237/12a33be7-795f-467a-87a4-42c5b218960b)


![image](https://github.com/psaumur/CCNA/assets/106411237/7b5953f7-77d3-4826-8efc-072498a7f9c0)


---

INTERFACE RANGE

Unused Interfaces can pose a security risk so it's a good idea to deactivate them.

However, if you have 28+ interfaces not in use, do you have to do them one at a time?

Answer: No! There is a command to apply configurations to a range of interfaces.

Inside Global Config Mode (config t):

![image](https://github.com/psaumur/CCNA/assets/106411237/06e2e267-1e07-48a1-8c8c-8edbd5bd48ae)


SW1(config)#interface range f0/5 - 12   // Choose all interfaces from 0/5 to 0/12

SW1(config-if-range)#description ## not in use ##

SW1(config-if-range)#shutdown

<< this will list all the interfaces being set to administratively down >>

Confirm with 'show interface status' in Privileged EXEC mode or if in CONFIG mode, use 'do show interface status'

![image](https://github.com/psaumur/CCNA/assets/106411237/8d1d49d3-e000-4570-ab7e-b994b959ebd5)

---

FULL / HALF DUPLEX

HALF DUPLEX:

- Device cannot send / receive data at the same time. If it is receiving a frame, it must wait before sending a frame.

FULL DUPLEX:

- Device CAN send / receive data at the same time. It does NOT have to wait.

MOST modern SWITCHES support FULL DUPLEX.

---

WHERE is HALF DUPLEX used? Almost nowhere.

In the past, LAN HUBS used HALF DUPLEX.

When multiple packets were received by the HUB, the HUB would simple FLOOD the connections with frame data, causing a COLLISION (on the interface), and hosts would not receive the frame  intact.

All devices connected to a HUB are called a COLLISION DOMAIN.

To DEAL with COLLISIONS, Ethernet devices use a mechanism called CSMA/CD.

CSMA/CD = CARRIER SENSE MULTIPLE ACCESS with COLLISION DETECTION.

- Before sending frames, devices 'listen' to the collision domain until they detect that other devices are not sending.
- IF a collision occurs, the device sends a jamming signal to inform the other devices that a collision happened.
- Each device will wait a random period of time before sending frames again.
- The process repeats.

---

SWITCHES are more sophisticated than HUBS.

HUBS are Layer 1 Devices - Collisions are common and use CSMA/CD.
SWITCHES are Layer 2 Devices - Collisions RARELY occur.

---

![image](https://github.com/psaumur/CCNA/assets/106411237/feff3816-1449-4282-bc44-71575333a1e0)


SPEED / DUPLEX AUTONEGOTIATION

- Interfaces that can run at different speeds (10/100 or 10/100/1000) have a default setting of SPEED AUTO and DUPLEX AUTO.
- Interfaces 'advertise' their capabilities to the neighbouring device, and they negotiate the best SPEED and DUPLEX settings they are both capable of.

WHAT if AUTONEGOTIATION is DISABLED on the device connected to the SWITCH ?

![image](https://github.com/psaumur/CCNA/assets/106411237/30519cf7-0a79-4996-a8d8-dfac689f4005)


- SPEED: The SWITCH will try to send at the speed that the other device is operating at.
If it fails to send the speed, it will use the slowest supported speed (ie: 10 Mbps on a 10/100/1000 interface).
- DUPLEX: If the speed is 10 or 100 Mbps the SWITCH will use HALF DUPLEX.
If the speed is 1000 Mbps or great, it will use FULL DUPLEX.

---

INTERFACE COUNTERS AND ERRORS

Show using the:

// Privileged EXEC mode

SW1#show interfaces <interface name>

Error stats will be at the bottom.

![image](https://github.com/psaumur/CCNA/assets/106411237/20d6affd-6014-427d-9ad9-c638ace358f8)


**Packets Received / Total bytes received.**

**Runts**: Frames that are smaller than the minimum frame size (64 bytes)

**Giants**: Frames that are larger than the maximum frame size (1518 bytes)

**CRC**: Frames that failed the CRC check (in the Ethernet FCS trailer)

**Frame**: Frames that have an incorrect format (due to an error)

**Input errors**: Total of various counters, such as the above four

**Output errors**: Frames the SWITCH tried to send, but failed due to an error
