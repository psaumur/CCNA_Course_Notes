# 54. VIRTUALIZATION AND CLOUD: PART 1

VIRTUAL SERVERS

- Although Cisco is more known for their networking DEVICES (ROUTERS, SWITCHES, FIREWALLS), they also offer HARDWARE SERVERS such as UCS (Unified Computing System)
- The largest vendors of HARDWARE SERVERS include Dell, EMC, HPE, and IBM

---

SERVERS BEFORE VIRTUALIZATION

![image](https://github.com/psaumur/CCNA/assets/106411237/365cde17-88c6-4149-91f2-d67c79590aec)

- Before VIRTUALIZATION, there was a one-to-one relationship between a PHYSICAL SERVER and OPERATION SYSTEM
- In that OPERATING SYSTEM, apps providing SERVICES (such as a WEB SERVER, EMAIL SERVER, etc) would run
- One PHYSICAL SERVER would be used for the WEB SERVER, one for the EMAIL SERVER, one for the DATABASE SERVER, etc.
- This is inefficient for multiple reasons:
    - Each PHYSICAL SERVER is expensive and takes up space, power, etc.
    - The RESOURCES on each PHYSICAL SERVER (CPU, RAM, STORAGE, NIC) are typically under-utilized

---

VIRTUALIZATION (TYPE 1 HYPERVISOR)

![image](https://github.com/psaumur/CCNA/assets/106411237/62a40737-7451-4b38-a5bd-abd9367cbd40)

- VIRTUALIZATION allows us to break the one-to-one relationships of HARDWARE to OS, allowing multiple OS’s to run on a single PHYSICAL SERVER
- Each INSTANCE is called a VM (Virtual Machine)
- A HYPERVISOR is used to manage and allocate the HARDWARE RESOURCES (CPU, RAM, etc.) to each VM
- Another name for a HYPERVISOR is VMM (Virtual Machine Monitor)
- The type of HYPERVISOR which runs directly on top of hardware is called a TYPE 1 HYPERVISOR
    - Examples include : VMware ESXi, Microsoft Hyper-V, etc.
- TYPE 1 HYPERVISORS are also called *bare-metal hypervisors* because they run directly on the hardware (metal).
    - Another term is *native hypervisor*
- This is the type of HYPERVISOR used in data center environments

---

VIRTUALIZATION (TYPE 2 HYPERVISOR)

![image](https://github.com/psaumur/CCNA/assets/106411237/25a29935-a56d-4ffe-b9e4-15c5c50bca46)

- TYPE 2 HYPERVISORS run as a program on an OS like a regular computer program
    - Examples: VMware Workstation, Oracle Virtualbox, etc
- The OS running directly on the hardware is called the HOST OS
- The OS running in a VM is called a GUEST OS
- Another name for a TYPE 2 HYPERVISOR is *hosted hypervisor*
- Although TYPE 2 HYPERVISORS are rarely used in data center environments, they are common on personal-use devices (for example, if a MAC/Linux user needs to run an app that is only supported on Windows, or vice-versa)

---

WHY VIRTUALIZATION?

- PARTITIONING :
    - Run multiple OS’s on ONE PHYSICAL MACHINE
    - Divide system resources between VIRTUAL MACHINES
    
- ISOLATION :
    - Provide FAULT and SECURITY ISOLATION at the hardware level
    - Preserve performance with advanced resource controls
- ENCAPSULATION :
    - Save the entire state of a virtual machine to files
    - Move and copy virtual machines as easily as moving and copying files

- HARDWARE INDEPENDENCE :
    - Provision or migrate any virtual machine to any physical server

![image](https://github.com/psaumur/CCNA/assets/106411237/f0f5f886-7924-46fc-addf-6916f0d2b2c9)

---

VIRTUAL NETWORKS

![image](https://github.com/psaumur/CCNA/assets/106411237/7bf3f22c-a7b8-41bf-bc1e-8c128a41f20f)

- VMs are connected to each other and the EXTERNAL NETWORK via a VIRTUAL SWITCH running on the HYPERVISOR
- Just like a regular PHYSICAL SWITCH, the vSWITCH’s INTERFACES can operate as ACCESS PORTS or TRUNK PORTS and use VLANs to separate the VMs at LAYER 2
- INTERFACES on the vSWITCH connect to the PHYSICAL NIC (or NICs) of the SERVER to communicate with the EXTERNAL NETWORK

---

INTRO TO CLOUD COMPUTING

- Traditional IT infrastructure deployments were some combination of the following:
    - ON-PREMISES
        - All SERVERS, NETWORK DEVICES, and other infrastructure are located on company property
        - All equipment is purchased and owned by the company using it
        - The company is responsible for the necessary space, power, and cooling
    
    - CO-LOCATION
        - Data centers that rent out space for customers to put their infrastructure (SERVERS, NETWORK DEVICES)
        - The data center provides the space, electricity, and cooling
        - The SERVERS, NETWORK DEVICES, etc are still the responsibility of the end customer, although they are not located on the customer’s premises
- CLOUD SERVICE provide an alternative that is hugely popular and is continuing to grow
    - Most people associate “CLOUD” with PUBLIC CLOUD PROVIDERS such as AWS
        - Although this is the most common USE of CLOUD SERVICES, it’s not the only one

---

CLOUD SERVICES

- The American NIST (National Institute of Standards and Technology) defined cloud computing in SP (Special Publication) 800-145

![image](https://github.com/psaumur/CCNA/assets/106411237/746a4f38-01b9-49cf-8dd9-5522b4cabf7b)

- To understand what the CLOUD is, let’s look at the following outlined in SP 800-145:
    - FIVE ESSENTIAL CHARACTERISTICS
    - THREE SERVICE MODELS
    - FOUR DEPLOYMENT MODELS

---

THE FIVE ESSENTIAL CHARACTERISTICS OF CLOUD

- ON-DEMAND SELF-SERVICE
    - The CUSTOMER is able to use the SERVICE (or stop the SERVICE) freely (via a web portal) without direct communication to the SERVICE PROVIDER

- BROAD NETWORK ACCESS
    - The SERVICE is available through standard NETWORK connections (ie: the Internet or PRIVATE WAN) and can be access through many kinds of DEVICES
- RESOURCE POOLING
    - A POOL of RESOURCES is provided by the SERVICE PROVIDER and when a CUSTOMER requests a SERVICE (for example creates a new VM), the RESOURCES to fulfill that request are allocated from the shared POOL
- RAPID ELASTICITY
    - CUSTOMERS can quickly expand the SERVICE they use in the CLOUD (for example: add new VMs, expand STORAGE, etc) from a POOL of RESOURCES that appear to be infinite. Likewise, they can quickly reduce their SERVICES when not needed
- MEASURED SERVICE
    - The CLOUD SERVICE PROVIDER measures the CUSTOMER’s usage of CLOUD RESOURCES and the CUSTOMER can measure their own use as well. CUSTOMERS are charged based on usage (for example: X Dollars per Gigabyte of STORAGE per day)

---

THE THREE SERVICE MODELS OF THE CLOUD

![image](https://github.com/psaumur/CCNA/assets/106411237/a3f0e08a-3207-4a69-aa81-d4142d6735a3)

- In CLOUD COMPUTING, everything is provided on a “SERVICE” model
- For example: rather than the END USER buying a PHYSICAL SERVER, mounting it on a rack, installing the hypervisor, creating the VM, etc. the SERVICE PROVIDER offers all of this as a SERVICE
- There are a variety of SERVICES referred to as “___________ as a SERVICE” or “__aaS”
- The THREE SERVICE MODELS of CLOUD COMPUTING are:
    
    SOFTWARE as a SERVICE (SaaS) - Example : MS Office 365
    
![image](https://github.com/psaumur/CCNA/assets/106411237/5bcfedb7-3ab6-462a-a089-09884d220ab7)
    
    PLATFORM as a SERVICE (PaaS) - Examples : AWS Lambda and Google App Engine 
    
![image](https://github.com/psaumur/CCNA/assets/106411237/e3886b6b-4ed8-4358-ba47-e2f50378c53d)
    
    INFRASTRUCTURE as a SERVICE (Iaas) - Examples: Amazon EC2 and Google Compute Engine
    
![image](https://github.com/psaumur/CCNA/assets/106411237/f8144a61-0d7f-4928-9e47-73fb969e0b4a)
    

---

DEPLOYMENT MODELS

- Most people assume that “CLOUD” means PUBLIC CLOUD PROVIDERS like AWS, AZURE, and GCP
- Although “PUBLIC CLOUD” is the most common deployment model, it’s not the ONLY one
- The FOUR DEPLOYMENT MODELS of CLOUD COMPUTING are:

- PRIVATE CLOUD

![image](https://github.com/psaumur/CCNA/assets/106411237/b8953a31-3861-41ef-99df-62a49b97610a)

- PRIVATE CLOUDS are generally only used by large enterprises
- Although the CLOUD is PRIVATE, it may be owned by a THIRD PARTY
    - For example: AWS provides PRIVATE CLOUD SERVICES for the American DoD
- PRIVATE CLOUDS may be ON or OFF PREMISES
    - Many people assume “CLOUD” and “ON-PREM” are two different things but that is not always the case
- The same kind of SERVICES offered are the same as in PUBLIC CLOUDS (SaaS, PaaS, IaaS) but the infrastructure is reserved for a SINGLE ORGANIZATION

- COMMUNITY CLOUD

![image](https://github.com/psaumur/CCNA/assets/106411237/1c9008e9-205b-4ca8-8236-fc0b02c3addc)

- Least common CLOUD deployment
- Similar to PRIVATE CLOUD, but the INFRASTRUCTURE is reserved for use by a SPECIFIC GROUP or ORGANIZATION

- PUBLIC CLOUD

![image](https://github.com/psaumur/CCNA/assets/106411237/94e9c895-9538-4664-93db-085f013ee9fb)

- The most common CLOUD deployment
- Popular PUBLIC CLOUD service providers include:
    - AWS
    - MS AZURE
    - GCP (Google Cloud Platform)
    - OCI (Oracle Cloud Infrastructure)
    - IBM Cloud
    - Alibaba Cloud

- HYBRID CLOUD
    
![image](https://github.com/psaumur/CCNA/assets/106411237/14f910cf-b6e2-4f75-8959-4589d2592e1c)
    
    - Basically ANY combination of the preview THREE DEPLOYMENT TYPES
    - Example: A PRIVATE CLOUD which can offload to a PUBLIC CLOUD when necessary

---

BENEFITS OF CLOUD COMPUTING

- COST
    - CapEx (Capital Expense) of buying HARDWARE and SOFTWARE, setting up DATA CENTERS, etc. are reduced or eliminated
- GLOBAL SCALE
    - CLOUD SERVICES can scale GLOBALLY at a rapid pace. SERVICES can be set up and offered to CUSTOMERS from a geographic location close to them

- SPEED / AGILITY
    - SERVICES are provide ON DEMAND and vast amounts of RESOURCES can be provisioned within minutes

- PRODUCTIVITY
    - CLOUD SERVICES remove the need for many time-consuming tasks such as procuring physical servers, racking them, cabling, installing and updating equipment, etc.
- RELIABILITY
    - Backups in the CLOUD are very easy to perform. Data can be mirrored at multiple sites in different geographic locations to support disaster recovery

---

CONNECTION TO PUBLIC CLOUDS

![image](https://github.com/psaumur/CCNA/assets/106411237/671747bb-6908-47bb-b9c8-47f2df82c821)
