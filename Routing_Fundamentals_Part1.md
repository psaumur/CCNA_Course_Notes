# 11. ROUTING FUNDAMENTALS : PART 1




### WHAT IS ROUTING ?



ROUTING is the process that routers use to determine the path that IP packets should take over a network to reach their destination.

- ROUTERS store routes to all their known destinations in a ROUTING TABLE
- When ROUTERS receive PACKETS, they look in the ROUTING TABLE to find the best route to forward that packet.

There are two main routing methods (methods that routers use to learn routes):

- DYNAMIC ROUTING : ROUTERS use Dynamic Routing Protocols (ie: OSPF) to share routing information with each other automatically and build their routing tables.
- STATIC ROUTING : A network engineer / Admin manually configures routes on the router.

A ROUTE tells the ROUTER :

- to send a packet to Destination X, you should send the pack to ***next-hop*** Y
- or if the Destination is directly connected to the router, *send the packet directly to the destination.*
- or if the Destination is the router’s own IP address, *receive the packet for yourself (don’t forward it).*

![image](https://github.com/psaumur/CCNA/assets/106411237/8ceefb10-d70d-4530-969d-40347ed34297)


WAN (Wide Area Network) = network that extends over a large geographic area.

![image](https://github.com/psaumur/CCNA/assets/106411237/b3555fdd-37a4-4bc8-b998-76e0b5455bb1)

![image](https://github.com/psaumur/CCNA/assets/106411237/99e75230-de1c-4f48-acd0-3482bba256af)

![image](https://github.com/psaumur/CCNA/assets/106411237/13a77d5c-497d-49ca-9717-ea3bb4a560d0)

![image](https://github.com/psaumur/CCNA/assets/106411237/6e3a2b3b-1590-4625-9bcf-cdaed95738d2)

![image](https://github.com/psaumur/CCNA/assets/106411237/891fcfbe-7dc5-4fb2-9b02-c6905236761e)
