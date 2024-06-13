# 40. SNMP (Simple Network Management Protocol)

SNMP OVERVIEW

- SNMP is an INDUSTRY-STANDARD FRAMEWORK and PROTOCOL that was originally released in 1988

These RFCs make up SNMPv1 (Do not need to memorize)

<aside>
💡 RFC 1065 - Structure and identification of management information for TCP/IP based internets

RFC 1066 - Management information base for network management of TCP/IP based internets

RFC 1067 - A simple network management protocol

</aside>

- Don’t let the ‘Simple’ in the name fool you !
- SNMP can be used to monitor the STATUS of DEVICES, make CONFIGURATION CHANGES, etc.
- There are TWO MAIN TYPES of DEVICES in SNMP:
    - MANAGED DEVICES
        - These are the DEVICES being managed using SNMP
            - Ex: ROUTERS, SWITCHES
    - NETWORK MANAGEMENT STATION (NMS)
        - The DEVICE / DEVICES managing the MANAGED DEVICES
        - THIS is the SNMP ‘SERVER’

---

SMNP OPERATIONS

![image](https://github.com/psaumur/CCNA/assets/106411237/bfa13793-5bc7-4344-8592-f38ef3a64784)

---

SMNP COMPONENTS

OVERVIEW

![image](https://github.com/psaumur/CCNA/assets/106411237/632a83c5-27c8-4adc-8b08-079030c5f52c)

NMS

![image](https://github.com/psaumur/CCNA/assets/106411237/aa59534d-01d5-404c-bdf6-e0fd92cf9d98)

MANAGED DEVICES

![image](https://github.com/psaumur/CCNA/assets/106411237/656e27b1-86a4-42c7-a1a1-94309aa19610)

SNMP OIDs

- SNMP Object IDs are ORGANIZED in a HIERARCHICAL STRUCTURE

![image](https://github.com/psaumur/CCNA/assets/106411237/79180299-7d9a-4607-a592-7e7d8d090cd1)

---

SNMP VERSIONS

- Many versions of SNMP have been proposed/developed, however, only three major versions have achieved wide-spread use:

- **SNMPv1**
    - The ORIGINAL version of SNMP
- **SNMPv2c**
    - Allows the NMS to retrieve LARGE AMOUNTS of information in a SINGLE REQUEST, so it is more efficient
    - ‘c’ refers to the ‘community strings’ used as PASSWORDS in SNMPv1, removed from SNMPv2, and then added BACK for SNMPv2
- **SNMPv3**
    - A much more SECURE version of SNMP that supports STRONG ENCRYPTION and AUTHENTICATION.
        
        <aside>
        💡 WHENEVER POSSIBLE, this version should be used!
        
        </aside>
        

---

SNMP MESSAGES

![image](https://github.com/psaumur/CCNA/assets/106411237/25b15c81-931a-41a6-8033-dff07bfb5f15)

1) SNMP READ

![image](https://github.com/psaumur/CCNA/assets/106411237/e7d671f6-f2b0-468a-95a2-6678a52945c4)

2) SMNP WRITE



3) SNMP NOTIFICATION



SNMP AGENT listens for MESSAGES on UDP Port 161

SNMP MANAGER listens for MESSAGES on UDP Port 162

![IMG_2985.jpeg](https://prod-files-secure.s3.us-west-2.amazonaws.com/4cdde10f-02e3-465a-88ff-7f4c39b1e84f/4ad2ce42-c01f-4475-80e8-6272c508a043/IMG_2985.jpeg)

---

SNMPv2c CONFIGURATION (Basic)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/4cdde10f-02e3-465a-88ff-7f4c39b1e84f/971dd829-9360-4dfa-9f5a-1db52a3ce599/Untitled.png)

WHAT HAPPENS WITH R1’s G0/1 INTERFACE GOES DOWN?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/4cdde10f-02e3-465a-88ff-7f4c39b1e84f/ba3a1a05-6235-433d-aef3-2555f7b53b82/Untitled.png)

NOTE:

UDP message sent to Destination Port 162 (SNMP Manager)

“version” is set to v2c

community is “Jeremy1” (Read Only - no Set messages)

snmpV2-trap : trap message sent due to interface G0/1 going down

variable-bindings : contains the OID sent to identify the issue.

---

SNMP SUMMARY

- SNMP helps MANAGE DEVICES over a NETWORK
- MANAGED DEVICES are the devices being managed using SNMP (such as ROUTERS, SWITCHES, FIREWALLS)
- NETWORK MANAGEMENT STATIONS (NMS) are the SNMP “servers” that manage the devices
    - NMS receives notifications from Managed Devices
    - NMS changes settings on Managed Devices
    - NMS checks status of Managed Devices
    
- Variables, such as Interface Status, Temperature, Traffic Load, Hostname, etc are STORED in the MANAGMENT INFORMATION BASE (MIB) and identified using Object IDs (OIDs)

<aside>
💡 Main SNMP versions : SNMPv1, SNMPv2c, SNMPv3

</aside>

<aside>
💡 SNMP MESSAGES : 
* Get / GetNext / GetBulk
* Set
* Trap
* Inform
* Response

</aside>
