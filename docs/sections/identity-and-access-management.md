<!-- nav:top -->[Contents](../../README.md#contents) · Previous: [Domain 4: Communication and Network Security](communication-and-network-security.md) · Next: [Domain 6: Security Assessment and Testing](security-assessment-and-testing.md)<!-- /nav:top -->

# Domain 5: Identity and Access Management

**In one line:** proving who or what is asking, deciding what they may do, and keeping that access right from the day an account is created to the day it is removed.

ISC2 gives this domain an average weight of **13%**. It covers people, devices and services alike, and ISC2 now treats identity as the main perimeter. Much of the domain is about the lifecycle: most real breaches involve access that was too broad, never reviewed or never removed.

## What it covers

| Subdomain (official title) | What you need to be able to do |
|---|---|
| 5.1 Control physical and logical access to assets | Apply access control to information, systems, devices, facilities, applications and services. |
| 5.2 Design identification and authentication strategy (e.g., people, devices, and services) | Groups and roles; AAA with MFA and password-less methods; session management; registration, proofing and establishment of identity; federated identity; credential management such as password vaults; single sign-on; just-in-time access. |
| 5.3 Federated identity with a third-party service | On-premise, cloud and hybrid federation. |
| 5.4 Implement and manage authorization mechanisms | RBAC, rule-based, MAC, DAC, ABAC, risk-based access control, and policy decision and enforcement points. |
| 5.5 Manage the identity and access provisioning lifecycle | Access reviews for user, system and service accounts; provisioning and deprovisioning for joiners, movers and leavers; role transitions; privilege escalation such as sudo and auditing its use; service account management. |
| 5.6 Implement authentication systems | Choose and run the systems that authenticate users and services. |

ISC2 says AI enters this domain through managing non-human identities such as AI agents and automated service accounts under least privilege, and through using AI for behavioural biometrics and adaptive authentication.

## Key concepts

### Identification, authentication, authorisation, accounting

- **Identification:** claiming an identity, such as a username.
- **Authentication:** proving it.
- **Authorisation:** deciding what the authenticated identity may do.
- **Accounting (or auditing):** recording what it did, so actions can be traced. Accountability needs unique IDs: shared accounts destroy it.

### Authentication factors

| Factor | Examples |
|---|---|
| Something you know | Password, PIN, answers to security questions |
| Something you have | Smart card, hardware token, phone authenticator app, passkey on a device |
| Something you are | Fingerprint, face, iris, voice |
| Context (sometimes added) | Location, time, device health, behaviour |

**Multi-factor** means factors of **different types**. A password plus a PIN is still one factor. Password-less methods such as FIDO2 passkeys use a private key held on the user's device, unlocked locally with a biometric or PIN, and resist phishing because the key is tied to the real site.

### Biometric accuracy

| Measure | Meaning | Also called |
|---|---|---|
| False rejection rate (FRR) | Legitimate users wrongly refused | Type I error |
| False acceptance rate (FAR) | Impostors wrongly accepted | Type II error |
| Crossover error rate (CER) | The setting where FAR equals FRR | Equal error rate |

A **lower CER means a more accurate system**, so CER is the measure for comparing products. For high-security areas, tune for a low FAR and accept more false rejections. Also consider enrolment time, throughput and user acceptance.

### Access control models

| Model | Who decides | Example |
|---|---|---|
| Discretionary (DAC) | The owner of the object | File owner shares a folder with colleagues |
| Mandatory (MAC) | The system, using labels and clearances set by policy | Classified systems with Secret and Top Secret labels |
| Role-based (RBAC) | Access follows job roles | "Accounts payable clerk" role gets the payment entry screen |
| Rule-based | Global rules applied to everyone | Firewall rules; no logins after 22:00 |
| Attribute-based (ABAC) | Policies combining attributes of user, resource, action and environment | Allow if department = Finance, device is managed and time is business hours |
| Risk-based | A risk score computed per request | Step up to MFA when login comes from a new country |

**Policy decision point (PDP):** evaluates the request against policy and decides. **Policy enforcement point (PEP):** sits in the path and carries out the decision, allowing or blocking. In zero trust designs every request passes through a PEP that asks a PDP.

### Single sign-on and federation

| Protocol | Role | Typical use |
|---|---|---|
| Kerberos | Ticket-based SSO inside an enterprise domain | Windows domains. A Key Distribution Center issues a ticket-granting ticket, then service tickets. Depends on synchronised clocks. |
| SAML 2.0 | XML assertions from an identity provider (IdP) to a service provider (SP) | Enterprise web SSO to SaaS applications |
| OAuth 2.0 | Delegated **authorisation**: an app gets a token to access an API on a user's behalf | "Let this app read my calendar" without sharing the password |
| OpenID Connect | An **authentication** layer on top of OAuth 2.0, returning an ID token | "Sign in with" buttons, modern web and mobile SSO |
| LDAP | Directory queries | Looking up users and groups; use LDAPS |
| RADIUS | Network access AAA | VPN and Wi-Fi authentication; UDP; encrypts only the password |
| TACACS+ | Device administration AAA | Router and switch admin logins; TCP; encrypts the whole payload and separates authentication, authorisation and accounting |

Federation lets one organisation trust identities from another. It can be on-premise, cloud or hybrid, for example an on-premise directory synchronised to a cloud identity provider.

### Identity proofing and the lifecycle

1. **Registration and proofing:** verify the person is who they claim before issuing credentials, in proportion to the access requested.
2. **Provisioning:** create accounts with access based on role, approved by the owner.
3. **Movers:** when someone changes role, add the new access **and remove the old**. Failing to remove it causes **privilege creep**.
4. **Reviews:** managers and data owners recertify access periodically, including system and service accounts.
5. **Deprovisioning:** disable access promptly when someone leaves, and immediately, at or before notification, for a hostile departure.

### Privileged and service accounts

- **Just-in-time (JIT) access:** privileges granted for a short window when needed, with approval, then removed. No standing admin rights.
- **Privileged access management (PAM):** vaults privileged credentials, brokers sessions, records them and rotates passwords.
- **sudo and elevation:** let users run specific commands with higher rights, and log every use.
- **Service accounts:** non-human, often highly privileged and forgotten. Give each an owner, least privilege, no interactive login, managed or rotated credentials, and regular review.
- **Password vaults** store and generate strong unique passwords for people and shared admin credentials.

### Session management

Expire idle and long sessions, regenerate the session identifier after login, bind sessions to secure, HTTP-only cookies over TLS, and offer a real logout that ends the session on the server.

## How the questions look

Most IAM items describe an access problem and ask for the BEST model, protocol or process. Expect items on true multi-factor combinations, biometric error rates, picking SAML, OAuth or OpenID Connect for a scenario, and lifecycle failures such as privilege creep or orphaned accounts. Management-style items ask what to do FIRST when access goes wrong.

## A method that works

1. **Separate the four steps.** Is the question about identification, authentication, authorisation or accounting?
2. **Name the subject.** A person, a device, a service account, an AI agent? Non-human identities need owners and least privilege too.
3. **For factors, count types, not items.** Two things you know is still one factor.
4. **For protocols, ask: authentication or authorisation, enterprise or web?** That separates Kerberos, SAML, OAuth and OpenID Connect quickly.
5. **For models, ask who decides.** The owner (DAC), the system by labels (MAC), the role (RBAC) or a policy on attributes (ABAC).
6. **For lifecycle problems, fix the process,** then the instance: reviews and mover procedures, then the one account.

## Traps that cost points

- **Counting a password and a PIN as two factors.** Same type, one factor.
- **Comparing biometrics on FAR or FRR alone.** Use CER for overall accuracy.
- **Using OAuth as if it authenticated users.** OAuth delegates access; OpenID Connect adds authentication.
- **Calling MAC a model where owners decide.** That is DAC.
- **Adding access on a role change without removing the old.** That is privilege creep.
- **Leaving service accounts ownerless.** They are prime targets.
- **Disabling a hostile leaver's account after the meeting.** Do it at or before notification.
- **Forgetting Kerberos needs synchronised time.** Clock skew breaks authentication.
- **Choosing RADIUS when the question wants full encryption of admin sessions.** TACACS+ encrypts the whole payload.

## Timing

IAM items are usually short. As guidance, 45 to 60 seconds each, slightly longer for lifecycle scenarios with several reasonable steps. For FIRST questions, pick the step that stops the exposure soonest without skipping authorisation.

## Practice items

These 12 items are original, written for these notes. They are not taken from ISC2 or any prep provider.

### Set 1

**Item 1.** Which login combination is true multi-factor authentication?

- A. A password and a PIN
- B. A password and a fingerprint
- C. A smart card and a building badge
- D. A password and the answer to a security question

**Item 2.** A security team is comparing two fingerprint systems for overall accuracy. Which single measure is BEST for the comparison?

- A. False acceptance rate
- B. False rejection rate
- C. Crossover error rate
- D. Enrolment time

**Item 3.** A biometric reader guards a bank's cash vault. Which error should the settings minimise above all?

- A. False rejection rate
- B. Crossover error rate
- C. Enrolment failure rate
- D. False acceptance rate

**Item 4.** A defence contractor's system assigns sensitivity labels to every file and clearances to every user. Users cannot change labels or grant access to others, and the system enforces access by comparing labels with clearances. Which model is this?

- A. Discretionary access control
- B. Role-based access control
- C. Attribute-based access control
- D. Mandatory access control

<details>
<summary>Answers and explanations, items 1 to 4</summary>

**Item 1: B.** A password is something you know and a fingerprint is something you are: two different factor types. *Why not A:* a password and a PIN are both something you know. *Why not C:* a smart card and a badge are both something you have.

**Item 2: C.** The crossover error rate is where FAR and FRR are equal. A lower CER means better overall accuracy, so it is the fair comparison. *Why not A:* FAR alone can be lowered by tuning, at the cost of a higher FRR, so it does not compare systems fairly. *Why not B:* the same applies to FRR.

**Item 3: D.** For a vault, letting an impostor in is far worse than turning away a legitimate user, so the false acceptance rate must be kept low. *Why not A:* false rejections are an inconvenience; staff can retry or use a backup procedure. *Why not B:* CER is a comparison measure for choosing a system, not a setting to minimise for a high-security use.

**Item 4: D.** System-enforced access based on labels and clearances, with no owner discretion, is mandatory access control. *Why not A:* in DAC the owner decides who gets access. *Why not C:* ABAC evaluates flexible combinations of attributes; this system uses fixed labels and clearances set by policy.

</details>

### Set 2

**Item 5.** A policy allows access to payroll reports only if the user is in the Finance department, is on a company-managed device, and connects during business hours. Which model is this?

- A. Attribute-based access control
- B. Discretionary access control
- C. Mandatory access control
- D. Role-based access control

**Item 6.** A mobile app needs permission to read a user's calendar from a separate online service, without ever seeing the user's password for that service. Which protocol is designed for this?

- A. SAML 2.0
- B. OAuth 2.0
- C. Kerberos
- D. LDAP

**Item 7.** An internal audit finds that an employee who has worked in sales, then marketing, then finance still holds access from all three roles. Which control BEST prevents this in future?

- A. Requiring longer passwords for all users
- B. Enabling multi-factor authentication on all finance applications for every user
- C. Removing old access at each role change and having managers recertify access periodically
- D. Logging all access to finance applications and reviewing the logs when an incident occurs

**Item 8.** A system administrator is being dismissed for misconduct. When should their access be disabled?

- A. At the same time as, or just before, they are told of the dismissal
- B. At the end of the working day, once the dismissal meeting has finished
- C. After the exit interview is complete and company equipment has been returned
- D. When their final pay is processed

<details>
<summary>Answers and explanations, items 5 to 8</summary>

**Item 5: A.** The decision combines attributes of the user (department), the device (managed) and the environment (time), which is attribute-based access control. *Why not D:* RBAC grants access by role alone and cannot express device or time conditions. *Why not B:* in DAC an owner grants access at their discretion, not through a central attribute policy.

**Item 6: B.** OAuth 2.0 delegates authorisation: the app gets a scoped token to call the calendar API on the user's behalf, without the password. *Why not A:* SAML is mainly used for enterprise web single sign-on between an identity provider and a service provider. *Why not C:* Kerberos is ticket-based SSO inside an enterprise domain.

**Item 7: C.** The cause is privilege creep: access was added at each move and never removed. The fix is the process: remove old access at transfers and recertify regularly. *Why not D:* logging records misuse but does not remove excess access. *Why not B:* MFA strengthens authentication, but the problem is authorisation.

**Item 8: A.** For a hostile departure, access must end at or before notification, so the person cannot retaliate. An administrator's access is especially dangerous. *Why not B:* hours of continued access give time for sabotage or data theft. *Why not C:* the exit interview does not need live system access.

</details>

### Set 3

**Item 9.** Users across a Windows domain suddenly cannot log in. Investigation finds the domain controllers' clocks have drifted well away from the workstations' clocks. Which protocol is MOST likely failing?

- A. RADIUS
- B. Kerberos
- C. TACACS+
- D. SAML

**Item 10.** Several engineers have permanent domain administrator rights that they use a few times a month. Which change BEST reduces this risk?

- A. Require them to change their passwords every 30 days
- B. Move their accounts into a separate organisational unit with stricter group policies
- C. Give them one shared administrator account so that every use can be counted centrally
- D. Grant admin rights just in time, on approved request, for a limited window

**Item 11.** In a zero trust architecture, which component evaluates each access request against policy and decides whether to allow it?

- A. The policy enforcement point
- B. The identity provider
- C. The policy decision point
- D. The SIEM

**Item 12.** A web application's sessions stay valid for weeks and keep the same identifier from before login to after. Which change BEST improves session security?

- A. Expire idle sessions and issue a new session identifier at login
- B. Store the session identifier in the URL so it is easy to track
- C. Extend session lifetime so users log in less often and choose stronger passwords
- D. Encrypt the session identifier with a key stored in the page source

<details>
<summary>Answers and explanations, items 9 to 12</summary>

**Item 9: B.** Kerberos tickets carry timestamps, and authentication fails when clocks differ by more than the allowed skew. *Why not A:* RADIUS is used for network access such as VPN and Wi-Fi and does not depend on this kind of clock agreement. *Why not D:* SAML assertions also carry validity times, but domain logins in a Windows domain use Kerberos.

**Item 10: D.** Just-in-time access removes standing privilege: rights exist only for an approved window, which shrinks the exposure. *Why not A:* frequent password changes do little against the real risk of always-on admin rights. *Why not C:* a shared account destroys individual accountability.

**Item 11: C.** The policy decision point evaluates requests and decides. *Why not A:* the enforcement point carries out the decision in the traffic path. *Why not B:* the identity provider authenticates identities; it is one input to the decision.

**Item 12: A.** Idle expiry limits how long a stolen session is useful, and a new identifier at login prevents session fixation. *Why not B:* identifiers in URLs leak through logs and referrer headers. *Why not D:* a key in the page source is available to anyone, so the encryption adds nothing.

</details>

## Score yourself

| Item | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Answer | B | C | D | D | A | B | C | A | B | D | C | A |

- **11 to 12:** strong. IAM ideas recur in Domains 7 and 8, so this helps elsewhere too.
- **8 to 10:** check whether misses were protocol confusion or lifecycle judgement, and drill that table.
- **7 or fewer:** rebuild the models table and the protocol table from memory, then redo the items.

## Next step

Put IAM against the clock with the [free CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp), then return to the traps list for anything you missed.

## Sources for this page

- [ISC2 CISSP Certification Exam Outline](https://www.isc2.org/certifications/cissp/cissp-certification-exam-outline), for the subdomains, weight and AI notes

---

<!-- nav:bottom -->← Previous: [Domain 4: Communication and Network Security](communication-and-network-security.md) | Next: [Domain 6: Security Assessment and Testing](security-assessment-and-testing.md) → | [Back to contents](../../README.md#contents)<!-- /nav:bottom -->
