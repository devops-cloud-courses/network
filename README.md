# Network in a Nutshell

An interactive presentation on **Computer Networking, Cloud Architecture, Kubernetes Networking, and Production Troubleshooting**, powered by [Reveal.js 6.0.2](https://revealjs.com/).

* **Live Presentation:** [https://devops-cloud-courses.github.io/network](https://devops-cloud-courses.github.io/network)
* **PDF Export View:** [https://devops-cloud-courses.github.io/network/?print-pdf&pdfSeparateFragments=false](https://devops-cloud-courses.github.io/network/?print-pdf&pdfSeparateFragments=false)

---

## Course Curriculum

1. **Introduction** (`slides/introduction.md`)
   * Course overview and interactive Reveal.js navigation guide
2. **Networking Basics** (`slides/basics.md`)
   * **Network Models & Layering**: OSI 7-layer model vs. TCP/IP 4-layer model (`HTTP/2`, `HTTP/3`, `QUIC`, `gRPC`, `TLS 1.3`, `VLAN 802.1Q`, `Wi-Fi 6E/7`, `Fiber Optics`)
   * **L2 Switching vs. L3 Routing & ARP**: MAC forwarding tables, VLANs, broadcast domains, ARP resolution, and inter-subnet gateway routing
   * **IPv4, CIDR & Subnetting**: Subnet masks, CIDR prefix math ($2^{(32 - \text{prefix})} - 2$), **RFC 1918** private ranges (`10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`), and special IPv4 blocks (`127.0.0.0/8`, `169.254.169.254` cloud metadata)
   * **IPv6 & Dual-Stack**: 128-bit hexadecimal addressing, SLAAC/ICMPv6, no NAT required, and Dual-Stack (`A` + `AAAA`) deployments
   * **DHCP & NAT**: `DORA` handshake (`Discover`, `Offer`, `Request`, `Acknowledge`), RFC 1918 to public IP translation, Cloud NAT / NAT Gateways, and `SNAT` vs. `DNAT`
   * **Routing & BGP**: Static vs. dynamic routing (`OSPF`, `BGP`), Autonomous Systems (AS), peering, and route announcements (`:179/TCP`)
   * **Transport Layer (L4) & Ports**: TCP 3-way handshake (`SYN`, `SYN-ACK`, `ACK`), UDP (`DNS :53`, `HTTP/3 & QUIC :443`, `WireGuard`, `WebRTC`), and common system/DevOps ports (`:22`, `:53`, `:80`, `:443`, `:3306`, `:5432`, `:6379`, `:6443`)
   * **DNS**: Recursive and authoritative resolution (`A`, `AAAA`, `CNAME`, `TXT`, `SRV`, `CAA`), `DoH` (DNS over HTTPS), `DoT` (DNS over TLS), and `DNSSEC`
   * **TLS 1.3 / HTTPS & Mutual TLS (mTLS)**: 1-RTT handshake, `ECDHE` forward secrecy, `Let's Encrypt` (`ACME`), and zero-trust workload identity (`SPIFFE` / mTLS)
   * **Firewalls, VPN & Cloud Interconnect**: Stateless (`Cloud NACLs`), Stateful (`conntrack`, `Cloud Security Groups`, `nftables`), Next-Gen / `eBPF` (`Cilium`) firewalls, `WireGuard`, `IPsec (IKEv2)`, dedicated private links (`AWS Direct Connect`, `GCP Cloud Interconnect`), and `ZTNA` (`Tailscale`, `Cloudflare Access`, `BeyondCorp`)
3. **Cloud & Production Architecture** (`slides/advanced.md`)
   * **DMZ & Perimeter Security**: Single-firewall and dual-firewall DMZ architectures
   * **VPC Peering, Transit & Private Connectivity**: Non-transitive VPC peering, hub-and-spoke (`AWS Transit Gateway`, `GCP Network Connectivity Center`), and private service endpoints (`AWS PrivateLink`, `GCP Private Service Connect`)
   * **Bastion & Zero-Trust Access**: Identity-aware proxies (`GCP IAP TCP Forwarding`, `AWS SSM Session Manager`, `Teleport`, `Tailscale SSH`) with zero public `:22` exposure
   * **Microsegmentation & SIEM / Observability**: `Kubernetes NetworkPolicy`, `Cilium eBPF`, `VPC Flow Logs`, `Cilium Hubble`, `Falco`, and `OpenTelemetry`
   * **Forward Proxy vs. Reverse Proxy**: Egress filtering (`SWG`, `Squid`) vs. ingress termination (`Envoy`, `NGINX`, `Traefik`, `Caddy`)
   * **Load Balancing (L4 vs. L7)**: Scheduling algorithms, health checks, connection pooling, and L4 (`NLB`) vs. L7 (`ALB` / `Envoy`) routing
   * **CDN & Edge Caching**: Anycast DNS, Edge PoPs, `Cache-Control`, TLS 1.3 / HTTP/3 edge termination, and Edge Workers
   * **WAF (Web Application Firewall)**: Layer 7 inspection, OWASP Top 10 protection, rate limiting, and managed cloud WAFs (`Cloudflare WAF`, `AWS WAF`, `Google Cloud Armor`)
   * **Container & Kubernetes Networking (CNI)**: Pod network namespaces, `veth` pairs, flat Pod networks (`Cilium`, `Calico`), `eBPF` service routing, and **Kubernetes Gateway API** / `Ingress`
   * **Service Mesh**: Data plane (`Envoy` sidecars or sidecarless **Ambient Mesh** `ztunnel` / `eBPF`) & control plane (`Istio`, `Linkerd`) for automatic mTLS, retries, traffic splitting, and telemetry
   * **Network Troubleshooting by Layer**: Bottom-up diagnostic workflow (L1/L2 → L3 → L4 → DNS → L7 → Firewall) using modern Linux CLI tools (`ip`, `ss`, `ping`, `mtr`, `dig`/`kdig`, `curl -v`, `tcpdump`, `nft`, `Cilium Hubble`)
4. **Conclusion** (`slides/conclusion.md`)
   * Key takeaways on cloud networking, observability, and resilient architecture design

---

## Repository Structure

```text
.
├── index.html          # Reveal.js 6.0.2 entrypoint (jsDelivr CDN, zero-build setup)
├── css/
│   └── custom.css      # Custom light theme, typography (Inter & JetBrains Mono), and responsive layout
├── img/                # Custom vector SVG architecture diagrams & author avatars
└── slides/             # Modular Markdown slide decks loaded dynamically by Reveal.js
```

---

## Running Locally

Because Reveal.js loads external Markdown files (`slides/*.md`) via `fetch`, serve the repository over a local HTTP server rather than opening `index.html` via `file://`:

### Option 1: Python (built-in)
```bash
python3 -m http.server 8000
```
Then open [http://localhost:8000](http://localhost:8000).

### Option 2: Node.js (`npx`)
```bash
npx serve .
```

### Option 3: Docker (`nginx`)
```bash
docker run --rm -p 8080:80 -v "$PWD":/usr/share/nginx/html:ro nginx:alpine
```
Then open [http://localhost:8080](http://localhost:8080).

---

## Exporting to PDF (Chrome / Chromium)

1. Open [https://devops-cloud-courses.github.io/network/?print-pdf&pdfSeparateFragments=false](https://devops-cloud-courses.github.io/network/?print-pdf&pdfSeparateFragments=false)
2. Press `Cmd + P` (macOS) or `Ctrl + P` (Windows/Linux)
3. Configure the print dialog settings:

| Setting | Value |
|---|---|
| **Destination** | Save as PDF |
| **Pages** | All |
| **Margins** | None / Default |
| **Options** | Enable **Background graphics** |

---

## Authors

* **Laurent Grangeau** — Cloud Solution Architect @ Google ([@laurentgrangeau](https://twitter.com/laurentgrangeau) | [github.com/laurentgrangeau](https://github.com/laurentgrangeau))
* **Arthur Mauvezin** — DevOps Engineer @ Ouidou Consulting ([@arthurmauvezin](https://twitter.com/arthurmauvezin) | [github.com/arthurmauvezin](https://github.com/arthurmauvezin))
