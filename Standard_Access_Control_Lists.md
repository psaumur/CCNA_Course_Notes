# 34. STANDARD ACCESS CONTROL LISTS (ACL)

WHAT ARE ACLs

- ACLs (Access Control Lists) have multiple uses
- In DAY 34 and DAY 35, we will focus on ACL’s from a security perspective
- ACLs function as a “packet filter” - instructing the ROUTER to ALLOW or DENY specific traffic
- ACLs can filter traffic based on:
    - SOURCE / DESTINATION IP ADDRESSES
    - SOURCE / DESTINATION LAYER 4 PORTS
    - etc.

---

HOW ACLs WORK

![image](https://github.com/psaumur/CCNA/assets/106411237/92d663ec-33a8-4ba4-b0a7-5d3942a9b67e)

<aside>
💡 REQUIREMENTS:

- Hosts in 192.168.1.0/24 should have ACCESS to the 10.0.1.0/24 NETWORK
- Hosts in 192.168.2.0/24 should not have ACCESS to the 10.0.10/24 NETWORK
</aside>

ACLs are configured GLOBALLY on the ROUTER (Global Config Mode)

- They are an ordered sequence of ACEs (Access Control Entries)

![image](https://github.com/psaumur/CCNA/assets/106411237/2eb0c042-21d0-4a40-ade3-9715bd2b3bcb)

- Configuring an ACL in Global Config Mode will not make the ACL take effect
- The ACL must be applied to an interface
    - ACLs are applied either INBOUND or OUTBOUND
- ACLs are made up of one or more ACEs
- When a ROUTER checks a PACKET against the ACL, it processes the ACEs in order, from top to bottom
- If the PACKET matches one of the ACEs in the ACL, the ROUTER takes the action and stops processing the ACL. All entries below the matching entry will be ignored

![image](https://github.com/psaumur/CCNA/assets/106411237/a4a86a8e-f73c-476b-b0e5-15bfb4f4748d)

![image](https://github.com/psaumur/CCNA/assets/106411237/6e4148e0-e908-4a44-9f23-358c9d7ade11)

---

IMPLICIT DENY

- What will happen if a PACKET doesn’t match any of the entries in an ACL ?
- There is an INPLICIT DENY at the end of ALL ACL’s
- The IMPLICIT DENY tells the ROUTER to DENY ALL TRAFFIC that doesn’t match ANY of the configured entries in the ACL

---

ACL TYPES

![image](https://github.com/psaumur/CCNA/assets/106411237/4856845e-80b2-45dc-b30c-cc3b170db69c)

---

STANDARD NUMBERED ACLs

- Match traffic based only on the SOURCE IP ADDRESS of the PACKET
- Numbered ACLs are identified with a number (ie: ACL 1, ACL 2, etc.)
- Different TYPES of ACLs have a different range of numbers that can be used
    
    <aside>
    💡 STANDARD ACLs can use 1-99 and 1300-1999
    
    </aside>
    

- The basic command to configure a STANDARD NUMBERED ACL
    - `R1(config)# access-list *number* {deny | permit} *ip wildcard-mask*`
    
    This is an example of denying a SPECIFIC host’s traffic
    
    REMEMBER : 0.0.0.0 wildcard is the same as 255.255.255.255 or a /32 host
    
    - Example : `R1(config)# access-list 1 deny 1.1.1.1 0.0.0.0`
    - Example : `R1(config)# access-list 1 deny 1.1.1.1`(identical to the above)
    - Example : `R1(config)# access-list 1 deny host 1.1.1.1`
    
    If you want to permit ANY traffic from ANY source
    
    - Example : `R1(config)# access-list 1 permit any`
    - Example : `R1(config)# access-list 1 permit 0.0.0.0 255.255.255.255`
    
    If you want to make a description for a specific ACL
    
    - Example : `R1(config)# access-list 1 remark ## BLOCK BOB FROM ACCOUNTING ##`

![image](https://github.com/psaumur/CCNA/assets/106411237/3e20e40c-6755-4638-9ef3-15fa747f93b6)

Order is important. Lower Numbers are processed FIRST

---
TO APPLY AN ACL TO AN INTERFACE

`R1(config-if)# ip access-group *number* {in | out}`

![image](https://github.com/psaumur/CCNA/assets/106411237/eed38afa-f067-4153-80bb-b07c52a21e53)

WHY WAS THIS RULE PLACED ON G0/2 OUT ? 

<aside>
💡 STANDARD ACLs should be applied as CLOSE to the DESTINATION as possible!

</aside>

---

STANDARD NAMED ACLs

- Standard ACLs match traffic based only on the SOURCE IP ADDRESS of the PACKET
- NAMED ACLs are identified with a NAME (ie: ‘BLOCK_BOB’)
- STANDARD NAMED ACLs are configured by entering ‘standard named ACL config mode’ then configuring EACH entry within that config mode
    - `R1(config)# ip access-list standard *acl-name*`
    - `R1(config-std-nacl)# [*entry-number*] {deny | permit} *ip wildcard-mask*`

![image](https://github.com/psaumur/CCNA/assets/106411237/94e9b58d-07f6-4ad6-9c92-b00c01ce311d)

![image](https://github.com/psaumur/CCNA/assets/106411237/a8a10f5f-8e5c-4e19-981f-862bf94b2788)

![image](https://github.com/psaumur/CCNA/assets/106411237/3b641f99-4c99-4d5f-a32b-1a626d1a02b4)

![image](https://github.com/psaumur/CCNA/assets/106411237/17a7d767-1052-4bc0-8a04-7278f16caeb6)

Here are the configurations for the above:

![image](https://github.com/psaumur/CCNA/assets/106411237/bbdcff70-1fd4-46a4-a4c2-5d5485fe5695)

Note, however, how the order is when viewing the ACLs 

![image](https://github.com/psaumur/CCNA/assets/106411237/74ad9dd4-d56f-4845-83b1-44366b4b94f6)

WHY THE REORDERING?

![image](https://github.com/psaumur/CCNA/assets/106411237/e5ed273d-1c24-4b78-884f-712e1cf6922a)

CISCOs PACKET TRACER does not reorder these, however.
