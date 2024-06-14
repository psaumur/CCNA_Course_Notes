# 57. WIRELESS SECURITY

INTRO TO WIRELESS NETWORK SECURITY

- Although SECURITY is important in ALL NETWORKS, it is even more essential in WIRELESS NETWORKS
- Because WIRELESS SIGNALS are not contained within a WIRE, any DEVICE within range of the signal can receive traffic
- In WIRED NETWORKS, traffic is often only ENCRYPTED when sent over an UNTRUSTED NETWORK such as the INTERNET
- In WIRELESS NETWORKS, it is VERY important to ENCRYPT traffic sent between the WIRELESS CLIENTS and the AP

- We will cover THREE MAIN CONCEPTS:
    - AUTHENTICATION
    - ENCRYPTION
    - INTEGRITY

---

AUTHENTICATION

- All CLIENTS must be AUTHENTICATED before they can associate with an AP
- In a corporate setting, only TRUSTED USERS / DEVICES should be given ACCESS to the NETWORK
    - In corporate settings, a separate SSID which doesn’t have ACCESS to the corporate NETWORK can be provided for GUEST USERS
- Ideally, CLIENTS should also AUTHENTICATE the AP to avoid associating with a malicious AP
- There are MULTIPLE WAYS to AUTHENTICATE:
    - PASSWORD
    - USERNAME / PASSWORD
    - CERTIFICATES

![image](https://github.com/psaumur/CCNA/assets/106411237/00d34740-8da7-428d-8b36-f8998ec2f0cd)

---

ENCRYPTION

- Traffic sent between CLIENTS and APs should be ENCRYPTED so that it can’t be read by anyone except the AP and the CLIENT
- There are many possible PROTOCOLS that can be used to ENCRYPT traffic
- All DEVICES on the WLAN will use the same PROTOCOL, however each CLIENT will use a unique ENCRYPTION / DECRYPTION KEY so that other DEVICES can’t read its traffic
- A “GROUP KEY” is used by the AP to ENCRYPT traffic that it wants to send to all of its clients
    - All of the CLIENTS associated with the AP keep that key so they can DECRYPT the traffic
    

---

INTEGRITY

- As explained in the “SECURITY FUNDAMENTALS” video of the course, INTEGRITY ensures that the message is not modified by a third-party
- The message that is sent by the SOURCE HOST should be the same as the message that is received by the DESTINATION HOST
- A MIC (Message Integrity Check) is added to the message to help protect their INTEGRITY.

![image](https://github.com/psaumur/CCNA/assets/106411237/b632c321-36e5-4a03-b08c-d0a2c2e215da)

---

AUTHENTICATION METHODS

The original 802.11 STANDARD included TWO OPTIONS for AUTHENTICATION:

- OPEN AUTHENTICATION
    - The CLIENT sends an AUTHENTICATION REQUEST and the AP just accepts it
    - The is clearly NOT a SECURE AUTHENTICATION method
    - After the CLIENT is AUTHENTICATED and associated with the AP, it’s possible to require the USER to AUTHENTICATE via other methods before ACCESS to the NETWORK is granted (ie: Starbucks WI-FI)
- WEP (Wired Equivalent Privacy)
    - WEP is used to provide both AUTHENTICATION and ENCRYPTION of WIRELESS traffic
    - For ENCRYPTION, WEP uses the RC4 ALGORITHM
    - WEP is a “SHARED-KEY” PROTOCOL, requiring the SENDER and RECEIVER to have the same KEY
    - WEP KEYS can be 40 bits or 104 bits in length
    - The above KEYS are combined with a 24-bit “IV” (INITIALIZATION VECTOR) to bring the total length to 64 bits or 128 bits
    - WEP ENCRYPTION is NOT SECURE and can easily be cracked
    - WEP can be used for AUTHENTICATION like this:
    

![image](https://github.com/psaumur/CCNA/assets/106411237/86e4f243-1692-41a6-9b15-6b2e99942e50)

---

EAP (Extensible Authentication Protocol)

- EAP is an AUTHENTICATION FRAMEWORK
- It defines a STANDARD SET of AUTHENTICATION FUNCTIONS that are used by the various *EAP METHODS*
- We will look at FOUR EAP METHODS:
    - LEAP
    - EAP-FAST
    - PEAP
    - EAP-TLS
- EAP is integrated with **802.1X** which provides *PORT-BASED NETWORK ACCESS CONTROL*

**802.1X** is used to limit NETWORK ACCESS for CLIENTS connected to a LAN or WLAN until they AUTHENTICATE

There are **THREE MAIN ENTITIES** in 802.1X:

- SUPPLICANT : The DEVICE that wants to connect to the NETWORK
- AUTHENTICATOR : The DEVICE that provides access to the NETWORK
- AUTHENTICATION SERVER (AS) : The DEVICE that receives CLIENT credentials and PERMITS / DENIES ACCESS

![image](https://github.com/psaumur/CCNA/assets/106411237/5565e646-696f-4245-b1e5-d728fe0e3380)

- LEAP (Lightweight EAP)
    - LEAP was developed by Cisco an an improvement over WEP
    - CLIENTS must provide a USERNAME and PASSWORD to AUTHENTICATE
    - In addition, *MUTUAL AUTHENTICATION* is provided by both the CLIENT and SERVER sending a CHALLENGE PHRASE to each other.
    - DYNAMIC WEP KEYS are used, meaning that the WEP KEYS are changed frequently
    - Like WEP, LEAP is considered vulnerable and should not be used anymore

![image](https://github.com/psaumur/CCNA/assets/106411237/0b9ecce2-4219-42d0-8275-086b92134cda)

- EAP-FAST (EAP FLEXIBLE AUTHENTICATION via SECURE TUNNELING)
    - EAP-FAST was also developed by Cisco
    - Consists of THREE PHASES:
        - A PAC (PROTECTED ACCESS CREDENTIAL) is generated and passed from SERVER to CLIENT
        - A SECURE TLS TUNNEL is established between the CLIENT and AUTHENTICATION SERVER
        - Inside of the SECURE (ENCRYPTED) TLS TUNNEL, the CLIENT and SERVER communicated further to AUTHENTICATE / AUTHORIZE the CLIENT
    

![image](https://github.com/psaumur/CCNA/assets/106411237/f17d6f7b-9f87-4cb2-be24-5d8c95dc0cfc)

- PEAP (PROTECTED EAP)
    - Like EAP-FAST, PEAP involves establishing a SECURE TLS TUNNEL between the CLIENT and SERVER
    - Instead of a PAC, the SERVER has a DIGITAL CERTIFICATE
    - The CLIENT uses this DIGITAL CERTIFICATE to AUTHENTICATE the SERVER
    - The CERTIFICATE is also used to establish a TLS TUNNEL
    - Because only the SERVER provides a CERTIFICATE for AUTHENTICATION, the CLIENT must still be AUTHENTICATED within the SECURE TUNNEL
        - Example: MS-CHAP (Microsoft Challenge-Handshake Authentication Protocol)

![image](https://github.com/psaumur/CCNA/assets/106411237/0f9babe7-d86f-49c8-b732-20f31ea26437)

- EAP-TLS (EAP TRANSPORT LAYER SECURITY)
    - Whereas PEAP only requires the AS to have a CERTIFICATE, EAP-TLS requires a CERTIFICATE on the AS and on every single CLIENT
    - EAP-TLS is the MOST SECURE WIRELESS AUTHENTICATION method, but it is more difficult to implement than PEAP because every CLIENT DEVICE needs a CERTIFICATE
    - Because the CLIENT and SERVER AUTHENTICATE each other with DIGITAL CERTIFICATES, there is no need to AUTHENTICATE the CLIENT within the TLS TUNNEL
    - The TLS TUNNEL is still used to exchange ENCRYPTION KEY information (ENCRYPTION methods will be discussed next)

![image](https://github.com/psaumur/CCNA/assets/106411237/c6c57595-fd75-4761-8760-29fab8dbf698)

---

ENCRYPTION / INTEGRITY METHODS

- TKIP (Temporal Key Integrity Protocol)
    - WEP was found to be vulnerable, but WIRELESS hardware at the time was built to use WEP
    - A temporary solution was needed until a new STANDARD was created and a new HARDWARE was built
    - TKIP adds various SECURITY FEATURES:
        - A MIC (Message Integrity Check) is added to protect the integrity of messages
        - A KEY MIXING ALGORITHM is used to create a unique WEP key for every frame
        - The INITIALIZATION VECTOR is doubled in length from 24 bits to 48 bits, making BRUTE-FORCE attacks much more difficult
        - The MIC includes the SENDER MAC ADDRESS to identify the FRAME’s SENDER
        - A TIMESTAMP is added to the MIC to prevent replay attacks. Replay attacks involved re-resending a FRAME that has already been transmitted
        - A TKIP SEQUENCE NUMBER is used to keep track of FRAMES sent from each SOURCE MAC ADDRESS. This also protects against REPLAY ATTACKS

** You probably don’t need to memorize ALL of the above features

** TKIP is used in WPA version 1, which will be discussed in the next section

- CCMP (Counter / CBC-MAC Protocol)
    - CCMP was developed after TKIP and is more SECURE
    - It is used in WPA2
    - To use CCMP, it must be supported by the DEVICE’S hardware.
    - Old hardware built only to use WEP / TKIP cannot use CCMP
    - CCMP consists of TWO DIFFERENT ALGORITHMS to provide ENCRYPTION and MIC :
        - AES (Advanced Encryption Standard) COUNTER MODE ENCRYPTION
            - AES is the MOST SECURE ENCRYPTION PROTOCOL currently available.
            - Widely used all over the world
            - There are multiple MODES of operation for AES.
            - CCMP uses “COUNTER MODE”
        - CBC-MAC (CIPHER BLOCK CHAINING MESSAGE AUTHENTICATION CODE)
            - Used as a MIC to ENSURE the INTEGRITY of MESSAGES

- GCMP (GALOIS / COUNTER MODE PROTOCOL)
    - GCMP is MORE SECURE and EFFICIENT than CCMP
    - Its increased efficiency allows higher data throughput than CCMP
    - It is used in WPA3
    - GCMP consists of TWO ALGORITHMS:
        - AES COUNTER MODE ENCRYPTION
        - GMAC (GALOIS MESSAGE AUTHENTICATION CODE)
            - Used as a MIC to ENSURE the INTEGRITY of MESSAGE

---

WI-FI PROTECTED ACCESS (WPA)

- The WI-FI Alliance has developed THREE WPA CERTIFICATIONS for WIRELESS DEVICES:
    - WPA
    - WPA2
    - WPA3
- To be WPA-CERTIFIED, EQUIPMENT must be TESTED in authorized testing labs
- All of the above support TWO AUTHENTICATION MODES:
    - PERSONAL MODE :
        - A PRE-SHARED KEY (PSK) is used for AUTHENTICATOIN
        - When you connect to a home WI-FI NETWORK, enter the PASSWORD and are AUTHENTICATED, that is PERSONAL MODE
        - This is common in small NETWORKS
        - The PSK itself is NOT sent over the air
        - A FOUR-WAY HANDSHAKE is used for AUTHENTICATION and the PSK is used to GENERATE ENCRYPTION KEYS
    - ENTERPRISE MODE :
        - 802.1X is used with an AUTHENTICATION SERVER (RADIUS SERVER)
        - No specific EAP METHOD is specified, so all are supported (PEAP, EAP-TLS, etc)
    
    WPA
    
    - The WPA CERTIFICATION was developed after WEP was proven to be vulnerable and includes the following PROTOCOLS:
        - TKIP (based on WEP) provides ENCRYPTION / MIC
        - 802.1X AUTHENTICATION (ENTERPRISE MODE) or PSK (PERSONAL MODE)
    
    WPA2
    
    - Was released in 2004 and includes the following PROTOCOLS:
        - CCMP provides ENCRYPTION / MIC
        - 802.1X AUTHENTICATION (ENTERPRISE MODE) or PSK (PERSONAL MODE)
    
    WPA3
    
    - Was released in 2018 and includes the following PROTOCOLS:
        - GCMP provides ENCRYPTION / MIC
        - 802.1X AUTHENTICATION (ENTERPRISE MODE) or PSK (PERSONAL MODE)
        
        - WPA3 also provides several additional security features:
            - PMF (PROTECTED MANAGEMENT FRAMES)
                - Protecting 802.11 MANAGEMENT FRAMES from eavesdropping / forging
            - SAE (SIMULTANEOUS AUTHENTICATION OF EQUALS)
                - Protects the four-way handshake when using PERSONAL MODE AUTHENTICATION
            - FORWARD SECRECY
                - Prevents DATA from being DECRYPTED after it has been transmitted over the air so an ATTACKER can’t capture WIRELESS FRAMES and then try to DECRYPT them later
