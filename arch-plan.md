# CLICK — Cuddles Learning, Interaction & Community Konnect

> **Architecture Research & Design Programme**
>
> A student-led software architecture exercise for the development of **CLICK**, the school social platform for **Cuddles Chat**.

---

## 1. Project Overview

**CLICK** stands for:

> **Cuddles Learning, Interaction & Community Konnect**

CLICK is a school-focused social platform designed to provide a safe, structured digital space where students, teachers, and authorised school administrators can communicate, share content, participate in communities, and interact with one another.

The project is being developed by students as a practical learning experience in:

* Software architecture
* Product design
* Research
* Prompt engineering
* AI-assisted development
* Git and GitHub
* VS Code
* GitHub Copilot
* Collaboration
* Critical thinking
* Responsible technology development

### The Most Important Principle

> **We do not begin by asking AI to build the entire application. We first decide what we are building and how it should work.**

The architecture is the blueprint that guides development.

---

# 2. Why Are We Designing the Architecture First?

AI coding tools such as GitHub Copilot are powerful, but they do not automatically understand the complete vision of a project.

Without a clear architecture, an AI coding assistant may:

* Create duplicate features
* Use inconsistent naming
* Invent unnecessary components
* Store data incorrectly
* Create conflicting systems
* Change previously established behaviour
* Introduce technologies that do not belong in the project
* Lose track of the original design as the codebase becomes larger

A documented architecture gives both the development team and AI coding assistants a reliable reference.

The CLICK architecture should therefore answer:

> **What are we building?**

> **Why are we building it this way?**

> **How should the different parts communicate?**

> **What rules must the system follow?**

---

# 3. The Student Architecture Programme

Each student will be responsible for researching and proposing the architecture of one section of CLICK.

You are **not being asked to write the complete code for your section yet**.

Your first responsibility is to understand the problem and design a sensible solution.

Your work will eventually be reviewed with the rest of the class.

The best ideas from different proposals may be combined into the final CLICK architecture.

### Important

Your proposal is **not automatically the final design**.

You are expected to:

1. Research.
2. Ask questions.
3. Explore alternatives.
4. Use AI as a research assistant.
5. Challenge AI-generated suggestions.
6. Make your own decisions.
7. Explain your reasoning.
8. Present your architecture.
9. Accept feedback.
10. Improve the design.

---

# 4. Student Assignments

| Student       | Assigned Section                                 | Difficulty  |
| ------------- | ------------------------------------------------ | ----------- |
| **Charles**   | Application Navigation & Overall User Experience | Medium      |
| **Ogechukwu** | User Profiles & Student Identity                 | Medium      |
| **Daniel**    | Authentication, Roles & Permissions              | Medium–High |
| **David**     | Home Feed / Timeline                             | Medium–High |
| **Ire**       | Chat & Messaging                                 | High        |
| **Fumilayo**  | Communities / Groups                             | Medium–High |
| **Kishi**     | Notifications                                    | Medium      |
| **Kemi**      | Posts, Comments & Reactions                      | Medium      |
| **Esther**    | Search                                           | **Light**   |
| **Kitan**     | Media, Photos & File Sharing                     | Medium      |
| **Komi**      | Reporting, Moderation & Safety                   | Medium–High |

### Special Note for Esther

Esther's assignment is intentionally smaller in scope.

The goal is for her to produce a clear and understandable architecture without being overloaded with complex system design.

Her section should focus on:

* Searching for users
* Searching for posts
* Searching for communities
* Search results
* Basic filters
* Search interface

She is **not expected to design a complex search engine or search infrastructure**.

---

# 5. What Does "Architecture" Mean?

Architecture is the blueprint of a software system.

Think about constructing a building.

Before constructing the building, you need to know:

* Where the rooms will be
* Where the doors will go
* Where electricity will run
* Where water will run
* How the rooms connect
* What materials are required

Software works in a similar way.

Before writing thousands of lines of code, we need to understand:

* What features exist
* What screens exist
* What data exists
* Who can access what
* How different features communicate
* What happens when something goes wrong
* What security rules exist

Your architecture is therefore more than a drawing.

It is a **technical explanation of how your section should work**.

---

# 6. What Every Student Must Research

Every student should answer the following questions about their assigned section.

## 6.1 Purpose

What is this section supposed to accomplish?

Example:

> The chat system allows students and authorised users to communicate through private and group conversations.

---

## 6.2 Target Users

Who will use this feature?

Possible users include:

* Students
* Teachers
* School administrators
* Moderators

Not every feature must be available to every user.

---

## 6.3 Features

What should users be able to do?

For example, a chat system might contain:

* Start a conversation
* Send a message
* Receive a message
* Create a group conversation
* Delete a message
* See message timestamps
* See read status

Do not assume that every possible feature belongs in CLICK.

Research and explain which features are actually useful.

---

## 6.4 User Flow

Explain what happens when a user performs an action.

For example:

```text
Student opens CLICK
        ↓
Student opens Chat
        ↓
Student selects another user
        ↓
Conversation opens
        ↓
Student writes a message
        ↓
Message is submitted
        ↓
Server validates the request
        ↓
Message is stored
        ↓
Recipient receives the message
```

Your user flow should explain the journey from beginning to end.

---

# 7. Interface / UI Proposal

You should propose what your feature could look like.

You may use:

* Paper sketches
* Figma
* Canva
* PowerPoint
* Draw.io
* Other suitable design tools

Your design does **not** need to be beautiful.

It needs to communicate your idea clearly.

For example:

```text
┌─────────────────────────────────────┐
│ CLICK                     🔔    👤  │
├─────────────────────────────────────┤
│ 🔍 Search conversations             │
├─────────────────────────────────────┤
│                                     │
│ 👤 David                            │
│    Are you coming tomorrow?         │
│                                     │
│ 👤 Charles                          │
│    Check the assignment             │
│                                     │
├─────────────────────────────────────┤
│ Home    Chat    Community    Me     │
└─────────────────────────────────────┘
```

This is only an example.

**You are encouraged to create your own design.**

---

# 8. Data Architecture

Every feature needs information to work.

Ask yourself:

> **What information does my feature need to store?**

For example, a messaging system may need:

```text
USER
────
id
name
profile_photo

CONVERSATION
────────────
id
created_at

CONVERSATION_MEMBER
───────────────────
conversation_id
user_id

MESSAGE
───────
id
conversation_id
sender_id
content
created_at
read_at
```

You do not need to know advanced SQL to complete this exercise.

Your responsibility is to identify:

* What information exists
* What each piece of information means
* How different pieces of information relate

---

# 9. Example Relationship

A chat architecture might look like:

```text
USER
  │
  ├───────────────┐
  │               │
  ↓               ↓
CONVERSATION_MEMBER
  │
  ↓
CONVERSATION
  │
  ↓
MESSAGE
  ↑
  │
USER
```

Your own section may have a completely different structure.

---

# 10. Connections to Other CLICK Systems

No major feature should be designed as if it exists alone.

Ask:

> **Which other parts of CLICK will my feature communicate with?**

For example:

```text
Posts ───────────┐
Messages ────────┤
Communities ─────┼──→ Notifications
Administration ──┘
```

A post might generate a notification.

A message might generate a notification.

A community invitation might generate a notification.

Therefore, the notification system needs to communicate with those systems.

This is why we need a **unified architecture**.

---

# 11. Security & Privacy

Every student must consider security.

Ask questions such as:

* Who is allowed to use this feature?
* Who can see the information?
* Who can create information?
* Who can edit it?
* Who can delete it?
* What happens if someone tries to access another user's information?
* What data should remain private?
* What should teachers be allowed to do?
* What should administrators be allowed to do?
* What should students not be allowed to do?

Security should not be something we add after building the application.

> **Security should be considered during architecture.**

---

# 12. Edge Cases

A good architecture also considers situations where things do not go normally.

For example:

### What if:

* The user has no internet connection?
* The message fails to send?
* A user deletes their account?
* A post is deleted?
* A user is blocked?
* A community is removed?
* A file is too large?
* A user attempts an action they are not authorised to perform?
* Two users perform conflicting actions at the same time?

You do not need to solve every problem.

You should demonstrate that you have **thought about the problems**.

---

# 13. Using AI for Research

AI tools are allowed and encouraged.

You may use:

* ChatGPT
* Microsoft Copilot
* Gemini
* Claude
* Other appropriate AI tools

However:

> **AI is your assistant, not your architect.**

Do not simply ask:

> "Build me a chat system."

and copy the answer.

Instead, use AI to:

* Understand concepts
* Compare approaches
* Find possible problems
* Explain unfamiliar technologies
* Challenge your ideas
* Suggest alternatives
* Help you improve your architecture

Then make your own decisions.

---

# 14. Recommended AI Research Prompt

You may use the following prompt as a starting point.

```text
You are a software architect helping me research one module of a
school social networking application called CLICK.

CLICK stands for:
Cuddles Learning, Interaction & Community Konnect.

The application is intended for students, teachers and authorised
school administrators.

The module I am researching is:

[INSERT YOUR MODULE]

Help me understand:

1. What is the purpose of this module?
2. Who should use it?
3. What features should it contain?
4. What are the important user flows?
5. What data would the system need?
6. What database entities might be required?
7. What screens and UI components might be required?
8. How should this module communicate with other modules?
9. What security and privacy issues should we consider?
10. What edge cases should we consider?
11. What are two or three possible architectural approaches?
12. What are the advantages and disadvantages of each approach?
13. What common mistakes should we avoid?

Do not assume that the first solution is automatically correct.
Explain your reasoning and give me alternatives so that I can
create my own architecture.
```

---

# 15. Challenge the AI

After receiving an AI response, **do not immediately accept it**.

Find at least three things that:

* You disagree with
* You do not understand
* You think could be improved
* You think may not be suitable for a school environment

Then ask the AI about them.

For example:

```text
You suggested allowing students to create unlimited group chats.

I am concerned that this could create moderation problems in a
school environment.

What alternative approaches could we use?

Compare the options and explain the security and moderation
implications.
```

This is an important part of the exercise.

### Prompt engineering is not simply asking AI questions.

It also means knowing enough to:

> **Question the answer.**

---

# 16. Required Architecture Submission

Every student must submit their work using this structure.

```text
# [MODULE NAME]

## 1. Purpose

What does this module do?

## 2. Target Users

Who can use it?

## 3. Features

What can users do?

## 4. User Flows

How does the user interact with it?

## 5. UI / Screen Proposal

What screens and components are required?

## 6. Data Requirements

What information does the system need?

## 7. Database Proposal

What entities/tables might be required?

## 8. Architecture Diagram

Show how the components connect.

## 9. Connections to Other Modules

Which CLICK systems does this module communicate with?

## 10. Security & Privacy

What security rules should exist?

## 11. Edge Cases

What could go wrong?

## 12. Design Decisions

Explain why you selected your approach.

## 13. Alternatives Considered

What other approaches did you consider?

## 14. AI Research

Which AI tools did you use?

## 15. AI Prompts

Show important prompts used during research.

## 16. What I Changed or Rejected

Explain what you disagreed with or changed from the AI suggestions.

## 17. Final Proposed Architecture

Present your final design.
```

---

# 17. Sample Completed Architecture

> **This is an example only. Do not copy it as your own architecture.**

## Notification System

### Purpose

The notification system informs users when something relevant happens to their account or activity.

### Users

* Students
* Teachers
* Administrators

### Possible Notification Events

```text
Someone comments on your post
        ↓
Notification created

Someone reacts to your post
        ↓
Notification created

You receive a message
        ↓
Notification created

You are invited to a community
        ↓
Notification created
```

### Proposed Data

```text
NOTIFICATION
─────────────
id
recipient_id
type
title
message
reference_id
is_read
created_at
```

### Possible Types

```text
COMMENT
REACTION
MESSAGE
COMMUNITY_INVITE
ANNOUNCEMENT
```

### UI Example

```text
┌────────────────────────────────────┐
│ Notifications                      │
├────────────────────────────────────┤
│ ● David commented on your post     │
│   5 minutes ago                    │
│                                    │
│ ● You received a message from      │
│   Charles                          │
│   15 minutes ago                   │
│                                    │
│ ○ New announcement from Cuddles    │
│   School                           │
└────────────────────────────────────┘
```

### Connections

```text
Posts ───────────┐
Messages ────────┤
Communities ─────┼──→ Notifications
Administration ──┘
```

### Security

* Users should only see their own notifications.
* Students should not be able to create administrative notifications.
* Notification links should not expose private content.
* Deleted content should not leave broken or misleading references.

---

# 18. The Bigger CLICK Architecture

Eventually, everyone's individual work should connect into one system.

A simplified conceptual architecture may look like:

```text
                         CLICK
                           │
          ┌────────────────┼────────────────┐
          │                │                │
        USERS            CONTENT      COMMUNICATION
          │                │                │
          │                │                ├── Chat
          │                │                └── Notifications
          │                │
          ├── Profiles     ├── Posts
          ├── Authentication
          ├── Roles        ├── Comments
          └── Permissions  ├── Reactions
                           └── Media

          ┌────────────────┼────────────────┐
          │                │                │
      COMMUNITY          SEARCH          SAFETY
          │                │                │
       Groups           Users           Reports
       Members          Posts           Moderation
       Activities       Groups          Administration
```

Underneath these modules will be the common technical layers:

```text
                         CLICK
                           │
                       Frontend
                           │
                        API Layer
                           │
                        Backend
                           │
                        Database
                           │
                 Authentication / Roles
                           │
                    Security / Rules
```

This is a conceptual example.

The final architecture will be created from the students' research and the team's decisions.

---

# 19. Important Rule: One Application, One Architecture

Students should not independently create completely different technology stacks.

For example, we should avoid a situation where:

```text
Charles → React
Daniel → Vue
David → Angular
Ire → PHP
Fumilayo → Firebase
Kishi → Supabase
```

That would create an inconsistent application.

The development team will establish the **global technology architecture**.

Individual students are responsible for designing their assigned module **within the agreed architecture**.

---

# 20. Expected Future Repository Structure

As the project develops, the architecture documentation may eventually look something like:

```text
CLICK/
│
├── README.md
│
├── docs/
│   │
│   ├── architecture/
│   │   ├── overview.md
│   │   ├── navigation.md
│   │   ├── authentication.md
│   │   ├── profiles.md
│   │   ├── feed.md
│   │   ├── posts.md
│   │   ├── comments.md
│   │   ├── reactions.md
│   │   ├── chat.md
│   │   ├── communities.md
│   │   ├── notifications.md
│   │   ├── search.md
│   │   ├── media.md
│   │   └── moderation.md
│   │
│   ├── database/
│   │   └── schema.md
│   │
│   ├── api/
│   │   └── endpoints.md
│   │
│   └── decisions/
│       └── architecture-decisions.md
│
├── apps/
│
├── packages/
│
└── .github/
    └── copilot-instructions.md
```

The exact structure may change as the project evolves.

The important idea is that the architecture should remain **documented, discoverable, and connected to the codebase**.

---

# 21. GitHub Copilot and the Architecture

Once the architecture has been reviewed and approved, it can become a source of truth for development.

For example, the repository may eventually contain:

```text
.github/
└── copilot-instructions.md
```

The instructions can tell Copilot things such as:

```text
You are contributing to CLICK:
Cuddles Learning, Interaction & Community Konnect.

Follow the architecture documented in /docs/architecture/.

Do not introduce a new technology without approval.

Do not create duplicate systems when an existing module
already provides the required functionality.

Follow the database conventions documented in /docs/database/.

Follow the security and role rules defined by the project.

Before making significant architectural changes, inspect the
relevant architecture documentation.
```

This allows the architecture created by the students to become part of the development workflow.

---

# 22. What We Are Actually Learning

This project is not only about building a school social platform.

Students are learning how professional software development works.

The workflow is:

```text
                    IDEA
                      ↓
                  RESEARCH
                      ↓
                AI ASSISTANCE
                      ↓
             CRITICAL THINKING
                      ↓
                 ARCHITECTURE
                      ↓
                   REVIEW
                      ↓
              UNIFIED BLUEPRINT
                      ↓
              DOCUMENTATION
                      ↓
                   CODING
                      ↓
              TESTING & REVIEW
                      ↓
              IMPROVEMENT
```

The goal is not:

> **"Let AI build everything."**

The goal is:

> **"Understand what we want, design it properly, and use AI to help us build it."**

---

# 23. Final Student Checklist

Before submitting your architecture, make sure you can answer **YES** to these questions:

* [ ] I understand my assigned module.
* [ ] I researched how similar systems work.
* [ ] I used AI as a research assistant where useful.
* [ ] I did not blindly copy AI-generated content.
* [ ] I can explain my design.
* [ ] I identified the main users.
* [ ] I identified the major features.
* [ ] I created the important user flows.
* [ ] I considered the required UI.
* [ ] I identified the important data.
* [ ] I proposed the required database entities.
* [ ] I considered how my module connects to other modules.
* [ ] I considered security and privacy.
* [ ] I considered possible edge cases.
* [ ] I considered alternative approaches.
* [ ] I explained why I selected my final approach.
* [ ] I documented the important AI prompts I used.
* [ ] I identified ideas from AI that I changed or rejected.
* [ ] I can present and defend my architecture to the class.

---

# 24. Final Principle

## **Think before you prompt.**

## **Research before you build.**

## **Design before you code.**

## **Question AI before you trust it.**

## **Document before the project becomes complicated.**

> **CLICK is not just a coding project. It is an opportunity to learn how real software systems are thought about, designed, built, tested, and improved.**

---

**Project:** CLICK
**Full Name:** Cuddles Learning, Interaction & Community Konnect
**Environment:** GitHub + VS Code + GitHub Copilot
**Approach:** Student-led research → Architecture → Review → Unified Blueprint → AI-assisted development
