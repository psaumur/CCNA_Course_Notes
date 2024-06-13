# 38. DNS (Domain Name System)

THE PURPOSE OF DNS

- DNS is used to *resolve* human-readable names (google.com) to IP ADDRESSES
- Machines such as PCs don’t use names, they use ADDRESSES (ie: IPv4/IPv6)
- Names are much easier for us to use and remember than IP ADDRESSES
    - What is the IP ADDRESS of [youtube.com](http://youtube.com) ?
- When you type ‘youtube.com` into a web browser, your device will ask a DNS SERVER for the IP ADDRESS of [youtube.com](http://youtube.com)
- The DNS SERVER(S) your DEVICE uses can be manually configured or learned via DHCP

---

BASIC FUNCTIONS OF DNS

![image](https://github.com/psaumur/CCNA/assets/106411237/059c6fa4-674c-47ce-a08e-0714b21cb39e)

Command `ipconfig /all` (Show local IP configuration on current DEVICE)

![image](https://github.com/psaumur/CCNA/assets/106411237/b43b1d98-b510-4d05-be96-f706a3d090d1)

![image](https://github.com/psaumur/CCNA/assets/106411237/7f56b6f1-12c6-4096-9f73-28c9f8cfd570)

Command `nslookup` (Shows IP information for a given DNS entry)

![image](https://github.com/psaumur/CCNA/assets/106411237/71e5cd97-528c-435f-86d3-29d6ad2808b6)

WIRESHARK CAPTURE of above  COMMANDS

![image](https://github.com/psaumur/CCNA/assets/106411237/9d9cd65c-8a8b-45b3-8914-28a53013618f)

![image](https://github.com/psaumur/CCNA/assets/106411237/469431b3-e981-47cf-994d-642f737e79a0)

Command `ipconfig /displaydns` (Displays DNS cache)

![image](https://github.com/psaumur/CCNA/assets/106411237/da36bc07-d834-4c5e-b7ab-71da025b912f)

Command `ipconfig /flushdns` (Clears DNS cache)

![image](https://github.com/psaumur/CCNA/assets/106411237/f8608c2f-840c-477d-9284-7060838f1f3e)

HOSTS Files

WINDOWS HOSTS location

![image](https://github.com/psaumur/CCNA/assets/106411237/771b6bd4-abe4-41b7-afc2-3984ccc23407)

![image](https://github.com/psaumur/CCNA/assets/106411237/ff56876a-3b80-482f-b73b-caa86e5d972f)

---

CONFIGURING DNS IN CISCO IOS

- For HOSTS in a NETWORK to use DNS, you don’t need to configure DNS on the ROUTERS.
    - They will simply FORWARD the DNS messages like any other packets
- However, a CISCO ROUTER can be configured as a DNS SERVER, although it’s rare
    - If an INTERNAL DNS SERVER is used, usually it’s a WINDOWS or LINUX SERVER
- A CISCO ROUTER can also be configured as a DNS CLIENT

Command `ip dns server` and `ip host <hostname> <ip address>`

![image](https://github.com/psaumur/CCNA/assets/106411237/f65a4118-ae59-4db5-8fc4-c83d39c3072d)

![image](https://github.com/psaumur/CCNA/assets/106411237/59743697-6347-41de-9359-ca7ef327af01)

![image](https://github.com/psaumur/CCNA/assets/106411237/8e9c34c4-1a53-4ce4-a268-8a6d801d45e9)

Command `show hosts`

![image](https://github.com/psaumur/CCNA/assets/106411237/306aa507-1523-43e5-ac48-251e8a75b5f8)

Command `ip name-server` and `ip domain lookup`

![image](https://github.com/psaumur/CCNA/assets/106411237/cf0deb90-f8be-4f11-9373-2b7ef4715baf)

---

COMMAND REVIEW:

![image](https://github.com/psaumur/CCNA/assets/106411237/6c3e7873-04c4-407e-a851-cb74a9f78eb9)
