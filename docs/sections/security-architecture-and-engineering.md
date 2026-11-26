<!-- nav:top -->
[Contents](../../README.md#contents) · Previous: [Domain 2: Asset Security](asset-security.md) · Next: [Domain 4: Communication and Network Security](communication-and-network-security.md)
<!-- /nav:top -->

# Domain 3: Security Architecture and Engineering

**In one line:** designing systems that are secure by construction: design principles, formal models, platform security features, cryptography and the physical site that houses it all.

ISC2 gives this domain an average weight of **13%**. It is the broadest technical domain, and for many candidates the one with the most to memorise: security models, cryptography and facility controls all live here. The good news is that the exam tests understanding of why each mechanism exists, not the maths inside it.

## What it covers

| Subdomain (official title) | What you need to be able to do |
|---|---|
| 3.1 Research, implement and manage engineering processes using secure design principles | Apply threat modeling, least privilege, defense in depth, secure defaults, fail securely, segregation of duties, keep it simple and small, zero trust or trust but verify, privacy by design, shared responsibility, and secure access service edge. |
| 3.2 Understand the fundamental concepts of security models (e.g., Biba, Star Model, Bell-LaPadula) | Say what each model protects and what its rules forbid. |
| 3.3 Select controls based upon systems security requirements | Turn requirements into controls, and know how evaluation schemes give assurance. |
| 3.4 Understand security capabilities of Information Systems (IS) (e.g., memory protection, Trusted Platform Module (TPM), encryption/decryption) | Know what the platform itself provides. |
| 3.5 Assess and mitigate the vulnerabilities of security architectures, designs, and solution elements | Weak points of client, server, database, cryptographic, ICS, cloud, distributed, IoT, microservices and API, container, serverless, embedded, high-performance, edge and virtualised systems. |
| 3.6 Select and determine cryptographic solutions | Cryptographic life cycle, symmetric, asymmetric, elliptic curve and quantum methods, and PKI. |
| 3.7 Understand methods of cryptanalytic attacks | Brute force, ciphertext only, known plaintext, frequency analysis, chosen ciphertext, implementation, side-channel, fault injection, timing, MITM, pass the hash, Kerberos exploitation, ransomware. |
| 3.8 Apply security principles to site and facility design | Plan sites so the layout itself deters and delays. |
| 3.9 Design site and facility security controls | Wiring closets, server rooms, media and evidence storage, work areas, utilities and HVAC, environmental issues, fire, and power. |
| 3.10 Manage the information system lifecycle | Security from stakeholder needs and requirements through design, build, integration, verification, deployment, operation and retirement. |

ISC2 says AI enters this domain through secure hosting of AI workloads, input validation against prompt injection and adversarial attacks, shared responsibility for cloud AI services, and explainability as a security requirement so AI behaviour can be audited.

## Key concepts

### Secure design principles

| Principle | Meaning | Example |
|---|---|---|
| Least privilege | Give only the access needed for the task | A backup service account cannot log in interactively |
| Defense in depth | Layer independent controls so one failure is not fatal | Firewall, then host hardening, then encryption, then monitoring |
| Secure defaults | Ship in the safest configuration | Admin interface off until enabled; no default passwords |
| Fail securely | On failure, fall to a safe state | A firewall that crashes blocks traffic rather than passing it |
| Segregation of duties | Split critical tasks between people or components | Developers cannot deploy to production alone |
| Keep it simple and small | Less code and fewer features, fewer flaws | A small, reviewable security kernel |
| Zero trust | Never trust by network location; verify every request | Each API call is authenticated and authorised |
| Privacy by design | Build privacy in from the start | Collect the minimum; pseudonymise by default |
| Shared responsibility | Split security duties between provider and customer | In IaaS the customer patches the guest operating system |
| Secure access service edge (SASE) | Network and security functions delivered from the cloud, close to users | Cloud-delivered secure web gateway, CASB and zero trust access |

One nuance: for doors that people may need to escape through, life safety wins, so they usually **fail safe** (unlock) rather than **fail secure** (stay locked). Systems protecting data usually fail secure.

### Security models

| Model | Protects | Core rules |
|---|---|---|
| Bell-LaPadula | Confidentiality | **Simple security property:** no read up. **Star (*) property:** no write down. **Strong star property:** read and write only at your own level. |
| Biba | Integrity | **Simple integrity property:** no read down. **Star (*) integrity property:** no write up. The inverse of Bell-LaPadula. |
| Clark-Wilson | Integrity in commercial systems | Users reach data only through approved programs (transformation procedures), with separation of duties and auditing. The access triple: subject, program, object. |
| Brewer-Nash (Chinese Wall) | Conflicts of interest | Access changes dynamically: once you work with one client, you are blocked from its competitors' data. |
| Graham-Denning and Harrison-Ruzzo-Ullman | How rights are created, granted and removed | Formal rules for managing subjects, objects and access rights. |
| Lattice-based models | Ordered levels | Each subject and object has a bounded set of levels it can reach. |

Memory hook: Bell-LaPadula keeps **secrets** from leaking down; Biba keeps **dirt** from flowing up.

### Assurance and evaluation

**Common Criteria** (ISO/IEC 15408) evaluates products against a **protection profile** (what a product type needs) and a **security target** (what this product claims). The **Evaluation Assurance Level** (EAL1 to EAL7) measures how rigorously it was tested, not how strong its features are. **Certification** is the technical evaluation of a system; **accreditation** (or authorisation) is management's formal acceptance of the risk of running it.

### Platform security capabilities

- **Memory protection:** each process has its own address space; the OS stops one process reading another's memory.
- **Protection rings:** ring 0 for the kernel, outer rings for user code. Code crosses rings only through controlled calls.
- **Trusted Platform Module (TPM):** a chip on the device that stores keys and measures the boot process, so it can release a disk encryption key only if the boot chain is unchanged.
- **Hardware security module (HSM):** a hardened appliance for generating, storing and using keys at scale, typically in a data centre.
- **Trusted execution environments:** isolated areas of the processor (secure enclaves) that protect code and data in use.

### Weak points by system type

| System | What to watch |
|---|---|
| Client | Malware, local data, unpatched browsers, cached credentials |
| Server | Exposed services, configuration drift, privilege escalation |
| Database | **Aggregation** (combining low-sensitivity items into something sensitive) and **inference** (deducing hidden facts from visible ones); use views, polyinstantiation and query controls |
| Industrial control systems (ICS, SCADA) | Long-lived, hard to patch, availability critical; segment them and monitor |
| Cloud (SaaS, PaaS, IaaS) | Shared responsibility, misconfiguration, identity; the customer always owns its data and access |
| IoT and embedded | Default credentials, no update path, weak crypto |
| Microservices and APIs | Authentication between services, input validation, rate limiting |
| Containers | Image provenance, shared kernel, secrets in images |
| Serverless | Function permissions, event injection, dependency risk |
| Virtualised | VM escape, VM sprawl, hypervisor patching |
| Edge and high-performance | Physical exposure at the edge; shared resources in HPC |

### Cryptography essentials

| | Symmetric | Asymmetric |
|---|---|---|
| Keys | One shared secret key | A key pair: public and private |
| Speed | Fast, good for bulk data | Slow, used for key exchange and signatures |
| Examples | AES, ChaCha20 | RSA, Diffie-Hellman, elliptic curve (ECC) |
| Key count for n people | n(n-1)/2 | 2n |
| Gives nonrepudiation? | No | Yes, with digital signatures |

- **Hashing** (SHA-2, SHA-3) gives a fixed-length digest; any change to the input changes the digest. It provides integrity, not confidentiality. MD5 and SHA-1 are considered broken for collision resistance.
- **Password storage:** use a slow, salted key derivation function such as bcrypt, scrypt, Argon2 or PBKDF2. A salt defeats precomputed rainbow tables; slowness defeats fast guessing.
- **Digital signature:** hash the message, then sign the hash with the sender's **private** key. Anyone verifies with the sender's **public** key. This gives integrity, authenticity and nonrepudiation.
- **Confidential message to Bob:** encrypt with **Bob's public key**; only Bob's private key decrypts it. In practice, a random symmetric session key does the bulk encryption and is itself encrypted with the public key (hybrid encryption).
- **PKI:** a Certificate Authority (CA) signs certificates binding a public key to an identity; a Registration Authority (RA) checks identity; revocation is checked through CRLs or OCSP.
- **Key life cycle:** generate, distribute, store, use, rotate, revoke, archive, destroy. Key strength and length should match how long the data must stay secret.
- **Quantum:** large quantum computers would break today's RSA and ECC. Post-quantum algorithms are being standardised to replace them. Quantum key distribution uses physics to detect eavesdropping during key exchange.

### Cryptanalytic and related attacks

| Attack | The attacker has or does |
|---|---|
| Brute force | Tries every key |
| Ciphertext only | Only ciphertext |
| Known plaintext | Some plaintext and its matching ciphertext |
| Chosen ciphertext | Can get chosen ciphertexts decrypted |
| Frequency analysis | Counts letter or symbol patterns; works on simple substitution |
| Side-channel | Measures power, timing, sound or emissions |
| Timing | A side-channel that measures how long operations take |
| Fault injection | Induces errors (voltage, heat, glitches) to leak secrets |
| Man-in-the-middle | Sits between parties and relays or alters traffic |
| Pass the hash | Reuses a captured password hash to authenticate without cracking it |
| Kerberos exploitation | Abuses tickets, for example forging tickets with a stolen key or cracking service tickets offline |
| Ransomware | Uses encryption against you |

### Site and facility security

- **Crime Prevention Through Environmental Design (CPTED):** natural surveillance, natural access control (paths and landscaping guide people), territorial reinforcement.
- Layers from outside in: perimeter, building, floor, room, rack. Data centres should not be on the ground floor or top floor or beside obvious hazards, and should not be signposted.
- Wiring closets, server rooms, media and evidence storage get access control, logging and environmental monitoring. Evidence storage also needs chain-of-custody records.

| Power problem | What happens |
|---|---|
| Fault | Momentary power loss |
| Blackout | Prolonged power loss |
| Sag | Momentary low voltage |
| Brownout | Prolonged low voltage |
| Spike | Momentary high voltage |
| Surge | Prolonged high voltage |

UPS covers short outages and cleans power; generators cover long ones.

| Fire class (US convention) | Fuel | Typical suppression |
|---|---|---|
| A | Ordinary combustibles: paper, wood | Water, foam |
| B | Flammable liquids and gases | CO2, foam, dry chemical |
| C | Energised electrical equipment | Non-conductive agents: CO2, clean agents |
| D | Combustible metals | Dry powder |
| K | Cooking oils and fats | Wet chemical |

Class letters differ in other countries, so learn the fuel types as well as the letters. For sprinklers: **wet pipe** holds water at all times; **dry pipe** holds air and fills on activation; **pre-action** needs a detector to fire first and a sprinkler head to open, which makes it the usual choice for data centres because accidental discharge is unlikely; **deluge** opens all heads at once and suits high-hazard areas. Clean-agent gas systems protect equipment without water.

HVAC: keep rooms cool, with positive air pressure so dust and smoke are pushed out, and moderate humidity: too dry causes static, too humid causes condensation and corrosion.

### The information system lifecycle

The outline lists stakeholder needs and requirements, requirements analysis, architectural design, development and implementation, integration, verification and validation, transition and deployment, operations and maintenance, and retirement and disposal. Security requirements are defined at the start and checked at each stage; retirement includes data sanitisation.

## How the questions look

Two styles dominate. Knowledge-in-context items describe a system and ask which model, algorithm, attack or control applies. Design judgement items ask which architecture or principle BEST meets a requirement. Cryptography items rarely need maths, apart from key counts, but they do require you to know which key does what.

## A method that works

1. **Name the property at stake.** Confidentiality, integrity, availability, authenticity or nonrepudiation. This narrows models and crypto choices at once.
2. **For crypto, write out who holds which key.** Sender private, sender public, receiver private, receiver public. Then ask what the operation needs.
3. **For models, find the direction.** Reading or writing, up or down, then apply the rule for confidentiality (BLP) or integrity (Biba).
4. **For architecture, find the weakest link.** Which component fails first or is most exposed?
5. **For facilities, protect people first,** then equipment, then data.
6. **Check the cloud model** before deciding who is responsible.

## Traps that cost points

- **Reversing Bell-LaPadula and Biba.** BLP: no read up, no write down. Biba: no read down, no write up.
- **Encrypting with the wrong key.** Confidentiality uses the receiver's public key. Signatures use the sender's private key.
- **Thinking hashing gives confidentiality.** It gives integrity only.
- **Using plain or fast hashes for passwords.** Use a salted, slow key derivation function.
- **Reading EAL as strength.** It measures depth of evaluation.
- **Choosing a wet pipe or deluge system for a data centre.** Pre-action or clean agent are the usual answers.
- **Forgetting who patches in IaaS.** The customer patches the guest operating system and applications.
- **Letting a door fail secure in an emergency exit.** Life safety comes first.
- **Mixing up the power terms.** Momentary versus prolonged, low versus high.

## Timing

Crypto and model items are fast once the rules are automatic: about 45 to 60 seconds. Architecture scenarios with several plausible designs can take 90 seconds. As guidance, if you are stuck, choose the option that applies the stated principle most directly and keep moving.

## Practice items

These 2 items are original, written for these notes. They are not taken from ISC2 or any prep provider.

**Item 1.** In a system enforcing Bell-LaPadula, a user cleared to Secret tries to save notes into a file labelled Confidential and is blocked. Which rule blocked the write?

- A. The simple security property
- B. The star (*) property
- C. The simple integrity property
- D. The discretionary security property

**Item 2.** A web application must store user passwords so that a stolen database is as hard as possible to crack. Which approach is BEST?

- A. Encrypt the passwords with AES-256 and store the key on the same server
- B. Store an unsalted SHA-256 hash of each password
- C. Store an MD5 hash of each password with one shared secret added
- D. Store the output of a slow, salted key derivation function such as Argon2 or bcrypt

<details>
<summary>Answers and explanations, items 1 and 2</summary>

**Item 1: B.** The star (*) property forbids writing down, from a higher level to a lower one, so Secret information cannot leak into a Confidential file. *Why not A:* the simple security property forbids reading up, not writing down. *Why not C:* simple integrity belongs to Biba, not Bell-LaPadula.

**Item 2: D.** A slow, salted key derivation function makes each guess expensive and defeats precomputed tables. *Why not B:* SHA-256 is fast and unsalted, so it is open to rainbow tables and rapid guessing. *Why not A:* encryption is reversible, and with the key on the same server a breach exposes every password.

</details>

Want more? The [free timed CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=557dqd&utm_content=cissp) has 25 questions across all eight domains, scored by domain.

## Score yourself

| Item | 1 | 2 |
|---|---|---|
| Answer | B | D |

- **2:** strong. Keep the crypto rules fresh with short mixed sets.
- **1:** draw the "who holds which key" grid and the two model rule tables from memory each day.
- **0:** work through Key concepts one block at a time, writing a one-line example for each row, then redo the items.

## Next step

Domain 3 rewards fast recall under pressure. Test it in a timed run with the [free CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=557dqd&utm_content=cissp), and return to the traps list for anything that slipped.

## Sources for this page

- [ISC2 CISSP Certification Exam Outline](https://www.isc2.org/certifications/cissp/cissp-certification-exam-outline), for the subdomains, weight and AI notes

---

<!-- nav:bottom -->
← Previous: [Domain 2: Asset Security](asset-security.md) | Next: [Domain 4: Communication and Network Security](communication-and-network-security.md) → | [Back to contents](../../README.md#contents)
<!-- /nav:bottom -->
