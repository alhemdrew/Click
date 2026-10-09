1. Introduction

The Communities & Groups feature will allow students and teachers at Cuddles to connect with others who share similar interests, hobbies, subjects, or activities.

Users will be able to create communities, join existing ones, participate in discussions, view community information, and interact with other members.

The purpose is to encourage learning, teamwork, creativity, and communication within the school community.

2. Main Objectives

The Communities & Groups feature aims to:

Help students and teachers connect through shared interests.
Provide organised spaces for discussions and collaboration.
Allow users to create and manage communities.
Make it easy to discover and join relevant communities.
Encourage respectful and safe interactions.
Support school clubs, academic groups, and extracurricular activities.
3. Creating Communities
Description

Users should be able to create communities based on interests, subjects, clubs, or activities.

Proposed Requirements
Users should be able to enter a community name and description.
Users should be able to select a category.
Each community should have a unique identifier.
The person who creates a community should initially become its administrator.
Community creators should be able to edit community information if they have the required permissions.
The system should prevent invalid or duplicate community creation where necessary.
Example

A student creates a community called "Young Programmers" for students interested in learning programming and developing projects together.

4. Joining Communities
Description

Users should be able to discover and join communities that interest them.

Proposed Requirements
Users should be able to browse available communities.
Users should be able to view community information before joining.
The system should support open communities and, if approved by the project team, communities requiring administrator approval.
Users should not be able to join the same community multiple times.
The system should update membership information when someone joins.
Users should receive clear feedback when their join request succeeds or fails.
Example

A student finds the Young Programmers community and selects "Join Community."

If membership is open, the student becomes a member immediately. If approval is required, the student receives a pending status until an administrator makes a decision.

5. Community Members
Description

Each community should have a members section showing the people who belong to it.

Proposed Requirements
Members should be able to view the community's member list, subject to its privacy settings.
The list should display appropriate profile information, such as usernames and profile pictures.
Community roles should be clearly identified where appropriate.
The system should keep membership records accurate.
Members who leave should no longer appear as active members.
Only authorised users should be able to perform membership-management actions.
Example

The Young Programmers community displays its members, including students and teachers who have joined.

6. Community Posts
Description

Community posts will allow members to share ideas, questions, updates, and information related to the community.

Proposed Requirements
Authorised members should be able to create community posts.
Posts should identify their authors and display their publication dates.
Members should be able to view posts they have permission to access.
The platform should reuse CLICK's shared Posts, Comments & Reactions features rather than create a separate, duplicate posting system.
Community posts should follow CLICK's moderation and safety rules.
The system should respect the permissions of users who create, edit, or remove posts.
Example

A member of the Young Programmers community creates a post asking if anyone wants to collaborate on a JavaScript game.

Other members can participate using the platform's approved interaction features.

7. Community Information
Description

Every community should have an information page explaining its purpose and important details.

Proposed Requirements

A community information page should support:

Community name.
Description.
Category.
Administrator information.
Membership information.
Community rules.
Creation date, if needed.
Membership settings, where appropriate.

Authorised administrators should be able to update community information.

Users should be able to view the information they need to decide whether the community is suitable for them.

8. Community Administrators
Description

Community administrators will be responsible for managing their communities and helping members follow the rules.

Proposed Requirements
The community creator should initially become an administrator.
The system should support authorised administrators managing community information.
Administrators should be able to manage membership according to their permissions.
Administrators should be able to use the platform's approved moderation tools.
The system should support more than one administrator if the project team approves this feature.
Administrative permissions should be separate from ordinary membership permissions.
The system should prevent a community from being left without an administrator.
Changes to administrator roles should be restricted to authorised users.
Example

An administrator updates the community description and handles a report about an inappropriate post using CLICK's moderation system.

9. Leaving a Community
Description

Members should be able to leave communities they no longer wish to participate in.

Proposed Requirements
Members should have access to a "Leave Community" option.
The system should update the membership record after a successful departure.
Users should receive confirmation that they have left.
Leaving should remove the user's membership permissions.
The system should define what happens to posts the user created before leaving.
Administrators should be required to transfer their responsibilities or arrange another administrator before leaving, if they are the last administrator.
Example

A student selects "Leave Community" and confirms their decision. The system removes their active membership while preserving existing posts according to the platform's agreed content policy.

10. User Roles and Permissions

The following permissions are proposed for team review.

Ordinary Member
View community information they are permitted to access.
Participate in community discussions.
View the member list where permitted.
Leave the community.
Community Administrator
Perform ordinary member activities.
Edit community information.
Manage membership within their authority.
Use approved community-management and moderation tools.
Assign or transfer administrator responsibilities if authorised.
Student or Teacher Who Has Not Joined
Discover communities available to them.
View information permitted by the community's privacy settings.
Join open communities or request membership where required.
Platform Administrator or Authorised Moderator
Carry out platform-wide or moderation duties according to their assigned permissions.
Handle reported content through CLICK's shared moderation system.

A person's school role and their role within an individual community should be treated separately. For example, being a teacher should not automatically grant someone administrator permissions in every community.

11. Connections to Other CLICK Features

The Communities & Groups feature must work with the other parts of CLICK.

Authentication, Accounts & User Roles

The system must identify the signed-in user and verify their permissions before allowing protected actions.

Profile & Personalization

Community pages may display appropriate profile information from the shared profile system.

Posts, Comments & Reactions

Community discussions should use the shared content and interaction features.

Moderation, Reporting & Safety

Community content and member interactions should follow CLICK's safety rules and reporting process.

Notifications

The platform may notify users about relevant community activity, depending on the agreed notification features and user settings.

Media, Photos & File Sharing

Community posts may support permitted images and files if the shared media system allows them.

Search & Finding Content

Users should be able to discover communities through the shared search system.

Home Page & Navigation

Users should have a clear way to access the Communities section.

These connections should be agreed upon by the relevant section owners before implementation.

12. Data Requirements

The system will need to store information about communities and their members.

Community
Unique community ID.
Community name.
Description.
Category.
Creator or original owner ID.
Creation date.
Membership settings.
Community status.
Membership
Community ID.
User ID.
Community role.
Date joined.
Membership status.
Community Posts

Community posts should use CLICK's shared post system, with a reference connecting each post to the relevant community.

The exact fields should be agreed upon with the Posts, Comments & Reactions section owner.

Administrator Information

Administrator roles should be linked to the relevant user and community, rather than stored as an unverified label.

The final database structure should be designed with the project's architecture team.

13. Safety and Privacy

Because CLICK is a school social platform, communities should be designed with student safety in mind.

Proposed safeguards include:

Only authorised users should be able to access protected community features.
Private community information should only be visible to permitted users.
Community administrators should have clearly defined permissions.
Members should be able to report inappropriate content through the shared reporting system.
Personal information should not be displayed unnecessarily.
Community rules should encourage respectful behaviour.
Administrative actions should be protected against unauthorised use.
Community membership and content should follow the school's policies.
14. Open Questions for the Coding Club

Before development begins, the team should decide:

Can both students and teachers create communities?
Should communities be open, approval-based, or support both options?
Can users belong to multiple communities?
Can every community have several administrators?
Who can delete or archive a community?
What happens to a community if its creator leaves?
Should community posts be visible to non-members?
Which community features are essential for the first version of CLICK?
Can administrators remove members directly, or must some cases go through moderation?
How should the platform handle communities that become inactive?

These decisions should be recorded in the shared project documentation so that developers and AI coding tools do not have to guess.

15. Acceptance Criteria

The Communities & Groups feature should be considered ready for release testing when the agreed requirements can be demonstrated.

Examples include:

An authorised user can create a community.
The system rejects invalid community details.
A user can join an eligible community.
Duplicate membership is prevented.
Community members can view permitted community information.
Authorised members can create community posts using CLICK's shared posting system.
Unauthorised users cannot perform administrator actions.
A member can leave a community successfully.
Administrator responsibilities are preserved when an administrator leaves.
Community membership and permissions remain consistent across the platform.
Reporting and moderation features work with community content.

The team should convert these criteria into specific tests before the feature is released.

Conclusion

The Communities & Groups feature will provide an organised space for students and teachers to connect around shared interests and activities.

A clear set of requirements, user permissions, data needs, and connections to other CLICK features will help the coding club build a consistent system.

By agreeing on the design before coding begins, the team can reduce duplicated functionality, avoid conflicting assumptions, and make future improvements easier.
