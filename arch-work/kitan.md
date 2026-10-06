Kitan — Media, Photos & File Sharing
1. The overall idea

Think of Kitan as the media and file-sharing system of CLICK.

It answers three fundamental questions:

What is being shared?
Who is sharing it?
Who is allowed to access it?

The system sits underneath features such as:

                         CLICK
                           │
                           ↓
              MEDIA & FILE SHARING
                           │
          ┌────────────────┼────────────────┐
          ↓                ↓                ↓
       Upload           Storage          Sharing
          │                │                │
          └────────────────┼────────────────┘
                           ↓
                    CLICK FEATURES
                           │
             ┌─────────────┼─────────────┐
             ↓             ↓             ↓
           Feed         Messaging       Groups
             │             │             │
             └─────────────┼─────────────┘
                           ↓
                    School Community

The important idea is that Kitan shouldn't just be treated as an "upload button."

It provides the infrastructure for storing, displaying, sharing, and controlling access to media throughout CLICK.

2. What can users share?

Kitan could support several types of content:

MEDIA
│
├── Photos
├── Videos
├── Documents
├── PDFs
├── Audio
└── Other files

You don't necessarily need to support every type initially.

A basic implementation could start with:

Images
Videos
Documents
PDFs

Additional file types can be added later.

3. Basic media flow

A simple upload flow could be:

User
  ↓
Select file
  ↓
Kitan receives file
  ↓
Validate file
  ↓
Store file
  ↓
Create media record
  ↓
Generate media reference
  ↓
Attach to CLICK feature
  ↓
Feed / Group / Message

For example:

Student
   ↓
Selects photo
   ↓
Kitan
   ↓
Photo stored
   ↓
Photo ID created
   ↓
Student creates post
   ↓
Post references photo
   ↓
Other users view photo
4. Media structure

A media item shouldn't just be:

filename

It could contain information such as:

MEDIA
│
├── Media ID
├── Owner
├── File name
├── File type
├── File size
├── Storage location
├── Upload date
├── Visibility
└── Status

For example:

Media
├── id
├── owner_id
├── filename
├── mime_type
├── size
├── storage_key
├── created_at
├── visibility
└── status

The actual file and the information about the file should be treated separately.

5. Storage

Kitan needs somewhere to keep uploaded files.

A simple architecture could be:

                  KITAN
                    │
                    ↓
              Upload Service
                    │
                    ↓
              File Storage
                    │
          ┌─────────┼─────────┐
          ↓         ↓         ↓
        Photos    Videos    Documents

The database doesn't necessarily need to contain the entire file.

Instead:

Database
   │
   └── Media metadata
          │
          └── Storage reference
                    │
                    ↓
                File Storage

For example:

media
│
├── id
├── owner_id
├── filename
├── mime_type
├── size
└── storage_key

The storage_key points to where the actual file is stored.

6. Sharing media

Kitan becomes particularly useful when media can be shared throughout CLICK.

A user could:

Select media
     ↓
Choose destination
     ↓
┌───────────────┐
│ Feed          │
│ Group         │
│ Conversation  │
└───────────────┘
     ↓
Share

For example:

Feed
User
 ↓
Upload photo
 ↓
Create post
 ↓
Attach photo
 ↓
Publish
Messaging
User
 ↓
Open conversation
 ↓
Select file
 ↓
Upload
 ↓
Send
Groups
User
 ↓
Open group
 ↓
Select media
 ↓
Upload
 ↓
Post media
7. Media permissions

Not every file should automatically be visible to everyone.

Kitan could use visibility levels such as:

VISIBILITY
│
├── Public / School-wide
├── Community-only
├── Class-only
├── Conversation-only
└── Private

For example:

Student uploads assignment
          ↓
      Class-only
          ↓
    Class members
          ↓
       Can view

While:

Student uploads profile photo
          ↓
     School-wide
          ↓
   Other users can view

The exact visibility model can be decided by the team.

8. How Kitan connects to CLICK

Kitan should function as infrastructure underneath other CLICK features.

                         CLICK
                           │
                           ↓
                         KITAN
                           │
          ┌────────────────┼────────────────┐
          ↓                ↓                ↓
        Feed           Messaging          Groups
          │                │                │
          ↓                ↓                ↓
        Posts        Conversations     Group Posts
          │                │                │
          └────────────────┼────────────────┘
                           ↓
                    Media References
                           │
                           ↓
                      File Storage
Feed

A post can reference one or more media items:

Post
│
├── Post ID
├── Author
├── Text
└── Media
      ├── Image
      ├── Image
      └── Video
Messaging

A message could contain:

Message
│
├── Sender
├── Text
└── Attachment
       │
       └── Media ID
Groups

A group post could contain:

Group Post
│
├── Author
├── Content
└── Media
      └── Media ID

This means the other CLICK systems don't need to manage actual files themselves.

They simply reference Kitan media records.

9. Basic database structure

A starting model could be:

users
│
└── media
      │
      ├── media_files
      ├── media_access
      └── media_links

Or more explicitly:

users
│
├── id
└── ...

media
│
├── id
├── owner_id
├── filename
├── mime_type
├── size
├── storage_key
├── visibility
├── status
└── created_at

media_access
│
├── media_id
├── user_id
└── permission

media_links
│
├── media_id
├── target_type
└── target_id

media_links could allow Kitan to connect media to different CLICK features.

For example:

media_id: 123
target_type: post
target_id: 456

Or:

media_id: 123
target_type: message
target_id: 789
10. Security & privacy

Because Kitan handles user files, security should be considered from the beginning.

File validation

Kitan should check:

File
 ↓
Type validation
 ↓
Size validation
 ↓
Security checks
 ↓
Storage

For example, the system could enforce maximum file sizes and only allow supported file types.

Authorization

Don't rely only on hiding download buttons.

For example:

User requests file
        ↓
Kitan checks:
        ↓
Does this user have access?
        │
     ┌──┴──┐
    YES    NO
     ↓      ↓
  Return   Deny
   file    access

The backend should enforce access permissions.

Private media

Private files should not simply have publicly guessable storage URLs.

The application should control access to protected media.

11. Common mistakes
❌ Treating Kitan as just an upload button

Kitan needs to handle:

Uploading
Storage
Metadata
Sharing
Permissions
Retrieval
❌ Storing everything directly in the database

Large media files can make database storage inefficient.

A better approach is usually:

Database → Metadata
Storage  → Actual file
❌ Trusting the frontend

The frontend saying:

"User can access this file"

doesn't make it true.

The backend must verify access.

❌ Giving every file the same visibility

A private message attachment shouldn't automatically become school-wide.

❌ Forgetting file limits

Without limits, users could upload extremely large files and consume unnecessary storage.

12. Possible architecture

A basic Kitan architecture could eventually look like:

                         CLICK
                           │
                           ↓
                     KITAN SYSTEM
                           │
             ┌─────────────┼─────────────┐
             ↓             ↓             ↓
          Upload        Storage       Access
             │             │             │
             └─────────────┼─────────────┘
                           ↓
                    MEDIA DATABASE
                           │
             ┌─────────────┼─────────────┐
             ↓             ↓             ↓
          Metadata      Ownership      Links
                           │
                           ↓
                    CLICK FEATURES
             ┌─────────────┼─────────────┐
             ↓             ↓             ↓
           Feed        Messaging        Groups

At the database level:

users
  │
  ↓
media
  │
  ├── media_access
  │
  └── media_links
          │
          ├── posts
          ├── messages
          └── groups
13. What I'd leave for the team to decide

Your team can decide:

Supported files
A. Images only
B. Images + videos
C. Images + videos + documents
D. All common file types
Storage
A. Local storage
B. Cloud/object storage
C. Combination
Maximum file size
A. Small files only
B. Different limits by file type
C. Configurable limits
Visibility
A. Public + private
B. School + class + private
C. School + community + class + private
Sharing
A. Feed
B. Messaging
C. Groups
D. All CLICK features
Media lifecycle
Uploaded
   ↓
Active
   ↓
Referenced
   ↓
Deleted
   ↓
Removed from storage
The key idea for Kitan

If the Authentication & Accounts section is the identity foundation underneath CLICK, then Kitan is the media foundation underneath CLICK.

                         CLICK
                           │
                           ↓
                     ┌───────────┐
                     │   KITAN   │
                     └───────────┘
                           │
             ┌─────────────┼─────────────┐
             ↓             ↓             ↓
          Upload        Storage        Access
             │             │             │
             └─────────────┼─────────────┘
                           ↓
                     Media Records
                           │
             ┌─────────────┼─────────────┐
             ↓             ↓             ↓
           Feed        Messaging        Groups
             │             │             │
             └─────────────┼─────────────┘
                           ↓
                    School Community
