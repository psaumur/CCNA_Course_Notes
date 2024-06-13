# 30. TCP and UDP (LAYER 4 PROTOCOLS)

BASICS OF LAYER 4

- Provides TRANSPARENT transfer of DATA between END HOSTS (Host To Host communication)

![image](https://github.com/psaumur/CCNA/assets/106411237/b0309c1e-a283-428b-9d8b-c9c1568e6a58)

- Provides (or DOESN’T provide) various SERVICES to APPLICATIONS:
    - Reliable DATA Transfer
    - Error Recovery
    - Data Sequencing
    - Flow Control
- Provides LAYER 4 ADDRESSING (PORT numbers) - NOT the physical interfaces / ports on network devices
    - IDENTIFY the APPLICATION LAYER protocol
    - Provides SESSION multiplexing

---

WHAT IS A SESSION ? 

- A SESSION is an EXCHANGE of DATA between TWO or MORE communicating DEVICES

![image](https://github.com/psaumur/CCNA/assets/106411237/2d8c6c74-24e5-4574-b454-bc694f056bec)

The FOLLOWING ranges have been designated by IANA (Internet Assigned Numbers Authority) 

- **Well-Known** Port Numbers : 0 - 1023
- **Registered** Port Numbers : 1024 - 49151
- **Ephemeral** / Private / Dynamic port numbers : 49152 - 65535

![image](https://github.com/psaumur/CCNA/assets/106411237/02d56940-33b6-40a8-8431-0a39c19bc66a)

---

TCP (TRANSMISSION CONTROL PROTOCOL)

- A CONNECTION-ORIENTED protocol
    - Before actually SENDING DATA to the DESTINATION HOST, the TWO HOSTS communicate to establish a CONNECTION. Once the CONNECTION is established, DATA exchange begins.

![image](https://github.com/psaumur/CCNA/assets/106411237/9fcb7294-da61-4fff-b483-c1da6a8d7b48)

![image](https://github.com/psaumur/CCNA/assets/106411237/1f5b0753-b625-463b-9d6f-79bf5b2454dc)

Establishing connections

![image](https://github.com/psaumur/CCNA/assets/106411237/877a8e35-2e2d-4cf4-af65-1a1834308ba9)

Terminating connections

![image](https://github.com/psaumur/CCNA/assets/106411237/3a0a9cff-8bc4-4c1f-a9b0-941807cf6f40)

- TCP provides RELIABLE communication
    - The DESTINATION HOST must acknowledge that it RECEIVED each TCP SEGMENT (Layer 4 PDU)
    - If a SEGMENT isn’t ACKNOWLEDGED, it is sent again
    

![image](https://github.com/psaumur/CCNA/assets/106411237/d8349049-7a5a-40a3-95fa-7ad86ec1049d)

- TCP provides SEQUENCING
    - SEQUENCE numbers in the TCP HEADER allow DESTINATION HOSTS to put SEGMENTS in the correct ORDER even if they arrive out of ORDER

![image](https://github.com/psaumur/CCNA/assets/106411237/a1df1c41-df4f-4211-ac56-144280a2d3bf)

- TCP provides FLOW CONTROL
    - The DESTINATION HOST can tell the SOURCE HOST to increase / decrease the RATE that DATA is sent

![image](https://github.com/psaumur/CCNA/assets/106411237/f5f3f467-5b1f-4a30-9ef7-8a5c0de65139)

![image](https://github.com/psaumur/CCNA/assets/106411237/fafc82c7-21a2-46cf-b82b-702b2d8c1d52)

---

UDP (USER DATAGRAM PROTOCOL)

![image](https://github.com/psaumur/CCNA/assets/106411237/773a7e94-50b1-4179-b2e6-0d45ec5c1b3d)

- UDP is NOT a CONNECTION-ORIENTED PROTOCOL
    - The SENDING HOST does NOT establish a CONNECTION with the DESTINATION HOST before sending DATA. The DATA is simply SENT

- UDP DOES NOT provide reliable COMMUNICATION
    - When UDP is used, ACKNOWLEDGEMENTS are NOT SENT for received SEGMENTS
    - If a SEGMENT is LOST, UDP has no mechanism to re-TRASMIT it
    - SEGMENTS are sent “best-effort”
    
- UDP DOES NOT provide SEQUENCING
    - There is NO SEQUENCE NUMBER FIELD in the UDP header
    - If SEGMENTS arrive out of order, UDP has no MECHANISM to put them back in ORDER
    
- UDP DOES NOT provide FLOW CONTROL
    - UDP has NO MECHANISM like TCP’s WINDOW SIZE to control the flow of DATA
    
- UDP DOES provide ERROR CHECKING (via CHECKSUM)

---

COMPARING TCP AND UDP

Number of Fields in their Headers

![image](https://github.com/psaumur/CCNA/assets/106411237/90fb3d62-5011-4970-9cf6-167cccfe3449)

- TCP provides MORE FEATURES than UDP but at a COST of ADDITIONAL OVERHEAD
- For applications that require RELIABLE communications (for example, downloading a file), TCP is PREFERRED
- For applications, like real-time voice and video, UDP is preferred
- There are SOME applications that use UDP, but provide RELIABILITY, etc. within the APPLICATION itself.
- Some applications use BOTH TCP and UDP, depending on the situation.

![image](https://github.com/psaumur/CCNA/assets/106411237/fcbef599-9277-4b06-8d59-2349ca70817a)

IMPORTANT PORT NUMBERS

![image](https://github.com/psaumur/CCNA/assets/106411237/9e1f0422-d027-4a06-a359-d47c5c39dba1)
