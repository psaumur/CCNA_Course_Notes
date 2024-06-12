# 3. OSI MODEL & TCP/IP SUITE

## What is a networking model?

Networking models categorize and provide a structure for networking protocols and standards.

(Protocols are a set of logical rules defining how network devices and software should work)

## OSI MODEL

- Open Systems Interconnection Model
- Conceptual model that categorizes and standardizes the different functions in a network.
- Created by the "International Organization for Standardization" (ISO)
- Functions are divided into 7 "Layers"
- These layers work together to make the network work.

![image](https://github.com/psaumur/CCNA/assets/106411237/bbf46de2-e025-4ddd-b52b-614b280598da)

As data moves from the top layer, downward, the process is called “encapsulation”

As data moves from the bottom layer, upward, the process is called “de-encapsulation”

When interactions occur on the same layer, it’s called “same-layer interaction”

![image](https://github.com/psaumur/CCNA/assets/106411237/b7cf4900-993c-49f0-b6ea-70f4f0719633)

Mnemonic to help remember the Data Layer Names / Order

![image](https://github.com/psaumur/CCNA/assets/106411237/01f532f6-b636-4b7c-99d0-a67f7e483a99)


### The layers are :

### 7 - APPLICATION

- This Layer is closest to end user.
- Interacts with software applications.
- HTTP and HTTPS are Layer 7 protocols

Functions of Layer 7 include:

- Identifying communication partners
- Synchronizing communication

---

### 6 - PRESENTATION

- Translates data to the appropriate format (between Application and Network formats) to be sent over the network.

---

### 5 - SESSION

- Controls dialogues (sessions) between communicating hosts.
- Establishes, manages, and terminates connections between local application and the remote application.

---

Network engineers don't usually work with the top 3 layers.
Application developers work with the top layers of the OSI model to connect their applications over networks.

---

### 4 - TRANSPORT

- Segments and reassembles data for communication between end hosts.
- Breaks large pieces of data into smaller segments which can be more easily sent over the network and are less likely to cause transmission problems if errors occur.
- Provides HOST-TO-HOST (end to end) communication

When Data from Layer 7-5 arrives, it receives a Layer 4 Header in the Transport layer.

<< DATA + L4 Header >>

This is called a SEGMENT.

---

### 3 - NETWORK

- Provides connectivity between end hosts on different networks (ie: outside of the LAN).
- Provides logical addressing (IP Addresses).
- Provides path selection between source and destination
- **ROUTERS** operate at Layer 3.

When Data and the Layer 4 Header arrive in the Network Layer, it receives a Layer 3 Header.

<< DATA + L4 Header + L3 Header >>

This is called a **PACKET**.

---

### 2 - DATA LINK

- Provides NODE-TO-NODE connectivity and data transfer (for example, PC to Switch, Switch to Router, Router to Router)
- Defines how data is formatted for transmission over physical medium (for example, copper UTP cables)
- Detects and (possibly) corrects Physical (Layer 1) errors.
- Uses Layer 2 addressing, separate from Layer 3 addressing.
- **SWITCHES** operate at Layer 2

When the Layer 3 Packet arrives, a Layer 2 Trailer and Header are added.

<< L2 Trailer + DATA + L4 Header + L3 Header + L2 Header >>

This is called a FRAME.

All the steps leading up to transmission is called ENCAPSULATION.
When the frame is sent to the receiver, it then goes through the reverse process, DE-ENCAPSULATION, stripping off layers while travelling from OSI Layer 1 to Layer 7.

---

### 1 - PHYSICAL

- Defines physical characteristics of the medium used to transfer data between devices. For example : voltage levels, maximum transmission distances, physical connectors, cable specs.
- Digital bits are converted into electrical (for wired connections) or radio (for wireless connections) signals.
- All of the information in SECTION 2 (NETWORKING DEVICES) is related to the Physical Layer

---

### OSI MODEL - PDU's

![image](https://github.com/psaumur/CCNA/assets/106411237/9b885a51-91cd-4fe6-b1be-e7fa7aa220b5)

A PDU is a Protocol Data Unit. Each step of the process is a PDU.

| OSI LAYER # | PDU NAME | PROTOCOL DATA ADDED |
| --- | --- | --- |
| 7-5 | DATA | Data |
| 4 | SEGMENT | Layer 4 Header Added |
| 3 | PACKET | Layer 3 Header Added |
| 2 | FRAME | Layer 2 Trailer and Header Added |
| 1 | BIT | 0s and 1s Transmission |

<< L2 Trailer + DATA + L4 Header + L3 Header + L2 Header >>

---

### TCP/IP Suite

- Conceptual model and set of communications protocols used in the Internet and other networks.
- Known as TCP/IP because those are two of the foundational protocols in the suite.
- Developed by the US Dept. of Defense through DARPA (Defense Advanced Research Projects Agency).
- Similar structure to the OSI Model, but fewer layers.
- THIS is the model actually in use in modern networks.
- * Note : The OSI Model still influences how network engineers think and talk about networks.

![image](https://github.com/psaumur/CCNA/assets/106411237/e9593c06-46a3-4ff9-aa01-863e0aeb5df3)


---

### Layer Interactions

![image](https://github.com/psaumur/CCNA/assets/106411237/372c45a0-bb3e-4342-af2b-79d3606384ec)


Adjacent-Layer Interactions:

- Interactions between different layers of the OSI Model on same host.

Example:

Layers 5-7 sending Data to Layer 4, which then adds a Layer 4 header (creating a SEGMENT).

Same-Layer Interactions:

- Interactions between the same Layer on different hosts.
- The concept of Same-Layer interaction allows you to ignore the other layers involved and focus on the interactions between a single layer on different devices.

Example:

The Application Layer of YouTube's web server and your PC's browser.
