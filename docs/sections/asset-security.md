<!-- nav:top -->
[Contents](../../README.md#contents) · Previous: [Domain 1: Security and Risk Management](security-and-risk-management.md) · Next: [Domain 3: Security Architecture and Engineering](security-architecture-and-engineering.md)
<!-- /nav:top -->

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

These 2 items are original, written for these notes. They are not taken from ISC2 or any prep provider.

**Item 1.** Solid-state drives that held secret project data are being retired and will leave the organisation for recycling. Which method is MOST reliable?

- A. Degaussing each drive
- B. Overwriting each drive three times
- C. Physically destroying each drive
- D. Reformatting each drive

**Item 2.** Policy says email is deleted after two years. Legal counsel warns that litigation is likely over a deal from three years ago, and copies of those emails still exist on backup tapes due to be overwritten next month. What should happen FIRST?

- A. Place a legal hold on the relevant data and suspend the scheduled overwrite
- B. Let the overwrite proceed, since the policy retention period has passed
- C. Restore the emails and have security staff review them for relevance
- D. Ask the staff involved whether they kept personal copies

<details>
<summary>Answers and explanations, items 1 and 2</summary>

**Item 1: C.** For sensitive data on SSDs leaving your control, physical destruction is the most certain method. *Why not A:* degaussing does not affect flash storage. *Why not B:* wear levelling and spare blocks mean overwrites may miss data on an SSD.

**Item 2: A.** Anticipated litigation creates a duty to preserve relevant data. A legal hold overrides the normal schedule and must come first, before the evidence is lost. *Why not B:* destroying evidence once litigation is foreseeable can bring serious legal penalties. *Why not C:* review comes later, under counsel's direction; preservation comes first.

</details>

Want more? The [free timed CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=557dqd&utm_content=cissp) has 25 questions across all eight domains, scored by domain.

## Score yourself

| Item | 1 | 2 |
|---|---|---|
| Answer | C | A |

- **2:** solid. Domain 2 is worth 10%, so move on to a heavier domain.
- **1:** list the term pairs you mixed up and write one line for each that separates them.
- **0:** reread the roles table and the sanitisation table until you can rebuild them from memory, then redo the items.

## Next step

Mix Domain 2 items with other domains so the distinctions hold up under pressure. The [free CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=557dqd&utm_content=cissp) gives you a timed mixed set.

## Sources for this page

- [ISC2 CISSP Certification Exam Outline](https://www.isc2.org/certifications/cissp/cissp-certification-exam-outline), for the subdomains, weight and AI notes

---

<!-- nav:bottom -->
← Previous: [Domain 1: Security and Risk Management](security-and-risk-management.md) | Next: [Domain 3: Security Architecture and Engineering](security-architecture-and-engineering.md) → | [Back to contents](../../README.md#contents)
<!-- /nav:bottom -->
