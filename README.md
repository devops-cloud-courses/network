# Network — In a nutshell

Interactive presentation covering computer networking fundamentals, modern protocols, cloud network architecture, Kubernetes networking, and production troubleshooting.

🔗 **Live Presentation**: [devops-cloud-courses.github.io/network](https://devops-cloud-courses.github.io/network/)

---

## 👥 Authors

* **Laurent Grangeau** — Cloud Solution Architect @ Google · [@laurentgrangeau](https://twitter.com/laurentgrangeau) · [github.com/laurentgrangeau](https://github.com/laurentgrangeau)
* **Arthur Mauvezin** — DevOps Engineer @ Ouidou Consulting · [@arthurmauvezin](https://twitter.com/arthurmauvezin) · [github.com/arthurmauvezin](https://github.com/arthurmauvezin)

---

## 📚 Lecture Curriculum (Bottom-Up Flow)

### Part 1 — Networking Basics (`slides/basics.md`)
1. **Network Models & Layering**: OSI 7-layer model vs. TCP/IP 4-layer model (`HTTP/2`, `HTTP/3`, `QUIC`, `gRPC`, `TLS 1.3`, `VLAN 802.1Q`, `Wi-Fi 6E/7`, `Fiber Optics`).
2. **L2 Switching vs. L3 Routing & ARP**: MAC forwarding tables, VLANs, broadcast domains, ARP resolution, and inter-subnet gateway routing.
3. **IP Addressing & Subnetting**:
   * **IPv4 & CIDR**: Subnet masks, CIDR prefix math ($2^{(32 - \text{prefix})} - 2$), RFC 1918 private ranges (`10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`), and special ranges (`127.0.0.0/8`, `169.254.169.254` cloud metadata).
   * **IPv6 & Dual-Stack**: 128-bit addressing, SLAAC/ICMPv6, no NAT required, and Dual-Stack (`A` + `AAAA`) deployments.
4. **Dynamic Host Configuration & NAT**:
   * **DHCP**: `DORA` handshake (`Discover`, `Offer`, `Request`, `Acknowledge`).
   * **NAT & PAT**: RFC 1918 to public IP translation, Cloud NAT / NAT Gateways, and `SNAT` vs. `DNAT`.
5. **Routing & Internet Backbone**:
   * **Routing**: Static vs. dynamic routing (`OSPF`, `BGP`).
   * **BGP (Border Gateway Protocol)**: Autonomous Systems (AS), peering, and route announcements (`:179/TCP`).
6. **Transport Layer (L4) & Ports**:
   * **TCP**: 3-way handshake (`SYN`, `SYN-ACK`, `ACK`), reliability, flow/congestion control.
   * **UDP**: Connectionless low-latency transport (`DNS :53`, `HTTP/3 & QUIC :443`, `WireGuard`, `WebRTC`).
   * **Common Ports**: System (`0–1023`), Registered (`1024–49151`), Dynamic/Ephemeral (`49152–65535`), and key cloud/DevOps ports (`:22`, `:53`, `:80`, `:443`, `:3306`, `:5432`, `:6379`, `:6443`).
7. **Application Services & Security Foundations**:
   * **DNS**: Recursive/authoritative resolution (`A`, `AAAA`, `CNAME`, `TXT`, `SRV`, `CAA`), `DoH`, `DoT`, and `DNSSEC`.
   * **TLS 1.3 / HTTPS vs. Mutual TLS (mTLS)**: 1-RTT handshake, `ECDHE` forward secrecy, `Let's Encrypt` (`ACME`), and zero-trust workload identity (`SPIFFE` / mTLS).
   * **Firewalls**: Stateless (`Cloud NACLs`), Stateful (`conntrack`, `Cloud Security Groups`, `nftables`), and Next-Gen / `eBPF` (`Cilium`) firewalls.
   * **VPN, WireGuard & Cloud Interconnect**: `WireGuard`, `IPsec (IKEv2)`, dedicated private links (`AWS Direct Connect`, `GCP Cloud Interconnect`), and Zero-Trust Network Access (`ZTNA` — `Tailscale`, `Cloudflare Access`, `BeyondCorp`).

### Part 2 — Cloud & Production Architecture (`slides/advanced.md`)
1. **Perimeter & Cloud Network Topology**:
   * **DMZ**: Single-firewall and dual-firewall DMZ architectures.
   * **VPC Peering, Transit & Private Connectivity**: Non-transitive VPC peering, hub-and-spoke (`AWS Transit Gateway`, `GCP Network Connectivity Center`), and private service endpoints (`AWS PrivateLink`, `GCP Private Service Connect`).
   * **Bastion & Zero-Trust Access**: Identity-aware proxies (`GCP IAP TCP Forwarding`, `AWS SSM Session Manager`, `Teleport`, `Tailscale SSH`) with zero public `:22` exposure.
   * **Microsegmentation & SIEM / Observability**: `Kubernetes NetworkPolicy`, `Cilium eBPF`, `VPC Flow Logs`, `Cilium Hubble`, `Falco`, and `OpenTelemetry`.
2. **Traffic Management, Edge & Security**:
   * **Forward Proxy vs. Reverse Proxy**: Egress filtering (`SWG`, `Squid`) vs. ingress termination (`Envoy`, `NGINX`, `Traefik`, `Caddy`).
   * **Load Balancing (L4 vs. L7)**: Scheduling algorithms, health checks, connection pooling, and L4 (`NLB`) vs. L7 (`ALB` / `Envoy`) routing.
   * **CDN & Edge Caching**: Anycast DNS, Edge PoPs, `Cache-Control`, TLS 1.3 / HTTP/3 edge termination, and Edge Workers.
   * **WAF (Web Application Firewall)**: Layer 7 inspection, OWASP Top 10 protection, rate limiting, and managed cloud WAFs (`Cloudflare WAF`, `AWS WAF`, `Google Cloud Armor`).
3. **Cloud-Native & Kubernetes Networking**:
   * **Container & Kubernetes Networking (CNI)**: Pod network namespaces, `veth` pairs, flat Pod networks (`Cilium`, `Calico`), `eBPF` service routing, and **Kubernetes Gateway API** / `Ingress`.
   * **Service Mesh**: Data plane (`Envoy` sidecars or sidecarless **Ambient Mesh** `ztunnel`/`eBPF`) & control plane (`Istio`, `Linkerd`) for automatic mTLS, retries, traffic splitting, and telemetry.
4. **Operations & Debugging**:
   * **Network Troubleshooting by Layer**: Step-by-step bottom-up methodology (L1/L2 → L3 → L4 → DNS → L7 → Firewall) using modern Linux CLI tools (`ip`, `ss`, `ping`, `mtr`, `dig`/`kdig`, `curl -v`, `tcpdump`, `nft`, `Cilium Hubble`).

---

## 🗂️ Repository Structure

```text
.
├── index.html                  # Reveal.js 6.0.2 presentation entrypoint
├── css/
│   └── custom.css              # Custom modern light theme & responsive layout
├── slides/
│   ├── title.md                # Title & speakers ("Who are we?")
│   ├── introduction.md         # Course introduction & navigation guide
│   ├── basics.md               # Part 1: Core networking models, IP, L4, DNS, TLS, VPN
│   ├── advanced.md             # Part 2: Cloud VPC, proxies, LB, CDN, WAF, K8s CNI, Mesh, CLI
│   └── conclusion.md           # Course wrap-up & key takeaways
└── img/                        # Local vector diagrams (SVG) & speaker avatars
    ├── avatar-laurent.jpg
    ├── avatar-arthur.jpg
    ├── bgp.svg
    ├── cdn-edge.svg
    ├── dhcp.svg
    ├── dual-fw.svg
    ├── firewall.svg
    ├── forward-vs-reverse-proxy.svg
    ├── ipv4-vs-ipv6.svg
    ├── k8s-cni.svg
    ├── l2-vs-l3-arp.svg
    ├── l4-vs-l7-lb.svg
    ├── load-balancing.svg
    ├── nat.svg
    ├── service-mesh.svg
    ├── single-fw.svg
    ├── syn-ack.svg
    ├── tls-mtls.svg
    ├── troubleshooting-flow.svg
    └── vpn.svg
```

---

## 🚀 Running Locally

Because Reveal.js loads external Markdown files (`slides/*.md`) via `fetch`, serve the repository over a local HTTP server:

```bash
# Using Python 3
python3 -m http.server 8000

# Or using Node.js
npx serve .
```

Then open [http://localhost:8000](http://localhost:8000) in your browser.

### Keyboard Shortcuts
* <kbd>←</kbd> <kbd>→</kbd> / <kbd>↑</kbd> <kbd>↓</kbd> or <kbd>Space</kbd>: Navigate horizontal and vertical slides
* <kbd>Esc</kbd> or <kbd>O</kbd>: Toggle slide overview mode
* <kbd>S</kbd>: Open speaker notes view
* <kbd>F</kbd>: Toggle fullscreen
* <kbd>?</kbd>: Show all Reveal.js keyboard shortcuts
