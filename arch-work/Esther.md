# CLICK — Search & Finding Content

## Student Architecture Proposal

**Assigned student:** Esther

### 1. Purpose

The Search feature will help users quickly find people, posts, and communities inside CLICK without having to scroll through the entire platform.

### 2. Users

* Students looking for classmates, posts, or communities.
* Teachers looking for students, discussions, or learning communities.
* Administrators looking for users or public content when their roles permit it.

### 3. Main Features

| Feature             | What it does                                                          |
| ------------------- | --------------------------------------------------------------------- |
| Search bar          | Allows users to type what they want to find.                          |
| Search users        | Finds people by display name or username.                             |
| Search posts        | Finds posts using words or phrases in their content.                  |
| Search communities  | Finds communities by name or description.                             |
| Search categories   | Separates results into People, Posts, and Communities.                |
| Basic filters       | Helps narrow results, such as by community or date where appropriate. |
| Recent searches     | Makes it easier to repeat a previous search.                          |
| Empty-state message | Explains when no matching results are found.                          |

### 4. User Flow

```text
Open CLICK
    ↓
Select Search
    ↓
Enter a name or keyword
    ↓
CLICK searches permitted content
    ↓
Display matching results
    ↓
Choose People, Posts, or Communities
    ↓
Apply a filter if needed
    ↓
Open the selected result
```

### 5. UI Idea

The search page could contain the following elements:

```text
┌────────────────────────────────────┐
│ CLICK                         🔔   │
├────────────────────────────────────┤
│ Search CLICK...                    │
│                                    │
│ [All] [People] [Posts] [Communities]│
│                                    │
│ Results                            │
│                                    │
│ PEOPLE                             │
│ [Photo] David Moses                │
│        @david                      │
│                                    │
│ POSTS                              │
│ [Photo] Science project discussion │
│        Shared by Kemi              │
│                                    │
│ COMMUNITIES                        │
│ [Icon] Science Club                │
│        Community description       │
└────────────────────────────────────┘
```

This is a basic wireframe to demonstrate the layout, not the final interface design.

### 6. Information / Data

The Search feature will use information already stored in other parts of CLICK. It should not create duplicate copies of users, posts, or communities.

**User result**

```text
User
- user_id
- username
- display_name
- profile_photo
```

**Post result**

```text
Post
- post_id
- author_id
- content
- created_at
- community_id (if applicable)
```

**Community result**

```text
Community
- community_id
- name
- description
- image
```

Search results should also contain enough information to open the correct profile, post, or community.

### 7. Connection to Other Sections

Search will connect with:

* **Accounts & User Roles:** Determines which users and information the current user can access.
* **Profiles:** Opens a selected user's profile.
* **Posts, Comments & Reactions:** Finds posts and opens the relevant discussion.
* **Communities & Groups:** Finds communities and opens their pages.
* **Media & File Sharing:** May help locate publicly searchable posts containing media.
* **Moderation & Safety:** Ensures removed or restricted content is not improperly exposed.
* **Home Page & Navigation:** Provides an accessible entry point to Search.

### 8. Safety & Privacy

* Users should only find information they are permitted to access.
* Private messages must not appear in public search results.
* Private profiles and restricted community content must respect their access rules.
* Deleted or moderator-removed content should not remain accessible through search.
* Search input should be validated to prevent malicious input.
* Recent searches should not be exposed to other users on a shared account.
* Search results should not reveal private contact details or other restricted information.

### 9. Final Idea

I recommend one search bar with three main categories: **People, Posts, and Communities**.

Users can begin with a keyword and then select the category they want. Basic filters can help them narrow down the results without making the feature complicated.

This design is suitable for CLICK because it is easy to understand, works across different sections of the platform, and can be improved later as the application grows.
