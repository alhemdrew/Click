# Moderation, Reporting & Safety Architecture

## 1. Overview

The **Moderation, Reporting & Safety** system is the safety layer of CLICK.

Its purpose is to protect students, manage inappropriate content and behaviour, support moderators, and give the school a controlled way to respond to safety issues.

It should not be designed as:

> Report → Delete

Instead, reporting, protection, detection, moderation, escalation, appeals, and auditing should work together as one safety architecture.

```text
                         CLICK SAFETY
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
     REPORTING            PROTECTION            DETECTION
        │                     │                     │
   Report Post           Block User          Spam Detection
   Report Comment        Mute User           Abuse Detection
   Report User           Privacy              Threat Detection
   Report Group          Controls             Policy Detection
        │                     │                     │
        └─────────────────────┼─────────────────────┘
                              │
                       MODERATION ENGINE
                              │
              ┌───────────────┼────────────────┐
              │               │                │
            REVIEW          ACTIONS         ESCALATION
              │               │                │
          Investigate      Warn/Remove       Serious Cases
          Case History     Restrict          Safeguarding
          Evidence         Suspend           School Admin
              │               │                │
              └───────────────┼────────────────┘
                              │
                         AUDIT & DATA
                              │
              Reports • Actions • Logs • Appeals
```

The key principle is:

> **A report is a signal that starts a safety process, not an automatic punishment.**

---

# 2. Where Moderation Fits in CLICK

Moderation should be integrated with the rest of the Community system rather than built as a completely separate product.

CLICK may contain areas such as:

* Posts
* Comments
* Groups
* Events
* Messaging
* Media
* User profiles
* Notifications

The safety layer sits across these systems.

```text
                           CLICK
                             │
             ┌───────────────┼───────────────┐
             │               │               │
           SOCIAL          GROUPS         MESSAGING
             │               │               │
          Posts           Members         Messages
          Comments        Discussions     Conversations
          Reactions       Events          Media
             │               │               │
             └───────────────┼───────────────┘
                             │
                       SAFETY LAYER
                             │
          ┌──────────────────┼──────────────────┐
          │                  │                  │
      REPORTING          DETECTION          PROTECTION
          │                  │                  │
          └──────────────────┼──────────────────┘
                             │
                      MODERATION ENGINE
```

This allows the same moderation architecture to work across posts, comments, messages, groups, events, and users.

---

# 3. Core Responsibilities

The safety system should primarily provide five capabilities.

## 3.1 Reporting

Users should be able to report problematic content or behaviour.

Examples:

* Report Post
* Report Comment
* Report User
* Report Message
* Report Group
* Report Event
* Report Media

## 3.2 User Protection

Users should have personal safety controls such as:

* Block
* Mute
* Restrict
* Privacy controls
* Message controls

## 3.3 Safety Detection

The platform may identify potentially harmful activity such as:

* Spam
* Harassment
* Bullying
* Threats
* Suspicious links
* Scams
* Impersonation
* Repeated abusive behaviour
* School-policy violations

Automated detection should generally provide **signals for review**, rather than becoming an unquestionable decision-maker.

## 3.4 Moderation

Authorized staff should be able to:

* Review
* Hide
* Remove
* Restore
* Warn
* Restrict
* Suspend
* Escalate

## 3.5 Accountability

The system should maintain records of:

* What was reported
* Who reported it
* What was reviewed
* Who reviewed it
* What decision was made
* What action was taken
* When it happened
* Whether the decision was appealed

---

# 4. Roles and Permissions

CLICK should use role-based access control for moderation.

A possible hierarchy is:

```text
                    SUPER ADMIN
                         │
                    SCHOOL ADMIN
                         │
              ┌──────────┴──────────┐
              │                     │
         SAFETY STAFF           MODERATOR
              │                     │
              └──────────┬──────────┘
                         │
                      STUDENT
```

Not every school needs every role.

A smaller deployment may only require:

```text
Student
   ↓
Moderator
   ↓
School Administrator
```

## Student

Students can:

* Submit reports
* Block users
* Mute users
* Manage available privacy controls
* View their own report status
* Appeal eligible moderation decisions

## Moderator

Moderators can:

* View assigned reports
* Review content
* Review available evidence
* Hide or remove content
* Issue warnings
* Apply restrictions
* Escalate serious cases

## School Administrator

School administrators can:

* Manage moderators
* Review serious cases
* Review moderation records
* Manage school safety policies
* Handle escalated cases
* Review appeals where appropriate

## Super Administrator

Super administrators manage the platform-level configuration and highest-level permissions.

---

# 5. Reporting System

Reporting is the most visible part of the safety architecture.

A user may encounter a menu such as:

```text
Post
 │
 └── ⋯
      │
      ├── Save
      ├── Share
      ├── Report
      └── ...
```

Selecting **Report** could open:

```text
┌─────────────────────────────────────────┐
│ Report Content                           │
├─────────────────────────────────────────┤
│                                         │
│ Why are you reporting this?             │
│                                         │
│ ○ Bullying or harassment                │
│ ○ Threat or dangerous behaviour         │
│ ○ Hate or discrimination                │
│ ○ Inappropriate content                 │
│ ○ Spam                                  │
│ ○ Impersonation                         │
│ ○ School policy violation               │
│ ○ Something else                        │
│                                         │
│ Additional information                  │
│ ┌─────────────────────────────────────┐ │
│ │                                     │ │
│ └─────────────────────────────────────┘ │
│                                         │
│ [+ Attach Screenshot]                   │
│                                         │
│ [Cancel]                 [Submit Report]│
└─────────────────────────────────────────┘
```

Evidence attachments can be useful, but introduce additional considerations around:

* Privacy
* Storage
* Access control
* Retention
* Sensitive media

---

# 6. Report Targets

The reporting system should support different target types.

```text
REPORT
 │
 ├── Post
 ├── Comment
 ├── Message
 ├── User
 ├── Group
 ├── Event
 └── Media
```

Different targets may require different moderation context.

### Reported Post

Potential context:

* Post
* Author
* Community
* Comments
* Attached media

### Reported User

Potential context:

* User profile
* Relevant activity
* Previous moderation cases

### Reported Message

Potential context:

* Sender
* Recipient
* Reported message
* Appropriate conversation context

Moderators should only receive information they are authorized to access.

---

# 7. Report Lifecycle

A typical report lifecycle could be:

```text
User sees content
       │
       ▼
      ⋯
       │
       ▼
     Report
       │
       ▼
 Select reason
       │
       ▼
Add details/evidence
       │
       ▼
 Submit report
       │
       ▼
Create moderation case
       │
       ▼
Moderation queue
       │
       ▼
Moderator review
       │
       ▼
    Decision
       │
   ┌───┼─────────┐
   ▼   ▼         ▼
Dismiss Warn    Action
               │
        ┌──────┼──────┐
        ▼      ▼      ▼
      Remove Restrict Escalate
```

A report should not automatically punish the reported user.

---

# 8. Moderation Cases

A useful architectural distinction is between a **Report** and a **Case**.

A report represents an individual user submission.

A case represents the broader moderation matter being investigated.

For example:

```text
REPORT #1 ─┐
REPORT #2 ─┤
REPORT #3 ─┼──► CASE #582
REPORT #4 ─┤
REPORT #5 ─┘
```

The case could contain:

* Reports
* Evidence
* Content context
* Moderator notes
* Decisions
* Moderation actions
* Appeals
* Escalation history

This prevents five users reporting the same post from necessarily creating five completely separate investigations.

### Important principle

Multiple reports may increase the **priority or visibility of a case**, but the number of reports should not automatically determine guilt.

---

# 9. Moderation Queue

Reports should enter a structured moderation queue.

```text
                    REPORT QUEUE
                         │
        ┌────────────────┼────────────────┐
        │                │                │
     Priority          Status            Type
        │                │                │
     Critical         Pending          Bullying
     High             Reviewing        Spam
     Medium           Resolved         Threat
     Low              Escalated        Other
```

Example:

```text
#10482
HIGH PRIORITY

Bullying / Harassment

Reported content:
Post #58291

Reported user:
Student123

Reports:
3

Created:
12 minutes ago

[Review]
```

Moderators should be able to filter and sort the queue by factors such as:

* Priority
* Status
* Report type
* Age
* Assigned moderator
* Escalation state

---

# 10. Moderation Dashboard

The moderation interface should be substantially different from the student interface.

```text
┌──────────────────────────────────────────────────────┐
│ MODERATION CENTER                                    │
├──────────────────────────────────────────────────────┤
│                                                      │
│ Pending        High Priority       Appeals           │
│   18                 4                2              │
│                                                      │
├──────────────────────────────────────────────────────┤
│ REPORT #10482                                         │
│                                                      │
│ Reason: Bullying / Harassment                        │
│                                                      │
│ Reported content:                                    │
│ ┌──────────────────────────────────────────────────┐ │
│ │ Reported content displayed here                  │ │
│ └──────────────────────────────────────────────────┘ │
│                                                      │
│ Reported user: Student123                            │
│ Community: Year 9                                    │
│                                                      │
│ [View Context] [View Evidence]                       │
│                                                      │
│ ACTION                                               │
│ [Dismiss] [Warn] [Remove] [Restrict] [Escalate]     │
└──────────────────────────────────────────────────────┘
```

Possible dashboard sections:

* Reports
* Cases
* Users
* Content
* Appeals
* Moderation Logs
* Policies

---

# 11. Detection and Automated Moderation

CLICK can eventually introduce automated safety detection.

A possible flow:

```text
                 USER CREATES CONTENT
                         │
                         ▼
                    SAFETY CHECK
                         │
             ┌───────────┼───────────┐
             │           │           │
            Safe      Suspicious    Severe
             │           │           │
             ▼           ▼           ▼
          Publish      Review      Hold/Block*
```

Potential detection systems include:

* Spam detection
* Abuse detection
* Threat detection
* Suspicious link detection
* Repeated harassment detection
* Flooding detection
* Mass messaging detection

*Any automatic blocking or holding mechanism should be carefully defined by the product's safety policy.

### Context matters

For example:

> "I hate this homework."

should not automatically be treated the same as:

> "I hate you and I'm going to hurt you."

Automated systems should therefore be treated as **signals and decision support**, especially for ambiguous cases.

---

# 12. User Protection

User-controlled protection should be separated from moderator enforcement.

## User Controls

```text
USER CONTROLS
 │
 ├── Block
 ├── Mute
 ├── Restrict messages
 └── Privacy settings
```

## Moderator Controls

```text
MODERATOR CONTROLS
 │
 ├── Warning
 ├── Content removal
 ├── Account restriction
 ├── Temporary suspension
 └── Escalation
```

### Block

Prevents another account from interacting with the user in defined ways.

### Mute

Stops the user from seeing another person's content without necessarily blocking that account.

### Restrict

Limits interactions without necessarily completely blocking the account.

These controls give students options for handling lower-level conflicts without every situation becoming a formal moderation case.

---

# 13. Moderation Actions

Actions can be organized into three categories:

```text
                 MODERATION ACTION
                         │
        ┌────────────────┼────────────────┐
        ▼                ▼                ▼
     Content          Account          Serious
      Action           Action           Action
        │                │                │
      Hide             Warn           Escalate
      Remove           Restrict       Safeguarding
      Restore          Suspend        Admin Review
```

Example progression:

### Low-level issue

```text
Spam
 ↓
Remove content
 ↓
Warning
```

### Repeated violation

```text
Multiple violations
 ↓
Account restriction
```

### Serious situation

```text
Threat / serious safety concern
          ↓
     Immediate review
          ↓
       Escalation
```

The exact consequences should be defined by the school's policies rather than hard-coded as assumptions by the software.

---

# 14. Appeals

Moderation decisions may be incorrect.

CLICK should therefore support appeals for eligible decisions.

```text
Moderation Decision
       │
       ▼
   User notified
       │
       ▼
   Can appeal?
       │
   ┌───┴────┐
   ▼        ▼
  Yes       No
   │
   ▼
Submit appeal
   │
   ▼
Appeal review
   │
   ▼
Final decision
```

Example:

```text
┌──────────────────────────────────────┐
│ Your post was removed                │
│                                      │
│ Reason: School policy violation      │
│                                      │
│ Think this was a mistake?            │
│                                      │
│ [Request an Appeal]                  │
└──────────────────────────────────────┘
```

Where practical, appeals should be reviewed by someone other than the original moderator.

---

# 15. Safety Escalation

Not every report requires the same response.

A basic priority model could be:

| Priority | Examples                                          | Response                                   |
| -------- | ------------------------------------------------- | ------------------------------------------ |
| Low      | Spam, minor inappropriate content                 | Normal queue                               |
| Medium   | Harassment, repeated inappropriate behaviour      | Priority review                            |
| High     | Threats, severe bullying, serious safety concerns | Immediate review and authorized escalation |

```text
LOW
 ↓
Normal moderation queue

MEDIUM
 ↓
Priority moderation

HIGH
 ↓
Immediate review
 ↓
Authorized school personnel
```

The platform should support escalation without attempting to make every real-world safeguarding decision automatically.

---

# 16. Database Architecture

Moderation should be represented as a set of related entities rather than one large object.

```text
users
 │
 ├── roles
 ├── profiles
 └── privacy_settings

content
 │
 ├── posts
 ├── comments
 ├── messages
 ├── media
 └── groups

moderation
 │
 ├── reports
 ├── moderation_cases
 ├── moderation_actions
 ├── moderation_logs
 ├── appeals
 └── restrictions
```

A report could contain fields such as:

```text
report
 ├── report_id
 ├── reporter_id
 ├── target_type
 ├── target_id
 ├── reported_user_id
 ├── reason
 ├── description
 ├── priority
 ├── status
 ├── assigned_moderator
 ├── created_at
 └── resolved_at
```

The exact schema should be finalized alongside CLICK's existing identity, content, group, messaging, and permissions architecture.

---

# 17. Moderation Logs

Important moderation actions should create audit records.

Example:

```text
MODERATION LOG

Moderator:
Admin123

Action:
Removed Post #9382

Reason:
School policy violation

Date:
05 Oct 2026

Case:
#10482
```

Another example:

```text
Moderator:
Mod456

Action:
Restricted User #182

Duration:
24 hours

Reason:
Repeated harassment

Case:
#10491
```

Audit records should help answer:

> **Who did what, when, and under which case or authorization?**

They can also help detect misuse of moderation privileges.

---

# 18. Privacy Architecture

Moderation information should follow explicit access policies.

```text
REPORT
 │
 ├── reporter_id
 ├── reported_user_id
 ├── visibility
 └── access_policy
```

Possible access:

```text
REPORTER
   │
   └── Basic report status

MODERATOR
   │
   └── Authorized case information

SCHOOL ADMIN
   │
   └── Authorized sensitive cases

OTHER STUDENTS
   │
   └── No report access
```

### Reporter privacy

The person being reported should **not automatically be told who submitted the report**.

This reduces the risk of:

* Retaliation
* Bullying
* Intimidation
* Social pressure

Sensitive cases should have stricter access controls.

---

# 19. Security Architecture

Security should underpin the entire moderation system.

```text
                         SECURITY
                            │
            ┌───────────────┼────────────────┐
            │               │                │
     Authentication    Authorization      Auditing
            │               │                │
            ▼               ▼                ▼
        Staff login        RBAC          Action logs
        MFA                Permissions    Access logs
        Sessions           Case access   Changes
```

Moderation accounts should have appropriate authentication protections.

Authorization should not simply be:

```text
if user.isModerator
```

Instead, permissions should be granular.

Examples:

```text
CAN_VIEW_REPORTS
CAN_REVIEW_CASE
CAN_REMOVE_CONTENT
CAN_RESTRICT_USER
CAN_SUSPEND_USER
CAN_ESCALATE_CASE
CAN_VIEW_SENSITIVE_CASE
```

This allows CLICK to give different moderators different capabilities.

---

# 20. Notifications

Moderation should integrate with CLICK's notification system.

Example:

```text
Report submitted
       ↓
Moderation Event
       ↓
Notification Engine
       ↓
Assigned Moderator
```

Or:

```text
Moderation decision
       ↓
Notification Engine
       ↓
Affected User
```

Possible notifications include:

* Your report has been received.
* Your report has been reviewed.
* Your content was removed because it violated a school policy.
* Your appeal has been received.
* Your appeal has been reviewed.

Notifications should avoid exposing unnecessary sensitive information.

---

# 21. Connecting Moderation Across CLICK

The moderation engine should be reusable across different Community features.

```text
                  MODERATION ENGINE
                         │
       ┌─────────────────┼─────────────────┐
       │                 │                 │
      POST            COMMENT           MESSAGE
       │                 │                 │
    Report            Report            Report
    Remove            Remove            Block
       │                 │                 │
       └─────────────────┼─────────────────┘
                         │
                    USER / GROUP
                         │
                    Restriction
```

This is preferable to maintaining completely independent systems such as:

```text
PostModeration
CommentModeration
MessageModeration
GroupModeration
```

Instead, these features should communicate with a shared moderation architecture.

---

# 22. Student Safety Center

The student-facing safety interface should remain simple.

```text
SAFETY CENTER

┌─────────────────────────────────────────┐
│ Your Safety                             │
├─────────────────────────────────────────┤
│                                         │
│ [Privacy Settings]                      │
│ [Blocked Accounts]                      │
│ [Muted Accounts]                        │
│ [Safety Guidelines]                     │
│                                         │
│ ─────────────────────────────────────── │
│                                         │
│ Your Reports                            │
│                                         │
│ #10482   Under Review                   │
│ #10421   Resolved                       │
│                                         │
│ ─────────────────────────────────────── │
│                                         │
│ [Report a Problem]                      │
└─────────────────────────────────────────┘
```

Students should not need to understand the underlying moderation architecture.

The moderator interface can remain significantly more detailed.

---

# 23. Common Design Mistakes

## 1. Treating reporting as the entire safety system

```text
Report → Delete
```

is not sufficient.

A complete system needs review, evidence, actions, escalation, auditing, and potentially appeals.

## 2. Automatically punishing users

A report is an allegation, not automatically proof.

## 3. Giving moderators excessive permissions

Use granular permissions and access policies.

## 4. Revealing reporters

Reporter identity should be protected where appropriate.

## 5. Collecting unnecessary information

Only collect information required for the safety process.

## 6. Depending entirely on AI

AI can assist moderators, but context can be complicated.

## 7. Forgetting appeals

Users need a mechanism for correcting incorrect moderation decisions.

## 8. Making reporting difficult

The report action should normally be close to the content:

```text
Post → ⋯ → Report
Comment → ⋯ → Report
Profile → ⋯ → Report
Message → ⋯ → Report
```

## 9. Treating every report equally

A spam report should not necessarily receive the same priority as a serious threat.

## 10. Building safety separately from CLICK

Safety should be part of the architecture from the beginning rather than bolted onto the platform later.

---

# 24. Reference Architecture

A clean high-level architecture for CLICK could look like this:

```text
                    ┌─────────────────────┐
                    │   CLICK COMMUNITY   │
                    └──────────┬──────────┘
                               │
        ┌──────────────────────┼──────────────────────┐
        │                      │                      │
        ▼                      ▼                      ▼
     CONTENT                 USERS                  GROUPS
        │                      │                      │
   Posts/Comments          Profiles              Communities
   Messages                Accounts              Events
   Media                   Interactions           Discussions
        │                      │                      │
        └──────────────────────┼──────────────────────┘
                               ▼
                         SAFETY LAYER
                               │
              ┌────────────────┼────────────────┐
              │                │                │
              ▼                ▼                ▼
          REPORTING        DETECTION        PROTECTION
              │                │                │
          Reports           Spam              Block
          Evidence          Abuse             Mute
          Categories        Threats            Privacy
              │                │                │
              └────────────────┼────────────────┘
                               ▼
                      MODERATION ENGINE
                               │
             ┌─────────────────┼─────────────────┐
             │                 │                 │
             ▼                 ▼                 ▼
          REVIEW             ACTIONS          ESCALATION
             │                 │                 │
          Cases             Warning          Safeguarding
          Evidence          Remove           Admin Review
          History           Restrict         Serious Cases
             │                 │                 │
             └─────────────────┼─────────────────┘
                               ▼
                       APPEALS & AUDITING
                               │
                               ▼
                         DATA LAYER
                               │
             Reports • Cases • Actions • Logs • Appeals
```

---

# 25. Recommended MVP

The complete architecture should be designed for expansion, but the first release should remain focused.

## Phase 1 — Basic Safety

* Report Post
* Report Comment
* Report User
* Block User
* Basic moderation queue
* Moderator roles

## Phase 2 — Moderation

* Report categories
* Case management
* Warnings
* Content removal
* Account restrictions
* Moderation logs

## Phase 3 — School Safety

* Priority levels
* Escalation
* Sensitive cases
* School administrator review
* Appeals
* Safety policies

## Phase 4 — Advanced Safety

* Spam detection
* Abuse detection
* Threat detection
* Suspicious behaviour detection
* Automated moderation assistance

## Phase 5 — Intelligence & Scale

* Duplicate report detection
* Risk signals
* Moderator workload management
* Advanced audit analytics
* Safety dashboards
* Moderation intelligence

The important principle is:

> **Build the safety foundation first. Add automation and intelligence after the underlying moderation workflow is reliable.**

---

# 26. Architectural Decisions for the Team

Before implementation, the team should explicitly decide the following.

## Reporting

* What can students report?
* Which report categories are required?
* Can users submit evidence?
* Should reports be anonymous to the reported person?
* Can multiple reports be grouped into one case?

## Moderation

* Who can moderate?
* What actions can each role perform?
* When does a case become high priority?
* When must a case be escalated?
* How long should moderation records be retained?

## Detection

* Will CLICK use automated detection?
* What should it detect?
* Should suspicious content be flagged after publication?
* Should certain content be temporarily held?
* What requires human review?

## Privacy

* Who can access a report?
* What information should moderators see?
* How should sensitive cases be protected?
* How long should sensitive evidence be retained?

## Appeals

* Which decisions can be appealed?
* Who reviews appeals?
* Can a moderator reverse another moderator's decision?
* What happens after an appeal?

## Architecture

* Should Reports and Cases be separate entities?
* Should moderation be a dedicated module/service?
* How should it communicate with Posts, Messaging, Groups, and Users?
* Which moderation events should trigger notifications?
* Which actions require elevated permissions?

---

# 27. Core Principles

The CLICK safety architecture should ultimately follow these principles:

1. **A report is a signal, not a verdict.**
2. **Moderation decisions should be traceable.**
3. **Moderator permissions should be granular.**
4. **Reporter identity should be protected where appropriate.**
5. **Users should have personal safety controls.**
6. **Serious cases should have clear escalation paths.**
7. **Moderation decisions should be appealable where appropriate.**
8. **Automation should assist human judgment, not blindly replace it.**
9. **Safety should be integrated with the Community architecture.**
10. **Privacy and security should be built into the system from the beginning.**

The goal is not simply to remove bad content.

The goal is to build a **controlled, accountable, privacy-aware safety system** that helps CLICK protect its community while giving authorized people the tools to review, respond, escalate, and correct mistakes.
