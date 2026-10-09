# CLICK — Authentication, Accounts & User Roles

## 1. The Overall Idea

Think of Authentication, Accounts & User Roles as the **identity and access system of CLICK**.

> It answers three fundamental questions: Who is this person? What account do they have? What are they allowed to do?

The system supports other parts of CLICK, including the feed, groups, messaging, notifications, and moderation.

```text
                         CLICK
                           |
                           v
              AUTHENTICATION & ACCOUNTS
                           |
            +--------------+--------------+
            |              |              |
            v              v              v
         Identity         Roles       Permissions
            |              |              |
            +--------------+--------------+
                           |
                           v
                     CLICK FEATURES
                      /    |    \
                     v     v     v
                   Feed  Groups Messaging
```

**Key idea:** Authentication is not just a login screen. It is a foundation that other parts of CLICK use to determine identity and access.

---

## 2. Who Should Use It?

CLICK could support several types of users. The team does not necessarily need every role listed below; it should choose roles that fit the school's needs.

```text
CLICK USERS
    |
    +-- Students
    +-- Teachers / Lecturers
    +-- School Staff
    +-- Moderators
    +-- School Administrators
```

### Student

A student might be able to:

- Manage their profile.
- Join permitted communities.
- Create posts.
- Comment and react.
- Participate in discussions.
- RSVP to events.
- Receive announcements.

### Teacher / Lecturer

A teacher could have additional capabilities:

- Create class communities.
- Post academic content.
- Create announcements.
- Moderate discussions.
- Manage certain class activities.

### Moderator

A moderator could focus mainly on safety:

- Review reports.
- Remove inappropriate content.
- Warn users.
- Escalate serious issues.

### School Administrator

An administrator could manage the wider platform:

- Accounts and user roles.
- Classes and communities.
- School announcements.
- Suspended accounts.
- Moderation settings.

### Questions to consider

- Does CLICK need a separate moderator role?
- Should club leaders have special permissions within their clubs?
- Should teachers be able to manage only their own classes or the entire school community?

---

## 3. Authentication

Authentication is the process of verifying that someone is associated with the account they are trying to access.

```text
User
 |
 v
Enter login information
 |
 v
CLICK verifies credentials
 |
 v
Authentication successful?
 |                       |
 No                      Yes
 |                       |
 v                       v
Show error          Identify account
                         |
                         v
                    Identify role
                         |
                         v
                  Load permissions
                         |
                         v
                     Enter CLICK
```

### Option A — School ID + Password

The user enters their school-issued ID and password.

**Advantages**
- Simple and school-focused.
- May work for students who do not have school email accounts.

**Disadvantages**
- Students may forget their IDs or passwords.
- School IDs should not be exposed unnecessarily.

### Option B — School Email + Password

The user logs in with a school email address and password.

**Advantages**
- Familiar login method.
- Can work well if every student already has a school account.

**Disadvantages**
- Requires school email accounts.
- Account recovery depends on access to the email account.

### Option C — School-Created Accounts

The school creates accounts before students use CLICK.

```text
School creates account
        |
        v
Student receives login details
        |
        v
Student logs in
        |
        v
Student completes profile
```

**Advantages**
- Gives the school greater control over membership.
- Reduces the risk of people outside the school registering.

**Disadvantages**
- Requires a process for creating and maintaining accounts.
- Someone must handle incorrect details and account recovery.

The team could also consider a combination, such as school-created accounts with school email login.

---

## 4. Account Structure

An account involves more than a username and password.

```text
USER
 |
 +-- Account
 |    +-- User ID
 |    +-- Login identifier
 |    +-- Password credential
 |    +-- Account status
 |
 +-- Profile
 |    +-- Display name
 |    +-- Profile picture
 |    +-- Class information
 |
 +-- Role
 |    +-- Student / Teacher / Admin / etc.
 |
 +-- Permissions
      +-- Create posts
      +-- Manage groups
      +-- Moderate content
      +-- Manage users
```

Separating account information from profile information can make the system easier to maintain. For example, changing a profile picture should not require changing login credentials.

This is a conceptual model, not a final database design.

---

## 5. User Roles and Permissions

One major architectural decision is how CLICK determines what each user can do.

A simple starting model might be:

```text
Student
 +-- View community
 +-- Create posts
 +-- Comment
 +-- Join permitted groups

Teacher
 +-- Student capabilities, where appropriate
 +-- Create class groups
 +-- Post authorized announcements

Administrator
 +-- Manage users
 +-- Manage roles
 +-- Manage communities
 +-- Manage platform settings
```

### What is RBAC?

**RBAC** means **Role-Based Access Control**. Users receive permissions based on their assigned roles.

For example:

```text
Role
 |
 v
Permissions
 |
 v
Allowed actions
```

Possible permission names include:

```text
Student
 +-- create_post
 +-- comment
 +-- join_group

Teacher
 +-- create_class_group
 +-- create_announcement

Administrator
 +-- manage_users
 +-- assign_roles
```

The system should not trust a user to choose their own privileged role. Role assignments need to be verified and protected.

### A design choice

The team could use:

- **Simple RBAC:** a small set of roles with predefined permissions.
- **More granular RBAC:** individual permissions can be assigned to roles, allowing more flexibility.

Simple RBAC may be easier for an early version. More detailed permissions may become useful as CLICK grows.

---

## 6. Simple User Flows

### New Student

```text
Receive CLICK account
        |
        v
Open CLICK
        |
        v
Log in
        |
        v
Verify account
        |
        v
Complete profile
        |
        v
Confirm class information
        |
        v
Enter Community
```

### Returning Student

```text
Open CLICK
    |
    v
Log in
    |
    v
Authenticate account
    |
    v
Load role and permissions
    |
    v
Open CLICK Home
```

### Administrator

```text
Log in
    |
    v
Authenticate account
    |
    v
Verify administrator permissions
    |
    v
Open CLICK
    |
    v
Access authorized admin tools
```

**Important distinction:** Logging in does not automatically give someone permission to perform every action.

---

## 7. What Information Does It Need?

Consider separating information into categories.

### Identity

- User ID.
- Display name.
- School ID, if needed.
- School.
- Class or year group, if relevant.

### Authentication

- Login identifier.
- Secure password credential.
- Account status.
- Recovery information, if needed.

### Profile

- Profile picture, optional.
- Bio, optional.
- Interests, optional.
- Class or community information, where appropriate.

### Authorization

- Assigned role.
- Permissions associated with that role.
- Community memberships.

### Account Management

- Account creation date.
- Session information.
- Suspension or disabled status.
- Security activity, where appropriate.

Do not automatically collect every field. Ask: **Does CLICK actually need this information?** Collecting less information can reduce privacy risks and simplify the system.

---

## 8. What Could the Interface Contain?

These are examples of possible interface components, not final designs.

### Login Screen

```text
+---------------------------------------+
|                 CLICK                 |
|                                       |
| Cuddles Learning, Interaction &       |
| Community Konnect                     |
|                                       |
| School ID / Email                     |
| [_______________________________]     |
|                                       |
| Password                              |
| [_______________________________]     |
|                                       |
|              [ LOG IN ]               |
|                                       |
| Forgot password?                      |
+---------------------------------------+
```

### Account Settings

```text
ACCOUNT

Profile
 +-- Display name
 +-- Profile picture
 +-- Class information

Security
 +-- Change password
 +-- Review active sessions
 +-- Log out

Privacy
 +-- Profile visibility
 +-- Messaging settings
```

### Admin Account Management

```text
USER MANAGEMENT

Search users [________________]

Name          Role          Status
Daniel        Student       Active
Sarah         Student       Active
Mr. James     Teacher       Active

[View] [Edit] [Suspend]
```

The interface can show different tools depending on the user's role. However, hiding a button is not enough to secure an action; the backend must also check permissions.

---

## 9. How It Connects to Other Parts of CLICK

Authentication and accounts connect to almost every major CLICK feature.

```text
                     USER ACCOUNT
                          |
          +---------------+----------------+
          |               |                |
          v               v                v
       Profile           Role          Permissions
          |               |                |
          +---------------+----------------+
                          |
                          v
                      CLICK APP
                     /    |     \
                    v     v      v
                  Feed  Groups  Messaging
                    |     |       |
                    v     v       v
                  Posts Members Conversations
```

### Feed

When someone creates a post, CLICK needs to know which account created it. The post can reference the user's unique account ID.

### Groups

A group may have an owner, moderators, and members. CLICK checks the user's membership and permissions before allowing group actions.

### Announcements

CLICK should verify whether a user is allowed to publish an official school announcement. A normal student post and an official announcement should not be treated as equivalent.

### Notifications

The account system provides the identity needed to determine which user should receive a notification.

### Moderation

Reports and moderation actions need to be associated with the relevant content and accounts, while access to sensitive moderation information should be limited.

---

## 10. Security and Privacy

Because CLICK is a school platform, security and privacy should be considered from the beginning.

### Password Security

- Never store passwords as plain text.
- Use a reputable authentication system or appropriate password hashing.
- Protect login traffic with HTTPS.
- Provide a safe password-recovery process.

### Authorization

Do not rely only on hiding buttons in the interface.

For example, hiding a "Delete User" button from students is not enough. The backend must check whether the person making the request is actually allowed to delete an account.

### Student Privacy

Consider who should be able to see:

- Full names.
- Class information.
- Profiles.
- Posts.
- Private messages.
- Student IDs.
- Contact information.

Not every piece of information needs to be visible to every user.

### Sessions

Consider:

- Secure session handling.
- Session expiration.
- Logout.
- Revoking sessions after a password change or account compromise.
- Reviewing active sessions, if appropriate.

### Least Privilege

Give each user only the permissions needed for their responsibilities. For example, a moderator may need to review reports without having permission to change school-wide account settings.

### Data Minimization

Avoid collecting information that CLICK does not need. Student data should be accessed only for appropriate purposes and by authorized people.

---

## 11. Common Mistakes

### Mistake 1 — Treating Authentication as Just a Login Page

Authentication also involves account verification, session management, account recovery, and related processes.

### Mistake 2 — Letting Users Choose Privileged Roles

Avoid letting someone select "Administrator" during registration and immediately receive administrator permissions. Privileged roles need a trusted assignment process.

### Mistake 3 — Giving Everyone the Same Permissions

Students, teachers, moderators, and administrators may have different responsibilities. Their permissions should reflect those responsibilities.

### Mistake 4 — Securing Only the Frontend

Hiding a button does not prevent someone from trying to call the backend directly. Sensitive actions must be authorized on the server.

### Mistake 5 — Collecting Unnecessary Information

More account fields do not automatically make the platform better. Collect only what is needed.

### Mistake 6 — Ignoring the Account Lifecycle

Think about what happens when:

```text
Account created
      |
      v
Active
      |
      +-- Class changes
      |
      +-- Role changes
      |
      +-- Password reset
      |
      +-- Suspended / Disabled
      |
      +-- Student graduates or leaves
```

CLICK needs a sensible process for each relevant situation.

---

## 12. Possible Architecture

One conceptual architecture could look like this:

```text
                       CLICK
                         |
                         v
              AUTHENTICATION SYSTEM
                         |
             +-----------+-----------+
             |           |           |
             v           v           v
          Identity      Roles      Sessions
             |           |           |
             +-----------+-----------+
                         |
                         v
                   ACCESS CONTROL
                         |
             +-----------+-----------+
             |           |           |
             v           v           v
           Feed        Groups     Messaging
             |           |           |
             +-----------+-----------+
                         |
                         v
                  ACCOUNT DATA LAYER
                         |
             +-----------+-----------+
             |           |           |
             v           v           v
           Users      Profiles   Memberships
```

Possible database entities to investigate include:

```text
users
profiles
roles
permissions
role_permissions
sessions
schools
classes
class_members
community_memberships
```

These are candidate entities, not a mandatory schema. For example, the team should decide whether class membership belongs in a separate table and whether CLICK needs multiple schools or just one.

---

## 13. Decisions for the Development Team

The purpose of this section is to help the team make informed choices, not to lock the architecture before requirements are clear.

### Account Creation

Possible options:

- School-created accounts.
- Student registration with school verification.
- Invitation-based registration.
- A combination of these approaches.

### Login Method

Possible options:

- School ID and password.
- School email and password.
- Both, if the system can safely support them.
- School single sign-on, if an existing school identity provider is available.

### Roles

Possible options:

**Simple roles**
- Student.
- Teacher.
- Administrator.

**More detailed roles**
- Student.
- Teacher.
- Moderator.
- Club Administrator.
- School Administrator.
- System Administrator.

Use only the roles that have a clear purpose.

### Permissions

Possible options:

- Simple permissions attached to each role.
- More granular role-based permissions.
- Additional checks based on context, such as whether a teacher manages a particular class.

### Profile Visibility

Possible options:

- Visible to the school community.
- Visible only to class or group members.
- Controlled by selected privacy settings.
- A combination of these options.

---

## 14. Suggested Development Phases

A phased approach can help the team avoid trying to build everything at once.

### Phase 1 — Foundation

- Account creation or provisioning.
- Login and logout.
- Basic profiles.
- Initial roles and permissions.
- Account status handling.

### Phase 2 — Account Management

- Password recovery.
- Profile editing.
- Class and school membership.
- Administrator account management.

### Phase 3 — Security and Privacy

- Server-side authorization checks.
- Secure session management.
- Privacy settings.
- Account suspension and recovery procedures.
- Appropriate audit records for sensitive actions.

### Phase 4 — Integration

- Connect accounts to posts and comments.
- Connect roles to groups and announcements.
- Connect accounts to notifications.
- Connect account status to moderation workflows.

The exact phases should depend on the team's timeline, technology, and school requirements.

---

## 15. The Key Idea

If CLICK's Community section is the digital campus, **Authentication, Accounts & User Roles provide the identity and access foundation beneath that campus**.

```text
                         CLICK
                           |
                           v
                    WHO ARE YOU?
                           |
                           v
                    Authentication
                           |
                           v
                    WHAT ACCOUNT?
                           |
                           v
                         Profile
                           |
                           v
                   WHAT CAN YOU DO?
                           |
                           v
                          Roles
                           |
                           v
                      Permissions
                           |
              +------------+------------+
              |            |            |
              v            v            v
            Feed         Groups      Messaging
```

Keep these two concepts distinct:

- **Authentication:** verifying who a user is.
- **Authorization:** deciding what that user is allowed to do.

Use this document as a starting point for discussion. Your team should confirm the requirements, choose the roles and permissions, and then develop the detailed database design and implementation plan.
