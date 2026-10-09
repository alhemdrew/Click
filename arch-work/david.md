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



# CLICK --- Moderation, Reporting & Safety

## Privacy-Protecting Chat Monitoring and Student Safety Architecture

## 1. The Overall Idea

The **Moderation, Reporting & Safety** system is responsible for keeping
CLICK a safe environment for students while protecting their privacy.

The system should allow students to report inappropriate posts,
comments, users, and messages. It should also detect cuss words and
other inappropriate language in private chats and notify authorized
moderators or the school administrator.

> **Core privacy rule:** Private chat threads must remain private.
> Moderators and the school administrator must not be able to open,
> browse, or read entire conversations. If inappropriate language is
> detected, they should see only the specific text that triggered the
> alert, the people involved, their classes, and the reason for the
> alert.

The aim is to combine effective reporting and protection with privacy
safeguards.

## 2. Main Safety Architecture

CLICK Safety should contain these main systems:

``` text
CLICK SAFETY SYSTEM
│
├── 1. REPORTING SYSTEM
│   ├── Report a Post
│   ├── Report a Comment
│   ├── Report a User
│   ├── Report a Group
│   └── Report a Message
│
├── 2. CHAT LANGUAGE DETECTION
│   ├── Cuss Word Detection
│   ├── Inappropriate Language Detection
│   ├── Threat and Harassment Detection
│   └── Safety Alert Generation
│
├── 3. STUDENT PROTECTION
│   ├── Block Users
│   ├── Mute Users
│   ├── Hide or Remove Content
│   └── Restrict Accounts
│
├── 4. MODERATION ENGINE
│   ├── Review Alerts
│   ├── Review Reports
│   ├── Issue Warnings
│   ├── Apply Restrictions
│   └── Escalate Serious Cases
│
├── 5. PRIVACY CONTROL
│   ├── Prevent Chat Thread Access
│   ├── Show Only Flagged Text
│   ├── Restrict Sensitive Information
│   └── Record Authorized Access
│
└── 6. SAFETY RECORDS
    ├── Reports
    ├── Flagged Text Excerpts
    ├── Moderator Decisions
    └── Appeals and Audit Logs
```

The privacy controls must apply throughout the system, not just on the
moderator dashboard.

## 3. Reporting System

Students should be able to report content or behaviour that violates
CLICK's safety rules.

### What students can report

-   Posts and comments
-   Inappropriate images or videos
-   Bullying or harassment
-   Threats or dangerous behaviour
-   Hate speech or discrimination
-   Impersonation
-   Spam or suspicious links
-   Inappropriate private messages
-   Groups that repeatedly violate safety rules

### Report interface

``` text
┌─────────────────────────────────┐
│          REPORT CONTENT         │
├─────────────────────────────────┤
│ Why are you reporting this?     │
│                                 │
│ ○ Bullying or harassment        │
│ ○ Cuss words or inappropriate  │
│   language                      │
│ ○ Threats or dangerous behaviour│
│ ○ Hate or discrimination        │
│ ○ Spam or suspicious links      │
│ ○ Impersonation                 │
│ ○ Other                         │
│                                 │
│ Additional details (optional)  │
│ [_____________________________] │
│                                 │
│ [Cancel]       [Submit Report]  │
└─────────────────────────────────┘
```

After submitting a report, the student should receive confirmation and
be able to check whether it is pending, under review, or resolved. They
should not be able to see another student's private disciplinary
information.

## 4. Private Chat Monitoring --- The Most Important Feature

CLICK should include a **targeted chat-language detection system**. Its
purpose is to detect potentially inappropriate language without giving
moderators or the school administrator access to private conversations.

### How it should work

1.  Two students exchange private messages.
2.  CLICK's automated safety system checks the message text against its
    published safety rules.
3.  If the message contains a recognised cuss word or potentially
    inappropriate language, the system generates an alert.
4.  The alert contains only the specific text that triggered the alert.
5.  The alert identifies the sender, recipient, and their respective
    classes.
6.  An authorized moderator or school administrator reviews the limited
    alert information.
7.  If necessary, the reviewer can issue a warning, apply an appropriate
    restriction, or escalate a serious concern.

**The system must not display the full conversation, surrounding
messages, chat history, or a button that opens the private chat
thread.**

### Example safety alert

``` text
┌───────────────────────────────────────────┐
│             CLICK SAFETY ALERT            │
├───────────────────────────────────────────┤
│ Alert type: Inappropriate language        │
│ Status: Pending review                    │
│                                           │
│ Sender: Student A                         │
│ Sender's class: JSS 3A                    │
│ Recipient: Student B                      │
│ Recipient's class: JSS 3B                 │
│                                           │
│ Flagged message text only:                │
│ "[only the flagged message text]"         │
│                                           │
│ Detection reason: Cuss word detected      │
│                                           │
│ [Dismiss] [Issue Warning] [Escalate]      │
└───────────────────────────────────────────┘
```

*The names and classes above are examples. CLICK should retrieve the
correct details from authorized student records.*

The alert should not include any other messages from either student's
conversation. If only part of a message contains the flagged language,
the system could show just that portion, provided enough text remains to
understand what triggered the alert.

### What moderators and administrators must not see

-   The complete chat thread
-   Messages sent before or after the flagged message
-   Unrelated private conversations
-   A student's entire chat history
-   Private messages that did not trigger an alert
-   Unnecessary personal information

The moderator dashboard must not provide a general-purpose private-chat
viewer. Access restrictions must be enforced by the backend, not simply
by hiding buttons in the interface.

## 5. How the Chat Detection System Should Work

CLICK could use one of three approaches.

### Option A --- Word and phrase list

CLICK checks messages against an approved list of cuss words and
prohibited expressions.

**Advantages** - Easier to build - Fast and relatively inexpensive -
Suitable for an early version of CLICK

**Limitations** - Slang and spelling variations may be missed. - Some
words may be used jokingly or without harmful intent. - A list alone
cannot reliably understand context.

### Option B --- Automated language classification

A language-classification model assesses whether a message may contain
inappropriate language, harassment, or threats.

**Advantages** - Can potentially recognise more variations and
expressions - May distinguish different types of safety concerns better
than a simple word list

**Limitations** - It may make mistakes. - It requires testing, ongoing
improvement, and careful handling of student data. - It should not
automatically decide that a student deserves punishment.

### Option C --- Combined approach

Use a word and phrase list for clear matches, supported by a classifier
for more complex cases.

This is an option worth investigating for CLICK. In every approach, a
detected word should be treated as a **potential violation**, not
automatic proof of misconduct. Context matters, and students should have
a way to challenge an incorrect decision.

## 6. What Happens After an Alert?

The alert should enter a separate moderation queue rather than granting
access to the chat.

``` text
Student sends a message
          │
          ▼
Automated safety check
          │
          ▼
Potentially inappropriate language detected?
          │
      ┌───┴────┐
      │        │
      No       Yes
      │        │
      ▼        ▼
Normal chat   Create limited
processing    safety alert
                 │
                 ▼
         Authorized reviewer
                 │
                 ▼
          Assess the alert
                 │
        ┌────────┼────────┐
        │        │        │
        ▼        ▼        ▼
     Dismiss   Warning  Escalate
        │        │        │
        └────────┼────────┘
                 ▼
        Record the decision
```

The system should distinguish between ordinary profanity, repeated
inappropriate language, targeted harassment, and credible threats. These
situations may require different responses.

A single detected word should not automatically result in suspension.
Repeated or serious behaviour may justify stronger action under school
policy.

## 7. Moderator Dashboard

The moderator dashboard should provide the tools needed to manage
reports and safety alerts without exposing private conversations.

``` text
CLICK MODERATION DASHBOARD
│
├── Reports
├── Chat Safety Alerts
├── Flagged Posts and Comments
├── Cases
├── Student Restrictions
├── Appeals
├── Safety Rules
└── Moderation Audit Logs
```

Each chat alert should show only:

-   Alert ID and date
-   Alert category and detection reason
-   Exact flagged text or flagged portion
-   Sender's name and class
-   Recipient's name and class
-   Review status
-   Previous relevant moderation actions, if authorized and necessary
-   Available actions

The dashboard must not provide search or browsing features for private
chat content.

### Possible moderator actions

  -----------------------------------------------------------------------
  Action                              Purpose
  ----------------------------------- -----------------------------------
  Dismiss alert                       The detection was incorrect or did
                                      not violate policy.

  Issue warning                       Remind a student of CLICK's
                                      language rules.

  Restrict an account                 Temporarily limit certain
                                      activities when justified.

  Escalate a case                     Refer serious or repeated concerns
                                      to designated school safeguarding
                                      staff.

  Record a decision                   Keep an accountable record of the
                                      action taken.
  -----------------------------------------------------------------------

The school administrator should have the permissions needed to oversee
serious cases and moderation policy, but **administrator status must not
automatically grant access to private chat threads**.

## 8. Blocking and Muting Users

Blocking and reporting should be separate actions.

When a student blocks another user, CLICK could:

-   Prevent the blocked user from starting new private chats with them.
-   Restrict other direct interactions according to the platform's
    rules.
-   Allow the student to unblock the person later.
-   Keep the blocker's choice private where possible.

Muting should silence notifications without necessarily preventing
messages from being sent.

Blocking a user should not automatically create a disciplinary report. A
student may simply want to stop receiving messages. They should still be
able to report threatening or inappropriate messages separately.

## 9. Basic Safety Rules

CLICK should publish clear, student-friendly safety rules:

1.  Treat other students with respect.
2.  Do not bully, threaten, or harass others.
3.  Avoid abusive or inappropriate language.
4.  Do not share sexual, violent, or otherwise prohibited content.
5.  Do not impersonate another person.
6.  Do not share another student's private information without
    permission.
7.  Do not spam or deliberately disrupt groups.
8.  Do not misuse reports to target other students.
9.  Respect other students' boundaries and blocking decisions.
10. Follow the school's rules for using CLICK.

The school should explain what happens when these rules are broken and
provide a fair process for reviewing decisions.

## 10. Database Architecture

The safety system should be separated from the private messaging system.

``` text
USERS
├── Student Profiles
├── Class Memberships
├── Roles and Permissions
└── Privacy Settings

MESSAGING
├── Private Messages
├── Chat Memberships
└── Message Delivery Records

SAFETY
├── Reports
├── Safety Alerts
├── Flagged Text Excerpts
├── Moderation Cases
├── Moderation Actions
├── Restrictions
├── Appeals
└── Audit Logs
```

### Important data fields

**Safety alerts** - Alert ID - Triggering message ID, stored as a
restricted internal reference if needed - Flagged text excerpt -
Detection category - Detection timestamp - Sender ID - Recipient ID -
Review status

**Student records** - Student ID - Display name - Class or year group

**Moderation actions** - Action ID - Related alert or report ID -
Authorized reviewer ID - Action type - Reason for the decision -
Timestamp

The system should retrieve class details from authorized student records
rather than relying on students to type their own class into a report.

**Privacy design choice:** The alert record should contain only the
minimum excerpt needed for review. The backend should not copy an entire
message or conversation into the moderation database. If CLICK retains
the original message in its messaging system, the moderation service
must still be unable to retrieve the rest of the thread.

## 11. Privacy and Security Architecture

The following rules should be built into CLICK from the beginning.

### Rule 1 --- No private-thread access

Moderators and the school administrator cannot open private chats or
search through chat histories.

### Rule 2 --- Limited alert visibility

Authorized reviewers can see only the flagged text, the people involved,
their classes, and the information needed to assess that specific alert.

### Rule 3 --- Backend permission checks

Every request for an alert must verify that the user has permission to
access it. Hiding a page or button is not enough.

### Rule 4 --- Limited data retention

Keep flagged excerpts only as long as necessary under the school's
approved safety and data-retention policy. Delete or anonymize them when
they are no longer required, subject to applicable safeguarding
obligations.

### Rule 5 --- Audit logs

Record which authorized staff member accessed an alert, what decision
they made, and when. Do not put full private conversations in the audit
log.

### Rule 6 --- Fair review

Automated detection can be wrong. Give students an appropriate way to
appeal warnings or restrictions and correct inaccurate records.

### Rule 7 --- Clear communication

Tell students that automated checks are used to detect certain
inappropriate language, what information may be shown to authorized
staff, and how alerts are handled. Do not claim that private messages
are completely unmonitored if the system checks them for safety.

## 12. How This Connects to Other CLICK Features

-   **Private Messaging:** Sends messages through the messaging system,
    with the safety detector checking message text under the published
    policy.
-   **Student Profiles:** Supplies verified names and classes for
    alerts.
-   **Reporting:** Allows students to report harmful behaviour that
    automated detection may miss.
-   **Notifications:** Alerts authorized staff when a new safety alert
    needs review.
-   **School Administration:** Allows designated staff to handle serious
    cases without granting general access to private conversations.
-   **Account Settings:** Provides blocking, muting, and privacy
    controls.
-   **Audit Logs:** Records moderation decisions and access to sensitive
    alert information.

## 13. Suggested MVP Development Plan

### Phase 1 --- Essential safety

-   Report posts, comments, and users.
-   Block and mute users.
-   Publish basic safety rules.
-   Build a simple moderation dashboard.
-   Enforce role-based permissions.

### Phase 2 --- Targeted chat alerts

-   Create an initial list of prohibited words and expressions.
-   Check messages for potential matches.
-   Display only the flagged text and the sender's and recipient's
    identities and classes.
-   Prevent moderators and administrators from opening private chat
    threads.
-   Add dismiss and warning actions.

### Phase 3 --- Stronger moderation

-   Add more detection categories.
-   Add escalation for threats and repeated harassment.
-   Add appeals and moderation audit logs.
-   Test false positives and spelling variations.
-   Establish data-retention rules and safeguarding procedures.

### Phase 4 --- Improve detection

-   Evaluate a language classifier if needed.
-   Test accuracy across common slang and relevant languages.
-   Measure false positives and missed detections.
-   Improve the system based on reviewed cases while limiting access to
    student data.

## 14. Questions for the Team to Decide

Before finalizing the architecture, the team should discuss:

1.  Which words and categories should trigger an alert?
2.  Should every cuss word trigger an alert, or only words that meet the
    school's defined policy?
3.  Should the alert display the entire flagged message or only the
    offending phrase?
4.  Which designated moderators can see alerts, and which serious cases
    should go to the school administrator?
5.  What happens when a message is flagged incorrectly?
6.  How long should alert excerpts be retained?
7.  How should CLICK handle credible threats, targeted bullying, or
    immediate safeguarding concerns?
8.  How will students be informed about chat-language detection?
9.  What appeal process should be available?
10. How can the team test the system without exposing real students'
    private conversations?

## 15. Final Architecture Principle

CLICK should combine student reporting, targeted language detection,
privacy protection, and fair moderation.

> **The central design decision:** Moderators and the school
> administrator may review a safety alert, but they may not browse
> private conversations. They see only the flagged text, the people
> involved, their classes, and the information necessary to respond.

This keeps the system focused on student safety while reducing
unnecessary access to private communications.

## Research Basis

The recommendations in this document are proposed design choices for
CLICK, informed by child-online-safety guidance. UNICEF's *Child
Protection in Digital Education: Technical Note* discusses the need for
accessible reporting mechanisms and clear response procedures.

-   [UNICEF --- Child Protection in Digital Education: Technical
    Note](https://www.unicef.org/media/134131/file/Child%20Protection%20in%20Digital%20Education%20Technical%20Note.pdf)
