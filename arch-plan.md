# CLICK — Cuddles Learning, Interaction & Community Konnect

> **Student Architecture Research & Design**

## 1. About the Project

**CLICK** means:

> **Cuddles Learning, Interaction & Community Konnect**

CLICK is a school social platform being designed and developed by students using **GitHub, VS Code, and GitHub Copilot**.

The goal is not simply to make a website.

The goal is to learn how a real software project is planned before it is built.

Before we begin serious coding, we need a **blueprint** that explains what each part of CLICK should do and how the different parts should work together.

---

# 2. Why Are We Doing This?

AI coding tools can generate code very quickly.

However, if we do not first decide what we want to build, AI can:

* Create unnecessary features
* Build things differently in different parts of the application
* Duplicate existing features
* Make assumptions about how the system should work
* Change the original idea as development continues

Therefore, our process is:

```text
IDEA
  ↓
RESEARCH
  ↓
DESIGN
  ↓
ARCHITECTURE
  ↓
REVIEW
  ↓
CODING
  ↓
TESTING
  ↓
IMPROVEMENT
```

The architecture becomes a reference that both the students and GitHub Copilot can use during development.

---

# 3. Student Sections

Each student will research and design one part of CLICK.

| Student       | Assigned Section                      |
| ------------- | ------------------------------------- |
| **David**     | Moderation, Reporting & Safety        |
| **Daniel**    | Authentication, Accounts & User Roles |
| **Ire**       | Chat & Messaging                      |
| **Ogechukwu** | Profile & Personalization             |
| **Fumilayo**  | Communities & Groups                  |
| **Kishi**     | Notifications                         |
| **Kitan**     | Media, Photos & File Sharing          |
| **Charles**   | Home Page & Navigation                |
| **Kemi**      | Posts, Comments & Reactions           |
| **Komi**      | Announcements & School Updates        |
| **Esther**    | Search & Finding Content              |

This gives us different parts of the application that can eventually be brought together into one architecture.

---

# 4. What Each Section Means

## David — Moderation, Reporting & Safety

Research how CLICK can remain a safe school environment.

Consider:

* Reporting a post or user
* Reporting inappropriate content
* What happens after something is reported
* Moderator actions
* Blocking users
* Removing inappropriate content
* Basic safety rules

---

## Daniel — Authentication, Accounts & User Roles

Research how users enter and use CLICK.

Consider:

* Creating an account
* Logging in
* Logging out
* Password recovery
* Student accounts
* Teacher accounts
* Administrator accounts
* What different users are allowed to do

---

## Ire — Chat & Messaging

Research how communication between users could work.

Consider:

* One-to-one chat
* Group conversations
* Sending messages
* Receiving messages
* Message timestamps
* Read/unread messages
* Basic chat interface

---

## Ogechukwu — Profile & Personalization

Research how users can make CLICK feel personal to them.

Consider:

* Profile photo
* Display name
* Bio/about section
* Profile layout
* Profile information
* Theme preferences
* Appearance/customization
* What parts of the profile a user can edit
* What information should remain private

Think about:

> **"If I open my CLICK profile, what should I be able to see and change?"**

---

## Fumilayo — Communities & Groups

Research how students and teachers could interact around shared interests or activities.

Consider:

* Creating communities
* Joining communities
* Community members
* Community posts
* Community information
* Community administrators
* Leaving a community

---

## Kishi — Notifications

Research how CLICK should tell users when something happens.

Consider:

* New messages
* Comments
* Reactions
* Community invitations
* School announcements
* Read/unread notifications

---

## Kitan — Media, Photos & File Sharing

Research how users can share media within CLICK.

Consider:

* Uploading images
* Viewing images
* Sharing files
* Profile pictures
* File size limitations
* Supported file types
* Removing uploaded media

---

## Charles — Home Page & Navigation

Research how users move around CLICK.

Consider:

* Home page
* Navigation menu
* Main sections
* Mobile navigation
* Desktop navigation
* Where Chat should appear
* Where Communities should appear
* Where Notifications should appear
* How users return to the home page

Think about:

> **"When someone opens CLICK, how do we help them understand where everything is?"**

---

## Kemi — Posts, Comments & Reactions

Research how users share and interact with content.

Consider:

* Creating a post
* Editing a post
* Deleting a post
* Comments
* Likes/reactions
* Viewing posts
* Basic post privacy

---

## Komi — Announcements & School Updates

Research a simple system for important information from the school.

Consider:

* School announcements
* Announcement title
* Announcement message
* Date
* Who can create announcements
* Where students see announcements
* Reading an announcement

Keep the design simple and focused.

---

## Esther — Search & Finding Content

Research how users can find things inside CLICK.

Consider:

* Searching for users
* Searching for posts
* Searching for communities
* Search results
* Basic filtering

The focus is simply:

> **"How can a user quickly find something inside CLICK?"**

---

# 5. What You Need to Produce

You do **not** need to write code yet.

For your assigned section, prepare a short architecture proposal containing:

### 1. Purpose

What is your section supposed to do?

### 2. Users

Who will use it?

### 3. Features

What should users be able to do?

### 4. User Flow

Show what happens when someone uses it.

Example:

```text
Open Chat
   ↓
Choose a person
   ↓
Open conversation
   ↓
Write message
   ↓
Send message
   ↓
Message appears in conversation
```

### 5. UI Idea

Draw or design what you think the feature could look like.

You can use:

* Paper
* Figma
* Canva
* PowerPoint
* Any suitable design tool

### 6. Information / Data

What information does your section need?

Example:

```text
Message
- sender
- receiver
- message
- date
- time
```

### 7. Connection to Other Sections

Explain what other parts of CLICK your feature might connect with.

### 8. Safety / Privacy

Think about what information should be protected and who should be allowed to perform certain actions.

### 9. Your Final Idea

Explain why you think your design is a good choice.

---

# 6. You May Use AI

You are encouraged to use AI during your research.

You may use:

* ChatGPT
* GitHub Copilot
* Gemini
* Claude
* Other suitable AI tools

But remember:

> **AI helps you think. It does not replace your thinking.**

Do not simply copy an AI answer.

Ask questions, compare ideas, and decide what makes sense for CLICK.

---

# 7. Suggested Research Prompt

You can give your AI assistant this prompt and modify it for your section:

```text
I am a student helping to design a school social platform called
CLICK — Cuddles Learning, Interaction & Community Konnect.

My assigned section is:

[INSERT YOUR SECTION]

Help me research how this type of feature could work.

Explain:

1. What the feature should do
2. Who should use it
3. Important features
4. A simple user flow
5. What information it needs
6. What the interface could contain
7. How it could connect with other parts of the application
8. Basic security and privacy concerns
9. Common mistakes to avoid

Give me different ideas where appropriate.

Do not simply design everything for me. Help me understand the
options so that I can create my own architecture.
```

---

# 8. Challenge Your AI

After your AI gives you an answer, don't immediately accept it.

Ask yourself:

> **Do I agree with this?**

> **Why did the AI suggest this?**

> **Could there be a better approach?**

> **Would this actually work for students and teachers?**

You should be able to identify at least a few things you would:

* Keep
* Change
* Remove
* Add

This is part of learning **prompt engineering and critical thinking**.

---

# 9. Sample Architecture

Here is a simple example for a **Notification System**.

### Purpose

To tell users when something important happens.

### Features

```text
New message
Comment
Reaction
Community invitation
School announcement
```

### Simple Flow

```text
Someone sends you a message
          ↓
CLICK detects the event
          ↓
Notification is created
          ↓
User sees notification
          ↓
User opens it
          ↓
User sees the related content
```

### Possible Data

```text
Notification
────────────
user
type
message
read/unread
date
```

### Possible UI

```text
┌───────────────────────────────┐
│ Notifications                 │
├───────────────────────────────┤
│ ● David commented on your post│
│   5 minutes ago               │
│                               │
│ ● You have a new message      │
│   from Charles                │
│                               │
│ ○ New school announcement     │
└───────────────────────────────┘
```

This is only a **sample**.

Your own architecture should reflect your own research and ideas.

---

# 10. How Everything Will Come Together

Each student's work is one piece of the larger CLICK system.

```text
                         CLICK
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
      USERS             CONTENT          COMMUNICATION
        │                  │                  │
     Profiles            Posts              Chat
     Accounts            Comments           Notifications
     Roles               Reactions
     Customization       Media

        ┌──────────────────┼──────────────────┐
        │                  │                  │
   COMMUNITIES          SEARCH             SAFETY
        │                  │                  │
      Groups             Users             Reports
      Members            Posts             Moderation
      Activities         Groups            Protection
```

The final architecture will be created after everyone's work has been reviewed.

---

# 11. One Project, One Architecture

Everyone is designing a **part of the same application**.

Therefore, your section must eventually fit into the larger CLICK system.

Do not independently decide that your section should use a completely different technology from everyone else.

The main technology choices will be agreed upon by the project team.

Your job is to design **how your section should work within CLICK**.

---

# 12. Future Development

Once the architecture has been reviewed and approved, we can begin implementation.

The process will become:

```text
Student Research
       ↓
Architecture
       ↓
Class Review
       ↓
Final CLICK Blueprint
       ↓
GitHub Documentation
       ↓
VS Code Development
       ↓
GitHub Copilot
       ↓
Testing
       ↓
Improvement
```

The architecture documentation will eventually help GitHub Copilot understand the project instead of forcing it to guess.

---

# 13. Final Checklist

Before submitting your work, make sure you have:

* [ ] Researched my assigned section
* [ ] Explained its purpose
* [ ] Identified the users
* [ ] Listed important features
* [ ] Created at least one user flow
* [ ] Designed a basic UI idea
* [ ] Identified the information/data required
* [ ] Explained connections to other sections
* [ ] Considered basic security/privacy
* [ ] Used AI responsibly where useful
* [ ] Questioned or improved some AI suggestions
* [ ] Explained my final design

---

# 14. The Principle

> **Think before you prompt.**
>
> **Research before you build.**
>
> **Design before you code.**
>
> **Question AI before you trust it.**

CLICK is not just about getting AI to write code.

It is about learning how to **think like the people who design the software before the software is built.**

---

**Project:** CLICK
**Full Name:** Cuddles Learning, Interaction & Community Konnect
**Tools:** GitHub · VS Code · GitHub Copilot
**Method:** Research → Architecture → Review → Development → Testing
