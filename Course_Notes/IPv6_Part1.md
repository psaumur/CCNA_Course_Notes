# 31. IPv6 : PART 1

HEXIDECIMAL (Review)

![image](https://github.com/psaumur/CCNA/assets/106411237/df3e0c7f-5325-4c4c-9d88-197b588cdfe4)

![image](https://github.com/psaumur/CCNA/assets/106411237/a23caee6-492b-4226-ba9f-7b3e44578fd4)

![image](https://github.com/psaumur/CCNA/assets/106411237/1a7e0af8-4f19-483d-b75c-27fa452ce8e9)

What about the reverse (Hex to Binary) ??? 

![image](https://github.com/psaumur/CCNA/assets/106411237/ceced09e-175f-452d-87e8-5b10af7621a1)

---

WHY IPv6?

- The **MAIN REASON** is that there are simply not enough IPv4 addresses available
- There are 2^32 IPv4 Addresses available (4,294,967,296)
- When IPv4 was being designed 30 years ago, the creators had NO idea the Internet would be as large as today
- VLSM, Private IPv4 ADDRESSES, and NAT have been used to conserve the use of IPv4 ADDRESS SPACE.
    - These are short-term solutions, however.
- The LONG -TERM solution is IPv6

- IPv4 ADDRESS assignments are controlled by IANA (Internet Assigned Number Authority)
- IANA distributes IPv4 ADDRESS space to various RIRs (Regional Internet Registries), which then assign them to companies that need them.

![image](https://github.com/psaumur/CCNA/assets/106411237/98fdf256-dbbf-4884-825a-6124251da6a7)

- On September 24th, 2015, ARIN declared exhaustion of the ARIN IPv4 address pool
- On August 21st, 2020, LACNIC announced that it had made its final IPv4 allocation

---

BASICS OF IPv6

- An IPv6 ADDRESS is **128 bits (8 "groups", 16 bits per "group". Groups are separated by ':')**

![image](https://github.com/psaumur/CCNA/assets/106411237/3e6fe314-c87f-4116-bf37-7f3cfd8e17b4)

- An IPv6 ADDRESS uses the / prefix number

SHORTENING (Abbreviating) IPv6 ADDRESSES

![image](https://github.com/psaumur/CCNA/assets/106411237/7796f62c-5daa-4e3c-a029-2c42e8abfc6c)

![image](https://github.com/psaumur/CCNA/assets/106411237/ee734193-9708-44a8-8702-c0d9d07afaad)

![image](https://github.com/psaumur/CCNA/assets/106411237/a19192b2-fcd9-4280-95c4-281ef08ffa5e)

![image](https://github.com/psaumur/CCNA/assets/106411237/07c413b6-1577-47c3-963c-4ccca8e20820)

![image](https://github.com/psaumur/CCNA/assets/106411237/ea5f5e40-1b4f-4fd8-942c-c17ca2535e35)

EXPANDING (Abbreviating) IPv6 ADDRESSES

![image](https://github.com/psaumur/CCNA/assets/106411237/934a089e-6ec1-4297-b0da-154b8240af35)

FINDING the IPv6 PREFIX (GLOBAL UNICAST ADDRESSES)

- Typically, an Enterprise requesting IPv6 ADDRESSES from their ISP will receive a /48 BLOCK
- Typically, IPv6 SUBNETS use a /64 PREFIX LENGTH
- That means an Enterprise has 16 bits to use to make SUBNETS
- The remaining 64 bits can be used for HOSTS

![image](https://github.com/psaumur/CCNA/assets/106411237/12448711-2636-4133-bed9-d655bedbd418)

![image](https://github.com/psaumur/CCNA/assets/106411237/fa872c5a-4d39-4519-9248-f4f552539bb8)

(Each digit is 4 bits / each 4 digit block is 16 bits)

**REMEMBER** : You can only remove the LEADING ZEROS !!!

2001 : 0DB8 : 8B00 : 0001 : FB89 : 017B : 0020 : 0011  /93

Because 93 lands in the middle of a 4 bit number, we need to convert the last digit to binary and borrow a “bit” from the first binary digit.

:: 017 [B] :: B = 0d11 = 0b1011 = 0b1000 (the first digit is borrowed, the remainder become 0)

![image](https://github.com/psaumur/CCNA/assets/106411237/1703e18d-da7a-4ee9-850e-d4e4a59ec72a)

![image](https://github.com/psaumur/CCNA/assets/106411237/c7e6fcec-ec8c-40df-86b6-72486e2a3165)

---

CONFIGURING IPv6 ADDRESSES

![image](https://github.com/psaumur/CCNA/assets/106411237/7ee88c71-617f-4bfc-8220-a4ef5bbe89e3)

This allows the ROUTER to perform IPv6 ROUTING

<aside>
💡 R1(config) #ipv6 unicast-routing

</aside>

Configuring an INTERFACE with an IPv6 Address

<aside>
💡 R1(config) #int g0/0
R1(config-if) #ipv6 address 2001:db8:0:0::1/64
R1(config) #no shutdown

</aside>

You can also type out the full address (if necessary)

![image](https://github.com/psaumur/CCNA/assets/106411237/c83977d3-678f-4922-9be2-f52c6a679d64)

NOTE ABBREVIATED IPv6 ADDRESSES SHOWN

LINK-LOCAL ADDRESSES are automatically added when creating an IPv6 INTERFACE (Covered in IPv6 - PART 2 Lecture)
