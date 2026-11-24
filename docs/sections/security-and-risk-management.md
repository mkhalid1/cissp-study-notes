<!-- nav:top -->[Contents](../../README.md#contents) · Previous: [5-minute diagnostic](../diagnostic.md) · Next: [Domain 2: Asset Security](asset-security.md)<!-- /nav:top -->

# Domain 1: Security and Risk Management

**In one line:** how a security programme is governed, justified and kept legal: ethics, risk, policy, law, continuity planning and people.

ISC2 gives this domain an average weight of **16%** of the exam, the largest of the eight. It is also the domain that sets the tone for every other one. When a question in any domain asks what you should do FIRST or BEST, the answer usually comes from the thinking in this chapter: understand the business, assess risk, get management support, follow policy, protect people.

## What it covers

The April 15, 2024 outline lists twelve subdomains:

| Subdomain (official title) | What you need to be able to do |
|---|---|
| 1.1 Understand, adhere to, and promote professional ethics | Apply the ISC2 Code of Ethics canons, in order, to a dilemma. |
| 1.2 Understand and apply security concepts | Use confidentiality, integrity, availability, authenticity and nonrepudiation precisely. |
| 1.3 Evaluate and apply security governance principles | Align security with business goals, roles and frameworks; know who is accountable. |
| 1.4 Understand legal, regulatory, and compliance issues that pertain to information security in a holistic context | Handle intellectual property, privacy, breach rules, import and export limits and cross-border data. |
| 1.5 Understand requirements for investigation types | Tell administrative, criminal, civil, regulatory and industry-standard investigations apart. |
| 1.6 Develop, document, and implement security policy, standards, procedures, and guidelines | Put each document type at the right level, mandatory or not. |
| 1.7 Identify, analyze, assess, prioritize, and implement Business Continuity (BC) requirements | Run a business impact analysis and set recovery targets. |
| 1.8 Contribute to and enforce personnel security policies and procedures | Screening, agreements, onboarding, transfers, termination, vendor staff. |
| 1.9 Understand and apply risk management concepts | Identify, assess, respond to and monitor risk; choose control types. |
| 1.10 Understand and apply threat modeling concepts and methodologies | Use a structured model such as STRIDE or PASTA to find threats early. |
| 1.11 Apply Supply Chain Risk Management (SCRM) concepts | Manage risk from suppliers, hardware, software and service providers. |
| 1.12 Establish and maintain a security awareness, education, and training program | Design training for different audiences and measure whether it works. |

ISC2 also says AI is woven into this domain: governing AI ethics and algorithmic bias, fitting machine learning models into risk management, and checking the security of third-party AI providers as part of supply chain risk.

## Key concepts

### The ISC2 Code of Ethics canons

ISC2 lists four canons. Treat them as an order of priority when they conflict.

| Order | Canon | In practice |
|---|---|---|
| 1 | Protect society, the common good, necessary public trust and confidence, and the infrastructure | Public safety beats your employer's convenience. |
| 2 | Act honorably, honestly, justly, responsibly, and legally | No lying, no illegal shortcuts, even if asked. |
| 3 | Provide diligent and competent service to principals | Do good work for your employer or client. |
| 4 | Advance and protect the profession | Mentor, share knowledge, do not bring the field into disrepute. |

If an employer (a principal, canon 3) asks you to hide something that harms the public (canon 1), canon 1 wins.

### Security concepts you must use precisely

- **Confidentiality:** only authorised parties can read it. Threats: disclosure, eavesdropping, shoulder surfing.
- **Integrity:** it has not been changed without authorisation, and you can tell if it has. Threats: tampering, unauthorised modification.
- **Availability:** authorised users can get it when they need it. Threats: denial of service, outages, lost keys.
- **Authenticity:** it really came from who it claims to come from.
- **Nonrepudiation:** the sender cannot credibly deny sending it. Needs a digital signature tied to one person's private key. A shared secret, such as a symmetric key or an HMAC key, cannot give nonrepudiation, because both parties hold it.

### Governance: who decides, who does

| Role | Responsibility |
|---|---|
| Board and senior management | Ultimately accountable for security. They set risk appetite, approve policy and fund the programme. |
| CISO or security lead | Designs and runs the programme, advises management, reports risk. |
| Data owner | A business manager who classifies data and decides who may access it. |
| Custodian | Usually IT. Implements the owner's decisions: backups, access settings, patching. |
| Users | Follow policy and report incidents. |
| Auditors | Independently check that controls work and report to management or the board. |

Frameworks you should recognise by purpose: ISO/IEC 27001 (a certifiable management system for information security), ISO/IEC 27002 (a catalogue of controls), NIST Cybersecurity Framework (outcomes organised by functions such as Identify, Protect, Detect, Respond, Recover, with Govern added in version 2.0), COBIT (governance and management of enterprise IT).

**Due care** is doing what a reasonable person would do: having and following the controls. **Due diligence** is the investigation and checking that tells you which controls are needed and whether they work, for example reviewing a supplier before signing.

### Policy documents, from top to bottom

| Document | Mandatory? | Example |
|---|---|---|
| Policy | Yes. High level, approved by senior management. | "All customer data must be encrypted at rest." |
| Standard | Yes. Specific, measurable requirements. | "Use AES with 256-bit keys." |
| Baseline | Yes. The minimum configuration for a system type. | "Every web server starts from this hardened build." |
| Procedure | Yes. Step-by-step instructions. | "How to rotate the database encryption key." |
| Guideline | No. Recommended practice. | "Tips for choosing a passphrase." |

### Law, intellectual property and investigations

| Protection | Protects | Key point |
|---|---|---|
| Patent | An invention | Must be novel, useful and not obvious. Time-limited. Public disclosure is the price. |
| Trademark | A name, logo or brand | Can be renewed indefinitely while in use. |
| Copyright | An expression of an idea, such as code or text | Automatic on creation in most countries. Protects the expression, not the idea. |
| Trade secret | Confidential business information, such as a formula | Protected only while you keep it secret, often with NDAs. |

| Investigation type | Who runs it | Usual standard of proof |
|---|---|---|
| Administrative | The organisation itself, about policy breaches | Internal; no court standard |
| Civil | Parties in a dispute, damages awarded | Preponderance of evidence (more likely than not) |
| Criminal | Law enforcement and prosecutors | Beyond a reasonable doubt, the highest standard |
| Regulatory | A government regulator | Depends on the regulator; can lead to fines |
| Industry standards | An industry body, for example a card payment standard | Contract and compliance consequences |

For privacy, know the common principles that laws such as the EU GDPR build on: lawful basis, purpose limitation, data minimisation, accuracy, storage limitation, integrity and confidentiality, and accountability. Transborder data flow rules limit where personal data may be sent.

### Risk management, with the numbers

- **Asset value (AV):** what the asset is worth.
- **Exposure factor (EF):** the share of the asset lost in one event, as a percentage.
- **Single loss expectancy (SLE)** = AV x EF.
- **Annualised rate of occurrence (ARO):** how many times a year it is expected. Once every 4 years is 0.25.
- **Annualised loss expectancy (ALE)** = SLE x ARO.
- **Value of a safeguard** = ALE before the control, minus ALE after the control, minus the annual cost of the control. If the result is negative, the control costs more than it saves.

Worked example: a warehouse system is worth 500,000. A flood would destroy 40% of it, so SLE = 200,000. Floods hit once every 10 years, ARO = 0.1, so ALE = 20,000 a year. A barrier costs 6,000 a year and cuts the ALE to 4,000. Its value is 20,000 minus 4,000 minus 6,000, which is 10,000 a year. Worth buying.

| Risk response | What it means | Example |
|---|---|---|
| Mitigate (reduce) | Add controls to lower likelihood or impact | Install a firewall, add MFA |
| Transfer (share) | Move the financial impact to someone else | Insurance, outsourcing with contractual liability |
| Avoid | Stop the activity that creates the risk | Do not launch the risky product |
| Accept | Knowingly live with it, with management sign-off | Document why the cost of control exceeds the loss |

You can never transfer accountability. The organisation still owns the risk even when a supplier or insurer carries the cost. Ignoring a risk is not acceptance: acceptance is a documented management decision.

**Control types** are administrative (policies, training), technical or logical (encryption, ACLs) and physical (locks, guards). **Control functions** are preventive, detective, corrective, deterrent, recovery, directive and compensating. A compensating control is an alternative used when the primary control is not feasible.

### Business continuity: the BIA and the time terms

The order is: get senior management support and scope, run the business impact analysis (BIA), choose recovery strategies, write the plan, train, test and maintain it.

| Term | Meaning |
|---|---|
| MTD (maximum tolerable downtime) | The longest a process can be down before the damage is unacceptable. Also called MTPD or MAO. |
| RTO (recovery time objective) | The target time to restore the system. |
| WRT (work recovery time) | Time after the system is back to verify data and resume normal work. |
| RPO (recovery point objective) | The maximum data loss you can accept, measured as time. An RPO of 4 hours means backups or replication at least every 4 hours. |

The rule to remember: **RTO + WRT must not exceed MTD.**

### Personnel security

- Screening before hire, in proportion to the role and allowed by local law.
- Agreements: NDAs, acceptable use, non-compete where lawful.
- **Separation of duties:** no one person can complete a sensitive task alone, which prevents fraud unless people collude.
- **Job rotation** and **mandatory vacations:** someone else does the job for a while, which helps detect fraud that depends on one person being present.
- **Least privilege** and **need to know.**
- Termination: disable access at or before the moment the person is told, collect assets, hold an exit interview, remind them of continuing obligations.

### Threat modeling and supply chain

**STRIDE** (from Microsoft) names threat categories: Spoofing (identity), Tampering (integrity), Repudiation (nonrepudiation), Information disclosure (confidentiality), Denial of service (availability), Elevation of privilege (authorisation). **PASTA** is a seven-stage, risk-centric process that starts from business objectives. Threat modeling is cheapest during design.

Supply chain risk management covers hardware provenance (counterfeit or tampered parts), software components and their updates, and service providers. Typical controls: buy through authorised channels, contract for security requirements and the right to audit, check assurance reports, keep a list of components, and plan for a supplier failing.

### Awareness, training and education

- **Awareness:** changes attention and behaviour for everyone, for example posters and phishing simulations.
- **Training:** teaches a skill for a job, for example secure coding for developers.
- **Education:** builds deep understanding over time, for example a degree or certification.

Measure outcomes, not attendance: phishing click and report rates over time, incidents reported, policy violations found.

## How the questions look

Most Domain 1 items are short scenarios written from the point of view of a security manager or adviser. You are asked what you should do FIRST, which option is BEST, or what is MOST important. Several options are often technically true. The right one is the one a senior security professional would choose for the business: it starts from risk and management direction, keeps people safe, and follows law and policy.

Some items are calculations (SLE, ALE, safeguard value) or ask which term fits a situation (due care or due diligence, transfer or acceptance). The arithmetic is simple; the trap is the unit, such as an ARO of "once every five years" being 0.2.

## A method that works

1. **Find the role and the stage.** Are you the CISO, a consultant, an employee? Is the organisation planning, building, running or recovering? The stage often decides what comes first.
2. **Find the asset and the business goal.** What is at stake: people, money, data, reputation, legal standing?
3. **Look for life safety.** If any option protects people, it usually wins.
4. **Prefer process before product.** Policy, risk assessment and management approval come before buying tools.
5. **Check who should decide.** Owners classify and accept risk; senior management approves policy and funds; you advise.
6. **Run the numbers if there are any.** Write AV, EF, SLE, ARO, ALE on your scratch area before looking at the options.
7. **Eliminate options that are true but out of scope.** A good control that does not address the stated problem is wrong.

## Traps that cost points

- **Fixing it yourself.** The CISSP wants you to advise, escalate and follow process. "Immediately reconfigure the firewall" is rarely right when the question is about governance.
- **Treating ignoring as acceptance.** Acceptance needs a documented decision by someone with authority.
- **Thinking you can transfer accountability.** Insurance moves cost, not ownership.
- **Mixing up RTO and RPO.** RTO is about time to restore; RPO is about how much data you can lose.
- **Getting ARO wrong.** "Once every eight years" is 0.125, not 8.
- **Picking a technical control before a BIA or risk assessment.** You cannot justify a control without knowing the risk.
- **Using HMAC or symmetric keys for nonrepudiation.** Only a private key held by one party gives nonrepudiation.
- **Reading the ethics canons as equal.** They are in order. Society first.
- **Confusing guidelines with standards.** Guidelines are optional; standards are mandatory.

## Timing

Across the exam you have 3 hours for up to 150 items, an average of 72 seconds each. As guidance, Domain 1 scenario items should take about 60 seconds, calculation items up to 90. If you find yourself on a second reread, choose the option that best fits "risk-based, management-supported, people first" and move on: you cannot go back on the CISSP.

## Practice items

These 2 items are original, written for these notes. They are not taken from ISC2 or any prep provider. Choose one answer for each.

**Item 1.** You are a security engineer at a medical device maker. You find that a shipping infusion pump can be made to deliver the wrong dose over its wireless interface. Your manager tells you to keep it quiet until next year's model ships. Which ISC2 canon should guide your response above the others?

- A. Provide diligent and competent service to principals
- B. Protect society, the common good, necessary public trust and confidence, and the infrastructure
- C. Advance and protect the profession
- D. Act honorably, honestly, justly, responsibly, and legally

**Item 2.** A risk has an ALE of 30,000 with no control. A proposed control would reduce the ALE to 12,000 and costs 21,000 a year to run. What is the annual value of the control?

- A. 18,000 saved
- B. 9,000 saved
- C. 3,000 saved
- D. A loss of 3,000

<details>
<summary>Answers and explanations, items 1 and 2</summary>

**Item 1: B.** A device that can harm patients is a threat to public safety, which falls under the first canon. The canons are applied in order, so protecting society comes before serving your employer. *Why not A:* serving principals is the third canon and gives way when it conflicts with the first. *Why not D:* acting honestly also applies, but the question asks which canon takes precedence, and canon 1 sits above it.

**Item 2: D.** Value = ALE before (30,000) minus ALE after (12,000) minus annual cost (21,000) = negative 3,000. The control costs more than the loss it prevents. *Why not A:* 18,000 is the reduction in ALE, before the control's own cost is subtracted. *Why not C:* the sign is reversed.

</details>

Want more? The [free timed CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp) has 25 questions across all eight domains, scored by domain.

## Score yourself

| Item | 1 | 2 |
|---|---|---|
| Answer | B | D |

- **2:** strong. Keep this domain warm with mixed sets and spend your time on weaker domains.
- **1:** look at the type of miss. Calculation slips mean drilling ARO and the safeguard formula. Judgement misses mean rereading the method, steps 3 to 5.
- **0:** reread Key concepts slowly, then explain the risk formulas, the BIA terms and the canon order out loud without notes before trying again.

## Next step

Domain 1 judgement is easier to train against a clock. Try a timed mixed set with the [free CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp), then come back to the traps list for anything you missed.

## Sources for this page

- [ISC2 CISSP Certification Exam Outline](https://www.isc2.org/certifications/cissp/cissp-certification-exam-outline), for the subdomains, weight and AI notes
- [ISC2 Code of Ethics](https://www.isc2.org/Ethics), for the canons

---

<!-- nav:bottom -->← Previous: [5-minute diagnostic](../diagnostic.md) | Next: [Domain 2: Asset Security](asset-security.md) → | [Back to contents](../../README.md#contents)<!-- /nav:bottom -->
