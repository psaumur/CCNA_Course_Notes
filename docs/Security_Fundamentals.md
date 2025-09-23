# 48. SECURITY FUNDAMENTALS

KEY SECURITY CONCEPTS

WHY SECURITY?

What is the purpose / goal of SECURITY in an ENTERPRISE ?

- The principles of the CIA TRIAD form the FOUNDATION of SECURITY:
    - CONFIDENTIALITY
        - Only AUTHORIZED USERS should be able to ACCESS DATA
        - Some INFORMATION / DATA is PUBLIC and can be accessed by ANYONE
        - Some INFORMATION / DATA is SECRET and should be only be accessed by SPECIFIC people
    - INTEGRITY
        - DATA should not be tampered with (modified) by unauthorized USERS
        - DATA should be CORRECT and AUTHENTIC
    - AVAILABILITY
        - The NETWORK / SECURITY should be OPERATIONAL and ACCESSIBLE to AUTHORIZED USERS

ATTACKERS can threaten the CONFIDENTIALITY, INTEGRITY, and AVAILBILITY of an enterprise’s SYSTEMS and INFORMATION

---

VULNERABILITY, EXPLOIT, THREAT, MITIGATION

- A VULNERABILITY is any potential weakness that can compromise the CIA of a SYSTEM / INFO
    - A potential weakness isn’t a problem in its own
- AN EXPLOIT is something that can potentially be used to exploit the vulnerability
    - Something than can *potentially* be used as an exploit isn’t a problem on it’s own.

- A THREAT is the potential of a VULNERABILITY to be EXPLOITED
    - A hacker EXPLOITING a VULNERABILITY in your system is a THREAT

- A MITIGATION TECHNIQUE is something that can protect against threats
    - Should be implemented everywhere a VULNERABILITY can be EXPLOITED:
        - Client Devices
        - Servers, Switches, Routers, Firewalls
        - etc.

<aside>
💡 NO SYSTEM IS PERFECTLY SECURE!

</aside>

---

COMMON ATTACKS

- DoS (Denial of Service) Attacks
- Spoofing Attacks
- Reflection / Amplification Attacks
- Man-in-the-Middle Attacks
- Reconnaissance Attacks
- Malware
- Social Engineering Attacks
- Password-Related Attacks

DoS (Denial of Service) Attacks

- DoS attacks threaten the AVAILABILITY of the SYSTEM
- One common DoS attack is the TCP SYN Flood
    - TCP Three-Way Handshake : SYN | SYN-ACK | ACK
    - The ATTACKER sends countless TCP SYN messages to the TARGET
    - The TARGET sends a SYN-ACK message in response to each SYN it receives
    - The ATTACKER never replies with the final ACK of the TCP Three-Way Handshake
    - The incomplete connections fill up the TARGET’S TCP connection table
    - The ATTACKER continues sending SYN messages
    - The TARGET is no longer able to make legitimate TCP connections

![image](https://github.com/psaumur/CCNA/assets/106411237/5b04eea4-c53a-48b7-9683-952c9b27c9db)

- In a DDoS (Distributed Denial of Service) Attack, the ATTACKER infects many computers with MALWARE and uses them to initiate a Denial-of-Service Attack.
- This group of infected computers is called a BOTNET

Example : A TCP SYN Flood Attack

![image](https://github.com/psaumur/CCNA/assets/106411237/fc394c8d-33f4-4fd4-84a0-3e49caa9c158)

---

SPOOFING ATTACKS

- To SPOOF an ADDRESS is to use a FAKE SOURCE ADDRESS (IP or MAC)
- Numerous attacks involve spoofing; it’s not a SINGLE kind of attack
- An example is a DHCP EXHAUSTION attack
- An ATTACKER uses spoofed MAC ADDRESSES to flood DHCP Discover messages
- The TARGET server’s DHCP POOL becomes full, resulting in a Denial-of-Service to other DEVICES

![image](https://github.com/psaumur/CCNA/assets/106411237/c539c50b-1be0-42f9-8ce3-fbeb47ea2034)

---

REFLECTION / AMPLIFICATION ATTACKS

- In a REFLECTION attack, the ATTACKER sends traffic to a *reflector*, and spoofs the SOURCE of the PACKET using the TARGET’S IP ADDRESS
- The *reflector* (ie: a DNS Server) sends the reply to the TARGET’S IP ADDRESS
- If the amount of traffic sent to the TARGET is large enough, this can result in a Denial-of-Service

- A REFLECTION attack becomes an AMPLIFICATION attack when the amount of traffic sent by the ATTACKER is small but it triggers a LARGE amount of traffic to be sent from the *reflector* to the TARGET

![image](https://github.com/psaumur/CCNA/assets/106411237/34ca977d-9884-4aeb-b99a-9f3677ba17fa)

---

MAN-IN-THE-MIDDLE ATTACKS

- In a MAN-IN-THE-MIDDLE attack, the ATTACKER places himself between the SOURCE and DESTINATION to eavesdrop on communications, or to modify traffic before it reaches the DESTINATION
- A common example is ARP SPOOFING, also known as ARP POISONING
- A HOST sends an ARP REQUEST, asking for the MAC ADDRESS of another DEVICE
- The TARGET of the request sends an ARP REPLY, informing the requester of it’s MAC ADDRESS
- The ATTACKER waits and sends another ARP REPLY after it’s legitimate replier

![image](https://github.com/psaumur/CCNA/assets/106411237/86cee6cd-845a-4732-bfec-4cfe18101322)

- In PC1’s ARP table, the entry for 10.0.0.1 will have the ATTACKER’S MAC ADDRESS
- When PC1 tries to send traffic to SRV1, it will be forwarded to the ATTACKER instead
- The ATTACKER can inspect the messages, and then forward them on to SRV1
- The ATTACKER can also modify the messages before forwarding them to SRV1
- This compromises the CONFIDENTIALITY and INTEGRITY of communication between PC1 and SRV1

![image](https://github.com/psaumur/CCNA/assets/106411237/07ebfebd-0686-436a-8990-853e3fee4377)

---

RECONNAISSANCE ATTACKS

- RECONNAISSANCE ATTACKS are not attacks themselves but they are used to gather information about a TARGET which can be used for a future attack
- This is often publicly available information
- IE: nslookup to learn the IP ADDRESS of a site

![image](https://github.com/psaumur/CCNA/assets/106411237/6e63b09d-a768-4cb3-ac06-87ad41d45c38)

- Or a WHOIS query to learn email addresses, phone numbers, physical addresses, etc.

https://lookup.icann.org/lookup

---

MALWARE

- MALWARE (MALICIOUS SOFTWARE) refers to a variety of harmful programs that can infect a computer
- VIRUSES infect other software (a ‘host program’)
    - The VIRUS spreads as the software is shared by USERS. Typically, they CORRUPT or MODIFY files on the TARGET computer
- WORMS do not require a host program. They are standalone malware and they are able to spread on their own, without user interaction. They spread of WORMS can congest the NETWORK but the ‘payload’ of a WORM can cause additional harm to TARGET DEVICES

- TROJAN HORSES are harmful software that is disguised as LEGITIMATE software. They are spread through user interaction such as opening email attachments, downloading a file from the Internet.

The above MALWARE types can exploit various VULNERABILITIES to threaten any of the CIA of a TARGET DEVICE

** There are MANY types of MALWARE

---

SOCIAL ENGINEERING ATTACKS

- SOCIAL ENGINEERING ATTACKS target the most vulnerable part of ANY system - PEOPLE!
- They involve psychological manipulation to make the TARGET reveal confidential information or perform some action

- PHISHING typically involves fraudulent emails that appear to come from a legitimate business (Amazon, bank, credit card company, etc) and contain links to a fraudulent website that seems legitimate. Users are told to login to the fraudulent website, providing their login credentials to the attacker.
    - SPEAR PHISHING is a more targeted form of phishing, ie: aimed at employees of a certain company
    - WHALING is a phishing targeted at high-profile individuals, ie: a company president
- VISHING (Voice Phishing) is phishing performed over a phone

- SMISHING (SMS Phishing) is phishing using SMS text messages

- WATERING HOLE attacks compromise sites that the TARGET victim frequently visits. If a malicious link is placed on a website the TARGET trusts, they might not hesitate to click it
- TAILGATING attack involves entering restricted, secured areas by simply walking in behind an authorized person as they enter. Often the TARGET will hold the door open for the ATTACKER to be polite, assuming the ATTACKER is also authorized to enter.

---

PASSWORD-RELATED ATTACKS

- Most systems use a USERNAME / PASSWORD combination to AUTHENTICATE users
- The USERNAME is often simple / easy to guess (for example the user’s email address) and the strength and secrecy of the password is relied on to provide the necessary security
- ATTACKERS can learn a user’s passwords via multiple methods:
    - Guessing
    - DICTIONARY ATTACK :
        - A program runs through a ‘dictionary’ or list of common words / passwords to find the TARGET’S password
    - BRUTE FORCE ATTACK :
        - A program tries every possible combination of letters, numbers, and special characters to find the TARGET’S password

- STRONG PASSWORDS should contain:
    - At LEAST 8 characters (preferably more)
    - A mixture of UPPERCASE and LOWERCASE letters
    - A mixture of LETTERS and NUMBERS
    - One of more SPECIAL CHARACTERS (# @ ! ? etc.)
    - Should be CHANGED REGULARLY

---

PASSWORDS / MULTI-FACTOR AUTHENTICATION (MFA)

- MULTI-FACTOR AUTHENTICATION involves providing more than just a USERNAME / PASSWORD to prove your identity
- It usually involves providing TWO of the following ( = Two-Factor Authentication) :
    - SOMETHING YOU KNOW
        - A USERNAME / PASSWORD combination, a PIN, etc.
        
    - SOMETHING YOU HAVE
        - Pressing a notification that appears on your phone, a badge that is scanned, etc.
    
    - SOMETHING YOU ARE
        - Biometrics such as a face scan, palm scan, fingerprint scan, retina scan, etc.

- Requiring multiple factors of AUTHENTICATION greatly increases the security. Even if the ATTACKER learns the TARGET’S PASSWORD (SOMETHING YOU KNOW), they won’t be able to login to the TARGET’S account

---

DIGITAL CERTIFICATES

- DIGITAL CERTIFICATES are another form of AUTHENTICATION used to prove the identity of the holder of the certificate
- They are used for websites to verify that the website being accessed is legitimate
- Entities that want a certificate to prove their identity send a CSR (CERTIFICATE SIGNING REQUEST) to a CA (CERTIFICATE AUTHORITY) which will generate and sign the certificate

---

CONTROLLING AND MONITORING USERS WITH AAA

- AAA (Triple-A) stands for AUTHENTICATION, AUTHORIZATION, and ACCOUNTING
- It is a framework for controlling and monitor users of a computer system (ie: a network)

- AUTHENTICATION
    - Process of verifying a user’s identity
    - Logging in = AUTHENTICATION
- AUTHORIZATION
    - Process of granting the user the appropriate access and permissions
    - Granting the user access to some files / services, restricting access to other files / services = AUTHORIZATION

- ACCOUNTING
    - Process of recording the user’s activities on the system
    - Logging when a user makes a change to a file = ACCOUNTING

- Enterprises typically use a AAA server to provide AAA services
    - ISE (Identity Services Engine) is Cisco’s AAA server

- AAA Servers usually support the following TWO AAA Protocols:
    - RADIUS :  Open Standard Protocol
        - Uses UDP PORTS 1812 and 1813
        
    - TACACS+ : Cisco Proprietary Protocol
        - Uses TCP PORT 49

<aside>
💡 FOR THE CCNA, KNOW THE DIFFERENCES BETWEEN AUTHENTICATION, AUTHORIZATION, and ACCOUNTING

</aside>

---

SECURITY PROGRAM ELEMENTS

- USER AWARENESS PROGRAMS are designed to make employees aware of potential security threats and risks
- USER TRAINING PROGRAMS are formal than USER AWARENESS PROGRAMS
- PHYSICAL ACCESS CONTROL protect equipment and data from potential attackers by only allowing authorized users into the protected areas such as NETWORK CLOSETS or DATA CENTER FLOORS
