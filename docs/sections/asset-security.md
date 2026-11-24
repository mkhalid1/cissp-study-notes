<!-- nav:top -->[Contents](../../README.md#contents) · Previous: [Domain 1: Security and Risk Management](security-and-risk-management.md) · Next: [Domain 3: Security Architecture and Engineering](security-architecture-and-engineering.md)<!-- /nav:top -->

# Domain 2: Asset Security

**In one line:** knowing what information and assets you have, who owns them, how sensitive they are, and how to protect them from creation to destruction.

ISC2 gives Asset Security an average weight of **10%**, one of the two smallest domains. It is small but dense with distinctions that examiners test directly: owner or custodian, controller or processor, clearing or purging, scoping or tailoring. Most points here are lost by mixing up two terms that sound alike.

## What it covers

| Subdomain (official title) | What you need to be able to do |
|---|---|
| 2.1 Identify and classify information and assets | Run data classification and asset classification schemes. |
| 2.2 Establish information and asset handling requirements | Set marking, labelling, storage, transmission and disposal rules per class. |
| 2.3 Provision information and assets securely | Information and asset ownership, asset inventory (tangible and intangible), asset management. |
| 2.4 Manage data lifecycle | Data roles (owners, controllers, custodians, processors, users and subjects), collection, location, maintenance, retention, remanence and destruction. |
| 2.5 Ensure appropriate asset retention (e.g., End of Life (EOL), End of Support) | Decide what to do when assets age out of support or retention. |
| 2.6 Determine data security controls and compliance requirements | Data states (in use, in transit, at rest), scoping and tailoring, standards selection, and protection methods such as DRM, DLP and CASB. |

ISC2 notes that AI assets now belong here: training datasets, pre-trained models and model weights are classified and protected like other high-value information, and their integrity matters because poisoned training data produces a poisoned model.

## Key concepts

### Classification

Classification assigns a sensitivity level based on the harm that disclosure, alteration or loss would cause. It is decided by the **owner**, not by IT.

| Typical government scheme | Typical commercial scheme |
|---|---|
| Top Secret | Confidential or Restricted |
| Secret | Private |
| Confidential | Sensitive or Internal |
| Unclassified | Public |

Exact labels vary by country and company. What matters for the exam:

- Classify by the value and impact, not by who created it.
- Fewer levels are easier to use correctly. Too many levels and people over-classify.
- Classification drives handling: who may access, how it is stored, sent, retained and destroyed.
- **Marking** is a human-readable notice ("Confidential"). **Labelling** is often used for the metadata or system-readable tag. Both must match the classification.
- Data should be reviewed and declassified when its sensitivity drops, or it is over-protected forever.

### Asset inventory and ownership

You cannot protect what you do not know you have. An inventory lists tangible assets (hardware, media) and intangible assets (data, software licences, intellectual property), each with an owner. Inventory comes before classification, which comes before choosing controls.

### Data roles

| Role | Who | Responsibility |
|---|---|---|
| Data owner | Senior business manager for that data | Classifies it, approves access, is accountable for its protection |
| Data controller | The organisation that decides why and how personal data is processed (privacy law term) | Legally responsible for lawful processing |
| Data processor | A party that processes personal data on the controller's behalf, for example a payroll provider | Processes only on the controller's instructions |
| Data custodian | Usually IT or operations | Implements the owner's decisions: backups, permissions, encryption |
| Data steward | A business role focused on data quality and metadata | Keeps data accurate and usable |
| Data subject | The person the personal data is about | Has rights under privacy law |
| User | Anyone who uses the data | Follows the handling rules |

### The data lifecycle

Create or collect, store, use, share, archive, destroy. Each stage has controls:

- **Collection:** collect only what the stated purpose needs (data minimisation), with a lawful basis.
- **Location:** know where data physically and legally sits, including cloud regions, because laws follow location.
- **Maintenance:** keep it accurate, backed up and access-controlled.
- **Retention:** keep it as long as law, regulation and business need require, and no longer. A **legal hold** suspends deletion for data relevant to expected or actual litigation, overriding the normal schedule.
- **Remanence and destruction:** see below.

### Data states and their controls

| State | Examples | Typical controls |
|---|---|---|
| At rest | Disks, databases, backups, laptops | Full-disk or database encryption, access control, physical security |
| In transit | Network traffic, email, API calls | TLS, VPNs, IPsec, DLP at gateways |
| In use | In memory or being processed | Access control, memory protection, secure enclaves, privacy techniques such as masking |

### Remanence and sanitisation

Data remanence is data left behind after deletion. Deleting a file or formatting a disk usually removes only the pointers.

| Method | What it does | Notes |
|---|---|---|
| Clearing | Overwrites with non-sensitive data so normal tools cannot recover it | Fine for reuse inside the organisation at the same sensitivity |
| Purging | Makes recovery infeasible even with lab techniques: degaussing, cryptographic erase, secure erase commands | Needed before media leaves your control |
| Destruction | Physical: shredding, disintegration, incineration, pulverising | Most certain. Use for the most sensitive media |
| Cryptographic erasure (crypto-shredding) | Destroy the keys to encrypted data | The practical answer in the cloud, where you cannot touch the disks |

Two facts that appear often: **degaussing does not work on SSDs or optical media**, because they do not store data magnetically, and overwriting is unreliable on SSDs because of wear levelling and spare blocks. For SSDs use the drive's secure erase or cryptographic erase, or destroy them.

### Retention and end of life

End of Life (EOL) usually means the vendor stops selling a product; End of Support (EOS) means no more patches. An unsupported system is a growing risk. Options in order of preference: replace or upgrade; buy extended support if offered; otherwise isolate it, add compensating controls such as network segmentation and extra monitoring, and have the owner formally accept the remaining risk until it is retired.

### Scoping, tailoring and standards selection

- **Standards selection:** choose a control framework or baseline that fits the organisation and its legal obligations.
- **Scoping:** decide which controls from the baseline apply. Removing wireless controls from a system that has no wireless is scoping.
- **Tailoring:** adjust the controls that remain to fit the environment, for example setting a session lock time or substituting a compensating control.

### DRM, DLP and CASB

| Tool | Protects | Typical use |
|---|---|---|
| Digital Rights Management (DRM) | The file itself, wherever it goes | Stop printing or forwarding, set expiry, revoke access later |
| Data Loss Prevention (DLP) | Sensitive data leaving through endpoints, email or the network | Detect and block card numbers in outbound email |
| Cloud Access Security Broker (CASB) | Use of cloud services | Discover unsanctioned SaaS (shadow IT), enforce policy, monitor activity |

## How the questions look

Expect short scenarios that hinge on one distinction. Who should classify this data? Which sanitisation method fits this media and this destination? Is this provider a controller or a processor? Which control protects data in this state? There are also management-style items about what to do FIRST, where the answer is usually inventory, ownership or classification before tools.

## A method that works

1. **Name the asset and its sensitivity.** What is it, and how bad would loss or disclosure be?
2. **Name the role in the question.** Owner, custodian, controller, processor? Many items are answered by who has the authority.
3. **Name the state or stage.** At rest, in transit, in use? Collection, retention or destruction?
4. **For disposal, ask where the media is going.** Staying inside at the same level allows clearing. Leaving your control needs purging or destruction.
5. **For disposal, ask what the media is.** Magnetic, SSD or flash, optical, cloud?
6. **Prefer foundations first.** Inventory, then classification, then handling rules, then tools.

## Traps that cost points

- **Letting IT classify data.** Custodians implement; owners classify.
- **Degaussing an SSD.** It does nothing useful. Use secure or cryptographic erase, or destroy it.
- **Treating formatting as sanitisation.** It leaves the data recoverable.
- **Confusing scoping with tailoring.** Scoping removes controls that do not apply; tailoring adjusts the ones that do.
- **Mixing up controller and processor.** The controller decides purpose and means; the processor follows instructions.
- **Deleting under a legal hold.** A hold overrides the normal retention schedule.
- **Choosing DLP when the question is about a file after it leaves.** That is DRM.
- **Collecting extra personal data "just in case".** Data minimisation says no.

## Timing

Most Domain 2 items are quick once you spot the distinction. As guidance, aim for about 50 to 60 seconds each and bank the time for longer architecture and operations scenarios.

## Practice items

These 12 items are original, written for these notes. They are not taken from ISC2 or any prep provider.

### Set 1

**Item 1.** HR has built a new dataset combining salary, disciplinary and medical leave records. Who should decide its classification?

- A. The database administrator who maintains it
- B. The HR director who is accountable for the data
- C. The CISO, who owns the classification policy
- D. The HR staff who enter records into it

**Item 2.** Solid-state drives that held secret project data are being retired and will leave the organisation for recycling. Which method is MOST reliable?

- A. Degaussing each drive
- B. Overwriting each drive three times
- C. Physically destroying each drive
- D. Reformatting each drive

**Item 3.** A company uses an outside payroll provider. The company decides which employee data is processed and for what purpose; the provider runs the calculations on the company's instructions. Under privacy law terminology, the provider is the:

- A. data controller.
- B. data processor.
- C. data custodian.
- D. data steward.

**Item 4.** A gateway rule scans outgoing email and blocks messages containing payment card numbers. Which data state does it primarily protect?

- A. Data at rest
- B. Data in use
- C. Data in transit
- D. Archived data

<details>
<summary>Answers and explanations, items 1 to 4</summary>

**Item 1: B.** The data owner, a business manager accountable for the data, classifies it. *Why not C:* the CISO writes the policy that defines the levels, but does not classify each business dataset. *Why not A:* the DBA is a custodian, who implements the owner's decisions.

**Item 2: C.** For sensitive data on SSDs leaving your control, physical destruction is the most certain method. *Why not A:* degaussing does not affect flash storage. *Why not B:* wear levelling and spare blocks mean overwrites may miss data on an SSD.

**Item 3: B.** A party that processes personal data on another's instructions is a processor. The company, which decides purpose and means, is the controller. *Why not C:* custodian is a security role, usually internal IT, not the privacy law term for an outside processor. *Why not A:* the provider does not decide the purpose.

**Item 4: C.** Email leaving through a gateway is moving across the network, so it is data in transit. *Why not A:* the rule does not touch stored data. *Why not B:* in use means data being processed in memory.

</details>

### Set 2

**Item 5.** An organisation adopts a control baseline. For a lab system with no wireless capability, the team removes the wireless controls because they do not apply, before adjusting any settings of the remaining controls. Removing the controls that do not apply is:

- A. tailoring.
- B. scoping.
- C. compensating.
- D. hardening.

**Item 6.** Policy says email is deleted after two years. Legal counsel warns that litigation is likely over a deal from three years ago, and copies of those emails still exist on backup tapes due to be overwritten next month. What should happen FIRST?

- A. Place a legal hold on the relevant data and suspend the scheduled overwrite
- B. Let the overwrite proceed, since the policy retention period has passed
- C. Restore the emails and have security staff review them for relevance
- D. Ask the staff involved whether they kept personal copies

**Item 7.** A database server runs an operating system that reached end of support last month. The vendor offers no extended support and the application cannot be migrated for nine months. What is the BEST approach?

- A. Keep running it as it is, since it has had no incidents
- B. Shut it down immediately until a migration is complete
- C. Install third-party antivirus on the server and record the risk as resolved in the register
- D. Isolate it, add compensating controls, and have the owner formally accept the remaining risk until migration

**Item 8.** Your organisation is leaving a public cloud provider and must ensure its stored data cannot be recovered from the provider's disks. All the data was encrypted with keys that your organisation manages, and you cannot access the hardware. Which approach is BEST?

- A. Ask the provider to degauss the disks that held your data
- B. Delete all objects and rely on the provider's standard process for reusing storage
- C. Destroy the encryption keys protecting the data so the remaining ciphertext is unreadable
- D. Overwrite every stored object with random data several times before deleting it

<details>
<summary>Answers and explanations, items 5 to 8</summary>

**Item 5: B.** Removing controls that do not apply to a system is scoping. *Why not A:* tailoring adjusts the controls that remain, such as setting parameters. Some frameworks, including NIST, describe scoping as one step within tailoring, but when the options separate them, removing inapplicable controls is scoping. *Why not C:* nothing is being substituted for a control that cannot be met.

**Item 6: A.** Anticipated litigation creates a duty to preserve relevant data. A legal hold overrides the normal schedule and must come first, before the evidence is lost. *Why not B:* destroying evidence once litigation is foreseeable can bring serious legal penalties. *Why not C:* review comes later, under counsel's direction; preservation comes first.

**Item 7: D.** With no support and no quick migration, the risk must be reduced with isolation and compensating controls, and the owner must accept what remains in writing. *Why not B:* an immediate shutdown ignores the business need and is not proportionate to a risk that can be reduced. *Why not A:* doing nothing is not acceptance; it is ignoring the risk.

**Item 8: C.** Cryptographic erasure is the practical method when you cannot reach the media. Without the keys, the ciphertext left on the provider's disks is useless. *Why not D:* in cloud storage, overwriting an object may write to new physical blocks and leave the old ones intact. *Why not A:* providers will not degauss shared disks for one tenant, and degaussing fails on SSDs anyway.

</details>

### Set 3

**Item 9.** A law firm wants to send draft contracts to clients and prevent the files from being printed, forwarded or opened after 30 days, even on the clients' own computers. Which control fits BEST?

- A. Digital rights management
- B. Data loss prevention
- C. Full-disk encryption
- D. A cloud access security broker

**Item 10.** The security team suspects staff are using dozens of unapproved file-sharing and AI tools in the cloud. They want to discover which services are in use and enforce policy on them. Which control fits BEST?

- A. Digital rights management
- B. Data loss prevention on each laptop
- C. A web application firewall
- D. A cloud access security broker

**Item 11.** A newly hired CISO is asked to improve protection of the company's information. Which should come FIRST?

- A. Build an inventory of information assets and identify their owners
- B. Deploy DLP on all endpoints
- C. Encrypt every server and laptop
- D. Write handling procedures for each classification level

**Item 12.** Marketing wants the newsletter sign-up form to ask for full date of birth "in case it is useful later". The newsletter has no age restriction. Which response follows privacy principles BEST?

- A. Collect it, but encrypt it at rest
- B. Collect it, as long as subscribers tick a consent box
- C. Collect it, and anonymise it after one year
- D. Do not collect it, because the stated purpose does not need it

<details>
<summary>Answers and explanations, items 9 to 12</summary>

**Item 9: A.** DRM controls what can be done with a file wherever it goes, including printing, forwarding and expiry. *Why not B:* DLP stops data leaving your environment; here the files are meant to leave. *Why not C:* disk encryption protects data at rest on your devices, not the file on a client's machine.

**Item 10: D.** A CASB discovers cloud service use, including shadow IT, and enforces policy on it. *Why not B:* endpoint DLP looks for sensitive content leaving devices; it does not map and govern cloud services. *Why not C:* a WAF protects your own web applications from attacks.

**Item 11: A.** You cannot classify or protect what you have not identified. Inventory and ownership come first, then classification, then handling rules and tools. *Why not D:* handling procedures depend on classification, which depends on knowing the assets. *Why not C:* blanket encryption is a tool choice made before knowing what needs protecting.

**Item 12: D.** Data minimisation means collecting only what the stated purpose needs. With no age rule, date of birth is not needed. *Why not B:* consent does not make unnecessary collection minimal. *Why not A:* encryption protects data you hold; the question is whether to hold it at all.

</details>

## Score yourself

| Item | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Answer | B | C | B | C | B | A | D | C | A | D | A | D |

- **11 to 12:** solid. Domain 2 is worth 10%, so move on to a heavier domain.
- **8 to 10:** list the term pairs you mixed up and write one line for each that separates them.
- **7 or fewer:** reread the roles table and the sanitisation table until you can rebuild them from memory, then redo the items.

## Next step

Mix Domain 2 items with other domains so the distinctions hold up under pressure. The [free CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp) gives you a timed mixed set.

## Sources for this page

- [ISC2 CISSP Certification Exam Outline](https://www.isc2.org/certifications/cissp/cissp-certification-exam-outline), for the subdomains, weight and AI notes

---

<!-- nav:bottom -->← Previous: [Domain 1: Security and Risk Management](security-and-risk-management.md) | Next: [Domain 3: Security Architecture and Engineering](security-architecture-and-engineering.md) → | [Back to contents](../../README.md#contents)<!-- /nav:bottom -->
