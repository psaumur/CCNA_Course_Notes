# 44. NAT (STATIC): PART 1

PRIVATE IPv4 ADDRESSES (RFC 1918)

- IPv4 doesn’t provide enough ADDRESSES for all DEVICES that need an IP ADDRESS in the modern world
- The long-term solution is to switch to IPv6
- There are THREE MAIN short-term solutions:
    - CIDR
    - PRIVATE IPv4 ADDRESS
    - NAT
- RFC 1918 specifies the following IPv4 ADDRESS RANGES as PRIVATE:
    
    ```
    10.0.0.0 /8       (10.0.0.0 to 10.255.255.255)             CLASS A 
    172.16.0.0 /12    (172.16.0.0 to 172.31.255.255)           CLASS B
    192.168.0.0 /16   (192.168.0.0 to 192.168.255.255)         CLASS C
    ```
    
- You are free to use these ADDRESSES in your NETWORKS. They don’t have to be GLOBALLY UNIQUE

![image](https://github.com/psaumur/CCNA/assets/106411237/c774460a-0479-40ed-ac62-1e9820960943)

---

INTRO TO NAT

- NETWORK ADDRESS TRANSLATION (NAT) is used to modify the SOURCE and / or DESTINATION IP ADDRESSES of packets
- There are various reasons to use NAT, but the MOST common reason is to ALLOW HOSTS with PRIVATE IP ADDRESSES to communicate with other HOSTS over the INTERNET
- For the CCNA you have to understand SOURCE NAT and how to configure it on CISCO ROUTERS

![image](https://github.com/psaumur/CCNA/assets/106411237/11cbc222-4b2d-4283-9a8f-86cfff2e109d)

---

STATIC NAT

- STATIC NAT involves statically configuring ONE-TO-ONE MAPPINGS of PRIVATE IP ADDRESSES to PUBLIC ADDRESSES

![image](https://github.com/psaumur/CCNA/assets/106411237/40867b28-66ff-4182-be97-8495a4c2de23)

![image](https://github.com/psaumur/CCNA/assets/106411237/b77177cc-f6e3-434f-87e0-fb5d0fe14c90)

![image](https://github.com/psaumur/CCNA/assets/106411237/daac56f4-5af8-482c-9d1d-63a0fb3bdcb1)

PRIVATE IP CANNOT BE MAPPED TO THE SAME GLOBAL IP

THE SECOND MAPPING WILL BE REJECTED

![image](https://github.com/psaumur/CCNA/assets/106411237/6dceb3c2-39d6-4299-b08d-90cbddb8d6b3)

---

STATIC NAT CONFIGURATIONS

![image](https://github.com/psaumur/CCNA/assets/106411237/1b0d6780-56d8-4ea0-870b-abb65d3a6e66)

![image](https://github.com/psaumur/CCNA/assets/106411237/add755f6-2d2c-4fe8-aae1-6d1aeecb6ea2)

Command `clear ip nat translation`

![image](https://github.com/psaumur/CCNA/assets/106411237/4266d928-0970-4386-82d7-159cc2b02df6)

Command `show ip nat statistics`

![image](https://github.com/psaumur/CCNA/assets/106411237/2e70576f-3879-4ba6-8ffa-307fd0c243c9)

---

COMMAND REVIEW

![image](https://github.com/psaumur/CCNA/assets/106411237/061f4c43-e755-41e8-b8b4-9e31e0723a19)
