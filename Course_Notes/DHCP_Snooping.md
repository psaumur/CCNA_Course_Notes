# 50. DHCP SNOOPING (LAYER 2)

WHAT IS DHCP SNOOPING?

- DHCP SNOOPING is a security feature of SWITCHES that is used to filter DHCP messages received on UNTRUSTED PORTS
- DHCP SNOOPING only filters DHCP MESSAGES.
    - Non-DHCP MESSAGES are not affected
- All PORTS are UNTRUSTED, by DEFAULT
    - Usually UPLINK PORTS are configured as TRUSTED PORTS, and DOWNLINK PORTS remain UNTRUSTED
    

![image](https://github.com/psaumur/CCNA/assets/106411237/9ed71d09-d94c-4fc9-ad87-1b31acfdd132)

![image](https://github.com/psaumur/CCNA/assets/106411237/9d7d23a6-9d54-4234-a07e-a5caea136c94)

---

ATTACKS ON DHCP

DHCP STARVATION

- An example of a DHCP-based ATTACK is a DHCP STARVATION ATTACK
- An ATTACKER uses spoofed MAC ADDRESSES to flood DHCP DISCOVER messages
- The TARGET server’s DHCP POOL becomes full, resulting in a DoS to other DEVICES

![image](https://github.com/psaumur/CCNA/assets/106411237/33dfbb8b-2b78-4700-b4ab-0dd95fc03eed)

DHCP POISONING (Man-in-the-Middle)

- Similar to ARP POISONING, DHCP POISONING can be used to perform a Man-in-the-Middle ATTACK
- A *spurious DHCP SERVER* replies to CLIENTS’ DHCP Discover messages and assigns them IP ADDRESSES but makes the CLIENTS use the *spurious SERVER’S IP* as a DEFAULT GATEWAY

** CLIENTS usually accept the first DHCP OFFER message they receive

- This will cause the CLIENT to send TRAFFIC to the ATTACKER instead of the legitimate DEFAULT GATEWAY
- The ATTACKER can then examine / modify the TRAFFIC before forwarding it to the legitimate DEFAULT GATEWAY

![image](https://github.com/psaumur/CCNA/assets/106411237/d0cd7a5c-9ff4-4ab7-bec6-4edec4ea2646)

![image](https://github.com/psaumur/CCNA/assets/106411237/1573bcb7-6fa8-46d7-8cb8-46e30bac559d)

---

DHCP MESSAGES

- When DHCP SNOOPING filters messages, it differentiates between DHCP SERVER messages and DHCP CLIENT messages

- Messages sent by DHCP SERVERS:
    - OFFER
    - ACK
    - NAK = Opposite of ACK - used to DECLINE a CLIENT’S REQUEST
- Messages sent by DHCP CLIENTS:
    - DISCOVER
    - REQUEST
    - RELEASE = Used to tell the SERVER that the CLIENT no longer needs its IP ADDRESS
    - DECLINE = Used to DECLINE the IP ADDRESS offered by a DHCP SERVER

---

HOW DOES IT WORK?

- If a DHCP MESSAGE is received on a TRUSTED PORT, forward it as normal without inspection
- If a DHCP MESSAGE is received on an UNTRUSTED PORT, inspect it and act as follows:
    - If it is a DHCP SERVER message, discard it
    - If it as a DHCP CLIENT message, perform the following checks:
        - DISCOVER / REQUEST messages :
            - Check if the FRAME’S SOURCE MAC ADDRESS and the DHCP MESSAGE’S CHADDR FIELDS match.
                - MATCH = FORWARD
                - MISMATCH = DISCARD
        - RELEASE / DECLINE messages:
            - Check if the PACKET’S SOURCE IP ADDRESS and the receiving INTERFACE match the entry in the *DHCP SNOOPING BINDING TABLE*
                - MATCH = FORWARD
                - MISMATCH = DISCARD
    
- When a CLIENT successfully leases an IP ADDRESS from a SERVER, create a new entry in the *DHCP SNOOPING BINDING TABLE*

---

DHCP SNOOPING CONFIGURATION

![image](https://github.com/psaumur/CCNA/assets/106411237/729466dc-9432-47d2-8799-652fa064b058)

SWITCH 2’s CONFIGURATION

![image](https://github.com/psaumur/CCNA/assets/106411237/8d6cacb8-ffd8-4cf0-bd96-fe9978377989)

SWITCH 1’s CONFIGURATION

![image](https://github.com/psaumur/CCNA/assets/106411237/bb11e4fd-a340-4dd3-a6f5-3cd280fc5a13)

DHCP SNOOPING RATE-LIMITING

- DHCP SNOOPING can limit the RATE at which DHCP messages are allowed to enter an INTERFACE
- If the RATE of DHCP messages crosses the configured LIMIT, the INTERFACE is `err-disabled`
- Like with PORT SECURITY, the interface can be manually re-enabled, or automatically re-enabled with `errdisable recovery`

![image](https://github.com/psaumur/CCNA/assets/106411237/6586df19-5a58-4ca3-a316-bd0aeb2ce67c)

- You wouldn’t set the limit rate to 1 since it’s so low, it would shut the port immediately but this shows how RATE-LIMITING works

`errdisable recovery cause dhcp-rate-limit`

![image](https://github.com/psaumur/CCNA/assets/106411237/83c324aa-baa0-4ae1-82ac-157e503e048a)

DHCP OPTION 82 (INFORMATION OPTION)

- OPTION 82, also known as a ‘DHCP RELAY AGENT INFOMRATION OPTION’ is one of MANY DHCP OPTIONS
- It provides additional information about which DHCP RELAY AGENT received the CLIENT’S message, on which INTERFACE, in which VLAN, etc.
- DHCP RELAY AGENTS can add OPTION 82 to message they forward to the remote DHCP SERVER
- With DHCP SNOOPING enabled, by default Cisco SWITCHES will add OPTION 82 to DHCP messages they receive from CLIENTS, even if the SWITCH isn’t acting as a DHCP RELAY AGENT
- By DEFAULT, Cisco SWITCHES will drop DHCP MESSAGES with OPTION 82 that are received on an UNTRUSTED PORT

![image](https://github.com/psaumur/CCNA/assets/106411237/2efc6edd-21fd-4c1a-bb11-9c1f761e1d32)

THIS command disables OPTION 82 for SW1 but NOT SW2 

![image](https://github.com/psaumur/CCNA/assets/106411237/84f1c3f2-9ad1-4367-97f3-95dab053b30c)

TRAFFIC gets passed to R1 and is DROPPED because of “inconsistent relay information” (packet contains OPTION 82 but wasn’t dropped by SW2)

![image](https://github.com/psaumur/CCNA/assets/106411237/5c4b547e-c588-4d62-8098-76902199a131)

By ENABLING OPTION 82 on both SWITCHES…

![image](https://github.com/psaumur/CCNA/assets/106411237/dda50cf6-ae86-47ec-9b4f-104669697f64)

PC1’s DHCP DISCOVER message gets passed, through SW1 and SW2, to R1.
R1 responds with an DHCP OFFER message, as normal

![image](https://github.com/psaumur/CCNA/assets/106411237/7e59cc5a-bf8e-482d-848d-5bfa0540c74b)

---

COMMAND SUMMARY

![image](https://github.com/psaumur/CCNA/assets/106411237/308e32fa-52bd-4ee4-9356-f14e65416e17)
