# 37. NTP

WHY IS TIME IMPORTANT FOR NETWORK DEVICES?

- All DEVICES have an INTERNAL CLOCK (ROUTERS, SWITCHES, PCs, etc)
- In CISCO IOS, you can view the time with the `show clock` command

![image](https://github.com/psaumur/CCNA/assets/106411237/0afc355a-a982-4caa-a470-e09070e9c74f)

- If you use the `show clock detail` command, you can see the TIME SOURCE

![image](https://github.com/psaumur/CCNA/assets/106411237/a49cc147-ddba-405d-8e70-745ae7434e5a)

- The INTERNAL HARDWARE CLOCK of a DEVICE will “drift’ over time, so it’s NOT the ideal time source.
- From a CCNA perspective, the most important reason to have accurate time on a DEVICE is to have ACCURATE logs for troubleshooting

- **Syslog**, the protocol used to keep device logs, will be covered in a later video

Command: `show logging`

![image](https://github.com/psaumur/CCNA/assets/106411237/33632e20-a4e9-40fd-aba0-527498cfb886)

Note : R3’s time stamp is completely different than R2’s !!!

![image](https://github.com/psaumur/CCNA/assets/106411237/7d0464c2-1abe-460a-93fb-dd4368c905a7)

---

MANUAL TIME CONFIGURATION

- You can manually configure the TIME on the DEVICE with the `clock set` command

![image](https://github.com/psaumur/CCNA/assets/106411237/fa5d40c2-bccb-48e2-9f6b-c85ad721f37f)

- Although the HARDWARE CALENDAR (built-in clock) is the DEFAULT time-source, the HARDWARE CLOCK and SOFTWARE CLOCK are separate and can be configured separately.

---

HARDWARE CLOCK (CALENDAR) CONFIGURATION

- You can MANUALLY configure the HARDWARE CLOCK with the `calendar set` command

![image](https://github.com/psaumur/CCNA/assets/106411237/b72c898a-4746-49de-86db-c519964b3916)

- Typically, you will want to SYNCHRONIZE the ‘clock’ and ‘calendar’
- Use the command `clock update-calendar` to sync the calendar to the clock’s time
- Use the command `clock read-calendar` to sync the clock to the calendar’s time

![image](https://github.com/psaumur/CCNA/assets/106411237/c9d24bfd-25b1-4c5d-a426-f2a8a2db108c)

![image](https://github.com/psaumur/CCNA/assets/106411237/104a5e27-0d5f-40fc-aea8-dbcf46c3e195)

---

CONFIGURING THE TIME ZONE

- You can configure the time zone with the `clock timezone` command

![image](https://github.com/psaumur/CCNA/assets/106411237/d9ef5a95-a102-4306-bc3d-269fc5fd1d9e)

DAYLIGHT SAVING TIME (SUMMER TIME)

![image](https://github.com/psaumur/CCNA/assets/106411237/591491d1-a5bd-4f99-b518-02e722f41e1a)

![image](https://github.com/psaumur/CCNA/assets/106411237/3319f4c0-fb72-4486-b14c-4648c2be7338)

Full command :

`R1(config)# clock summer-time EDT recurring 2 Sunday March 02:00 1 Sunday November 02:00`

This covers the START of Daylight Savings and the end of Daylight Savings
---

SUMMARY OF COMMANDS

![image](https://github.com/psaumur/CCNA/assets/106411237/33557221-c045-4063-8ca0-9e8fb045ce52)

---

NTP BASICS

- Manually configuring the time on DEVICES is NOT Scalable
- The manually configured clocks will “drift”, resulting in inaccurate time
- NTP (Network Time Protocol) allows AUTOMATIC synchronization of TIME over a NETWORK
- NTP CLIENTS request the TIME from NTP SERVERS
- A DEVICE can be an NTP SERVER and an NTP CLIENT at the same time
- NTP allows accuracy of TIME with ~1 millisecond if the NTP SERVER is in the same LAN - OR within ~50 milliseconds if connecting to the NTP SERVER over a WAN / the INTERNET
- Some NTP SERVERS are ‘better’ than others. The ‘distance’ of an NTP SERVER from the original **reference clock** is called **stratum**

<aside>
💡 NTP uses UDP port 123 to communicate

</aside>

REFERENCE CLOCK

- A REFERENCE CLOCK is usually a VERY accurate time device like an ATOMIC CLOCK or GPS CLOCK
- REFERENCE CLOCKS are **stratum 0** within the NTP hierarchy
- NTP SERVERS directly connected to REFERENCE CLOCKS are **stratum 1**

![image](https://github.com/psaumur/CCNA/assets/106411237/003bf28a-03fe-49a8-954c-728f8e79dbd9)

(Peering with Devices is called …)

![image](https://github.com/psaumur/CCNA/assets/106411237/e2b91988-9be4-419b-b0b3-ad4ac32ae5cc)

- An NTP CLIENT can SYNC to MULTIPLE NTP SERVERS

![image](https://github.com/psaumur/CCNA/assets/106411237/32146173-fa80-4926-9524-ad66de3f9a6b)

---

NTP CONFIGURATION

![image](https://github.com/psaumur/CCNA/assets/106411237/6ee32d55-a33d-419c-9286-d1683f250d37)

![image](https://github.com/psaumur/CCNA/assets/106411237/453bd559-d88f-46c8-b4c9-cea958ef216d)

![image](https://github.com/psaumur/CCNA/assets/106411237/6adb6092-0290-4ae9-961d-55d25ec1d3c7)

Using key argument “prefer” makes a given server the PREFERRED SERVER

(To show configuration servers)

![image](https://github.com/psaumur/CCNA/assets/106411237/aabee138-5cb3-4316-8411-8da38d6dd2d5)

`sys.peer` = This is the SERVER that the current ROUTER (R1) is being synchronized to

`st` = Stratum Tier

(To show NTP Status)

![image](https://github.com/psaumur/CCNA/assets/106411237/4501f436-3e52-48c4-b22c-a733547b8b98)

`stratum 2` because it’s synchronizing from Google (stratum 1)

(To show NTP clock details)

![image](https://github.com/psaumur/CCNA/assets/106411237/bde14525-17e6-4d63-9d0b-b992c3dd7725)

This command configures the ROUTER to update the HARDWARE CLOCK (Calendar) with the time learned via NTP

`R1(config)# ntp update-calendar` 

The HARDWARE CLOCK tracks the DATE and TIME on the DEVICE - even if it restarts, power is lost, etc.

When the SYSTEM is restarted, the HARDWARE CLOCK is used to INITIALIZE the SOFTWARE CLOCK

---

CONFIGURE A LOOPBACK INTERFACE FOR AN NTP SERVER

![image](https://github.com/psaumur/CCNA/assets/106411237/21cac8d8-7c7f-41e1-8f0a-bfb6418c6085)

Why configure a LOOPBACK DEVICE on R1 for NTP ?

If one of R1’s ROUTER INTERFACES goes down, it will still be accessible via R3’s ROUTING path

![image](https://github.com/psaumur/CCNA/assets/106411237/9ead84f6-8645-489c-a30d-0b3c7ebf6ba1)

SET NTP SERVER for R2 using the LOOPBACK INTERFACE on R1

![image](https://github.com/psaumur/CCNA/assets/106411237/8a05e16e-cab9-429c-836e-e74a1007cbcb)

SETTING R3 NTP SOURCE SERVERS using R1 and R2

![image](https://github.com/psaumur/CCNA/assets/106411237/bcbd2426-1745-437a-9ebd-fe80dce6b527)

NOTE : R1 has PREFERENCE because it’s STRATUM TIER is HIGHER than R2s

---

CONFIGURING NTP SERVER MODE

![image](https://github.com/psaumur/CCNA/assets/106411237/038c5e31-587e-4a54-ae80-cc290a0ff805)

![image](https://github.com/psaumur/CCNA/assets/106411237/903a6aba-e99d-4ee6-a9c5-e077eed0592a)

![image](https://github.com/psaumur/CCNA/assets/106411237/0b5928d9-6594-4f3d-8663-8f4f19d3245b)

![image](https://github.com/psaumur/CCNA/assets/106411237/0aad6e81-5b7b-41ad-82b1-6c98690a9a4c)

![image](https://github.com/psaumur/CCNA/assets/106411237/e68f0ab9-25f5-4e65-8e80-f07b15878f69)

---

CONFIGURING NTP SYMMETRIC ACTIVE MODE

Command to configure NTP SYMMETRIC MODE 
`R2(config)#ntp peer <peer ip address>`

![image](https://github.com/psaumur/CCNA/assets/106411237/a0c27863-86d7-40e4-a935-6c73fce39439)

![image](https://github.com/psaumur/CCNA/assets/106411237/d430e372-8480-4378-92e4-5e5ca06f2ac1)

---

CONFIGURE NTP AUTHENTICATION

- NTP AUTHENTICATION can be configured, although it is OPTIONAL
- It allows NTP CLIENTS to ensure they only sync to the intended SERVERS
- To CONFIGURE NTP AUTHENTICATION:
    - `ntp authenticate` (Enables NTP AUTHENTICATION)
    - `ntp authenticate-key *key-number* md5 *key*` (Create the NTP AUTHENTICATION Key(s))
    - `ntp trusted-key *key-number`* (Specify the Trusted Key(s))
    - `ntp server *ip-address* key *key-number`* (Specify which key to use for the server)

 

EXAMPLE CONFIGURATIONS

![image](https://github.com/psaumur/CCNA/assets/106411237/d8f54d79-8975-4dfe-b0c0-e4e2b44f7b31)

---

NTP COMMAND REVIEW

![image](https://github.com/psaumur/CCNA/assets/106411237/2888ef4e-f53a-4ca3-ad34-0b04742edfd9)
