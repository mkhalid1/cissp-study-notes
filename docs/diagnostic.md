<!-- nav:top -->[Contents](../README.md#contents) · Previous: [The CISSP exam explained](test-overview.md) · Next: [Domain 1: Security and Risk Management](sections/security-and-risk-management.md)<!-- /nav:top -->

# 15-minute diagnostic

Twenty-four short, original items, three from each domain, to show you where to start. Most people finish in 15 to 20 minutes. Set a timer for 20 minutes, answer everything without looking anything up, then check each part and read the table at the bottom.

These items are original, written for these notes. They are not taken from ISC2 or any prep provider. They are shorter and more direct than real CISSP items, because the goal here is to find gaps in knowledge quickly. The domain guides have longer, exam-style scenarios.

If you already know your weak areas, skip this and take the [free CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp) for a timed, mixed set instead.

## Part A: Security and Risk Management

**D1.** A loss event is expected once every 20 years. What is its annualised rate of occurrence?

- A. 20
- B. 0.05
- C. 0.2
- D. 2

**D2.** Who is ultimately accountable for information security in an organisation?

- A. The CISO
- B. The IT operations manager
- C. Senior management
- D. Internal audit

**D3.** Buying cyber insurance is an example of which risk response?

- A. Transfer
- B. Avoidance
- C. Acceptance
- D. Mitigation

<details>
<summary>Answers, part A</summary>

**D1: B.** Once every 20 years is 1/20 = 0.05 per year.

**D2: C.** Senior management is accountable. The CISO runs the programme and advises, but accountability stays at the top.

**D3: A.** Insurance transfers the financial impact. Accountability for the risk stays with the organisation.

</details>

## Part B: Asset Security

**D4.** Degaussing reliably sanitises which type of media?

- A. Magnetic hard disk drives
- B. Solid-state drives
- C. Optical discs
- D. USB flash drives

**D5.** Who carries out backups and access settings according to the data owner's decisions?

- A. The data subject
- B. The data custodian
- C. The data controller
- D. The auditor

**D6.** Records being processed in a server's memory are in which data state?

- A. At rest
- B. In transit
- C. In use
- D. Archived

<details>
<summary>Answers, part B</summary>

**D4: A.** Degaussing works on magnetic media only. SSDs, flash and optical media do not store data magnetically.

**D5: B.** The custodian, usually IT, implements the owner's decisions.

**D6: C.** Data being processed in memory is in use.

</details>

## Part C: Security Architecture and Engineering

**D7.** Which provides integrity but not confidentiality?

- A. AES encryption
- B. RSA encryption
- C. A SHA-256 hash
- D. A TLS session

**D8.** To send Bob a message only he can read, you encrypt it with:

- A. your private key.
- B. Bob's public key.
- C. Bob's private key.
- D. your public key.

**D9.** Which model enforces "no read up, no write down"?

- A. Biba
- B. Clark-Wilson
- C. Brewer-Nash
- D. Bell-LaPadula

<details>
<summary>Answers, part C</summary>

**D7: C.** A hash detects changes but does not hide the content.

**D8: B.** Only Bob's private key can decrypt what is encrypted with Bob's public key.

**D9: D.** Bell-LaPadula protects confidentiality with those two rules. Biba is the integrity model with the opposite rules.

</details>

## Part D: Communication and Network Security

**D10.** Which protocol should replace Telnet for remote device administration?

- A. SSH
- B. FTP
- C. SNMPv1
- D. HTTP

**D11.** At which OSI layer do routers mainly operate?

- A. Layer 2
- B. Layer 3
- C. Layer 4
- D. Layer 7

**D12.** Which IPsec protocol provides encryption?

- A. AH
- B. IKE
- C. ESP
- D. GRE

<details>
<summary>Answers, part D</summary>

**D10: A.** SSH encrypts the session, including credentials. Telnet sends them in clear text.

**D11: B.** Routers forward packets by IP address at the network layer.

**D12: C.** ESP encrypts. AH gives integrity and authentication only, and IKE negotiates keys.

</details>

## Part E: Identity and Access Management

**D13.** A smart card used with a fingerprint represents how many different factor types?

- A. One
- B. Two
- C. Three
- D. None

**D14.** In discretionary access control, who decides who may access a file?

- A. The file's owner
- B. The operating system, using labels
- C. The user's job role
- D. A central attribute policy

**D15.** Which control BEST finds accounts belonging to people who have already left?

- A. Longer password requirements
- B. Multi-factor authentication
- C. Single sign-on
- D. Periodic access reviews reconciled against HR records

<details>
<summary>Answers, part E</summary>

**D13: B.** Something you have (the card) and something you are (the fingerprint).

**D14: A.** In DAC the owner decides. Labels are MAC, roles are RBAC, attribute policies are ABAC.

**D15: D.** Reviews that compare accounts with current staff find orphaned accounts. The other options strengthen logins but do not find accounts that should not exist.

</details>

## Part F: Security Assessment and Testing

**D16.** A vulnerability scan that logs in to each system with an account is called:

- A. a credentialed scan.
- B. a non-credentialed scan.
- C. a passive scan.
- D. an external scan.

**D17.** In a security exercise, which team defends?

- A. Red
- B. Blue
- C. Purple
- D. Green

**D18.** Re-running earlier tests after a code change, to check nothing else broke, is:

- A. coverage analysis.
- B. fuzzing.
- C. misuse case testing.
- D. regression testing.

<details>
<summary>Answers, part F</summary>

**D16: A.** A credentialed scan authenticates and sees much more of each system's configuration and patch level.

**D17: B.** Blue defends, red attacks, purple is the two working together.

**D18: D.** Regression testing re-runs tests to confirm changes did not break existing behaviour.

</details>

## Part G: Security Operations

**D19.** A full backup runs on Sunday and incremental backups run Monday to Friday. The server fails on Saturday morning. What do you need to restore it?

- A. Sunday's full backup only
- B. Sunday's full backup and Friday's incremental
- C. Sunday's full backup and all five incrementals
- D. Friday's incremental only

**D20.** Which disaster recovery test shuts down the primary site?

- A. Parallel
- B. Simulation
- C. Tabletop
- D. Full interruption

**D21.** In any disaster, what is the first priority?

- A. The safety of people
- B. Protecting data
- C. Notifying customers
- D. Restoring critical systems

<details>
<summary>Answers, part G</summary>

**D19: C.** Each incremental holds only the changes since the previous backup, so you need the full and every incremental in order.

**D20: D.** A full interruption moves operations to the recovery site by shutting down the primary. It is the most realistic and the riskiest test.

**D21: A.** Life safety always comes first.

</details>

## Part H: Software Development Security

**D22.** Which testing approach analyses code without running it?

- A. DAST
- B. SAST
- C. IAST
- D. Fuzzing

**D23.** What is the main fix for cross-site scripting?

- A. Context-aware output encoding
- B. Parameterised queries
- C. TLS
- D. Anti-CSRF tokens

**D24.** Which CMM level is characterised by continuous process improvement?

- A. Initial
- B. Defined
- C. Managed
- D. Optimising

<details>
<summary>Answers, part H</summary>

**D22: B.** Static testing reads source or binaries without executing them.

**D23: A.** Encoding output for the context where it appears stops user content running as script. Parameterised queries fix SQL injection, and CSRF tokens fix forged requests.

**D24: D.** Level 5, Optimising, is about continuous improvement. Level 4, Managed, is where processes are first controlled by measurement.

</details>

## What your result means

Count your correct answers in each part.

| Part | Your score | If you scored 0 or 1 | If you scored 2 | If you scored 3 |
|---|---|---|---|---|
| A. Security and Risk Management | /3 | Start with [Domain 1](sections/security-and-risk-management.md) | Do its practice items, focus on the risk formulas | Light review only |
| B. Asset Security | /3 | Start with [Domain 2](sections/asset-security.md) | Relearn the roles and sanitisation tables | Light review only |
| C. Architecture and Engineering | /3 | Start with [Domain 3](sections/security-architecture-and-engineering.md) | Drill "who holds which key" and the model rules | Light review only |
| D. Network Security | /3 | Start with [Domain 4](sections/communication-and-network-security.md) | Rebuild the OSI table from memory | Light review only |
| E. Identity and Access | /3 | Start with [Domain 5](sections/identity-and-access-management.md) | Relearn the access models and protocols | Light review only |
| F. Assessment and Testing | /3 | Start with [Domain 6](sections/security-assessment-and-testing.md) | Relearn the testing techniques table | Light review only |
| G. Security Operations | /3 | Start with [Domain 7](sections/security-operations.md) | Relearn the backup, site and DR test tables | Light review only |
| H. Software Development | /3 | Start with [Domain 8](sections/software-development-security.md) | Relearn the testing tools and weakness fixes | Light review only |

A perfect score here does not mean you are ready: these items test recall, and the real exam tests judgement in harder scenarios. Use the result to choose your first two domains, then pick a plan: the [7-day plan](study-plans.md#7-day-plan) for your final week, or the [2-day plan](study-plans.md#2-day-plan) if the exam is close.

---

<!-- nav:bottom -->← Previous: [The CISSP exam explained](test-overview.md) | Next: [Domain 1: Security and Risk Management](sections/security-and-risk-management.md) → | [Back to contents](../README.md#contents)<!-- /nav:bottom -->
