<!-- nav:top -->[Contents](../../README.md#contents) · Previous: [Domain 7: Security Operations](security-operations.md) · Next: [How CISSP scoring works](../scoring.md)<!-- /nav:top -->

# Domain 8: Software Development Security

**In one line:** building security into software from the first requirement to the last patch, and judging the security of software you buy or borrow.

ISC2 gives this domain an average weight of **10%**. You do not need to be a developer to pass it, but you do need to know where security fits in each development model, which testing tool finds which kind of flaw, and how the common coding weaknesses are fixed at their root.

## What it covers

| Subdomain (official title) | What you need to be able to do |
|---|---|
| 8.1 Understand and integrate security in the Software Development Life Cycle (SDLC) | Development methodologies (Agile, Waterfall, DevOps, DevSecOps, Scaled Agile Framework), maturity models (CMM, SAMM), operation and maintenance, change management, Integrated Product Team. |
| 8.2 Identify and apply security controls in software development ecosystems | Programming languages, libraries, tool sets, IDE, runtime, CI/CD, software configuration management, code repositories, and application security testing (SAST, DAST, software composition analysis, IAST). |
| 8.3 Assess the effectiveness of software security | Auditing and logging of changes, risk analysis and mitigation. |
| 8.4 Assess security impact of acquired software | COTS, open source, third-party, managed services such as enterprise applications, and cloud services (SaaS, IaaS, PaaS). |
| 8.5 Define and apply secure coding guidelines and standards | Source-level weaknesses and vulnerabilities, API security, secure coding practices, software-defined security. |

ISC2 says AI enters this domain through AI-assisted coding tools (the risk of insecure or invented code and dependencies), automated AI security testing in CI/CD, and the security of machine learning libraries in the software supply chain.

## Key concepts

### Where security fits in the lifecycle

| Phase | Security activity |
|---|---|
| Requirements | Security and privacy requirements, abuse cases, compliance needs |
| Design | Threat modeling, secure architecture, design review |
| Development | Secure coding standards, peer review, SAST, dependency checks |
| Testing | DAST, IAST, fuzzing, penetration testing, security regression tests |
| Deployment | Hardened configuration, secrets management, signed releases, approval |
| Operations and maintenance | Monitoring, patching, vulnerability management, change management |
| Retirement | Data migration and sanitisation, decommissioning |

The earlier a flaw is found, the cheaper it is to fix. That is the idea behind "shift left".

### Development methodologies

| Model | How it works | Security note |
|---|---|---|
| Waterfall | Sequential phases, each finished before the next | Security requirements set early; late changes are expensive |
| Spiral | Repeated cycles, each with risk analysis | Risk-driven by design |
| Agile (for example Scrum) | Short iterations delivering working software | Add security stories, abuse cases and a definition of done that includes security checks |
| DevOps | Development and operations share ownership, with heavy automation | Fast change needs automated controls |
| DevSecOps | DevOps with security built into the pipeline and shared by everyone | Automated testing in CI/CD, security champions in teams |
| Scaled Agile Framework (SAFe) | Agile coordinated across many teams | Security as a shared, planned capability across trains |

An **Integrated Product Team** brings together people from different disciplines (development, operations, security, business) to own a product together.

### Maturity models

| CMM / CMMI level | Description |
|---|---|
| 1 Initial | Ad hoc, depends on individuals |
| 2 Repeatable (called Managed in CMMI) | Basic project management; success can be repeated on similar projects |
| 3 Defined | Processes documented and standardised across the organisation |
| 4 Managed (called Quantitatively Managed in CMMI) | Processes measured and controlled with data |
| 5 Optimising | Continuous improvement based on measurement |

**OWASP SAMM** (Software Assurance Maturity Model) rates practices across business functions: governance, design, implementation, verification and operations.

### The development ecosystem

- **Languages:** memory-safe and type-safe languages remove whole classes of flaws such as buffer overflows. Compiled code is harder to read but not secret; interpreted code is exposed at runtime.
- **Libraries:** most applications are mostly third-party code. Track every component (a software bill of materials, SBOM) and its known vulnerabilities.
- **Tool sets and IDEs:** plug-ins can flag insecure code as it is written; they are also part of the supply chain and need vetting.
- **Runtime:** keep frameworks and interpreters patched; run with least privilege.
- **CI/CD:** protect the pipeline itself: access control, secrets kept out of code, signed artefacts, mandatory checks before deployment.
- **Software configuration management and code repositories:** version control with branch protection, required reviews, and logging of every change.

### Application security testing

| Tool | How | Finds | When |
|---|---|---|---|
| SAST (static) | Analyses source or binaries without running them | Injection-prone code, unsafe functions, hard-coded secrets | Early: on commit or build |
| DAST (dynamic) | Attacks the running application from outside | Runtime issues, configuration flaws, missing headers | Test or staging environment |
| IAST (interactive) | An agent inside the running application watches code paths during tests | Flaws with the exact line of code, fewer false positives | During functional or QA testing |
| Software composition analysis (SCA) | Inventories third-party components and checks them against vulnerability databases and licences | Vulnerable or risky libraries | Build time and continuously |

### Common weaknesses and their root fixes

| Weakness | Root fix |
|---|---|
| SQL and other injection | Parameterised queries (prepared statements) and safe APIs; validate input on the server |
| Cross-site scripting (XSS) | Context-aware output encoding, input validation, content security policy |
| Cross-site request forgery (CSRF) | Anti-CSRF tokens tied to the session, SameSite cookies, re-authentication for sensitive actions |
| Buffer overflow | Bounds checking, memory-safe languages, compiler and OS protections |
| Race condition (time of check to time of use) | Atomic operations and proper locking |
| Broken access control | Check authorisation on the server for every request, deny by default |
| Insecure deserialisation | Do not deserialise untrusted data, or use safe formats with integrity checks |
| Server-side request forgery | Allow-list destinations, block internal address ranges |
| Hard-coded secrets | Secrets vault, rotation, scanning repositories |
| Verbose errors | Generic messages to users, detailed logs kept internally |

Client-side validation improves usability but provides no security: an attacker bypasses the browser entirely. Validate on the server.

### API security

Authenticate every call (for example with OAuth 2.0 tokens), authorise per object and per function, validate input, limit rates, avoid exposing more data than needed, version and inventory every API, and log access.

### Acquired software

| Type | Main risks | How to assess |
|---|---|---|
| COTS | No source access, vendor patch timing | Vendor security attestations and certifications, independent test results, contract terms for vulnerability handling, your own testing in staging |
| Open source | Unmaintained projects, vulnerable dependencies, licences | SCA, project health, SBOM, internal review |
| Third-party custom | Quality varies | Contractual secure coding requirements, code escrow, right to test |
| Managed services and enterprise applications | You depend on the provider's operations | Assurance reports, SLAs, right to audit |
| Cloud services (SaaS, PaaS, IaaS) | Shared responsibility, configuration | Know your share, review assurance reports, check configuration continuously |

A newer supply chain risk: AI coding assistants sometimes suggest packages that do not exist. Attackers register those names with malicious code. Verify every dependency against an approved source before it is added.

### Secure coding practices

Validate input, encode output, use parameterised queries, apply least privilege, handle errors safely, keep secrets out of code, log security events without logging sensitive data, use vetted cryptographic libraries rather than writing your own, keep dependencies updated, and peer review changes. **Software-defined security** means security controls expressed as code (policy as code, infrastructure as code), versioned and tested like the application.

## How the questions look

Expect scenarios about a development team ("releases daily", "found secrets in the repository", "users' comments run scripts") asking for the BEST control or the right test tool. Some items ask about maturity levels or methodologies. Management-style items ask how to bring security into a fast-moving team without stopping delivery.

## A method that works

1. **Find the phase.** Requirements, design, code, test, deploy, operate or retire. The right control belongs to the earliest phase that can stop the problem.
2. **Fix the root cause, not the symptom.** Parameterised queries beat a WAF for SQL injection.
3. **Match the test tool to the question.** Source without running: SAST. Running app from outside: DAST. Inside during tests: IAST. Third-party components: SCA.
4. **Prefer automation and guardrails in fast teams.** Security in the pipeline beats a gate at the end.
5. **For acquired software, ask what you can see.** No source code means relying on assurance, contracts and your own testing.
6. **Remember people and process.** Separation of duties and change management apply to code too.

## Traps that cost points

- **Relying on client-side validation.** It can be bypassed.
- **Choosing a WAF as the fix for an injection flaw.** It is a compensating control; fix the code.
- **Mixing up SAST and DAST.** Static reads code; dynamic attacks the running app.
- **Thinking deleting a leaked key from the repository is enough.** It remains in history and copies; revoke and rotate it.
- **Writing your own cryptography.** Use vetted libraries.
- **Adding a final security gate to a DevOps pipeline and calling it DevSecOps.** Security must be built in throughout.
- **Confusing CMM level 2 and level 3.** Level 3 is standardised across the organisation.
- **Assuming open source is safe because many people can read it.** Someone has to actually check it.
- **Giving developers direct production access.** It breaks separation of duties and change control.

## Timing

As guidance, Domain 8 items take 45 to 70 seconds. Code-level questions are quick if you know the root fixes; process questions about methodologies and maturity take a little longer.

## Practice items

These 12 items are original, written for these notes. They are not taken from ISC2 or any prep provider.

### Set 1

**Item 1.** A team wants to catch coding flaws such as unsafe string handling on every commit, before the application is even built and run. Which testing approach fits?

- A. Static application security testing
- B. Dynamic application security testing
- C. Interactive application security testing
- D. A penetration test

**Item 2.** A company wants to know which of its applications include an open-source logging library with a newly published critical vulnerability. Which tool answers this BEST?

- A. Dynamic application security testing
- B. A web application firewall
- C. Software composition analysis
- D. Manual code review of each application

**Item 3.** During automated functional testing, an agent running inside the application reports security flaws with the exact line of code involved. What is this?

- A. Static application security testing
- B. Software composition analysis
- C. Dynamic application security testing
- D. Interactive application security testing

**Item 4.** A login form is vulnerable to SQL injection. What is the BEST fix?

- A. Add JavaScript validation in the browser to reject quotes
- B. Rewrite the database calls to use parameterised queries
- C. Place a web application firewall in front of the site
- D. Hide database error messages from users

<details>
<summary>Answers and explanations, items 1 to 4</summary>

**Item 1: A.** SAST analyses source code without running it, so it can run on every commit, early in the pipeline. *Why not B:* DAST needs a running application. *Why not C:* IAST also needs the application running under test.

**Item 2: C.** Software composition analysis inventories third-party components and matches them against known vulnerabilities, across all applications. *Why not D:* manual review of every codebase is slow and error-prone for a question SCA answers directly. *Why not A:* DAST tests behaviour from outside and does not reliably list the libraries inside.

**Item 3: D.** IAST uses an agent inside the running application during tests and can point to the exact code involved. *Why not C:* DAST tests from outside and cannot see the code. *Why not A:* SAST does not run the application.

**Item 4: B.** Parameterised queries keep data separate from the SQL command, which removes the root cause. *Why not C:* a WAF is a compensating control that can be bypassed; the flaw stays in the code. *Why not A:* browser-side checks are bypassed by sending requests directly.

</details>

### Set 2

**Item 5.** An organisation's software processes are documented and standardised across all teams, but are not yet managed with quantitative measures. Which CMM level is this?

- A. Initial
- B. Repeatable
- C. Defined
- D. Optimising

**Item 6.** A product team deploys many times a day. A manual security review at the end of each release is causing delays, so teams have started skipping it. What is the BEST approach?

- A. Build automated security tests into the CI/CD pipeline and name a security champion in each team
- B. Remove security reviews to keep delivery fast
- C. Replace the reviews with a penetration test once a quarter
- D. Freeze releases until the security team can manually review every change, however long that takes

**Item 7.** Before buying a commercial application that will process sensitive customer data, you must judge its security. The vendor will not share source code. What is the BEST approach?

- A. Insist on a full copy of the source code and refuse to proceed with the purchase until it is provided
- B. Rely on the vendor's marketing claims about security
- C. Assume it is secure because many other companies use it
- D. Review independent security assessments, set security terms in the contract, and test it yourself in staging

**Item 8.** A developer finds that a cloud API key was committed to a public repository three months ago. What is the MOST important action?

- A. Delete the file containing the key from the repository
- B. Revoke the key and issue a new one, then review its recent use
- C. Make the repository private
- D. Add the file to the repository's ignore list

<details>
<summary>Answers and explanations, items 5 to 8</summary>

**Item 5: C.** Documented, organisation-wide standard processes are the Defined level, level 3. *Why not B:* Repeatable means basic project discipline that can be repeated on similar projects, not organisation-wide standards. *Why not D:* Optimising needs measurement-driven continuous improvement.

**Item 6: A.** DevSecOps moves security into the pipeline as automated checks, with champions in each team, so security keeps pace with delivery. *Why not C:* a quarterly test leaves months of releases unchecked. *Why not D:* freezing releases ignores the business need and will be bypassed again.

**Item 7: D.** Without source code, assurance comes from independent assessments, contractual commitments and your own testing. *Why not A:* COTS vendors rarely share source, and refusing to proceed ignores other ways to gain assurance. *Why not C:* popularity is not evidence of security.

**Item 8: B.** The key has been exposed for months and may already be copied. Revoking it stops misuse; reviewing its use shows whether it was abused. *Why not A:* deleting the file leaves the key in history and in any copies. *Why not C:* making the repository private now does not undo three months of exposure.

</details>

### Set 3

**Item 9.** Comments posted by users on a forum run as scripts in other users' browsers. What is the BEST fix?

- A. Require users to choose stronger passwords and turn on multi-factor authentication
- B. Serve the forum over HTTPS only
- C. Encode user content for the context where it is displayed, and validate input on the server
- D. Add anti-CSRF tokens to the comment form so that forged submissions are rejected

**Item 10.** A logged-in user visits a malicious site, which silently makes their browser submit a funds transfer to the user's bank. Which control BEST prevents this?

- A. Context-aware output encoding
- B. TLS on the bank's website
- C. Input length checks on the transfer form
- D. Anti-CSRF tokens tied to the user's session

**Item 11.** Developers use an AI coding assistant. A review finds it sometimes suggests importing packages that do not exist in the public registry. What is the BEST control?

- A. Ban all third-party packages and write every component in-house from now on
- B. Check every new dependency against an approved source and software composition analysis before it is added
- C. Let the assistant install packages automatically, then remove any that fail to build
- D. Rely on the assistant's own confidence scores

**Item 12.** Which control BEST prevents unauthorised code changes from reaching production?

- A. Required peer review and an approved pipeline that deploys signed builds, with no direct developer access to production
- B. Allowing senior developers to deploy directly to production, provided they note each change afterwards
- C. A monthly review of production server logs by the operations team to spot unexpected changes
- D. Asking developers to describe their changes in the team chat

<details>
<summary>Answers and explanations, items 9 to 12</summary>

**Item 9: C.** This is stored cross-site scripting. Encoding output for its context stops content being run as script, and server-side validation reduces bad input. *Why not D:* CSRF tokens stop forged requests, not scripts embedded in content. *Why not B:* HTTPS protects data in transit; the script still runs.

**Item 10: D.** This is cross-site request forgery. A token tied to the session, which the malicious site cannot know, makes forged requests fail. *Why not A:* output encoding stops XSS, not forged requests. *Why not B:* TLS encrypts the request but the browser still sends it with valid cookies.

**Item 11: B.** Invented package names can be registered by attackers with malicious code, so every dependency must be verified before use. *Why not A:* banning all packages is not proportionate and would stop most development. *Why not C:* automatic installation is exactly how a malicious look-alike package would get in.

**Item 12: A.** Peer review, a controlled pipeline, signed builds and no direct production access enforce separation of duties and change control. *Why not C:* a monthly log review detects changes after the fact and does not prevent them. *Why not B:* direct deployment by individuals bypasses review.

</details>

## Score yourself

| Item | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Answer | A | C | D | B | C | A | D | B | C | D | B | A |

- **11 to 12:** strong. Keep the testing tools table fresh.
- **8 to 10:** check whether misses were about tools, weaknesses or process, and redo that table.
- **7 or fewer:** learn the lifecycle table and the weakness-to-fix table, then redo the items.

## Next step

Mix Domain 8 with the other domains in the [free CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp), then return to the traps list for anything you missed.

## Sources for this page

- [ISC2 CISSP Certification Exam Outline](https://www.isc2.org/certifications/cissp/cissp-certification-exam-outline), for the subdomains, weight and AI notes

---

<!-- nav:bottom -->← Previous: [Domain 7: Security Operations](security-operations.md) | Next: [How CISSP scoring works](../scoring.md) → | [Back to contents](../../README.md#contents)<!-- /nav:bottom -->
