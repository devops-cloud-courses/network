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

| Layer # | Name | Example protocols & technologies |
|---|---|---|
| 7 | Application layer | `HTTPS`, `HTTP/3`, `gRPC`, `DNS`, `SSH`, `WebSockets` |
| 6 | Presentation layer | `TLS 1.3` *(replaces deprecated `SSL`)*, `Protobuf`, `JSON` |
| 5 | Session layer | `RPC`, `gRPC Sessions`, `TLS Session Resumption`, `WebSockets` |
| 4 | Transport layer | `TCP`, `UDP`, `QUIC` |

----

### OSI Model

| Layer # | Name | Example protocols & technologies |
|---|---|---|
| 3 | Network layer | `IPv4`, `IPv6`, `ICMP`, `IPsec`, `BGP`, `OSPF` |
| 2 | Data link layer | `Ethernet (802.3)`, `VLAN (802.1Q)`, `Wi-Fi (802.11)`, `ARP` |
| 1 | Physical layer | `Fiber Optics`, `Twisted Pair (Cat6/8)`, `Wi-Fi RF (Wi-Fi 6E/7)` |

----

### TCP/IP Model

| Layer # | Name | Example protocols & technologies |
|---|---|---|
| 4 | Application layer | `HTTPS`, `HTTP/3`, `gRPC`, `DNS`, `SSH`, `TLS 1.3` |
| 3 | Transport layer | `TCP`, `UDP`, `QUIC` |
| 2 | Network layer | `IPv4`, `IPv6`, `ICMP`, `IPsec`, `BGP` |
| 1 | Network interface layer | `Ethernet`, `VLAN`, `Wi-Fi (IEEE 802.11)`, `Fiber` |

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

----

### NAT

- **Network address translation (NAT)** is a method of mapping an IP address space into another
- One Internet-routable IP address of a NAT gateway can be used for an entire private network

<img src="img/nat.svg" alt="NAT" />

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
- Connectionless transport protocol with minimal overhead (`8-byte` header, no handshake or head-of-line blocking)
- Powers modern latency-sensitive protocols: **`DNS` (`:53`)**, **`HTTP/3` & `QUIC` (`:443`)**, **`WireGuard` VPN**, **`WebRTC`** video/voice, and real-time gaming

----

### Ports

- A **port** (`16-bit` unsigned integer: `0–65535`) is a logical communication endpoint on a host
- Combined with an IP address and transport protocol (`TCP` / `UDP`) to form a **socket**
- **Well-known ports (`0–1023`)**: Reserved for core system and network services
- **Registered (`1024–49151`) & Ephemeral ports (`49152–65535`)**: Used by application services and short-lived client connections

----

### Common port numbers

| Number | Assignment |
|---|---|
| 22 | Secure Shell (`SSH`) & `SFTP` *(replaces legacy plaintext `FTP :20/:21`)* |
| 25 / 587 | Simple Mail Transfer Protocol (`SMTP`) email relay & submission |
| 53 | Domain Name System (`DNS`) — `UDP` & `TCP` (`:853` for `DoT`) |
| 80 | Hypertext Transfer Protocol (`HTTP`) — typically redirects to `:443` |

----

### Common port numbers

| Number | Assignment |
|---|---|
| 443 | `HTTPS` (`HTTP/1.1` & `HTTP/2` over `TCP/TLS`, `HTTP/3` over `UDP/QUIC`) |
| 3306 / 5432 | Relational Databases (`MySQL` `:3306`, `PostgreSQL` `:5432`) |
| 6379 | In-Memory Data Store (`Redis` / `Valkey`) |
| 6443 | `Kubernetes` API Server (`HTTPS`) |

----

### DNS

- The **Domain Name System (DNS)** is a hierarchical and decentralized naming system for computers, services, or other resources connected to the Internet or a private network
- Modern DNS supports encrypted transport via **DNS over HTTPS (`DoH`)** and **DNS over TLS (`DoT`)**, plus **DNSSEC** cryptographic record signing

----

### DNS

- Common DNS record types:
  - `A` / `AAAA`: Maps a domain name to an `IPv4` (`A`) or `IPv6` (`AAAA`) address
  - `CNAME`: Alias of one domain name to another canonical name
  - `NS`: Delegates a DNS zone to authoritative name servers
  - `MX`: Maps a domain name to mail exchange servers
  - `TXT` / `SRV` / `CAA`: Domain verification (`SPF`/`DKIM`), service discovery, and Certificate Authority authorization

<p class="ref-link"><a href="https://en.wikipedia.org/wiki/List_of_DNS_record_types" target="_blank">https://en.wikipedia.org/wiki/List_of_DNS_record_types</a></p>

----

### TLS / HTTPS & mTLS

- **Transport Layer Security (`TLS 1.3`)** provides encryption, integrity, and authentication in transit (`SSL` and `TLS 1.0/1.1` are deprecated)
- **Standard TLS (One-Way)**: Client verifies the server's `X.509` certificate (automated via `Let's Encrypt` / `ACME`) and negotiates ephemeral forward-secret keys (`ECDHE` + `AES-GCM` / `ChaCha20-Poly1305`) in `1-RTT`
- **Mutual TLS (`mTLS`)**: Both client and server verify short-lived certificates (`SPIFFE` / internal `CA`) — the foundation of **Zero Trust** service-to-service security

----

### TLS vs. mTLS

![TLS vs mTLS](img/tls-mtls.svg)

----

### Firewalls

- A **firewall** enforces security policies by filtering incoming and outgoing network traffic
- **Stateless Packet Filters (`L3/L4`)**: Inspect individual packet headers (`Src/Dst IP`, `Protocol`, `Port`) against static Access Control Lists *(e.g., Cloud Subnet `NACLs`)*
- **Stateful Firewalls (`L4`)**: Track active connections (`conntrack`) so return traffic for established sessions is automatically permitted *(e.g., Cloud `Security Groups`, Linux `nftables`)*
- **Next-Generation & eBPF Firewalls (`L3–L7`)**: Deep packet inspection, application/identity awareness, and kernel-level `eBPF` policy enforcement *(replacing legacy `iptables`)*

----

### Firewalls

![Firewall](img/firewall.svg)

----

### DMZ

- A **DMZ (Demilitarized Zone)** is an isolated perimeter subnet that exposes public-facing gateways (`Reverse Proxies`, `Load Balancers`, `API Gateways`) to untrusted networks (`Internet`)
- Prevents direct external access to internal private subnets (`Application Tiers`, `Databases`)

----

### DMZ: Single firewall

![Single FW](img/single-fw.svg)

----

### DMZ: Dual firewalls

![Dual FW](img/dual-fw.svg)

----

### VPN, WireGuard & Cloud Interconnect

- A **Virtual Private Network (`VPN`)** creates encrypted tunnels (`Layer 3`) across untrusted public networks to connect remote users or branch/cloud networks
- **Modern VPN Protocols**: **`WireGuard`** (modern, high-speed cryptographic tunnel in the Linux kernel) and **`IPsec` (`IKEv2`)** have replaced legacy protocols like `PPTP` and `L2TP`
- **Enterprise & Cloud Connectivity**: Dedicated private links (**`AWS Direct Connect`**, **`GCP Cloud Interconnect`**, **`SD-WAN`**) and **Zero Trust Network Access (`ZTNA` / `Tailscale` / `BeyondCorp`)** replace traditional `MPLS` and perimeter VPNs

----

### VPN, WireGuard & Cloud Interconnect

![VPN](img/vpn.svg)
