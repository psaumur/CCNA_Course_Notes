# 42. SSH (Secure Shell)

CONSOLE PORT SECURITY

- By DEFAULT, no password us needed to access the CLI of a CISCO IOS DEVICE via the CONSOLE PORT
- You can CONFIGURE a PASSWORD on the *console line*
    - A USER will have to enter a PASSWORD to ACCESS the CLI via the CONSOLE PORT

![image](https://github.com/psaumur/CCNA/assets/106411237/9609b0af-0fb1-4563-89e4-82b58b29325e)

- Alternatively, you can configure the CONSOLE LINE to require USERS to LOGIN using one of the configured USERNAMES on the DEVICE

![image](https://github.com/psaumur/CCNA/assets/106411237/04588b3a-3640-41af-b19e-41768f63b2bc)

---

LAYER 2 SWITCH MANAGEMENT IP

- LAYER 2 SWITCHES do not perform PACKET ROUTING and build a ROUTING TABLE. They are NOT IP ROUTING aware
- However, you CAN assign an IP ADDRESS to an SVI to allow REMOTE CONNECTIONS to the CLI of the SWITCH (using Telnet or SSH)

![image](https://github.com/psaumur/CCNA/assets/106411237/64a9e983-f353-4670-8a99-1e22129eb661)

---

TELNET

- TELNET (Teletype Network) is a PROTOCOL used to REMOTELY ACCESS the CLI of a REMOTE HOST
- TELNET was developed in 1969
- TELNET has been largely REPLACE by SSH, which is MORE Secure
- TELNET sends data in PLAIN TEXT. NO ENCRYPTION(!)

<aside>
💡 TELNET SERVERS listen for TELNET traffic on TCP PORT 23

</aside>

![image](https://github.com/psaumur/CCNA/assets/106411237/9dffe7fb-4fa4-4ee9-90bf-d27461bb5190)

---

VERIFY TELNET CONFIGURATION

![image](https://github.com/psaumur/CCNA/assets/106411237/e077b5fd-3130-4fb0-9b17-d28bdef665df)

---

SSH

- SSH (Secure Shell) was developed in 1995 to REPLACE LESS SECURE PROTOCOLS, like TELNET
- SSHv2, a major revision of SSHv1, was released in 2006
- If a DEVICE supports both v1 and v2, it is said to run ‘version 1.99’
- Provides SECURITY features; such as DATA ENCRYPTION and AUTHENTICATION

CHECK SSH SUPPORT

![image](https://github.com/psaumur/CCNA/assets/106411237/441c38b7-4b79-4c80-8eca-0463960124b6)

RSA KEYS

- To ENABLE and use SSH, you must first generate an RSA PUBLIC and PRIVATE KEY PAIR
- The KEYS are used for DATA ENCRYPTION / DECRYPTION, AUTHENTICATION, etc.

![image](https://github.com/psaumur/CCNA/assets/106411237/73bd5a86-32da-4ec6-b385-fe5425a72808)

VTY LINES

![image](https://github.com/psaumur/CCNA/assets/106411237/04e9072f-ccde-476d-a84d-3034e0b39d19)

---

SUMMARY ABOUT SSH CONFIGURATIONS

![image](https://github.com/psaumur/CCNA/assets/106411237/bb6d358f-e742-434b-835c-5c7cd762abdb)

![image](https://github.com/psaumur/CCNA/assets/106411237/bb2e760b-90c3-42a7-93f6-0ccc7e472d00)
