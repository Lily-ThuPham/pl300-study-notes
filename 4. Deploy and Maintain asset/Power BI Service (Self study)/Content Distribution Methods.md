## Comparison of Power BI Sharing Models

| Sharing Method            | What is Shared?                                                                      | Best For...                                                                                                                    | Key Features & Limitations                                                                                                                                                                                                                                                                                                     |
| ------------------------- | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Workspace Roles** 👥    | **Everything** in the workspace (all reports, dashboards, and semantic models).      | **Internal team collaboration** where all members are actively working on the same set of content.                             | <ul><li>**Four roles:** Viewer, Contributor, Member, Admin.</li><li>It's an **"all-or-nothing"** approach; you can't hide specific items.</li><li>Row-Level Security (RLS) is enforced for the **Viewer** role.</li></ul>                                                                                                      |
| **Item-level Sharing** 🔗 | A **single, specific report or dashboard**.                                          | **Granular, ad-hoc sharing** with specific individuals or small groups, including external partners.                           | <ul><li>Overcomes the "all-or-nothing" limitation of workspaces.</li><li>Recipients can view and interact but **cannot edit**.</li><li>Can share via direct access or links.</li><li>Useful when you want to maintain tighter control.</li><li>Grants access to the underlying semantic model unless RLS is applied.</li></ul> |
| **Power BI Apps** 📦      | A **curated collection** of reports, dashboards, and other content bundled together. | **Broad, formal distribution** of a finished set of content to a large audience, like a department or the entire organization. | <ul><li>Provides a streamlined, professional experience for consumers.</li><li>The workspace acts as a **staging area**, giving creators control over when updates are published.</li><li>Simplifies permission management for large audiences.</li><li>**Limitation:** A workspace can only have **one** app.</li></ul>       |
| **Publish to web** 🌐     | Sharing data with the **general public**.                                            |                                                                                                                                |                                                                                                                                                                                                                                                                                                                                |
## Workspace Roles 👥
This method grants users access to **everything** within a workspace and is best for internal teams who are actively collaborating on a set of reports. It's an "all-or-nothing" approach, as you cannot hide specific items from users who have access to the workspace. Roles can be assigned to individuals, security groups, Microsoft 365 groups, and distribution lists.
- **Viewer:** The most restrictive role. Can only view and interact with content. This is the **only role where Row-Level Security (RLS) is enforced**, making it ideal for securely sharing sensitive data with consumers.
- **Contributor:** Can create, edit, and delete content (reports, semantic models) but cannot manage workspace settings or publish the app.
- **Member:** Has all Contributor permissions, plus the ability to publish and update the app, share items, and manage data settings.
- **Admin:** Has full control over the workspace, including managing user permissions and deleting the workspace.
## Item-level Sharing 🔗
This method provides a more granular approach, allowing you to share a **single, specific report or dashboard** without granting access to the entire workspace.
- **Use Case:** Ideal for ad-hoc sharing with individuals or small groups, especially external partners, when you want to keep the rest of the workspace content private.
- **Permissions:** Recipients can view and interact with the shared item but **cannot edit it**. They also gain access to the underlying semantic model unless Row-Level Security (RLS) is applied to their account.
- **Sharing Links:** You can control access by configuring the link type:
    - **People in your organization:** Anyone with the link inside your company can view.
    - **People with existing access:** A convenient link for users who already have permission.
    - **Specific people:** Only the individuals you specify can use the link.
## Power BI Apps 📦
An app is the most professional and scalable way to distribute a **collection of related content** to a large audience. It bundles multiple reports and dashboards into a single, polished package.
- **Use Case:** Formally distributing a finished set of content to an entire department or organization.
- **Staging Area:** The workspace acts as a **staging environment**. You can make changes to your reports, test them, and then explicitly **republish the app** to release the updates to your audience. This gives you full control over when changes go live.
- **Consumer Experience:** Users can find and access the app through a direct link, from the **Apps marketplace** in the Power BI service, or have it **automatically installed** in their account if an admin configures it.
- **Limitation:** Each workspace can only have **one** published app.

## Managing Permissions for Datasets and Apps
In Power BI, it is crucial to manage data access effectively to ensure data integrity while still enabling team collaboration. Power BI provides granular permission settings at both the individual **dataset** level and the **workspace app** level.
Before changing permissions or modifying a dataset, it is critical to understand what other assets depend on it.
[[Data Lineage and Workspace Collaboration]]
### Managing Dataset-Level Permissions
This method controls who can access a single dataset and what they can do with it (e.g., read, reshare, or modify)
- **How to Access:** 
    1. In your workspace, hover over the dataset.
    2. Select **More options (...)** > **Manage Permissions**.
- **How to Grant Access:**
    1. At the top of the **Manage permissions** pane, select **Add User**.
    2. Enter the user's email address or security group name.
    3. **Configure Permissions:** Use the checkboxes to grant specific permissions. To safeguard the dataset and maintain it as a single source of truth, you would **uncheck** options like:
        - `Allow recipients to modify this dataset`
        - `Allow recipients to share this dataset`
    4. You can also grant ==**Build permission** (`Allow recipients to build content with the data associated with this dataset`)== to allow them to create their own reports from it.
- **How to Modify Access:** You can return to this pane at any time to remove or change a user's permissions by clicking the ellipsis next to their name.
### Managing App Permissions (Audiences)
This is the most powerful way to control content distribution for a large audience. It allows you to maintain one app but show **different sets of content** to different teams.
- **How to Access:**
    1. In your workspace, select the **Update app** button (you must be an Admin or Member).
    2. Navigate to the **Audience** tab.
- **How to Configure:**
    1. **Modify Existing Audiences:** You can change who is in an audience, for example, from "Entire organization" to "Specific users or groups" and enter the Sales team's security group.
    2. **Create a New Audience:**
        - Select **New audience** and give it a name (e.g., "Marketing Team").
        - **Assign Users:** Add the specific users or groups who belong to this new audience.
        - **Control Content Visibility:** Use the **eye icon** (hide/show) next to each report and dashboard in the content list to define _exactly_ what this specific audience will see. This is the key to personalizing the app.
    3. **Set Advanced Permissions (per Audience):** For each audience, you can expand the **Advanced** settings to control:
        - `Allow people to share the dataset in this app audience`
        - `Allow people to build content with the dataset in this app audience` (grants Build permission)
- **Final Step:** Once configured, select **Update app** to publish the changes to your users.