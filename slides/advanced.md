## Advanced

----

### VPC Peering, Transit & PrivateLink

- **VPC Network Peering**: Direct, non-transitive `Layer 3` private connectivity between two Virtual Private Clouds (requires non-overlapping `CIDR` blocks)
- **Hub-and-Spoke Transit (`AWS Transit Gateway` / `GCP Network Connectivity Center`)**: Scales connectivity across dozens or hundreds of VPCs and on-prem networks via a central routing hub
- **Private Service Endpoints (`AWS PrivateLink` / `GCP Private Service Connect`)**: Exposes specific services privately across VPCs or tenants without public IPs or CIDR overlap

----

### Bastion & Zero-Trust Access (IAP / SSM)

- **Traditional Bastion (Jump Host)**: A hardened server placed in a public/DMZ subnet acting as the single `SSH`/`RDP` entry point into private networks
- **Modern Zero-Trust Access (Identity-Aware Proxy)**: Cloud architectures increasingly replace public SSH bastions with **identity-brokered tunnels** (`GCP IAP TCP Forwarding`, `AWS SSM Session Manager`, `Teleport`, `Tailscale SSH`)
  - No public IP or open inbound port `:22` required
  - Enforces `IAM` + `MFA` and records session audit logs

----

### Microsegmentation

- **Microsegmentation** isolates workloads individually across cloud VPCs and Kubernetes clusters rather than trusting an entire internal LAN
- Enforces **Zero Trust ("Never Trust, Always Verify")** policies between workloads (`East–West` traffic) using identity, labels, and `eBPF` (`Kubernetes NetworkPolicy`, `Cilium`, `Cloud Firewall Tags`)

----

### SIEM & Network Observability

- **Security Information and Event Management (`SIEM`)** aggregates and correlates real-time security telemetry across network infrastructure, cloud control planes, and workloads
- Modern stacks combine **VPC Flow Logs**, **DNS Query Logs**, **`eBPF` runtime telemetry (`Cilium Hubble`, `Falco`)**, and **OpenTelemetry** into cloud-native SIEMs (`Google SecOps / Chronicle`, `Microsoft Sentinel`, `Elastic` / `Datadog`)

----

### Proxy

- A **proxy server** is a server application that acts as an intermediary between a client requesting a resource and the server providing that resource
- **Forward Proxy** *(client-side)*: Sits in front of internal clients (`Secure Web Gateway`, `Envoy`, `Squid`) to enforce egress filtering, inspect outbound traffic, or mask client IPs
- **Reverse Proxy** *(server-side)*: Sits in front of backend servers (`Envoy`, `NGINX`, `Traefik`, `HAProxy`, `Caddy`) to handle `TLS 1.3` termination, `L7` routing, rate limiting, and load balancing

----

### Forward vs. Reverse Proxy

![Forward vs Reverse Proxy](img/forward-vs-reverse-proxy.svg)

----

### Load balancing

- **Load balancing** distributes incoming network traffic across multiple healthy backend instances to maximize throughput, minimize latency, and eliminate single points of failure

----

### Load balancing

<img src="img/load-balancing.svg" alt="Load balancing" />

----

### L4 vs. L7 Load Balancing

- **Layer 4 Load Balancer (`Transport`)**: Routes `TCP`/`UDP` connections based strictly on `IP` + `Port` (`5-tuple` hash) with ultra-low latency and millions of packets/sec (`AWS NLB`, `GCP Passthrough NLB`, `IPVS` / `eBPF`)
- **Layer 7 Load Balancer (`Application`)**: Terminates `TLS` and inspects `HTTP/2`, `HTTP/3`, `gRPC` headers, paths (`/api`, `/pay`), hostnames, and cookies for smart routing (`AWS ALB`, `GCP Cloud App LB`, `Envoy`)

----

### L4 vs. L7 Load Balancing

![L4 vs L7 Load Balancing](img/l4-vs-l7-lb.svg)

----

### CDN & Edge Caching

- A **Content Delivery Network (`CDN`)** caches content and terminates `TLS` / `HTTP/3 (QUIC)` across globally distributed **Edge PoPs (Points of Presence)** close to end users
- Uses **Anycast BGP** routing so users automatically connect to the nearest edge node (reducing `RTT` latency from `100+ ms` to `< 10 ms`)
- Absorbs volumetric `DDoS` attacks at the edge and offloads `90%+` of read traffic from cloud origin servers (`Cloudflare`, `Fastly`, `CloudFront`, `Cloud CDN`)

----

### CDN & Edge Caching

![CDN Edge Caching](img/cdn-edge.svg)

----

### WAF (Web Application Firewall)

- A **Web Application Firewall (`WAF`)** operates at **Layer 7** in front of CDNs, API Gateways, and Reverse Proxies to inspect `HTTP/S` and `gRPC` traffic
- Protects web applications and APIs against **OWASP Top 10** attacks (`SQL Injection`, `XSS`, `SSRF`, `Log4Shell`), credential stuffing, bots, and application-layer `DDoS` (`Cloudflare WAF`, `AWS WAF`, `Google Cloud Armor`)

----

### Container & Kubernetes Networking (CNI)

- In Kubernetes, every `Pod` gets its own routable IP address and communicates with any other `Pod` across nodes without `NAT`
- **CNI (`Container Network Interface`)** plugins (**`Cilium`**, **`Calico`**) use **`eBPF` native routing** (replacing legacy `iptables` & `kube-proxy`) or **Overlay tunnels (`Geneve` / `VXLAN`)**
- Traffic is exposed via virtual IPs (`Service ClusterIP`) and the modern **`Kubernetes Gateway API`** (successor to legacy `Ingress`)

----

### Container & Kubernetes Networking (CNI)

![Kubernetes CNI Networking](img/k8s-cni.svg)

----

### Service Mesh

- A **Service Mesh** (**`Istio`**, **`Linkerd`**, **`Cilium Mesh`**) manages **East–West** traffic between microservices transparently without changing application code
- Uses lightweight **Data Plane** proxies (**`Envoy` sidecars** or **sidecarless Ambient / node-level `eBPF` + `ztunnel`**) configured by a central **Control Plane**
- Provides automatic **Mutual TLS (`mTLS`)** with `SPIFFE` identities, `L7` traffic splitting/canary, retries, circuit breaking, and **OpenTelemetry** tracing

----

### Service Mesh

![Service Mesh Architecture](img/service-mesh.svg)

----

### Network Troubleshooting by Layer

| Layer | What to Check | Modern CLI Tools *(replaces legacy `net-tools`)* |
|---|---|---|
| `L2 / L3` | Interface IPs, ARP/NDP neighbors, routes, reachability | `ip a`, `ip route`, `ip neigh`, `ping`, `mtr` *(replaces `ifconfig`/`route`)* |
| `L4` | Listening sockets, firewall rules, TCP handshake | `ss -tulnp`, `nc -zv <host> <port>`, `nft` *(replaces `netstat`/`iptables`)* |
| `L7 DNS` | Authoritative records, DNS server resolution & TTL | `dig +short <domain>`, ` doggo` / `kdig`, `resolvectl` |
| `L7 App` | TLS 1.3 cert chain, HTTP/2 & HTTP/3 headers, status codes | `curl -Iv https://...`, `openssl s_client -connect host:443` |
| `Packet` | Kernel drops, eBPF flow logs & raw wire frames | `tcpdump -nn -i any port 443`, `Wireshark`, `Cilium Hubble` / `pwru` |

----

### Network Troubleshooting Workflow

![Network Troubleshooting Workflow](img/troubleshooting-flow.svg)
