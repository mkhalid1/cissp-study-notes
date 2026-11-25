<!-- nav:top -->
[Contents](../README.md#contents) · Previous: [The CISSP exam explained](test-overview.md) · Next: [Domain 1: Security and Risk Management](sections/security-and-risk-management.md)
<!-- /nav:top -->

# 5-minute diagnostic

Eight short, original items, one from each domain, to show you where to start. Most people finish in 5 to 7 minutes. Set a timer for 7 minutes, answer everything without looking anything up, then check each part and read the table at the bottom.

These items are original, written for these notes. They are not taken from ISC2 or any prep provider. They are shorter and more direct than real CISSP items, because the goal here is to find gaps in knowledge quickly. The domain guides have longer, exam-style scenarios.

If you already know your weak areas, skip this and take the [free CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp) for a timed, mixed set instead.

## Part A: Security and Risk Management

**D1.** A loss event is expected once every 20 years. What is its annualised rate of occurrence?

- A. 20
- B. 0.05
- C. 0.2
- D. 2

<details>
<summary>Answers, part A</summary>

**D1: B.** Once every 20 years is 1/20 = 0.05 per year.

</details>

## Part B: Asset Security

**D2.** Degaussing reliably sanitises which type of media?

- A. Magnetic hard disk drives
- B. Solid-state drives
- C. Optical discs
- D. USB flash drives

<details>
<summary>Answers, part B</summary>

**D2: A.** Degaussing works on magnetic media only. SSDs, flash and optical media do not store data magnetically.

</details>

## Part C: Security Architecture and Engineering

**D3.** To send Bob a message only he can read, you encrypt it with:

- A. your private key.
- B. Bob's public key.
- C. Bob's private key.
- D. your public key.

<details>
<summary>Answers, part C</summary>

**D3: B.** Only Bob's private key can decrypt what is encrypted with Bob's public key.

</details>

## Part D: Communication and Network Security

**D4.** Which protocol should replace Telnet for remote device administration?

- A. SSH
- B. FTP
- C. SNMPv1
- D. HTTP

<details>
<summary>Answers, part D</summary>

**D4: A.** SSH encrypts the session, including credentials. Telnet sends them in clear text.

</details>

## Part E: Identity and Access Management

**D5.** A smart card used with a fingerprint represents how many different factor types?

- A. One
- B. Two
- C. Three
- D. None

<details>
<summary>Answers, part E</summary>

**D5: B.** Something you have (the card) and something you are (the fingerprint).

</details>

## Part F: Security Assessment and Testing

**D6.** A vulnerability scan that logs in to each system with an account is called:

- A. a credentialed scan.
- B. a non-credentialed scan.
- C. a passive scan.
- D. an external scan.

<details>
<summary>Answers, part F</summary>

**D6: A.** A credentialed scan authenticates and sees much more of each system's configuration and patch level.

</details>

## Part G: Security Operations

**D7.** A full backup runs on Sunday and incremental backups run Monday to Friday. The server fails on Saturday morning. What do you need to restore it?

- A. Sunday's full backup only
- B. Sunday's full backup and Friday's incremental
- C. Sunday's full backup and all five incrementals
- D. Friday's incremental only

<details>
<summary>Answers, part G</summary>

**D7: C.** Each incremental holds only the changes since the previous backup, so you need the full and every incremental in order.

</details>

## Part H: Software Development Security

**D8.** What is the main fix for cross-site scripting?

- A. Context-aware output encoding
- B. Parameterised queries
- C. TLS
- D. Anti-CSRF tokens

<details>
<summary>Answers, part H</summary>

**D8: A.** Encoding output for the context where it appears stops user content running as script. Parameterised queries fix SQL injection, and CSRF tokens fix forged requests.

</details>

Want more? The [free timed CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp) has 25 questions across all eight domains, scored by domain.

## What your result means

Count your correct answers in each part.

| Part | Your score | If you scored 0 | If you scored 1 |
|---|---|---|---|
| A. Security and Risk Management | /1 | Start with [Domain 1](sections/security-and-risk-management.md). Do its practice items, focus on the risk formulas | Light review only |
| B. Asset Security | /1 | Start with [Domain 2](sections/asset-security.md). Relearn the roles and sanitisation tables | Light review only |
| C. Architecture and Engineering | /1 | Start with [Domain 3](sections/security-architecture-and-engineering.md). Drill "who holds which key" and the model rules | Light review only |
| D. Network Security | /1 | Start with [Domain 4](sections/communication-and-network-security.md). Rebuild the OSI table from memory | Light review only |
| E. Identity and Access | /1 | Start with [Domain 5](sections/identity-and-access-management.md). Relearn the access models and protocols | Light review only |
| F. Assessment and Testing | /1 | Start with [Domain 6](sections/security-assessment-and-testing.md). Relearn the testing techniques table | Light review only |
| G. Security Operations | /1 | Start with [Domain 7](sections/security-operations.md). Relearn the backup, site and DR test tables | Light review only |
| H. Software Development | /1 | Start with [Domain 8](sections/software-development-security.md). Relearn the testing tools and weakness fixes | Light review only |

A perfect score here does not mean you are ready: these items test recall, and the real exam tests judgement in harder scenarios. Use the result to choose your first two domains, then pick a plan: the [7-day plan](study-plans.md#7-day-plan) for your final week, or the [2-day plan](study-plans.md#2-day-plan) if the exam is close.

---

<!-- nav:bottom -->
← Previous: [The CISSP exam explained](test-overview.md) | Next: [Domain 1: Security and Risk Management](sections/security-and-risk-management.md) → | [Back to contents](../README.md#contents)
<!-- /nav:bottom -->
