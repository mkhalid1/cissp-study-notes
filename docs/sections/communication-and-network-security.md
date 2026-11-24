<!-- nav:top -->[Contents](../../README.md#contents) · Previous: [Domain 3: Security Architecture and Engineering](security-architecture-and-engineering.md) · Next: [Domain 5: Identity and Access Management](identity-and-access-management.md)<!-- /nav:top -->

# Domain 4: Communication and Network Security

**In one line:** designing and protecting networks: the layered models, secure protocols, segmentation, wireless and remote access, and the components that move data safely.

ISC2 gives this domain an average weight of **13%**. Candidates with a networking background often find it the most comfortable domain, which is exactly why they lose marks: the exam asks for the most secure design that meets the business need, not the configuration you would type at the console.

## What it covers

| Subdomain (official title) | What you need to be able to do |
|---|---|
| 4.1 Apply secure design principles in network architectures | OSI and TCP/IP models, IPv4 and IPv6, secure protocols (IPSec, SSH, SSL/TLS), multilayer and converged protocols (iSCSI, VoIP, InfiniBand over Ethernet, Compute Express Link), transport architecture and planes, performance metrics, north-south and east-west traffic, physical and logical segmentation, micro-segmentation, edge networks, wireless (Bluetooth, Wi-Fi, Zigbee, satellite), cellular (4G, 5G), CDNs, SDN, virtual private clouds, and monitoring and management. |
| 4.2 Secure network components | Operating infrastructure (redundant power, warranty, support), transmission media, Network Access Control (NAC), and endpoint security. |
| 4.3 Implement secure communication channels according to design | Voice, video and collaboration, remote access, data communications such as backhaul and satellite, and third-party connectivity. |

ISC2 notes that AI touches this domain in two ways: isolating AI training environments with micro-segmentation and zero trust architecture, and using AI-driven network detection and response to spot anomalies that signature-based tools miss.

## Key concepts

### The OSI model, with what lives at each layer

| Layer | Name | Data unit | Examples | Typical devices and attacks |
|---|---|---|---|---|
| 7 | Application | Data | HTTP, DNS, SMTP, SNMP, LDAP | Web application firewall; injection, phishing payloads |
| 6 | Presentation | Data | Encoding, compression, encryption formats | Format and encoding tricks |
| 5 | Session | Data | Session setup and teardown, RPC | Session hijacking |
| 4 | Transport | Segment (TCP) or datagram (UDP) | TCP, UDP | Stateful firewall; SYN flood, port scans |
| 3 | Network | Packet | IP, ICMP, IPsec, routing protocols | Router, packet-filtering firewall; IP spoofing, ICMP floods |
| 2 | Data link | Frame | Ethernet, ARP, 802.1Q VLAN tags, 802.11 MAC | Switch, bridge; ARP spoofing, MAC flooding, VLAN hopping |
| 1 | Physical | Bits | Cables, radio, fibre | Hub, repeater; wiretapping, jamming, cable cuts |

The TCP/IP model folds these into four layers: Application (OSI 5 to 7), Transport (4), Internet (3) and Link or Network Access (1 and 2).

TLS is usually described as working between the transport and application layers; place it where the question's options let you, and remember that what matters is that it protects application data end to end.

### Ports worth knowing

| Port | Service | Secure alternative or note |
|---|---|---|
| 20, 21 | FTP | SFTP (over SSH, 22) or FTPS |
| 22 | SSH, SFTP | |
| 23 | Telnet | Replace with SSH |
| 25 | SMTP | Use STARTTLS; 587 for submission |
| 53 | DNS | DNSSEC adds integrity and origin authentication, not confidentiality |
| 80 / 443 | HTTP / HTTPS | |
| 88 | Kerberos | |
| 161, 162 | SNMP | Use SNMPv3, which adds authentication and encryption |
| 389 / 636 | LDAP / LDAPS | |
| 445 | SMB | Never expose to the internet |
| 3389 | RDP | Put behind a VPN or gateway with MFA |

### IPv4, IPv6 and address types

- **Unicast** to one host, **broadcast** to all hosts on a segment (IPv4 only), **multicast** to a group, **anycast** to the nearest of several hosts sharing an address (used by DNS and CDNs).
- IPv6 has no broadcast, uses 128-bit addresses, and includes IPsec support in its design. Dual-stack networks need security controls for both, or IPv6 becomes an unmonitored path.

### Secure protocols

- **IPsec:** Authentication Header (AH) gives integrity and origin authentication, no encryption. Encapsulating Security Payload (ESP) gives encryption plus integrity. **Transport mode** protects the payload, host to host. **Tunnel mode** wraps the whole original packet in a new one, gateway to gateway, hiding internal addresses. Keys are negotiated by IKE.
- **TLS:** use TLS 1.2 or 1.3. SSL and TLS 1.0 and 1.1 are deprecated and should be disabled.
- **SSH:** encrypted remote administration and file transfer; replaces Telnet, rlogin and FTP.

### Multilayer and converged protocols

Multilayer protocols such as DNP3 in industrial systems carry many functions over one stack; they are flexible but can hide covert channels and bypass filters. Converged protocols carry storage or voice over ordinary IP networks: **iSCSI** (block storage over IP), **VoIP**, **InfiniBand over Ethernet** and **Compute Express Link** for fast interconnects. The risk is that sensitive traffic shares the data network, so isolate it on dedicated segments and authenticate endpoints.

### Architecture, planes and metrics

- **Data plane** forwards traffic, **control plane** decides routes, **management plane** configures devices. Protect the management plane most tightly.
- **Cut-through** switching forwards a frame as soon as it reads the destination; **store-and-forward** reads the whole frame and checks it first.
- **Performance metrics:** bandwidth (capacity), throughput (actual delivered rate), latency (delay), jitter (variation in delay, which ruins voice and video), signal-to-noise ratio (quality of a radio or line signal).
- **North-south** traffic enters or leaves the data centre; **east-west** moves between internal systems. Attackers who get in move east-west, so internal traffic needs inspection too.

### Segmentation

| Type | Examples | Point |
|---|---|---|
| Physical | In-band vs out-of-band management, air gap | Out-of-band management uses a separate network for device administration. An air gap has no network connection at all. |
| Logical | VLANs, VPNs, virtual routing and forwarding, virtual domains | Separate traffic on shared hardware. |
| Micro-segmentation | Overlays and encapsulation, distributed firewalls and IDS/IPS, zero trust | Policy per workload, so a compromised server cannot freely reach its neighbours. |

### Firewalls and related devices

| Type | Decides on | Note |
|---|---|---|
| Packet filter | Addresses, ports, protocol in each packet | Fast, no context |
| Stateful | Connection state plus the above | Knows whether a packet belongs to an allowed session |
| Application proxy | Application content | Breaks the connection and inspects; slower, deeper |
| Next-generation firewall | Applications, users, content, threat signatures | Combines several functions |
| Web application firewall | HTTP requests to a web app | Blocks injection and similar attacks |

**NAC** checks a device's identity and health (patches, antivirus, configuration) before granting network access, and can quarantine non-compliant devices. It can use 802.1X on ports and wireless.

### Wireless and mobile

| Option | Use |
|---|---|
| WPA3-Personal (SAE) | Small sites with a shared passphrase; resists offline guessing better than WPA2-Personal |
| WPA3-Enterprise or WPA2-Enterprise with 802.1X | Each user authenticates individually through a RADIUS server, usually with EAP-TLS or similar; accounts can be revoked one at a time |
| WEP, open networks | Do not use for business data |

Bluetooth risks include bluejacking (unsolicited messages), bluesnarfing (data theft) and bluebugging (taking control). Zigbee is a low-power mesh protocol common in IoT, with weak security if left at defaults. Satellite links add latency and can be intercepted, so encrypt traffic over them. 5G improves encryption of subscriber identity compared with earlier generations, but the device and the services it reaches still need their own controls.

### SDN, CDN and VPC

- **Software-defined networking** separates the control plane into a central controller managed through APIs. SD-WAN applies the idea to wide-area links. Network functions virtualisation runs firewalls and routers as software. Protect the controller: it is a single point of control.
- **Content distribution networks** cache content at many edge locations, improving speed and absorbing denial-of-service traffic.
- **Virtual private cloud** is an isolated network in a public cloud with its own subnets, routing and security groups.

### Common network attacks and the control that fits

| Attack | Control |
|---|---|
| SYN flood | SYN cookies, rate limiting, upstream DDoS protection |
| ARP spoofing | Dynamic ARP inspection on switches, static entries for key hosts |
| MAC flooding | Port security limiting MAC addresses per port |
| VLAN hopping | Disable trunking on user ports, change the native VLAN, prune unused VLANs |
| DNS cache poisoning | DNSSEC, randomised source ports |
| Eavesdropping on the wire | Encryption in transit, physical protection of cabling |

### Secure channels

- **Remote access:** VPN or zero trust access with MFA; administrators reach devices through a hardened jump host, never directly from the internet.
- **Voice, video and collaboration:** encrypt signalling and media, lock meetings, control recordings.
- **Third-party connectivity:** contract for security, give least-privilege access that is time-limited and monitored, and review it regularly.

## How the questions look

Expect scenarios naming a business need ("connect two offices", "let a vendor support our servers", "protect the storage network") and asking for the BEST design or control. Some items test placement: which OSI layer, which port, which IPsec mode. Others describe symptoms ("voice calls break up although bandwidth is fine") and ask which metric or attack explains them.

## A method that works

1. **State the requirement in one line.** Confidentiality between sites? Individual authentication? Isolation of a workload?
2. **Locate it on the OSI model.** Knowing the layer rules out many options.
3. **Prefer secure-by-design over add-ons.** Segmentation and strong protocols beat monitoring a weak design.
4. **Apply least privilege to network paths.** Who needs to reach what, from where, and when?
5. **Protect management and control planes first.** Compromise there means compromise everywhere.
6. **Check for a deprecated protocol in the options.** Telnet, FTP, SNMPv1, WEP and old SSL or TLS versions are almost never the answer.

## Traps that cost points

- **Choosing AH when confidentiality is needed.** AH does not encrypt.
- **Confusing transport and tunnel mode.** Tunnel mode hides the original headers; it is the gateway-to-gateway choice.
- **Treating DNSSEC as encryption.** It provides integrity and authentication of DNS data.
- **Thinking a VLAN is a security boundary on its own.** It needs filtering between VLANs and protection against hopping.
- **Ignoring east-west traffic.** Perimeter controls do not stop lateral movement.
- **Picking a shared Wi-Fi passphrase for a large workforce.** Individual 802.1X authentication allows revocation per user.
- **Mixing up bandwidth, throughput and jitter.** Choppy voice with ample bandwidth points to jitter.
- **Giving vendors standing access.** Access should be on request, time-limited, logged and MFA-protected.

## Timing

Network items are usually quick: about 50 to 70 seconds. Spend longer only on design scenarios with several workable answers, and decide by asking which option meets the stated requirement with the least exposure.

## Practice items

These 2 items are original, written for these notes. They are not taken from ISC2 or any prep provider.

**Item 1.** Two offices are joined over the internet by VPN gateways. The design must encrypt all traffic and hide the internal IP addresses of both networks. Which IPsec configuration fits?

- A. AH in transport mode
- B. ESP in transport mode
- C. ESP in tunnel mode
- D. AH in tunnel mode

**Item 2.** After a breach, investigators find the attacker moved freely from a compromised web server to database and file servers in the same data centre segment. Which control would have limited this MOST?

- A. Micro-segmentation with policy enforced per workload
- B. A larger perimeter firewall with more rules
- C. A content distribution network in front of the web server
- D. More bandwidth between the data centre switches

<details>
<summary>Answers and explanations, items 1 and 2</summary>

**Item 1: C.** ESP encrypts, and tunnel mode encapsulates the whole original packet, hiding internal addresses. That is the standard gateway-to-gateway design. *Why not B:* transport mode leaves the original IP header visible. *Why not D:* AH provides integrity but no encryption.

**Item 2: A.** Micro-segmentation applies policy between individual workloads, so a compromised web server cannot freely reach database or file servers. *Why not B:* the perimeter firewall governs north-south traffic and was already behind the attacker. *Why not C:* a CDN speeds up and protects public content; it does nothing for internal traffic.

</details>

Want more? The [free timed CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp) has 25 questions across all eight domains, scored by domain.

## Score yourself

| Item | 1 | 2 |
|---|---|---|
| Answer | C | A |

- **2:** strong. Watch that your hands-on habits do not override "most secure design" on the real exam.
- **1:** redo the OSI and attack-to-control tables from memory and check them.
- **0:** start with the OSI table, then IPsec modes and segmentation, then redo the items.

## Next step

Practise switching between network detail and design judgement in a timed run. The [free CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp) mixes domains the way the exam does.

## Sources for this page

- [ISC2 CISSP Certification Exam Outline](https://www.isc2.org/certifications/cissp/cissp-certification-exam-outline), for the subdomains, weight and AI notes

---

<!-- nav:bottom -->← Previous: [Domain 3: Security Architecture and Engineering](security-architecture-and-engineering.md) | Next: [Domain 5: Identity and Access Management](identity-and-access-management.md) → | [Back to contents](../../README.md#contents)<!-- /nav:bottom -->
