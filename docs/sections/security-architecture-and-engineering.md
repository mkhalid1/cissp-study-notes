<!-- nav:top -->[Contents](../../README.md#contents) · Previous: [Domain 2: Asset Security](asset-security.md) · Next: [Domain 4: Communication and Network Security](communication-and-network-security.md)<!-- /nav:top -->

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

These 12 items are original, written for these notes. They are not taken from ISC2 or any prep provider.

### Set 1

**Item 1.** In a system enforcing Bell-LaPadula, a user cleared to Secret tries to save notes into a file labelled Confidential and is blocked. Which rule blocked the write?

- A. The simple security property
- B. The star (*) property
- C. The simple integrity property
- D. The discretionary security property

**Item 2.** A plant's main concern is that data from untrusted field sensors must never corrupt its high-integrity production records. Which model's rules address this MOST directly?

- A. Bell-LaPadula
- B. Brewer-Nash
- C. Biba
- D. Graham-Denning

**Item 3.** A consulting firm advises several banks that compete with each other. Once a consultant opens files for one bank, the system must block that consultant from the other banks' files. Which model fits?

- A. Bell-LaPadula
- B. Clark-Wilson
- C. Biba
- D. Brewer-Nash

**Item 4.** A team of 50 people needs every pair to communicate privately using only symmetric keys. How many unique keys are needed?

- A. 1,225
- B. 100
- C. 2,450
- D. 50

<details>
<summary>Answers and explanations, items 1 to 4</summary>

**Item 1: B.** The star (*) property forbids writing down, from a higher level to a lower one, so Secret information cannot leak into a Confidential file. *Why not A:* the simple security property forbids reading up, not writing down. *Why not C:* simple integrity belongs to Biba, not Bell-LaPadula.

**Item 2: C.** Biba protects integrity. Its rules stop high-integrity subjects from reading low-integrity data and stop low-integrity subjects from writing up. *Why not A:* Bell-LaPadula protects confidentiality. *Why not B:* Brewer-Nash handles conflicts of interest.

**Item 3: D.** Brewer-Nash, the Chinese Wall model, changes access based on what a user has already accessed, to prevent conflicts of interest. *Why not B:* Clark-Wilson enforces integrity through approved programs and separation of duties, not conflicts between clients. *Why not A:* clearance levels do not change after access, so Bell-LaPadula cannot express this rule.

**Item 4: A.** Pairwise symmetric keys: n(n-1)/2 = 50 x 49 / 2 = 1,225. *Why not B:* 100 is 2n, the number of keys in an asymmetric scheme. *Why not C:* 2,450 forgets to divide by 2, counting each pair twice.

</details>

### Set 2

**Item 5.** Alice signs a contract file and sends it to Bob. Which key does Bob use to verify that Alice signed it?

- A. Alice's private key
- B. Bob's private key
- C. Alice's public key
- D. Bob's public key

**Item 6.** A web application must store user passwords so that a stolen database is as hard as possible to crack. Which approach is BEST?

- A. Encrypt the passwords with AES-256 and store the key on the same server
- B. Store an unsalted SHA-256 hash of each password
- C. Store an MD5 hash of each password with one shared secret added
- D. Store the output of a slow, salted key derivation function such as Argon2 or bcrypt

**Item 7.** An attacker with physical access to a smart card measures how long it takes to respond to many operations and uses the variations to recover its private key. What type of attack is this?

- A. Fault injection
- B. Timing attack
- C. Chosen ciphertext
- D. Frequency analysis

**Item 8.** An attacker dumps password hashes from a workstation's memory and then uses one hash directly to authenticate to a file server, without ever learning the plaintext password. What is this called?

- A. Pass the hash
- B. Brute force
- C. A rainbow table attack
- D. Known plaintext

<details>
<summary>Answers and explanations, items 5 to 8</summary>

**Item 5: C.** Signatures are created with the signer's private key and verified with the signer's public key, which anyone can obtain. *Why not A:* only Alice holds her private key; Bob cannot and should not have it. *Why not D:* Bob's keys are used when someone sends Bob a confidential message, not to check Alice's signature.

**Item 6: D.** A slow, salted key derivation function makes each guess expensive and defeats precomputed tables. *Why not B:* SHA-256 is fast and unsalted, so it is open to rainbow tables and rapid guessing. *Why not A:* encryption is reversible, and with the key on the same server a breach exposes every password.

**Item 7: B.** Measuring how long operations take to infer secret values is a timing attack, a kind of side-channel attack. *Why not A:* fault injection deliberately causes errors, such as voltage glitches; here the attacker only observes. *Why not C:* the attacker is not choosing ciphertexts to be decrypted.

**Item 8: A.** Reusing a captured hash as the credential, with no cracking, is pass the hash. *Why not C:* a rainbow table attack recovers the plaintext from a hash; here the plaintext is never needed. *Why not B:* nothing is being guessed.

</details>

### Set 3

**Item 9.** A company is building a data centre and wants a water-based sprinkler system with the lowest risk of accidental discharge onto equipment. Which type is BEST?

- A. Wet pipe
- B. Deluge
- C. Pre-action
- D. Dry pipe

**Item 10.** A perimeter firewall's software crashes. Which behaviour reflects the principle of failing securely?

- A. It passes all traffic until it is restarted, to keep the business online
- B. It blocks all traffic until it is restored
- C. It raises an alert and continues to pass traffic using its last rule set
- D. It switches to monitoring mode and logs all traffic

**Item 11.** A company moves its web servers to an Infrastructure as a Service provider. Who is responsible for patching the operating systems on those virtual machines?

- A. The provider, because it owns the hardware
- B. The provider and the customer equally, under a joint arrangement
- C. The hypervisor vendor
- D. The customer

**Item 12.** Laptops use full-disk encryption. The security team wants each laptop to release its disk key only if the firmware and boot loader have not been tampered with. Which component provides this?

- A. A Trusted Platform Module in each laptop
- B. A hardware security module in the data centre
- C. A firmware administrator password
- D. A smart card issued to each user

<details>
<summary>Answers and explanations, items 9 to 12</summary>

**Item 9: C.** Pre-action needs a detection event and then a head to open before water flows, so a single failure does not cause discharge. It is the usual water-based choice for data centres. *Why not D:* dry pipe avoids frozen pipes but releases water as soon as a head opens, without needing a separate detection event. *Why not B:* deluge floods the whole area at once.

**Item 10: B.** Failing securely means falling to a state that protects the assets. For a firewall, that is blocking traffic. *Why not A:* passing all traffic is failing open, which favours availability over security and is not the principle asked about. *Why not C:* a crashed process cannot be trusted to enforce its old rules correctly.

**Item 11: D.** In IaaS the provider secures the physical hosts and the virtualisation layer; the customer manages the guest operating system, applications and data, including patching. *Why not A:* owning the hardware does not make the provider responsible for software the customer installs. *Why not B:* shared responsibility splits duties by layer; it does not make each one joint.

**Item 12: A.** A TPM measures the boot chain and can seal the disk key so it is released only if the measurements match. *Why not B:* an HSM is a data centre key store and cannot measure each laptop's boot process. *Why not C:* a firmware password limits changes to settings but does not tie the disk key to an unchanged boot chain.

</details>

## Score yourself

| Item | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Answer | B | C | D | A | C | D | B | A | C | B | D | A |

- **11 to 12:** strong. Keep the crypto rules fresh with short mixed sets.
- **8 to 10:** draw the "who holds which key" grid and the two model rule tables from memory each day.
- **7 or fewer:** work through Key concepts one block at a time, writing a one-line example for each row, then redo the items.

## Next step

Domain 3 rewards fast recall under pressure. Test it in a timed run with the [free CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp), and return to the traps list for anything that slipped.

## Sources for this page

- [ISC2 CISSP Certification Exam Outline](https://www.isc2.org/certifications/cissp/cissp-certification-exam-outline), for the subdomains, weight and AI notes

---

<!-- nav:bottom -->← Previous: [Domain 2: Asset Security](asset-security.md) | Next: [Domain 4: Communication and Network Security](communication-and-network-security.md) → | [Back to contents](../../README.md#contents)<!-- /nav:bottom -->
