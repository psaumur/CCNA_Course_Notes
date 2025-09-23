# 53.  WAN ARCHITECTURES

INTRODUCTION TO WANS

- WAN stands for WIDE AREA NETWORK
- A WAN is a NETWORK that extends over a large geographic area
- WANs are used to connect geographically separate LANs
- Although the Internet can be considered a WAN, the term “WAN” is typically used to refer to an enterprise’s private connections that connect their offices, data centers, and other sites together
- Over public/shared networks like the Internet, VPNs (Virtual Private Networks) can be used to create private WAN connections
- There have been many different WAN technologies over the years. Depending on the location, some will be available and some will not be
- Technologies which are considered “legacy” (old) in one country, might still be used in other countries

---

WAN OVER DEDICATED CONNECTION (LEASED LINE)

HUB-and-SPOKE topology

![image](https://github.com/psaumur/CCNA/assets/106411237/57575fad-883d-4999-a56d-a77fa1542976)

![image](https://github.com/psaumur/CCNA/assets/106411237/cfc23064-a133-445a-b854-e044828eca7d)

WAN CONNECTION VIA ETHERNET (FIBER)

![image](https://github.com/psaumur/CCNA/assets/106411237/022ccdbd-7ce9-41fd-9f99-9e9c6dcb9f76)

WAN OVER SHARED INFRASTRUCTURE (INTERNET VPN)

![image](https://github.com/psaumur/CCNA/assets/106411237/38eff264-7ed4-43fd-943b-47e9e1ce995e)

---

LEASED LINES

- A LEASED LINE is a dedicated physical link, typically connecting two sites
- LEASED LINES use serial connections (PPP or HDLC encapsulation)
- There are various standards that provide different speeds and different standards are available in different countries.
- Due to the HIGHER cost, HIGHER installation lead time, and SLOWER speeds of LEASED LINES, Ethernet WAN technologies are becoming MORE popular

![image](https://github.com/psaumur/CCNA/assets/106411237/77dd5503-8b29-4919-8747-6dd80eec28fa)

MPLS VPNs

- MPLS stands for “Multi Protocol Label Switching”
- Similar to the Internet, service providers’ MPLS NETWORKS are shared infrastructure because many customer enterprises connect to and share the same infrastructure to make WAN connections
- However, the “label switching” in the name of MPLS allows VPNs to be created over the MPLS infrastructure through the use of LABELS
- IMPORTANT terms:
    - CE ROUTER = Customer Edge ROUTER
    - PE ROUTER = Provider Edge ROUTER
    - P ROUTER = Provider Core ROUTER

![image](https://github.com/psaumur/CCNA/assets/106411237/166bff5b-d977-48dc-9a74-b9a523b91e1b)

- When the PE ROUTERS receive FRAMES from the CE ROUTERS, they add a LABEL to the FRAME
- These LABELS are used to make forwarding decisions within the SERVICE PROVIDER NETWORK - NOT the DESTINATION IP
- The CE ROUTERS do NOT USE MPLS, it is only used by the PE/P ROUTERS
- When using a LAYER 3 MPLS VPN, the CE and PE ROUTERS peer using OSPF, for example, to share ROUTING information

EXAMPLE: 

OFFICE A’s CE will peer with one PE

OFFICE B’s CE will peer with the other PE

OFFICE A’s CE will learn about OFFICE B’s ROUTES via this OSPF peering

OFFICE B’s CE will learn about OFFICE A’s ROUTES as well

![image](https://github.com/psaumur/CCNA/assets/106411237/2b3d8d6e-3501-4d54-a6f8-5a05c9140d24)

- When using a LAYER 2 MPLS VPN, the CE and PE ROUTERS do NOT form PEERINGS
- The SERVICE PROVIDER NETWORK is entirely *transparent* to the CE ROUTERS
- In effect, it is like the TWO CE ROUTERS are directly connected.
    - Their WAN INTERFACES will be in the SAME SUBNET
- If a ROUTING protocol is used, the TWO CE ROUTERS will peer directly with each other

CE ROUTERS connected via LAYER 2 MPLS VPN

![image](https://github.com/psaumur/CCNA/assets/106411237/b0b19dfd-e417-40ce-ac36-ce0ace8484cc)

![image](https://github.com/psaumur/CCNA/assets/106411237/cc5c9508-a2b0-4fe7-9c83-6c03e7d2d861)

---

MPLS 

- Many different technologies can be used to connect to a SERVICE PROVIDER’s MPLS NETWORK for WAN Service

![image](https://github.com/psaumur/CCNA/assets/106411237/c6e6e60d-2a96-415e-82a2-a090c38a68a3)

INTERNET CONNECTIVITY

- There are countless ways for an enterprise to connect to the INTERNET
- For example, PRIVATE WAN technologies such as LEASED LINES and MPLS VPNs can be used to connect to a SERVICE PROVIDER’s INTERNET infrastructure
- In addition, technologies such as CATV and DSL commonly used by consumers (Home Internet Access) can also be used by an enterprise
- These days for both enterprise and consumer INTERNET access, FIBER OPTIC ETHERNET connections are growing in popularity due to high speeds they provide over long distances
- Let’s briefly look at TWO INTERNET access technologies mentioned above:
    - CABLE (CATV)
    - DSL

---

DIGITAL SUBSCRIBER LINE (DSL)

- DSL provides INTERNET connectivity to customers over phone lines and can share the same phone line that is already installed in most homes
- A DSL MODEM (Modulator / Demodulator) is required to convert DATA into a format suitable to be sent over the phone lines
    - The MODEM might be a separate DEVICE or it might be incorporated in to a “HOME ROUTER”

![image](https://github.com/psaumur/CCNA/assets/106411237/a708b6b4-6de5-4a72-8c77-13f569f4c2d5)

CABLE INTERNET

- CABLE INTERNET provides INTERNET ACCESS via the same CATV (Cable Television) lines used for TV service
- Like DLS, a CABLE MODEM is required to convert DATA into a format suitable to be sent over the CATV CABLES.
    - Like a DSL MODEM, this can be a separate device or built into the HOME ROUTER

![image](https://github.com/psaumur/CCNA/assets/106411237/a33bb999-83bc-49a8-ad37-e7ca91fcb954)

---

REDUNDANT INTERNET CONNECTIONS

![image](https://github.com/psaumur/CCNA/assets/106411237/af770f82-a55c-4af5-af7b-5708b39833c4)

---

INTERNET VPNs

- PRIVATE WAN SERVICES such as LEASED LINES and MPLS provide security because each customer’s TRAFFIC is separated by using dedicated physical connections (LEASED LINE) or by MPLS TAGS
- When using the INTERNET as a WAN to connect SITES together, there is no built-in security by DEFAULT
- To provide secure communications over the Internet, VPNs (Virtual Private Networks) are used
- We will cover two kinds of Internet VPNs:
    - SITE-TO-SITE VPNS using IPSec
    - REMOTE-ACCESS VPNs using TLS

SITE-TO-SITE VPNs (IPSec)

- A “SITE-TO-SITE” VPN is a VPN between two DEVICES and is used to connect TWO SITES together over the INTERNET
- A VPN “TUNNEL” is created between the TWO DEVICES by ENCAPSULATING the original IP PACKET with a VPN HEADER and a new IP HEADER
    - When using IPSec, the original PACKET is encrypted before its ENCAPSULATED with the new HEADER

![image](https://github.com/psaumur/CCNA/assets/106411237/b17c6149-90b2-4bc7-beb7-c53698d588a0)

![image](https://github.com/psaumur/CCNA/assets/106411237/d41295a9-af54-4cd5-acc8-4b60c39c40c2)

PROCESS SUMMARY:

1) The SENDING DEVICE combines the original PACKET and SESSION KEY (ENCRYPTION KEY) and runs them through an ENCRYPTION FORMULA

2) The SENDING DEVICE encapsulates the ENCRYPTED PACKET with a VPN HEADER and a new IP HEADER

3) The SENDING DEVICE sends the NEW PACKET to the DEVICE on the other side of the TUNNEL

4) The RECEIVING DEVICE decrypts the DATA to get the original PACKET and then forwards the original PACKET to it’s DESTINATION

- In a “SITE-TO-SITE” VPN, a TUNNEL is formed only between TWO TUNNEL ENDPOINTS (for example, the TWO ROUTERS connected to the INTERNET)
- All OTHER DEVICES in each site DO NOT need to create a VPN for themselves. They can send unencrypted DATA to their site’s ROUTER, which will ENCRYPT it and FORWARD it in the TUNNEL as described above.

---

LIMITATIONS OF STANDARD IPSec

1) IPSec doesn’t support BROADCAST or MULTICAST TRAFFIC, only UNICAST.

- This means that ROUTING PROTOCOLS such as OSPF cannot be used over the TUNNELS because they rely on MULTICAST TRAFFIC
    - This can be SOLVED with “GRE over IPSec”

2) Configuring a full mesh of TUNNELS between many sites is a labor-intensive task

Let’s look at each of the above SOLUTIONS

---

GRE over IPSec

- GRE (GENERIC ROUTING ENCAPSULATION) creates TUNNELS like IPSec, however it does not ENCRYPT the original PACKET, so it is NOT SECURE
- However, it has the advantage of being able to encapsulate a WIDE variety of a LAYER 3 PROTOCOLS as well as BROADCAST and MULTICAST messages
- To get the FLEXIBILITY of GRE with the SECURITY of IPSec, “GRE over IPSec” can be used
- The original PACKET will be ENCAPSULATED by a GRE HEADER and a new IP HEADER, and then the GRE PACKET will be ENCRYPTED and ENCAPSULATED within an IPSec VPN HEADER and a NEW IP HEADER

![image](https://github.com/psaumur/CCNA/assets/106411237/09c7da0c-debe-453e-822c-b97c0b8658ef)

![image](https://github.com/psaumur/CCNA/assets/106411237/3dfd6b86-28bb-489d-931b-5cc74669c1ac)

![image](https://github.com/psaumur/CCNA/assets/106411237/939ce5af-5ffc-44da-96fc-def2ca99ecae)

---

DMVPN

- DMVPN (Dynamic Multipoint VPN) is a Cisco-Developed solution that allows ROUTERS to dynamically create a FULL MESH of IPSec TUNNELS without having to manually configure every SINGLE TUNNEL

1) CONFIGURE IPSec TUNNELS to a HUB SITE

![image](https://github.com/psaumur/CCNA/assets/106411237/00c33e7f-2b28-4a33-908d-7aceff1e4092)

2) The HUB ROUTER gives each ROUTER information about HOW to form an IPSec TUNNEL with the OTHER ROUTERS

![image](https://github.com/psaumur/CCNA/assets/106411237/7a621160-10d4-4e14-868b-3c23f6bb0a64)

DMVPN provides the configuration simplicity of HUB-AND-SPOKE (each SPOKE ROUTER only needs one TUNNEL configured) and the EFFICIENCY of DIRECT SPOKE-TO-SPOKE communication (SPOKE ROUTERS can communicate directly without TRAFFIC passing through the HUB)

---

REMOTE-ACCESS VPNs

- Whereas SITE-TO-SITE VPNs are used to make a POINT-TO-POINT connection between TWO SITES over the INTERNET, REMOTE-ACCESS VPNs are used to allow END DEVICES (PCs, Mobile Phone) to ACCESS the company’s internal resources securely over the INTERNET
- REMOTE-ACCESS VPNs typically use TLS (TRANSPORT LAYER SECURITY)
    - TLS is also what provides security for HTTPS (HTTP SECURE)
    - TLS was formerly known as SSL (Secure Socket Layer) and developed by Netscape, but it was renamed to TLS when it was standardized by the IETF
- VPN client software  (for example Cisco AnyConnect) is installed on END DEVICES (for example company-provided laptops that employees use to work from home)
- These END DEVICES then form SECURE TUNNELS to one of the company’s ROUTERS / FIREWALLS acting as a TLS SERVER
- This allows the END USERS to securely access RESOURCES on the company’s INTERNAL NETWORK without being directly connected to the company NETWORK

![image](https://github.com/psaumur/CCNA/assets/106411237/f4a77cb7-9d42-4daa-9a25-630c0fb260cf)

---

SITE-TO-SITE versus REMOTE-ACCESS VPN

- SITE-TO-SITE VPNs typically use IPSec
- REMOTE-ACCESS VPNs typically use TLS
- SITE-TO-SITE VPNs provide SERVICE to many DEVICES within the SITES they are connecting
- REMOTE-ACCESS VPNs provide SERVICE to the ONE END DEVICE the VPN CLIENT SOFTWARE is installed on

- SITE-TO-SITE VPNs are typically used to permanently connect TWO SITES over the INTERNET
- REMOTE-ACCESS VPNs are typically used to provide ON-DEMAND ACCESS for END DEVICES that want to securely ACCESS company resources while connected to a NETWORK which is not SECURE

---

LAB COMMANDS

Create the Tunnel interface

`R1(config)#int tunnel <tunnel number>`

This changes the mode to the Tunnel Interface

The exit interface for the tunnel

`tunnel source <interface>` 

IP of the Tunnel Destination Interface

`tunnel destination <destination ip address>`

Set the IP of the Source Tunnel Interface (from step 1)

`ip address <tunnel IP> <netmask>`

Configure a Default Route to the Service Provider Network

`R1(config)#ip route 0.0.0.0 0.0.0.0 <next hop interface>`

This will now bring the Tunnel Interface Administratively Up / Up

================================================

Now you need to set up the TUNNEL ROUTERS as OSPF Neighbors for the Service Provider Network so they can share routes

`R1(config)router ospf <ospf process ID>`

This switches to the OSPF Router configuration mode

`network <tunnel interface IP> <wildcard mask> area <area #>`

Since the tunnel is a single HOST, you would use 0.0.0.0 for the Wildcard Mask

`network <router gateway IP> <wildcard mask> area <area #>`

Since the router gateway is also a single HOST, you would use 0.0.0.0 for the Wildcard Mask

`passive-interface <router gateway IP interface>`

This removes the Router Gateway from broadcasting over OSPF
