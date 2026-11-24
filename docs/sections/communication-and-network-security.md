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

These 12 items are original, written for these notes. They are not taken from ISC2 or any prep provider.

### Set 1

**Item 1.** A device forwards frames between ports based on MAC addresses. At which OSI layer does it mainly operate?

- A. Layer 1
- B. Layer 2
- C. Layer 3
- D. Layer 4

**Item 2.** Two offices are joined over the internet by VPN gateways. The design must encrypt all traffic and hide the internal IP addresses of both networks. Which IPsec configuration fits?

- A. AH in transport mode
- B. ESP in transport mode
- C. ESP in tunnel mode
- D. AH in tunnel mode

**Item 3.** A company with 2,000 staff wants every employee to authenticate to Wi-Fi with their own credentials, so access can be removed for one person on their last day. Which option fits BEST?

- A. WPA2-Personal with a passphrase changed every quarter
- B. An open network with a captive portal
- C. WEP with MAC address filtering
- D. WPA3-Enterprise with 802.1X authentication

**Item 4.** After a breach, investigators find the attacker moved freely from a compromised web server to database and file servers in the same data centre segment. Which control would have limited this MOST?

- A. Micro-segmentation with policy enforced per workload
- B. A larger perimeter firewall with more rules
- C. A content distribution network in front of the web server
- D. More bandwidth between the data centre switches

<details>
<summary>Answers and explanations, items 1 to 4</summary>

**Item 1: B.** Forwarding by MAC address is the job of a switch at the data link layer. *Why not C:* layer 3 devices, routers, forward by IP address. *Why not A:* layer 1 devices such as hubs repeat bits without reading addresses.

**Item 2: C.** ESP encrypts, and tunnel mode encapsulates the whole original packet, hiding internal addresses. That is the standard gateway-to-gateway design. *Why not B:* transport mode leaves the original IP header visible. *Why not D:* AH provides integrity but no encryption.

**Item 3: D.** Enterprise mode with 802.1X authenticates each user against a central server, so one account can be disabled without affecting anyone else. *Why not A:* a shared passphrase cannot be revoked for one person; every leaver means a change for everyone. *Why not C:* WEP is broken and MAC addresses are easy to spoof.

**Item 4: A.** Micro-segmentation applies policy between individual workloads, so a compromised web server cannot freely reach database or file servers. *Why not B:* the perimeter firewall governs north-south traffic and was already behind the attacker. *Why not C:* a CDN speeds up and protects public content; it does nothing for internal traffic.

</details>

### Set 2

**Item 5.** A vulnerability scan shows a public web server still accepts SSL 3.0 and TLS 1.0 connections. What is the BEST action?

- A. Keep them enabled for older browsers and add a web application firewall
- B. Move the site to a non-standard port
- C. Disable the old versions and allow only TLS 1.2 and 1.3
- D. Require client certificates for all connections

**Item 6.** When a laptop plugs into an office network port, it is checked for current patches and running endpoint protection. Non-compliant laptops are placed in a remediation VLAN. What technology is doing this?

- A. An intrusion detection system
- B. Network access control
- C. Data loss prevention
- D. A security information and event management system

**Item 7.** An attacker on the same office LAN sends forged ARP replies so that other machines send their traffic through the attacker's laptop. Which control at the switch MOST directly prevents this?

- A. Dynamic ARP inspection
- B. DNSSEC on the internal DNS servers
- C. TLS on all internal web applications
- D. A stateful firewall at the internet edge

**Item 8.** What is the BEST way to protect the administrative interfaces of routers and switches?

- A. Allow Telnet from any internal host, since it is inside the perimeter
- B. Publish the web management interface on a public address with a strong password
- C. Manage devices in-band using SNMPv1 community strings
- D. Use a separate out-of-band management network reachable only by administrators

<details>
<summary>Answers and explanations, items 5 to 8</summary>

**Item 5: C.** SSL 3.0 and TLS 1.0 have known weaknesses and are deprecated. Disabling them removes the risk at its source. *Why not A:* a WAF does not fix weak transport encryption. *Why not D:* client certificates add authentication but leave the weak protocol versions available.

**Item 6: B.** Checking device health and placing non-compliant devices in a quarantine network is network access control. *Why not A:* an IDS detects suspicious traffic; it does not decide whether a device may join. *Why not D:* a SIEM collects and correlates logs; it does not control port access.

**Item 7: A.** Dynamic ARP inspection checks ARP messages against trusted bindings and drops forged replies, directly stopping ARP spoofing. *Why not C:* TLS would protect the content of some traffic, but traffic would still be redirected and other protocols exposed. *Why not B:* DNSSEC protects DNS answers, not ARP.

**Item 8: D.** Out-of-band management keeps the management plane off the production network and limits who can reach it. *Why not A:* Telnet sends credentials in clear text, and any compromised internal host could reach the devices. *Why not C:* SNMPv1 community strings travel in clear text.

</details>

### Set 3

**Item 9.** A hardware vendor needs occasional remote access to support your storage arrays. Which arrangement is BEST?

- A. A permanent VPN account for the vendor that is always enabled
- B. Remote desktop exposed to the internet, limited to the vendor's IP range
- C. Access through a jump host with MFA, enabled only on request for a set window, with sessions recorded
- D. Sharing the array's administrator password with the vendor's support team

**Item 10.** Staff report choppy, broken-up audio on internal VoIP calls. Monitoring shows ample spare bandwidth and no packet loss. Which metric is MOST likely the cause?

- A. Throughput
- B. Jitter
- C. Bandwidth
- D. Signal-to-noise ratio

**Item 11.** Which statement BEST describes software-defined networking?

- A. Routing and policy decisions are centralised in a controller, separate from the devices that forward traffic
- B. Each switch makes its own forwarding decisions using locally configured rules
- C. All network functions run on one large physical appliance
- D. Wireless and wired networks are merged into one broadcast domain

**Item 12.** Network administrators still use Telnet and FTP to manage and update devices. Which replacement pair BEST improves security?

- A. HTTP and TFTP
- B. SNMPv1 and rlogin
- C. Telnet over a VLAN and FTP over a VLAN
- D. SSH and SFTP

<details>
<summary>Answers and explanations, items 9 to 12</summary>

**Item 9: C.** Least privilege for third parties means access only when needed, through a controlled point, with strong authentication and recording. *Why not A:* standing access is available to an attacker who compromises the vendor at any time. *Why not B:* exposing remote desktop to the internet invites attack, and IP ranges can be spoofed or shared.

**Item 10: B.** Jitter, the variation in packet delay, breaks up real-time voice even when there is plenty of capacity and no loss. *Why not C:* the question says bandwidth is ample. *Why not D:* signal-to-noise ratio matters for radio and line quality, not for internal VoIP over a wired network.

**Item 11: A.** SDN separates the control plane into a central controller, managed through APIs, while devices forward traffic as instructed. *Why not B:* that describes traditional distributed networking. *Why not C:* running functions as software is network functions virtualisation, and it does not imply one appliance.

**Item 12: D.** SSH replaces Telnet and SFTP replaces FTP, both with encryption and authentication. *Why not C:* a VLAN separates traffic but does not encrypt clear-text credentials. *Why not A:* HTTP and TFTP are also clear text, and TFTP has no authentication at all.

</details>

## Score yourself

| Item | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Answer | B | C | D | A | C | B | A | D | C | B | A | D |

- **11 to 12:** strong. Watch that your hands-on habits do not override "most secure design" on the real exam.
- **8 to 10:** redo the OSI and attack-to-control tables from memory and check them.
- **7 or fewer:** start with the OSI table, then IPsec modes and segmentation, then redo the items.

## Next step

Practise switching between network detail and design judgement in a timed run. The [free CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp) mixes domains the way the exam does.

## Sources for this page

- [ISC2 CISSP Certification Exam Outline](https://www.isc2.org/certifications/cissp/cissp-certification-exam-outline), for the subdomains, weight and AI notes

---

<!-- nav:bottom -->← Previous: [Domain 3: Security Architecture and Engineering](security-architecture-and-engineering.md) | Next: [Domain 5: Identity and Access Management](identity-and-access-management.md) → | [Back to contents](../../README.md#contents)<!-- /nav:bottom -->
