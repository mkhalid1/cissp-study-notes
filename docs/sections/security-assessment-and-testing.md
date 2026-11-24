<!-- nav:top -->[Contents](../../README.md#contents) · Previous: [Domain 5: Identity and Access Management](identity-and-access-management.md) · Next: [Domain 7: Security Operations](security-operations.md)<!-- /nav:top -->

# Domain 6: Security Assessment and Testing

**In one line:** proving that controls actually work: planning assessments and audits, choosing the right test, collecting evidence and reporting it so problems get fixed.

ISC2 gives this domain an average weight of **12%**. It sits between design and operations: Domains 3 to 5 build controls, Domain 7 runs them, and this domain checks them. Questions test whether you can match a goal to the right kind of test and whether you know what each kind of report can and cannot tell you.

## What it covers

| Subdomain (official title) | What you need to be able to do |
|---|---|
| 6.1 Design and validate assessment, test, and audit strategies | Plan internal, external and third-party assessments across on-premises, cloud and hybrid locations. |
| 6.2 Conduct security control testing | Vulnerability assessment; penetration testing with red, blue and purple teams; log reviews; synthetic transactions and benchmarks; code review and testing; misuse case testing; coverage analysis; interface testing (user, network, API); breach attack simulations; compliance checks. |
| 6.3 Collect security process data (e.g., technical and administrative) | Account management, management review and approval, key performance and risk indicators, backup verification data, training and awareness, DR and BC data. |
| 6.4 Analyze test output and generate report | Remediation, exception handling and ethical disclosure. |
| 6.5 Conduct or facilitate security audits | Internal, external and third-party audits across locations. |

ISC2 says AI appears here as red teaming of AI systems (testing model robustness against evasion and extraction attacks and logic flaws in outputs) and as AI-assisted vulnerability management that prioritises fixes using threat intelligence.

## Key concepts

### Assessment, test and audit

- **Test:** checks a specific control, for example a scan of one subnet.
- **Assessment:** a broader review of a system or programme, often combining tests, interviews and document review, to judge risk.
- **Audit:** a formal, independent evaluation against a standard or criteria, producing an opinion or findings for management, regulators or customers.

| Who performs it | Meaning in the outline |
|---|---|
| Internal | Staff within the organisation's control, such as an internal audit function |
| External | People outside the organisation's control, for example an outside audit firm engaged by you |
| Third-party | Outside the enterprise's control altogether, for example an independent auditor whose report you rely on about a supplier |

Independence matters most: whoever tests a control should not be the person who built or runs it.

### Vulnerability assessment and penetration testing

| | Vulnerability assessment | Penetration test |
|---|---|---|
| Goal | Find and rank known weaknesses broadly | Show whether weaknesses can be exploited to reach a goal |
| Method | Mostly automated scanning, then validation | Manual and tool-assisted attack, chaining weaknesses |
| Risk to systems | Low | Higher; needs careful rules of engagement |
| Output | List of vulnerabilities with severity, for example CVSS scores | Narrative of attack paths, impact and fixes |

**Credentialed** scans log in and see far more than **non-credentialed** scans, which show what an outsider sees. Always validate findings: scanners produce false positives.

A penetration test starts with **written authorisation** from someone with authority over the systems, plus agreed scope and rules of engagement. Then: reconnaissance, scanning and enumeration, exploitation, post-exploitation (privilege escalation, lateral movement), and reporting. Clean up anything the testers installed.

| Knowledge level | Testers know | Defenders know |
|---|---|---|
| Zero knowledge (black box) | Nothing beyond the target name | Varies |
| Partial knowledge (grey box) | Some details, such as an account or a diagram | Varies |
| Full knowledge (white box) | Everything, including source and architecture | Varies |
| Blind | Little about the target | The defenders are told a test is happening |
| Double-blind | Little about the target | The defenders are **not** told, which tests detection and response too |

**Red team** attacks, **blue team** defends, **purple team** is the two working together to improve detection, sharing what worked. **Breach and attack simulation** tools run automated, repeatable attack scenarios against your controls continuously.

### Other control testing techniques

| Technique | What it does | Good for |
|---|---|---|
| Log review | Examine logs for anomalies and policy violations | Detecting misuse, checking logging works |
| Synthetic transactions | Scripted transactions run on a schedule | Availability and performance monitoring before users notice |
| Real user monitoring | Measures actual users' sessions passively | Seeing real experience, but only after users are affected |
| Code review | Manual review by peers, or formal inspection such as Fagan inspection | Logic flaws tools miss |
| Static testing (SAST) | Analyse source without running it | Early, broad coverage of coding flaws |
| Dynamic testing (DAST) | Test the running application | Runtime and configuration issues |
| Fuzzing | Send malformed or random input; mutation fuzzing alters valid inputs, generation fuzzing builds inputs from a model of the format | Crashes, input handling flaws |
| Misuse case testing | Test scenarios written from an attacker's point of view | Business logic abuse |
| Coverage analysis | Measure how much code or how many requirements tests exercise | Judging whether testing is complete |
| Interface testing | Test user interfaces, network interfaces and APIs, including error handling between components | Integration points |
| Compliance checks | Compare configuration with a required baseline | Drift from standards |
| Regression testing | Re-run tests after changes | Confirming fixes did not break other things |

### Service organisation reports

| Report | Covers | Audience |
|---|---|---|
| SOC 1 | Controls relevant to the customer's **financial reporting** | Customers' financial auditors |
| SOC 2 | Controls relevant to security, availability, processing integrity, confidentiality and privacy | Customers and their auditors, under NDA |
| SOC 3 | Same areas as SOC 2, as a short general-use summary | Anyone, often published |
| Type I | Design of controls **at a point in time** | |
| Type II | Design **and operating effectiveness over a period**, typically several months to a year | |

When a question asks whether controls **worked over time**, the answer is a Type II report.

### Security process data

Measure the programme as well as the technology:

- **Account management:** orphaned accounts, time to deprovision leavers, access review completion.
- **Management review and approval:** evidence that leaders review and sign off risk.
- **Key performance indicators (KPIs)** show how well a process performs, for example the percentage of critical patches applied within the target time. **Key risk indicators (KRIs)** warn that risk is rising, for example the number of internet-facing systems with known critical vulnerabilities.
- **Backup verification:** job success logs show a backup ran; only **test restores** show you can recover.
- **Training and awareness:** completion, plus behaviour measures.
- **DR and BC:** test results, plan update dates, gaps found.

### Reporting, remediation and exceptions

A good report states findings, evidence, risk rating, and recommended fixes, written for its audience: technical detail for owners, risk summary for management. Then:

- **Remediation:** owners fix findings by agreed dates, and retesting confirms the fix.
- **Exception handling:** when a finding cannot be fixed in time, record a formal exception with the business reason, compensating controls, the owner's acceptance, and an expiry or review date.
- **Ethical disclosure:** when you find a flaw in someone else's product, report it privately to the vendor first and allow reasonable time for a fix before any public disclosure (coordinated or responsible disclosure).

## How the questions look

Typical items describe a goal ("prove controls operated all year", "find out if an attacker could reach payroll", "check the API rejects bad tokens") and ask which test, report or metric fits BEST. Others ask what must happen FIRST before testing, or what to do when a finding cannot be fixed. Watch for words that decide the answer: "over a period", "exploit", "without telling the SOC", "at a point in time".

## A method that works

1. **Name the question the test must answer.** Is there a weakness? Can it be exploited? Did the control work for a year? Is the system available?
2. **Match the depth.** Breadth (scan), depth (pentest), proof over time (Type II audit), behaviour (log review, metrics).
3. **Check authorisation and scope.** Any active test needs written approval first.
4. **Check independence.** The tester should not be the builder or operator.
5. **Ask who will read the result.** Management needs risk; owners need fixes; customers need assurance reports.
6. **Follow through.** Findings lead to remediation and retesting, or to a documented exception.

## Traps that cost points

- **Calling a scan a penetration test.** Scans find; pentests exploit.
- **Starting a test without written authorisation.** Verbal approval or a technician's go-ahead is not enough.
- **Choosing Type I when the question says "over a period".** Type II covers operating effectiveness over time.
- **Using SOC 1 for security assurance.** SOC 1 is about financial reporting controls.
- **Treating backup success logs as proof of recovery.** Only restores prove it.
- **Letting the operations team audit its own controls.** That lacks independence.
- **Ignoring a finding because it cannot be fixed now.** Record an exception with compensating controls and an expiry.
- **Publishing a vendor's flaw immediately.** Coordinate with the vendor first.
- **Confusing blind and double-blind.** Double-blind means defenders are not told either.

## Timing

As guidance, Domain 6 items take about 50 to 70 seconds. Most turn on one decisive word in the stem, so read the stem fully before the options and underline it mentally.

## Practice items

These 12 items are original, written for these notes. They are not taken from ISC2 or any prep provider.

### Set 1

**Item 1.** The board wants to know whether an outside attacker could actually reach customer card data by chaining weaknesses in the company's systems. Which activity answers this BEST?

- A. A credentialed vulnerability scan
- B. A penetration test with that objective
- C. A review of firewall logs
- D. A configuration compliance check

**Item 2.** A penetration testing firm has been chosen. What is MOST important before testing begins?

- A. Written authorisation from management that defines scope and rules of engagement
- B. A full list of the scanning and exploitation tools the testers plan to use
- C. A copy of the latest vulnerability scan results
- D. Notifying all staff in advance that a penetration test will take place that week

**Item 3.** A customer's auditor needs evidence that a cloud provider's security controls operated effectively throughout the last twelve months. Which report fits BEST?

- A. SOC 1 Type I
- B. SOC 2 Type I
- C. SOC 2 Type II
- D. SOC 3

**Item 4.** Every five minutes, a script logs in to the online shop from several regions, adds an item to the basket and checks out with a test card. Alerts fire if any step fails or slows down. What is this?

- A. Real user monitoring
- B. Fuzz testing
- C. Misuse case testing
- D. Synthetic transaction monitoring

<details>
<summary>Answers and explanations, items 1 to 4</summary>

**Item 1: B.** Whether weaknesses can be exploited and chained to reach a target is what a penetration test is designed to show. *Why not A:* a scan lists weaknesses but does not show whether they can be exploited together to reach the data. *Why not D:* a compliance check compares configuration with a baseline.

**Item 2: A.** Written authorisation from someone with authority, with an agreed scope and rules of engagement, protects both parties and the systems. Without it, testing may be illegal. *Why not D:* telling all staff can be wrong when detection is part of the test, and it is not the most important step. *Why not C:* earlier results are helpful, but not essential.

**Item 3: C.** SOC 2 covers security and related criteria, and Type II tests operating effectiveness over a period. *Why not B:* Type I covers design at a single point in time. *Why not D:* SOC 3 is a short general-use summary without the detailed testing an auditor needs.

**Item 4: D.** Scripted transactions run on a schedule to check availability and performance are synthetic transactions. *Why not A:* real user monitoring measures actual customers, so problems are found only after users meet them. *Why not B:* fuzzing sends malformed input to find crashes; this script sends valid transactions.

</details>

### Set 2

**Item 5.** A tester sends thousands of malformed and random inputs to a file parser to see whether it crashes or behaves unexpectedly. What technique is this?

- A. Static application security testing
- B. Fuzz testing
- C. Regression testing
- D. Synthetic transaction monitoring

**Item 6.** Testers write scenarios describing how a dishonest customer might abuse a funds-transfer feature, such as entering negative amounts or replaying a request, and then test each scenario. What is this?

- A. Coverage analysis
- B. Interface testing
- C. Misuse case testing
- D. Compliance checking

**Item 7.** A development manager asks what share of the application's code paths the test suite actually exercises. Which technique answers this?

- A. Coverage analysis
- B. Fuzz testing
- C. Log review
- D. Breach and attack simulation

**Item 8.** A team tests that a payment API rejects requests without a valid token, returns safe error messages, and handles malformed responses from the fraud-check service it calls. What kind of testing is this?

- A. Synthetic transaction monitoring
- B. Static code analysis
- C. Real user monitoring
- D. Interface testing

<details>
<summary>Answers and explanations, items 5 to 8</summary>

**Item 5: B.** Feeding malformed or random input to find crashes and unexpected behaviour is fuzzing. *Why not A:* SAST analyses source code without running it. *Why not C:* regression testing re-runs existing tests after a change.

**Item 6: C.** Tests built from an attacker's or abuser's point of view are misuse case tests. *Why not B:* interface testing checks how components and interfaces handle input and errors in general, not abuse scenarios written from the attacker's view. *Why not A:* coverage analysis measures how much code tests exercise.

**Item 7: A.** Coverage analysis measures how much of the code, or how many requirements, the tests exercise. *Why not B:* fuzzing finds input-handling flaws; it does not report coverage of the test suite. *Why not D:* breach and attack simulation tests security controls against attack scenarios.

**Item 8: D.** Checking how an API handles authentication, errors and responses from the services it depends on is interface testing. *Why not B:* static analysis reads code without exercising the interface. *Why not A:* synthetic transactions check availability and performance with valid scripted actions.

</details>

### Set 3

**Item 9.** Both sides have limited knowledge: the testers receive only the company's name, and the security operations centre is not told that a test is under way. What kind of test is this?

- A. Blind
- B. Double-blind
- C. Full knowledge
- D. Partial knowledge

**Item 10.** Backup jobs have reported "success" every night for a year. What is the MOST reliable evidence that data can actually be recovered?

- A. The nightly success messages in the backup logs
- B. The growth in backup storage used over the year
- C. Results of periodic test restores of real data
- D. The backup vendor's assurance letter

**Item 11.** During an authorised test of your own network, a tester discovers a serious flaw in a commercial product that many other organisations also use. What is the BEST next step?

- A. Report it privately to the vendor and allow reasonable time for a fix before any public disclosure
- B. Publish full technical details at once so that other organisations can protect themselves quickly
- C. Keep it confidential indefinitely to avoid helping attackers
- D. Post it to an anonymous forum to warn the community without legal risk

**Item 12.** An audit finding requires replacing an old system, but the replacement cannot be live for six months. What is the BEST way to handle the finding in the meantime?

- A. Close the finding, since a replacement is already planned
- B. Ask the auditors to remove the finding from the report
- C. Leave the finding open in the report with no further action until the replacement system goes live
- D. Record a formal exception with compensating controls, the owner's risk acceptance and an expiry date

<details>
<summary>Answers and explanations, items 9 to 12</summary>

**Item 9: B.** In a double-blind test the testers have little information and the defenders are not told, so detection and response are tested too. *Why not A:* in a blind test the testers have little information, but the defenders know the test is happening. *Why not D:* partial knowledge means the testers get some details beyond the name.

**Item 10: C.** Only a restore proves that backups are complete and usable. *Why not A:* a success message shows the job ran, not that the data can be restored. *Why not D:* a vendor letter is not evidence about your own backups.

**Item 11: A.** Coordinated disclosure gives the vendor a chance to fix the flaw before attackers learn of it, which protects every customer. *Why not B:* immediate publication hands attackers the flaw before a fix exists. *Why not C:* permanent silence leaves every customer exposed and the vendor unaware.

**Item 12: D.** An exception keeps the risk visible, reduces it with compensating controls, records who accepted it and forces a review. *Why not A:* planning a fix does not reduce today's risk. *Why not C:* leaving it open without compensating controls or ownership is ignoring the risk.

</details>

## Score yourself

| Item | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Answer | B | A | C | D | B | C | A | D | B | C | A | D |

- **11 to 12:** strong. Keep this domain fresh with mixed sets.
- **8 to 10:** check which decisive words you skipped, such as "over a period" or "not told".
- **7 or fewer:** relearn the testing techniques table and the SOC report table, then redo the items.

## Next step

Try these distinctions under time pressure with the [free CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp), then return to the traps list for any you missed.

## Sources for this page

- [ISC2 CISSP Certification Exam Outline](https://www.isc2.org/certifications/cissp/cissp-certification-exam-outline), for the subdomains, weight and AI notes

---

<!-- nav:bottom -->← Previous: [Domain 5: Identity and Access Management](identity-and-access-management.md) | Next: [Domain 7: Security Operations](security-operations.md) → | [Back to contents](../../README.md#contents)<!-- /nav:bottom -->
