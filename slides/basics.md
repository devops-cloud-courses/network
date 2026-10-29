## Basics

----

### OSI Model

| Layer # | Name | Description |
|---|---|---|
| 7 | Application layer | Human-computer interaction layer, where applications can access the network services |
| 6 | Presentation layer | Ensures that data is in a usable format and is where data encryption occurs |

----

### OSI Model

| Layer # | Name | Description |
|---|---|---|
| 5 | Session layer | Maintains connections and is responsible for controlling ports and sessions |
| 4 | Transport layer | Transmits data using transmission protocols including `TCP` and `UDP` |

----

### OSI Model

| Layer # | Name | Description |
|---|---|---|
| 3 | Network layer | Decides which physical path the data will take |
| 2 | Data link layer | Defines the format of data on the network |
| 1 | Physical layer | Transmits raw bit stream over the physical medium |

----

### OSI Model

| Layer # | Name | Example protocols |
|---|---|---|
| 7 | Application layer | `HTTP`, `FTP`, `DNS`, `SNMP` |
| 6 | Presentation layer | `SSL`, `TLS` |
| 5 | Session layer | `NetBIOS`, `PPTP` |
| 4 | Transport layer | `TCP`, `UDP` |

----

### OSI Model

| Layer # | Name | Example protocols |
|---|---|---|
| 3 | Network layer | `IP`, `ARP`, `ICMP`, `IPSec` |
| 2 | Data link layer | `PPP`, `ATM`, `Ethernet` |
| 1 | Physical layer | `Ethernet`, `USB`, `Bluetooth`, `IEEE 802.11` |

----

### TCP/IP Model

| Layer # | Name | Example protocols |
|---|---|---|
| 4 | Application layer | `HTTP`, `FTP`, `DNS`, `SNMP`, `SQL`, `SMB`, `SSL`, `TLS` |
| 3 | Transport layer | `TCP`, `UDP` |
| 2 | Network layer | `IP`, `ARP`, `ICMP`, `IPSec` |
| 1 | Network interface layer | `Ethernet`, `USB`, `Bluetooth`, `IEEE 802.11` |

----

### TCP

- **TCP** stands for **Transmission Control Protocol**
- TCP provides reliable, ordered, and error-checked delivery of a stream of octets (bytes) between applications running on hosts communicating via an IP network
- TCP is connection-oriented, and a connection between client and server is established before data can be sent

----

### 3-way handshake

- 3 steps to initiate a connection
  - `SYN` (synchronized)
  - `SYN/ACK` (synchronize / acknowledge)
  - `ACK` (acknowledged)

<img src="img/syn-ack.svg" alt="3-way handshake" />

----

### UDP

- **UDP** stands for **User Datagram Protocol**
- Uses a simple connectionless communication model with a minimum of protocol mechanisms

----

### IPv4

- `32-bit` address (`~4.3 billion` total addresses)
- From `0.0.0.0` to `255.255.255.255`
- Associated with a subnet mask to be able to identify a machine and the network associated with this machine
- For example
  - `192.168.0.1` is the IP address
  - `255.255.255.0` is the mask address

----

### IPv6

- `128-bit` hexadecimal address (`3.4 × 10³⁸` addresses) designed to solve **IPv4 exhaustion**
- Written as 8 groups of 4 hexadecimal digits separated by colons (e.g., `2001:0db8:85a3::8a2e:0370:7334`)
- Eliminates the need for **NAT** with end-to-end global reachability, simplified `40-byte` headers, and **SLAAC** (stateless auto-configuration)
- Modern networks run **Dual-Stack** (`IPv4` + `IPv6` side by side)

----

### IPv4 vs. IPv6

![IPv4 vs IPv6](img/ipv4-vs-ipv6.svg)

----

### Subnets

- Logical division of an IP network
- Routing prefix expressed in **CIDR** notation
- Followed by a `/` and ending with the bit-length of the network prefix
- Total addresses in a subnet: `2^(32 - prefix)`
  - E.g. `198.51.100.0/24` → `2^(32 - 24) = 256` IPs (`198.51.100.0` to `198.51.100.255`)
  - Standard networks reserve `2` IPs (Network & Broadcast); Cloud VPCs typically reserve `4–5` IPs per subnet

----

### CIDR & Private IPs (RFC 1918)

<p class="cidr-subtitle">Classless Inter-Domain Routing &amp; Private Ranges</p>

- **10.0.0.0/8** — *Class A private range (24 host bits)*
  - `10.0.0.0` – `10.255.255.255` (`16,777,216` IPs)
- **172.16.0.0/12** — *Class B private range (20 host bits)*
  - `172.16.0.0` – `172.31.255.255` (`1,048,576` IPs)
- **192.168.0.0/16** — *Class C private range (16 host bits)*
  - `192.168.0.0` – `192.168.255.255` (`65,536` IPs)

----

### Special IPv4 Ranges

<p class="cidr-subtitle">Reserved &amp; Special-Purpose Blocks</p>

- **Default Route**: `0.0.0.0/0` — Matches all IPv4 addresses (Internet gateway route)
- **Host / Single IP**: `/32` — Pinpoints a single host address (e.g., `203.0.113.5/32`)
- **Loopback**: `127.0.0.0/8` (`127.0.0.1` / `localhost`) — Local host network stack
- **Link-Local / Cloud Metadata**: `169.254.0.0/16` (`169.254.169.254` in AWS/GCP/Azure)
- **Multicast (Class D)**: `224.0.0.0/4` & **Reserved (Class E)**: `240.0.0.0/4`

----

### Static vs Dynamic (DHCP)

- The **Dynamic Host Configuration Protocol (DHCP)** is a network management protocol used on Internet Protocol (IP) networks for automatically assigning IP addresses and other communication parameters to devices connected to the network using a client–server architecture

----

### Static vs Dynamic (DHCP)

<img src="img/dhcp.svg" alt="DHCP" />

----

### Ports

- A **port** is a communication endpoint
- A port number is always associated with an IP address of a host and the type of transport protocol used for communication (`TCP` or `UDP`)
- Specific port numbers are reserved to identify specific services
- Port numbers lower than `1024` identify the historically most commonly used services
- Higher-numbered ports are available for general use by applications

----

### Common port numbers

| Number | Assignment |
|---|---|
| 20 | File Transfer Protocol (`FTP`) Data Transfer |
| 21 | File Transfer Protocol (`FTP`) Command Control |
| 22 | Secure Shell (`SSH`) Secure Login |
| 25 | Simple Mail Transfer Protocol (`SMTP`) email delivery |

----

### Common port numbers

| Number | Assignment |
|---|---|
| 53 | Domain Name System (`DNS`) service |
| 80 | Hypertext Transfer Protocol (`HTTP`) used in the World Wide Web |
| 443 | HTTP Secure (`HTTPS`) HTTP over `TLS/SSL` |

----

### TLS / HTTPS & mTLS

- **Transport Layer Security (`TLS`)** provides encryption, data integrity, and authentication in transit
- **Standard TLS (One-Way)**: The client verifies the server's `X.509` certificate against a trusted **Certificate Authority (`CA`)** before negotiating a fast symmetric session key (`AES-GCM` / `ChaCha20`)
- **Mutual TLS (`mTLS`)**: Both client and server present and verify certificates — the foundation of **Zero Trust** service-to-service security

----

### TLS vs. mTLS

![TLS vs mTLS](img/tls-mtls.svg)

----

### Firewalls

- A **firewall** is a network security system that monitors and controls incoming and outgoing network traffic based on predetermined security rules
- Operates on `layer 4` of the OSI model

----

### Firewalls

- **Packet filter**
  - The first reported type of network firewall is called a packet filter, which inspects packets transferred between computers. The firewall maintains an access control list which dictates what packets will be looked at and what action should be applied

----

### Firewalls

- **Connection tracking**
  - Second-generation firewalls perform the work of their first-generation predecessors but also maintain knowledge of specific conversations between endpoints by remembering which port number the two IP addresses are using

----

### Firewalls

![Firewall](img/firewall.svg)

----

### DMZ

- A **DMZ** is a physical or logical subnetwork that contains and exposes an organization's external-facing services to an untrusted, usually larger, network such as the Internet
- Add an additional layer of security to an organization's local area network (`LAN`)

----

### DMZ: Single firewall

![Single FW](img/single-fw.svg)

----

### DMZ: Dual firewalls

![Dual FW](img/dual-fw.svg)

----

### DNS

- The **Domain Name System (DNS)** is a hierarchical and decentralized naming system for computers, services, or other resources connected to the Internet or a private network
- Associates various information with domain names assigned to each of the participating entities

----

### DNS

- For example
  - `A record`: associate a DNS name to an IPv4
  - `AAAA record`: associate a DNS name to an IPv6
  - `CNAME record`: Alias of one name to another
  - `NS record`: Delegates a DNS zone to use the given authoritative name servers
  - `MX record`: Maps a domain name to a list of message transfer agents for that domain

<p class="ref-link"><a href="https://en.wikipedia.org/wiki/List_of_DNS_record_types" target="_blank">https://en.wikipedia.org/wiki/List_of_DNS_record_types</a></p>

----

### NAT

- **Network address translation (NAT)** is a method of mapping an IP address space into another
- One Internet-routable IP address of a NAT gateway can be used for an entire private network

<img src="img/nat.svg" alt="NAT" />

----

### VPN / MPLS

- A **virtual private network (VPN)** extends a private network across a public network and enables users to send and receive data across shared or public networks
- The benefits of a VPN include increases in functionality, security, and management of the private network
- Operates on `layer 2` or `3`

----

### VPN / MPLS

- **Multi-Protocol Label Switching (MPLS)** often overlays VPNs, often with quality-of-service control over a trusted delivery network
- `L2TP` which is a standards-based replacement, and a compromise taking the good features from each, for two proprietary VPN protocols

----

### VPN / MPLS

![VPN](img/vpn.svg)

----

### Router

- A **router** is a networking device that forwards data packets between computer networks (`Layer 3`)
- A router is connected to two or more data lines from different IP networks

----

### L2 Switching vs. L3 Routing & ARP

- **Layer 2 (`Switch` / `VLAN`)**: Delivers Ethernet frames within the **same local subnet** using hardware `MAC` addresses
- **ARP (`Address Resolution Protocol`)**: Translates a known `L3` IPv4 address into its `L2` `MAC` address inside the local broadcast domain
- **Layer 3 (`Router`)**: Forwards IP packets **between different subnets**; source and destination IPs remain unchanged end-to-end while `MAC` addresses are rewritten at every router hop

----

### L2 Switching vs. L3 Routing & ARP

![L2 vs L3 and ARP](img/l2-vs-l3-arp.svg)

----

### Routing (BGP)

- **Border Gateway Protocol (BGP)** is a standardized exterior gateway protocol designed to exchange routing and reachability information among autonomous systems (`AS`) on the Internet

![BGP](img/bgp.svg)
