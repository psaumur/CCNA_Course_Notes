# 7. IPv4 ADDRESSING : PART 1

OSI MODEL - NETWORK LAYER (Layer 3)

- Provides connectivity between end hosts on DIFFERENT networks (ie: outside of the LAN)
- Provides logical addressing (IP addresses)
- Provides path selection between SOURCE and DESTINATION
- ROUTERS operate at LAYER 3

ROUTING

SWITCHES (Layer 2 Devices) do no separate different networks. They connect and EXPAND networks within the same LAN.

By adding a ROUTER, however, between two SWITCHES, you create a SPLIT in the network; each with it's own network IP address.

Example:
192.168.1.0/24 (255.255.255.0)
192.168.2.0/24 (255.255.255.0)

![image](https://github.com/psaumur/CCNA/assets/106411237/3d414956-cb53-46f6-b386-3fc9bba11802)


ROUTERS have unique IP Addresses for EACH of their interface connections, depending on their location.

The IP Address for the ROUTER's G0/0 Interface is:
192.168.1.254/24

The IP Address for the ROUTER's G0/1 Interface is:
192.168.2.254/24

![image](https://github.com/psaumur/CCNA/assets/106411237/6e593774-4113-4493-89bb-4d394cb29e1d)


The IP Address depends on network address of the LAN it is connects to.

The NETWORK portion of given IP Address will be the same for all HOSTS on a given LAN.

Example:

192.168.1.100
192.168.1.105
192.168.1.205

All of these addresses are on the SAME Network because the NETWORK PORTION of their IP Address is the same (192.168.1) while the HOST part (100,105,205) is UNIQUE!

When a BROADCAST message hits a ROUTER, it does NOT continue onward. It stays within the LOCAL LAN (Switch/Hosts).

---

IPv4 HEADER

![image](https://github.com/psaumur/CCNA/assets/106411237/4f4bd7da-1876-4000-8229-be4b8792a86d)


IP (or Internet Protocol) is the primary Layer 3 protocol in use today. Version 4 is the version in use in most networks.

IPv4 Headers contain MORE fields than the ETHERNET header.

IPv4 Headers contain a SOURCE IP Address and DESTINATION IP Address field.

This FIELD is 32-bits(4-bytes) in length (0-31)

192.168.1.254 (each decimal number represents 8 bits)

Translated to Binary:

11000000 . 10101000 . 00000001 . 11111110

EACH of these 8 bit groups are referred to as an OCTET

Since Binary is difficult to read for people, we use the Dotted Decimal format.

---

REVIEW of DECIMAL and HEXADECIMAL

![image](https://github.com/psaumur/CCNA/assets/106411237/e45f0ea9-a705-463b-bb9b-d81034cf130d)


Decimal (base 10)

Ex: 3294 = (3 * 1000) + (2 * 100) + (9 * 10) + (4 * 1)

Hexadecimal (base 16)

Ex: 3294, would be CDE
```
C (C * 256 / 12 * 256 = 3072) // 256ths position
D (D * 16 / D=13 so 16*13 = 208) // 16ths position
E (E * 1 / E = 14)	// 1s position
```
Adding these up, we get 3294

---

So, how do we convert a BINARY NUMBER to a DECIMAL NUMBER?
The same way we convert to Hexadecimal.

10001111

So:
```
1 * 128 = 128
1 * 8 = 8
1 * 4 = 4
1 * 2 = 2
1 * 1 = 1
```
Add them all up : 128 + 8 + 4 + 2 + 1 = 143

The answer is 143.

---

Another example:

01110110
```
1 * 64 = 64
1 * 32 = 32
1 * 16 = 16
1 * 4 = 4
1 * 2 = 2
```
Add them all up: 64 + 32 + 16 + 4 + 2 = 118

The answer is 118.

---

Another example:

11101100
```
1 * 128 = 128
1 * 64 = 64
1 * 32 = 32
1 * 8 = 8
1 * 4 = 4
```
Add them all up: 128 + 64 + 32 + 8 + 4 = 236

The answer is 236.

---

So, how do we convert a DECIMAL NUMBER to a BINARY NUMBER?

Take the number 221.

We can take that number and start subtracting it from LEFT to RIGHT of our Binary slots.

221
```
221 - 128 = 93 so we place a 1 in the "128" slot
```
10000000
```
93 - 64 = 29 so we place another 1 in the "64" slot

29 - 32 isn't possible so we place a 0 in the "32" slot

29 - 16 = 13 so we place a 1 in the "16" slot

13 - 8 = 5 so we place a 1 in the "8" slot

5 - 4 = 1 so we place a 1 in the "4" slot

1 - 2 isn't possible so we put a 0 in the "2" slot

1 - 1 is possible so we put a 1 in the "1" slot
```
This, then, allows us to the write out the BINARY number for 221.

It is : 11011101

---

Another example: 127
```
127 - 128 is not possible so 0 in "128"
127 - 64 is possible so 1 in "64"
63 - 32 is possible so 1 in "32"
31 - 16 is possible so 1 in "16"
15 - 8 is possible so 1 in "8"
7 - 4 is possible so 1 in "4"
3 - 2 is possible so 1 in "2"
1 is possible so 1 in "1"
```
So 127, in BINARY, is 0111 1111

---

Another example: 207

Alternatively, you can subtract the number from '255' (which is 1111111).
The remainder, then, can be used to "find" where the 0's are in the binary number.

255 - 207 = 48 so ...

1 1 0 0 1 1 1 1 (32 + 16 = 48)

11001111 is the correct answer.

---

IPv4 ADDRESSES

So we now know that IP Addresses are the Dotted Decimal conversion of a series of BINARY NUMBERS (broken up into 4 OCTETS) like so:

192.168.1.254/24

But what does the /24 stand for?

![image](https://github.com/psaumur/CCNA/assets/106411237/808fa7fa-0239-42fa-9706-79db87ea167e)


It means the FIRST 24 BITS of this address represent the NETWORK portion of the address.

192.168.1 is the NETWORK PORTION (the first 3 OCTETS)

.254 is the HOST PORTION (the last OCTET)

![image](https://github.com/psaumur/CCNA/assets/106411237/2e7c64e1-5689-486a-bba0-9623f5e8de7d)


---

CONVERT this BINARY number into an IPv4 Address:

10011010010011100110111100100000

10011010 . 01001110 . 01101111 . 00100000

Octets:

1. 128 + 16 + 8 + 2 = 154
2. 64 + 8 + 4 + 2 = 78
3. 64 + 32 + 8 + 4 + 2 + 1 = 111
4. 32

The IPv4 address is: 154.78.111.32/16

154.78 is the NETWORK PORTION
111.32 is the HOST PORTION

Another Example:

00001100100000001111101100010111

00001100 . 10000000 . 11111011 . 00010111

Octets:

1. 8 + 4 = 12
2. 128
3. 255 - 4 = 251
4. 16 + 4 + 2 + 1 = 23

The IPv4 address is: 12.128.251.23/8

12 is the NETWORK PORTION
128.251.23 is the HOST PORTION

---

IPv4 ADDRESS CLASSES

IPv4 ADDRESSES are split up into 5 different 'classes'.
The class of an IPv4 is determined by the FIRST OCTET of the address.

CLASS 		FIRST OCTET 		FIRST OCTET NUMBERIC RANGE

A 			 0xxxxxxx 				0-126 + 127 'loopback'
B 			 10xxxxxx 				128-191
C 			 110xxxxx 				192-223
D 			 1110xxxx 				224-239
E 			 1111xxxx 				240-255

From the above chart, if the FIRST OCTECT STARTS with 0, the numeric RANGE of possible first DOTTED DECIMAL is between 0-127.

The CLASSES we will be focusing on are CLASS A to CLASS C.

![image](https://github.com/psaumur/CCNA/assets/106411237/7cc286bf-ce76-4eee-af52-062a63dac2b4)


D CLASS are reserved for 'MULTICAST' ADDRESSES

E CLASS are reserved for 'EXPERIMENTAL' ADDRESSES

---

A CLASS USUALLY have a range of 1-126? WHY?

Because 127 is usually reserved for 'loopback addresses'

127.0.0.0 to 127.255.255.255 are used to test the network.

- Used to test the 'Network stack' (OSI & TCP/IP model) on the local device.

---

![image](https://github.com/psaumur/CCNA/assets/106411237/25f7db1a-f934-4c73-9926-66bb207fd292)


The PREFIX LENGTH is the LENGTH of the NETWORK PORTION of the Address.

From the examples above:

12.128.251.23/8 is a CLASS A Address
154.78.111.32/16 is a CLASS B Address
192.168.1.254/24 is a CLASS C Address

Because the NETWORK portion of CLASS A is so short, it means there are a LOT more potential Hosts.

Because the NETWORK portion of CLASS C is so long, it means fewer potential Hosts.

---

NETMASK

![image](https://github.com/psaumur/CCNA/assets/106411237/874c022f-9b8c-4862-a495-597682b014a4)


A NETMASK is written like a Dotted Decimal IP Address

CLASS A: /8 = 255.0.0.0

CLASS B: / 16 = 255.255.0.0

CLASS C: /24 = 255.255.255.0

---

NETWORK ADDRESSES

![image](https://github.com/psaumur/CCNA/assets/106411237/12178b46-2604-468b-a11c-2a94087b023d)


If the HOST PORTION of an IP ADDRESS is ALL 0's, it means it is the NETWORK ADDRESS = the identifier of the network itself.

Example: 192.168.1.0/24 = THIS is a NETWORK ADDRESS.

A NETWORK ADDRESS cannot be assigned to a HOST.
A NETWORK ADDRESS is the FIRST ADDRESS.

![image](https://github.com/psaumur/CCNA/assets/106411237/53eafb43-2a6f-422c-af19-866946d78efa)


If the HOST PORTION of an IP ADDRESS is ALL 1's, it means it is the BROADCAST ADDRESS for the network.

A BROADCAST ADDRESS cannot be assigned to a HOST.

DESTINATION IP : 192.168.1.255 (Broadcast IP address)
DESTINATION MAC : FFFF.FFFF.FFFF (Broadcast MAC address)

Because of the two 'reserved' addresses, the range of USABLE HOST ADDRESSES is 1 to 254.
