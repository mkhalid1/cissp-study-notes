<!-- nav:top -->
[Contents](../../README.md#contents) · Previous: [Domain 6: Security Assessment and Testing](security-assessment-and-testing.md) · Next: [Domain 8: Software Development Security](software-development-security.md)
<!-- /nav:top -->

# Domain 7: Security Operations

**In one line:** running security day to day: investigations, monitoring, incident response, patching and change, backups and recovery, physical security and keeping people safe.

ISC2 gives this domain an average weight of **13%**, but it has the most subdomains of any domain: fifteen. That makes it broad rather than deep. Many questions are about order: what to collect first, what to do first in an incident, which test to run first, which backup to restore.

## What it covers

| Subdomain (official title) | What you need to be able to do |
|---|---|
| 7.1 Understand and comply with investigations | Evidence collection and handling, reporting and documentation, investigative techniques, digital forensics tools, tactics and procedures, and artifacts from data, computers, networks and mobile devices. |
| 7.2 Conduct logging and monitoring activities | IDPS, SIEM, continuous monitoring and tuning, egress monitoring, log management, threat intelligence and hunting, UEBA. |
| 7.3 Perform Configuration Management (CM) (e.g., provisioning, baselining, automation) | Build and keep systems in a known, approved state. |
| 7.4 Apply foundational security operations concepts | Need to know and least privilege, separation of duties, privileged account management, job rotation, SLAs. |
| 7.5 Apply resource protection | Media management and protection, data at rest and in transit. |
| 7.6 Conduct incident management | Detection, response, mitigation, reporting, recovery, remediation, lessons learned. |
| 7.7 Operate and maintain detection and preventative measures | Firewalls, IDS and IPS, allow and deny lists, third-party security services, sandboxing, honeypots and honeynets, anti-malware, machine learning and AI-based tools. |
| 7.8 Implement and support patch and vulnerability management | Find, prioritise, test and deploy fixes. |
| 7.9 Understand and participate in change management processes | Request, review, approve, test, implement, document. |
| 7.10 Implement recovery strategies | Backup storage, recovery sites, multiple processing sites, resilience, high availability, QoS and fault tolerance. |
| 7.11 Implement Disaster Recovery (DR) processes | Response, personnel, communications, assessment, restoration, training and awareness, lessons learned. |
| 7.12 Test Disaster Recovery Plans (DRP) | Read-through or tabletop, walkthrough, simulation, parallel, full interruption, and communications about tests. |
| 7.13 Participate in Business Continuity (BC) planning and exercises | Support the wider continuity programme. |
| 7.14 Implement and manage physical security | Perimeter and internal controls. |
| 7.15 Address personnel safety and security concerns | Travel, training on insider threat, social media and 2FA fatigue, emergency management, duress. |

ISC2 says AI appears here in security orchestration and automated response, in correlating alerts to reduce alert fatigue, and in monitoring production AI for model drift and live adversarial attacks.

## Key concepts

### Investigations and evidence

Evidence must be **relevant** (it relates to the case), **material** (it matters to the outcome) and **competent** (it was obtained legally and handled properly) to be admissible.

| Evidence type | Meaning |
|---|---|
| Best evidence | The original, such as the original document or drive |
| Secondary | A copy; acceptable when the original is unavailable |
| Direct | Proves a fact on its own, such as an eyewitness |
| Circumstantial | Supports a fact by inference |
| Corroborative | Supports other evidence |
| Hearsay | Second-hand; computer records may fall here unless they qualify as business records made in the normal course of business |

- **Chain of custody:** a record of who had the evidence, when, where and why, from collection to court. A gap can make evidence inadmissible.
- **Order of volatility:** collect the most volatile first: CPU registers and cache, then memory (RAM), then network state and running processes, then temporary files, then disk, then remote logs and backups. Pulling the plug destroys memory evidence.
- **Forensic imaging:** take a bit-for-bit copy using a write blocker, hash the original and the image to prove they match, and work only on copies.
- **Artifacts:** data files, system logs and registry, network captures and flow records, mobile device data. Mobile and cloud evidence may need provider cooperation and legal process.
- Investigations can be administrative, criminal, civil or regulatory (see Domain 1). Involve legal counsel early and do not tip off a suspect.

### Logging, monitoring and detection

| Tool | What it does |
|---|---|
| IDS | Detects and alerts. Network-based (NIDS) watches traffic; host-based (HIDS) watches one system. |
| IPS | Sits inline and can block. |
| Signature detection | Matches known patterns; few false positives, misses new attacks. |
| Anomaly or behaviour detection | Learns normal and flags deviations; catches new attacks, more false positives. |
| SIEM | Collects, normalises and correlates logs from many sources, and alerts. |
| SOAR | Automates response playbooks across tools. |
| UEBA | Builds baselines of user and entity behaviour and flags unusual activity, such as a huge download at 3 a.m. |
| Threat intelligence and hunting | Feeds of indicators and attacker techniques; proactive searching for threats that evaded alerts. |
| Egress monitoring | Watches outbound traffic for data theft and command-and-control, including DLP. |

Log management means synchronised time across sources, protection of logs from tampering (send them to a separate system), defined retention, and regular review. **Tuning** reduces false positives so analysts do not ignore alerts.

### Foundational operations concepts

- **Need to know and least privilege** limit what each person can see and do.
- **Separation of duties** splits sensitive tasks; **two-person control** requires two people at once for critical actions.
- **Privileged account management** vaults, monitors and limits admin access.
- **Job rotation** reduces dependence on one person and helps uncover fraud.
- **Service-level agreements** set measurable commitments, such as uptime and response times, with consequences.
- **Configuration management** keeps systems at an approved **baseline**, often through automation, and detects drift.

### Incident management

The outline's stages are detection, response, mitigation, reporting, recovery, remediation and lessons learned. Read them as:

1. **Detection:** confirm it is a real incident and assess its scope.
2. **Response:** activate the team and the plan.
3. **Mitigation (containment):** stop the spread. Isolate affected systems, but preserve evidence where you can.
4. **Reporting:** inform management and, when required, regulators, customers or law enforcement.
5. **Recovery:** restore systems to normal operation, carefully, with monitoring.
6. **Remediation:** fix the root cause so it cannot recur.
7. **Lessons learned:** review what happened and improve the plan, controls and training.

Containment comes before eradication and recovery. Reimaging a machine before containment lets the attack spread; before evidence capture, it destroys evidence.

### Preventive and detective measures

Allow lists (whitelisting) permit only approved software and are stronger than deny lists (blacklisting), which block known bad items. **Sandboxing** runs suspicious files in isolation to observe them. **Honeypots** and **honeynets** are decoys that attract attackers and reveal their methods; they must not be used to entrap, and must be isolated. Third-party managed security services still need contracts, SLAs and oversight.

### Patch, vulnerability and change management

- Patch process: learn of the fix, assess and prioritise by risk (exposure, exploitation, asset value), test, deploy through change management, verify, and report. Actively exploited flaws on exposed systems go first, often through an emergency change.
- Change management: request, impact and risk review, approval by a change advisory board or authority, testing, scheduled implementation with a back-out plan, documentation, and post-implementation review. **Emergency changes** follow a faster path but are still documented and reviewed afterwards.

### Recovery strategies

| Backup type | Backs up | Restore needs | Archive bit |
|---|---|---|---|
| Full | Everything | The last full | Cleared |
| Incremental | Changes since the last backup of any type | The last full plus **every** incremental since | Cleared |
| Differential | Changes since the last **full** | The last full plus the **latest** differential | Not cleared |

Store copies offsite or in the cloud, far enough away to escape the same disaster, and keep at least one copy offline or immutable against ransomware.

| Recovery site | Ready in | Cost | Notes |
|---|---|---|---|
| Hot | Minutes to hours | Highest | Fully equipped, data current or near current |
| Warm | Hours to days | Medium | Equipment present, data must be loaded |
| Cold | Days to weeks | Lowest | Space and power only |
| Mobile | Varies | Varies | Trailers or containers brought to a location |
| Reciprocal agreement | Varies | Low | Another organisation hosts you; hard to enforce, capacity often lacking |
| Cloud or multiple processing sites | Varies by design | Varies | Active-active sites can make recovery near instant |

| RAID level | How | Survives |
|---|---|---|
| 0 | Striping, no redundancy | No disk failure |
| 1 | Mirroring | One disk of a mirrored pair |
| 5 | Striping with distributed parity, three or more disks | One disk |
| 6 | Striping with double parity | Two disks |
| 10 (1+0) | Mirrored sets, striped | One disk per mirror |

**High availability** keeps services running through clustering and failover; **fault tolerance** keeps working despite a component failure with no interruption; **QoS** prioritises critical traffic. RAID is not a backup: it does not protect against deletion, corruption or ransomware.

### DR processes and DR tests

During a disaster: protect people first, assess damage, declare the disaster, activate teams and communications, restore critical functions in priority order at the recovery site, then restore the primary site and fail back carefully, starting with the least critical functions.

| Test (from least to most disruptive) | What happens |
|---|---|
| Read-through or tabletop (checklist) | Team members review the plan, alone or around a table, for accuracy and gaps |
| Walkthrough | Team members talk through a scenario together, step by step |
| Simulation | A realistic scenario is played out, short of moving operations |
| Parallel | Systems are brought up at the recovery site and process real data while the primary keeps running |
| Full interruption | The primary site is shut down and operations move to the recovery site. Most realistic, highest risk; needs senior management approval |

Communicate test status to stakeholders, and to regulators where required.

### Physical security and personnel safety

- Perimeter: fences, lighting, bollards, gates, CCTV, guards. Internal: badges, mantraps, locks, visitor escorts, alarms.
- People's safety comes first, always: evacuation plans, emergency management, and training.
- **Duress:** a code word, silent alarm or duress PIN lets someone signal they are being forced, without alerting the attacker.
- **Travel:** loaner devices, VPN, awareness of local laws and border device searches.
- Training topics in the outline include insider threat, social media oversharing, and **2FA fatigue**, where attackers flood users with push prompts hoping one is approved.

## How the questions look

Domain 7 items are scenario-heavy and often about sequence. Expect questions such as: what to collect FIRST, what the incident team should do NEXT, which site meets a stated RTO, which backups are needed to restore, which DR test fits the risk appetite. Some items test fine distinctions such as IDS versus IPS, or incremental versus differential.

## A method that works

1. **Protect people first.** If any option protects life safety, start there.
2. **Find the stage.** Investigation, detection, containment, recovery, or lessons learned? Pick the action that belongs to the current stage, not a later one.
3. **For evidence, preserve before you analyse.** Volatile data first, chain of custody throughout, work on copies.
4. **For recovery, match the requirement.** Read the RTO and RPO and pick the cheapest option that meets them.
5. **For backups, write the week out** with each day's backup type before choosing.
6. **For changes and patches, follow the process,** using the emergency path when risk demands, never skipping documentation.

## Traps that cost points

- **Powering off a compromised machine first.** You lose memory evidence. Isolate it from the network instead, unless doing so would cause harm.
- **Eradicating before containing.** Contain first.
- **Restoring every differential.** You need only the full and the latest differential.
- **Forgetting incrementals.** You need the full and every incremental since.
- **Choosing a cold site for a short RTO.** Cold sites take days or weeks.
- **Running a full interruption test casually.** It is the riskiest test and needs senior approval.
- **Treating RAID as a backup.** It does not protect against deletion or ransomware.
- **Skipping change control in an emergency.** Use the emergency process and document it.
- **Using a honeypot to entrap.** Decoys may observe, not induce crimes.
- **Leaving lessons learned out.** It is where future improvement comes from.

## Timing

As guidance, sequence and scenario items here take 60 to 80 seconds; recall items such as RAID levels take 30 to 45. When two steps both seem right, ask which one must happen before the other is even possible.

## Practice items

These 2 items are original, written for these notes. They are not taken from ISC2 or any prep provider.

**Item 1.** The SOC confirms that ransomware is spreading across several workstations. What should the incident response team do FIRST?

- A. Wipe and reimage the affected workstations
- B. Isolate the affected workstations from the network
- C. Restore the encrypted files from backup
- D. Issue a press statement about the incident

**Item 2.** A full backup runs every Sunday night and a differential backup runs on Monday to Saturday nights. The server fails on Thursday morning before that night's backup. What is needed to restore it?

- A. Sunday's full backup and the differentials from Monday, Tuesday and Wednesday
- B. Sunday's full backup and Wednesday's differential
- C. Wednesday's differential only
- D. Sunday's full backup only

<details>
<summary>Answers and explanations, items 1 and 2</summary>

**Item 1: B.** Containment comes first: isolating the machines stops the ransomware spreading further and preserves evidence. *Why not A:* reimaging before containment lets it keep spreading and destroys evidence. *Why not C:* restoring before containment risks the restored data being encrypted again.

**Item 2: B.** A differential holds all changes since the last full, so the last full plus the latest differential is enough. *Why not A:* the Monday and Tuesday differentials are already included in Wednesday's. *Why not C:* a differential without its full backup cannot restore the system.

</details>

Want more? The [free timed CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp) has 25 questions across all eight domains, scored by domain.

## Score yourself

| Item | 1 | 2 |
|---|---|---|
| Answer | B | B |

- **2:** strong. Domain 7 is broad, so keep doing mixed sets.
- **1:** most misses here are sequence errors. Write the incident stages and the order of volatility from memory.
- **0:** work through the backup, site, RAID and DR test tables until you can rebuild them, then redo the items.

## Next step

Sequence questions are where nerves hurt most. Practise them timed with the [free CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp), then come back to the traps list.

## Sources for this page

- [ISC2 CISSP Certification Exam Outline](https://www.isc2.org/certifications/cissp/cissp-certification-exam-outline), for the subdomains, weight and AI notes

---

<!-- nav:bottom -->
← Previous: [Domain 6: Security Assessment and Testing](security-assessment-and-testing.md) | Next: [Domain 8: Software Development Security](software-development-security.md) → | [Back to contents](../../README.md#contents)
<!-- /nav:bottom -->
