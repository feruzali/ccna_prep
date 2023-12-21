---
description: Virtualization & Cloud, Containers, VRF
---

# Day 54

Besides networking devices, Cisco also offers **UCS** (Unified Computing System).

<figure><img src=".gitbook/assets/image (13).png" alt="UCS examples" width="563"><figcaption></figcaption></figure>

Before virtualization, there was a one-to-one relationship between a physical and an operation system. In that OS, apps providing services such as a web server, email server, etc. would run. One physical server would be used for the web server, one for the email server, one for the database server, etc. This is inefficient because each physical server is expensive and takes up space, power, etc. and the resources on each physical server are under-used.

<figure><img src=".gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt="server&#x27;s structure" width="375"><figcaption></figcaption></figure>

### Virtualization

Virtualization allows us to break the one-to-one relationship of hardware to OS, allowing multiple OS's to run on a single device. Each instance is called a **VM** (Virtual Machine). A **hypervisor** (aka **VMM** - Virtual Machine Monitor) is used to manage and allocate the hardware resources to each VM. Virtualization provides:

* Partitioning - run multiple OS on one physical machine
* Isolation - provide fault and security isolation at the hardware level
* Encapsulation - save the entire state of a VM to files
* Hardware Independence - migrate any VM to any physical server

The type of hypervisor which runs directly on top of the hardware is called a **Type 1** hypervisor (aka **bare-metal hypervisor**/**native hypervisor**), e.g. VMware ESXi or Microsoft Hyper-V. It is used in data center environments.

<figure><img src=".gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt="type 1 hypervisor" width="375"><figcaption></figcaption></figure>

**Type 2** hypervisors (aka **hosted hypervisor**) run as a program on an OS like a regular program, e.g. VMware Workstation or Oracle VirtualBox. The OS running directly on the hardware is called the **Host OS**, and the OS running in a VM is called a **Guest OS**. Type 2 hypervisors are usually used on personal-use devices.

To connect VMs to the network, a virtual switch running on the hypervisor is used. Virtual switches act the same as regular switches.

<figure><img src=".gitbook/assets/image (3) (1) (1) (1) (1) (1).png" alt="vSwitch demo" width="563"><figcaption></figcaption></figure>

### Cloud

Traditional IT infrastructure deployments were a combination of the following:

* On-Premises: All servers, network devices and other infrastructure are located on company property. The company is responsible for the necessary space, power, and cooling.
* Colocation: Data centers that rent out space for customers to put their infrastructure. The data center provides space, electricity, and cooling. The servers and network devices are still the responsibility of the end customer.

Cloud computing is a model for enabling ubiquitous, convenient, on-demand network access to a shared pool of configurable computing resources (networks, servers, storage, applications, and services) that can be rapidly provisioned and released with minimal management effort or service provider interaction. This cloud model is composed of five essential characteristics, three service models, and four deployment models.

Five essential characteristics:

* On-demand self-service: the customer can use the service freely without direct communication with the service provider.&#x20;
* Broad network access: the service is available through standard network connections and can be accessed through many kinds of devices.
* Resource pooling: A pool of services is provided by the service provider, and when a customer requests a service, the resources are allocated from the shared pool.
* Rapid elasticity: Customers can quickly expand or reduce the services they use in the cloud from a pool of resources that appears to be infinite.&#x20;
* Measured service: The cloud service provider measures the customer's usage of cloud resources. Customers are charged based on usage.

In cloud computing, everything is provided on a service model. Three service models of cloud computing:

* Software as a Service
* Platform as a Service
* Infrastructure as a Service

<figure><img src=".gitbook/assets/image (4) (1) (1) (1) (1).png" alt="service model" width="563"><figcaption></figcaption></figure>

The four deployment models of cloud computing (all may exist on or off premises):

* Private cloud: mainly used by large enterprises.&#x20;
* Community cloud: the least common one, similar to private cloud but the infrastructure is reserved for use by only a specific group of organizations.&#x20;
* Public cloud: the most common one. Open use by the general public.
* Hybrid cloud: a combination of two or more of the above, e.g. a private cloud which can offload to public when necessary.

The ways to connect to cloud resources:

<figure><img src=".gitbook/assets/image (5) (1) (1) (1) (1).png" alt="connection to cloud" width="563"><figcaption></figcaption></figure>

### Containers

**Containers** are software packages that contain an App and all dependencies for the contained app to run. Containers run on a **Container Engine** (ie. Docker Engine). The container engine runs on a host OS.  Containers are lightweight and include only the dependencies required to run the specific app. A **Container Orchestrator** (ie. Kubernetes) is a software platform for automating the deployment, management, scaling, etc. In small numbers, manual operation is possible but large-scale systems can require thousands of containers. **Microservice Architecture** is an approach to software architecture that divides a larger solution into smaller parts (microservices). Those microservices all run in containers that can be orchestrated by a container orchestrator.

<figure><img src=".gitbook/assets/image (7) (1) (1) (1) (1).png" alt="containers example" width="375"><figcaption></figcaption></figure>

#### VMs vs Containers

* VMs can take minutes to boot up as each VM runs its own OS. Containers can boot up in milliseconds.
* VMs take up more disk space compared to containers.
* VMs use more CPU/RAM resources compared to containers.
* VMs are portable and can move between physical systems running the same hypervisor. Containers are more portable and can be run on nearly any container service.
* VMs are more isolated compared to containers because they run their own OS.

### VRF

**VRF** (Virtual Routing and Forwarding) is used to divide a single router into multiple virtual routers, similar to VLANs. It does this by allowing a router to build multiple separate routing tables. Layer 3 interfaces and routes are configured to be in a specific VRF. Traffic in one VRF cannot be forwarded out of an interface in another VRF. This is **VRF-lite** (VRF without MPLS). VRF is commonly used to facilitate MPLS. VRF-lite is commonly used by service providers to allow one device to carry traffic from multiple customers. Each customer's traffic is isolated and their IP addresses can overlap without any issues.

<figure><img src=".gitbook/assets/image (8) (1) (1) (1).png" alt="VRF demo" width="563"><figcaption></figcaption></figure>

To configure VRF on a router, first create a VRF with the command `ip vrf` followed by a name. Then assign interfaces to VRFs with the command `ip vrf forwarding` followed by the VRF name in the interface config mode. If an interface has an IP address configured, it is removed when the interface is assigned to a VRF. To view the routing table of VRF, use the command `show ip route vrf` followed by the VRF name.

{% file src=".gitbook/assets/Day 54 (part 1) Flashcards - Virtualization _ Cloud.apkg" %}

{% file src=".gitbook/assets/Day 54 (part 2) Flashcards - Containers.apkg" %}

{% file src=".gitbook/assets/Day 54 (part 3) Flashcards - VRF.apkg" %}

{% embed url="https://youtu.be/swqADfQk2jM" %}
