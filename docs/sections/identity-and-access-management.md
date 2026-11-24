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

These 2 items are original, written for these notes. They are not taken from ISC2 or any prep provider.

**Item 1.** A biometric reader guards a bank's cash vault. Which error should the settings minimise above all?

- A. False rejection rate
- B. Crossover error rate
- C. Enrolment failure rate
- D. False acceptance rate

**Item 2.** An internal audit finds that an employee who has worked in sales, then marketing, then finance still holds access from all three roles. Which control BEST prevents this in future?

- A. Requiring longer passwords for all users
- B. Enabling multi-factor authentication on all finance applications for every user
- C. Removing old access at each role change and having managers recertify access periodically
- D. Logging all access to finance applications and reviewing the logs when an incident occurs

<details>
<summary>Answers and explanations, items 1 and 2</summary>

**Item 1: D.** For a vault, letting an impostor in is far worse than turning away a legitimate user, so the false acceptance rate must be kept low. *Why not A:* false rejections are an inconvenience; staff can retry or use a backup procedure. *Why not B:* CER is a comparison measure for choosing a system, not a setting to minimise for a high-security use.

**Item 2: C.** The cause is privilege creep: access was added at each move and never removed. The fix is the process: remove old access at transfers and recertify regularly. *Why not D:* logging records misuse but does not remove excess access. *Why not B:* MFA strengthens authentication, but the problem is authorisation.

</details>

Want more? The [free timed CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp) has 25 questions across all eight domains, scored by domain.

## Score yourself

| Item | 1 | 2 |
|---|---|---|
| Answer | D | C |

- **2:** strong. IAM ideas recur in Domains 7 and 8, so this helps elsewhere too.
- **1:** check whether misses were protocol confusion or lifecycle judgement, and drill that table.
- **0:** rebuild the models table and the protocol table from memory, then redo the items.

## Next step

Put IAM against the clock with the [free CISSP practice test on PrepClubs](https://prepclubs.com/free-practice-tests/cissp?utm_source=github&utm_medium=referral&utm_campaign=study-notes&utm_content=cissp), then return to the traps list for anything you missed.

## Sources for this page

- [ISC2 CISSP Certification Exam Outline](https://www.isc2.org/certifications/cissp/cissp-certification-exam-outline), for the subdomains, weight and AI notes

---

<!-- nav:bottom -->← Previous: [Domain 4: Communication and Network Security](communication-and-network-security.md) | Next: [Domain 6: Security Assessment and Testing](security-assessment-and-testing.md) → | [Back to contents](../../README.md#contents)<!-- /nav:bottom -->
