[Learn more about the details of creating workspaces](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-create-the-new-workspaces).
**Power BI service workspaces** are specialized, containerized environments that act like dedicated rooms for organizing and managing distinct datasets, reports, and dashboards. They are essential for efficient data management, especially when handling numerous data assets.
Workspaces are the central places in the Power BI service for collaborating with colleagues to create and manage collections of content, such as datasets, reports, and dashboards. 
Types of Workspaces 
- **My Workspace** 
- **Shared workspaces**

## Advantages of using Workspaces (Coursera)
- **Organization**: Each workspace serves as a unique container for related reports, dashboards, and datasets. This structure helps keep data assets tidy and easy to locate.
- **Access Control**: Workspaces provide robust access control features to safeguard data from unauthorized users. You can define specific permissions to determine who can view or edit the content, which is crucial when working with confidential data.
- **Collaboration**: Shared workspaces are designed for team collaboration, functioning like conference rooms where analysts can collectively discuss, build, and refine data insights.
- **Streamlined Updates**: Having all related assets in a structured workspace makes updating projects much more efficient. Whether pulling in new data or revising visualizations, a well-organized workspace ensures consistency and clarity.
---
## Best Practice for Workspaces management (Coursera)
- **Regular Cleanup**: Periodically review your workspace and remove outdated or irrelevant reports and datasets. This proactive approach ensures optimal performance and prevents confusion.
- **Clear Naming Conventions**: Establish and adhere to clear naming conventions for all data assets (reports, dashboards, datasets). Consistency aids in easy retrieval and is especially beneficial in shared workspaces.
- **Frequent Review of Access Controls**: Continually monitor and assign access levels based on user roles and responsibilities. This is essential for maintaining data security and preventing unintended modifications.
- **Regular Backups**: Safeguarding your work is paramount. Implement a regular backup schedule to protect against unexpected data loss and ensure project continuity, which is vital on large teams.
- **Encourage Collaboration and Feedback**: Foster a culture of open discussion and continuous feedback. Actively seeking and implementing suggestions from team members helps to refine data visualizations, optimize reports, and create a more collaborative and effective environment.

---
## Workspace Audiences
**Workspace audiences** are a feature of Power BI Apps that allow you to show different sets of content (reports, dashboards, links) to different groups of users, all from within a single app.
#### Managing Audiences in Workspace Apps
**Workspace audiences** are a feature of Power BI Apps that allow you to show different sets of content (reports, dashboards, links) to different groups of users, all from within a single app.
This is useful for personalizing content and ensuring users only see data that is relevant to their roles, rather than creating multiple separate apps for different teams.
#### Advantages of Using Audiences
- **Personalized Content:** You can tailor the data landscape to meet the diverse needs of different departments or teams.
- **Improved User Experience:** Users don't have to sift through irrelevant data; they are guided directly to the content that is pertinent to them. This also enhances data storytelling within the app.
- **Simplified Management:** You can manage content visibility for many different groups from a single workspace and a single app, which is more efficient than managing multiple apps or workspaces.
#### The User Experience
- For an end-user, each audience they belong to appears as a **tab** at the top of the app's navigation.
- If a user belongs to only one audience, they will see only the content for that group.
- If a user belongs to multiple audiences, they can switch between the different views by selecting the corresponding tabs.
#### How to Configure an Audience
You configure audiences on the **Audience** tab during the app creation or update process.
1. **Create and Name the Audience:** Select **New Audience** to create a new group. You can double-click the name to rename it (e.g., "Sales Reports," "Internal Users").
2. **Set Content Visibility:** For the selected audience, use the **hide/show eye symbol** next to each item in the content list to control which reports, dashboards, and links are visible to that specific group.
3. **Assign Users:** In the **Manage audience access** pane, specify the users or security groups that belong to this audience.

---
## Workspace License Modes

The license mode determines the features available and who can access the content.

- **Pro:** Suitable for small to medium teams. All users who create or view content in a Pro workspace must have a Pro license. It does not support advanced features like larger model sizes.
- **Premium Per User (PPU):** Includes all Pro features plus advanced capabilities like AI features and larger model sizes. Content in a PPU workspace can only be accessed by other users who also have a PPU license. A diamond-with-person icon ( 💎👤) identifies these workspaces.
- **Fabric Capacity:** An enterprise-grade option with dedicated cloud resources (a capacity). It supports all advanced features, real-time streaming, and allows for the creation of other Fabric items like data warehouses. A diamond icon (💎) identifies these workspaces.
---
## Comparison of Workspace Roles
[Roles in workspaces in Power BI - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-roles-new-workspaces)
Knowing the exact differences between the four roles is frequently tested. Use this table to compare their key permissions.

| Permission / Action                                                                        | Admin                                                                  | Member                                                                                   | Contributor                                                                                                    | Viewer                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Workspace Management**                                                                   |                                                                        |                                                                                          |                                                                                                                |                                                                                                                                                                                                 |
| Delete the workspace                                                                       | ✅                                                                      | ❌                                                                                        | ❌                                                                                                              | ❌                                                                                                                                                                                               |
| Add or modify user roles (including other Admins)                                          | ✅                                                                      | ❌                                                                                        | ❌                                                                                                              | ❌                                                                                                                                                                                               |
| Update workspace metadata                                                                  | ✅                                                                      | ❌                                                                                        | ❌                                                                                                              | ❌                                                                                                                                                                                               |
| Configure workspace settings (e.g., Contact list)                                          | ✅                                                                      | ✅                                                                                        | ❌                                                                                                              | ❌                                                                                                                                                                                               |
| **Content Management**                                                                     |                                                                        |                                                                                          |                                                                                                                |                                                                                                                                                                                                 |
| Create, edit, and delete reports, dashboards, datasets                                     | ✅                                                                      | ✅                                                                                        | ✅                                                                                                              | ❌                                                                                                                                                                                               |
| View and interact with content                                                             | ✅                                                                      | ✅                                                                                        | ✅                                                                                                              | ✅                                                                                                                                                                                               |
| Share items (reports, dashboards) with others                                              | ✅                                                                      | ✅                                                                                        | ❌                                                                                                              | ❌                                                                                                                                                                                               |
| Feature contents                                                                           | ✅<br>✅ Turn of feature entirely for the workspace                      | ✅                                                                                        | ✅                                                                                                              | ❌                                                                                                                                                                                               |
| Setting sematic models refresh schedule                                                    | ✅                                                                      | ✅                                                                                        | ✅                                                                                                              | ❌                                                                                                                                                                                               |
| Read Access (View dataset data, Analyze in Excel)                                          | ✅                                                                      | ✅                                                                                        | ✅                                                                                                              | ❌ <br>(Can only see data _through_ existing reports, cannot connect directly to the semantic model, browse its tables in the Data Hub, use Analyze in Excel, or create new reports based on it) |
| **App Publishing & Distribution**                                                          |                                                                        |                                                                                          |                                                                                                                |                                                                                                                                                                                                 |
| Publish, update, or unpublish the app                                                      | ✅                                                                      | ✅                                                                                        | ❌                                                                                                              | ❌                                                                                                                                                                                               |
| Build permission (automatically) - use sematic models **in and outside of the workspace**. | ✅                                                                      | ✅                                                                                        | ❌                                                                                                              | ❌                                                                                                                                                                                               |
| **Data & Gateway Management**                                                              |                                                                        |                                                                                          |                                                                                                                |                                                                                                                                                                                                 |
| Manage gateway connections and schedule refresh                                            | ✅                                                                      | ✅                                                                                        | ✅                                                                                                              | ❌                                                                                                                                                                                               |
| Access and build reports from datasets                                                     | ✅                                                                      | ✅                                                                                        | ✅                                                                                                              | 👁️ (Can view reports, but not see datasets)                                                                                                                                                    |
| **Summary Use Case**                                                                       | **Workspace Owner:** Full control over everything, including security. | **Lead Developer:** Can manage all content and publish the app, but cannot manage users. | **Content Creator/ Standard Developer:** Can build and edit reports but cannot share or publish the final app. | **Audience/Reviewer:** Read-only access to view content within the workspace.                                                                                                                   |
#### _**Key Takeaway:**_ The biggest drop-offs in permissions are:
- From **Admin** to **Member**: Loses the ability to manage users and delete the workspace.
- From **Member** to **Contributor**: Loses the ability to publish the app and share content.
- From **Contributor** to **Viewer**: Loses all editing and content creation rights.
#### _**Tip for Easy Memorization**_
Think of the roles like a movie production crew:
- **Admin:** The **Producer** - Hires/fires the crew (manages users) and can shut down the whole project (delete workspace).
- **Member:** The **Director** - In charge of the final cut (publishes the app) and manages the content, but can't fire the producer.
- **Contributor:** The **Actor/Writer** - Creates the content (builds reports) but can't decide on the final cut (can't publish the app).
- **Viewer:** The **Audience** - Can only watch the movie (view content), nothing else.
### How to Assign a Role in a Workspace
You will likely be tested on the process of managing workspace access. Follow these steps.
1. **Navigate to the Workspace:** In the Power BI service, open the workspace you want to manage.
2. **Open the Access Pane:** In the top-right corner of the workspace view, click the **Access** button.
3. **Add Users or Groups:** In the Access pane that opens, type the name of the user or security group into the "Enter a name or email address" field.
4. **Select the Role:** From the dropdown menu next to the name, select the desired role (**Admin**, **Member**, **Contributor**, or **Viewer**).
5. **Confirm the Assignment:** Click the **Add** button to grant the user access with the selected role. The user will now appear in the access list.
---
## Comparison of Power BI Sharing Methods
[Power BI Sharing Methods Comparison – All in One Review - RADACAD](https://radacad.com/power-bi-sharing-methods-comparison-all-in-one-review/)

| Method                             | Best for...                                                                        | Audience                                                                              | Permission Control                                                                                                                                            | Key Limitation                                                                                                                                             |
| ---------------------------------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Workspace Roles** 👥             | **Internal team collaboration** on content development.                            | A small group of **internal creators and developers** who need access to all content. | Access is controlled by four roles: **Admin, Member, Contributor, and Viewer**.                                                                               | It's an **"all-or-nothing"** approach; you cannot hide specific items within the workspace. Not for external sharing.                                      |
| **Direct/Item-level Sharing** 🔗   | **Quick, ad-hoc, and granular sharing** of a single item with specific colleagues. | **Specific individuals or small groups** inside your organization.                    | Managed via the "Share" dialog. You can control who has access, whether they can **reshare**, and if they can **build** new reports from the data.            | Can become difficult to manage permissions for many different users. Sharing the report also shares the underlying semantic model (unless RLS is applied). |
| **Publishing an App** 📦           | **Formal, broad distribution** of a finished and curated collection of content.    | A **large group of consumers**, like a department or the entire organization.         | The app audience is managed separately from the workspace. Consumers have a **read-only** experience by default. Updates are controlled by the app publisher. | Less flexible for one-off sharing. Requires republishing the app to push updates to all consumers.                                                         |
| **Share Outside Your Org** 🛡️     | Securely sharing specific content with **external partners, vendors, or clients**. | **External users** who must be **Microsoft Entra B2B guest users**.<br>               | Managed via direct access. The external user **must sign in** to view. RLS is enforced. Forwarding the link does not grant access.                            | Requires Azure AD B2B setup. The external user needs a proper license, or the content must be in a Premium capacity.                                       |
| **Publish to web** 🌐              | Sharing data with the **general public** on a website, blog, or social media post. | **Anyone on the internet**. Access is **anonymous**.                                  | **None.** Anyone with the link can view the data. You can delete the link to revoke access, but you cannot restrict it to specific users.                     | **NOT SECURE.** Should **never** be used for confidential or proprietary data. Row-Level Security (RLS) is **not** supported.                              |
| **Microsoft Teams Integration** 💬 | **Embedding insights directly** into a team's workflow for real-time discussion.   | Members of a specific **Teams channel or chat**.                                      | Relies on the underlying Power BI permissions (the user must already have access via a workspace role, an app, or a share).                                   | Users in Teams still need the appropriate Power BI license and permissions to view the conte                                                               |

### Prerequisites & Limitations for Sharing
This is a critical area for exam questions. You must know what is required to share and what the boundaries are.

| Aspect                                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ---------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Prerequisites (Who needs a license?)** | **To Share Content:** You (the creator) must have a **Power BI Pro** or **Premium Per User (PPU)** license to share content from a workspace. <br><br> **For Viewers to See Content:** The viewers **also** need a **Power BI Pro** or **PPU** license... **UNLESS** the workspace is hosted in a **Power BI Premium capacity**. If it's in a Premium capacity, users with a **Free** license can view the content shared with them.                                                                                                                                                                                                                                                                       |
| **Limitations**                          | **Workspace Storage:** Workspaces have a storage limit (e.g., 10 GB for Pro, 100 GB for PPU/Premium). Large datasets can exceed this. <br><br> **App Updates are Manual:** When you update a report in a workspace, you **must manually update and republish the app**. Changes are not automatically pushed to the app's audience. <br><br> **Direct Sharing is Hard to Manage:** Sharing individual reports with many different users becomes difficult to track and audit. It can create a complex web of permissions that is hard to govern. <br><br> **External Users:** Sharing with external (guest) users requires specific Azure Active Directory B2B settings to be enabled by an administrator. |

---
### Creating and Managing Workspaces
[Create a workspace in Power BI - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-create-the-new-workspaces)
#### How to Create a Workspace
1. Select **Create > Workspaces > New workspace**.
2. Provide a **unique name**.
3. Configure optional settings (see below).
4. Select **Save**.
- r select **+ New** (if shown) > **Workspace**.
![Screenshot of the Create a new workspace dialog.](https://learn.microsoft.com/en-us/power-bi/collaborate-share/media/service-create-the-new-workspaces/power-bi-workspace-create-new.png)
#### Key Workspace Settings (Found under "Advanced")
[Create a workspace in Power BI - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-create-the-new-workspaces#workspace-settings)
- **Contact List:** Specifies who receives notifications about workspace issues. By default, this is the list of workspace admins, but you can add other users or groups. This helps users know who to contact for help.
- **Workspace OneDrive:** Links a Microsoft 365 Group's SharePoint document library to the workspace, providing a shared file storage location. You create the M365 Group outside of Power BI first and then enter its name in this setting.
- **Allow contributors to update the app:** This is a crucial delegation setting. ==By default, only Admins and Members can update the app for the workspace==. Enabling this setting gives users with the **Contributor** role permission to update an _existing_ app (though they still cannot create or publish it for the first time or manage its permissions).
- **Premium Capacity:** Assigns the workspace to a Premium or Premium Per User (PPU) capacity to unlock advanced features like larger datasets, higher refresh rates, and the ability to share with Free users.
##### Set a workspace OneDrive
The Workspace OneDrive feature allows you to configure a Microsoft 365 Group whose SharePoint document library is available to workspace users.
1. Create the Group (OneDrive shared library) _outside_ of Power BI first
2. A best practice is to give [access to the workspace](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-give-access-new-workspaces) to the same Microsoft 365 Group whose file storage you configured.
3. In the nav pane, select the arrow next to **Workspaces**, select **More options** (...) next to the workspace name > **Workspace settings**. The **Settings** pane opens.
![Screenshot of the Workspace settings pane.](https://learn.microsoft.com/en-us/power-bi/collaborate-share/media/service-create-the-new-workspaces/power-bi-workspace-new-settings.png)
4. Under **Advanced** > **Workspace OneDrive**, type the name (not the URL) of the Microsoft 365 group that you created earlier.
5. Select **save**.

#### Managing Workspaces
- **Giving Access:** After creating a workspace, you must add colleagues to specific **roles** (Admin, Member, Contributor, Viewer) to enable collaboration. [Give users access to workspaces - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-give-access-new-workspaces)
- **Pinning Workspaces:** For quick access, you can hover over a workspace in your list and select the **Pin to top** icon. This keeps your favorite workspaces in a "Pinned" list at the top.


---
### Terms and Definitions 

| Term                                       | Definition                                                                                                                                | Application & Use Case                                                                                                                                                        | Relation to Collaboration/Sharing                                                                                                                                             |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Workspace**                              | A shared, collaborative environment where teams create and manage collections of Power BI content like datasets, reports, and dashboards. | **Use Case:** A project team uses a workspace as a central development area to build a new set of sales analytics before they are ready for wider distribution.               | This is the **foundation of team-based collaboration**. It's the "kitchen" where developers work together on the raw ingredients of a report.                                 |
| **My Workspace**                           | A private, personal sandbox for an individual user. Content here cannot be shared with or accessed by other users.                        | **Use Case:** An analyst uses their "My Workspace" to experiment with a new dataset or build a draft report before moving it to a shared team workspace.                      | This is the **opposite of collaboration**. It is explicitly for individual work that is not yet ready for a team environment.                                                 |
| **App**                                    | A packaged collection of reports and dashboards from a single workspace, designed for broad, read-only consumption by end-users.          | **Use Case:** Publishing a formal "Official Sales App" to the entire sales organization so everyone has access to the same set of curated, finalized reports.                 | This is the primary method for **formal, large-scale distribution**. It's the "finished meal" served to a wide audience, providing a polished, controlled experience.         |
| **Role**                                   | A set of permissions (Admin, Member, Contributor, Viewer) assigned to users within a workspace to control their actions.                  | **Use Case:** Assigning the **Contributor** role to a data analyst so they can build reports, but not publish the final app to the organization.                              | Roles are the **core mechanism for managing collaboration**. They define who can create, edit, manage, and distribute content within the team.                                |
| **Direct Sharing (or Share)**              | The action of providing access to a single report or dashboard to specific individuals or groups via a direct link.                       | **Use Case:** Quickly sharing a single, work-in-progress report with a manager for immediate feedback, without giving them access to the entire workspace.                    | This is a method for **informal, small-scale sharing**. It's like sharing a single document, useful for ad-hoc requests but hard to manage at scale.                          |
| **Contact List**                           | A setting in the workspace that specifies which users receive system notifications, separate from the roles that grant permissions.       | **Use Case:** Setting the project manager as the contact so they are notified of any refresh failures, even if they are not an Admin of the workspace.                        | This is a **governance and communication tool** that supports collaboration by keeping key stakeholders informed, without granting them editing rights.                       |
| **Workspace OneDrive**                     | A feature to link a Microsoft 365 Group's SharePoint library for shared file storage.                                                     | A team configures a Workspace OneDrive to have a central, shared location for all the Excel and CSV source files used in their Power BI report                                | A feature that **enhances collaboration** by providing a common, integrated file repository for the team.                                                                     |
| **"Allow contributors to update the app"** | A security setting that delegates permission to update an existing app to users with the Contributor role.                                | An admin enables this setting so that the data analysts (Contributors) on the team can add new reports to the app without needing to ask a Member or Admin to do it for them. | An admin enables this setting so that the data analysts (Contributors) on the team can add new reports to the app without needing to ask a Member or Admin to do it for them. |

---
### Practice Questions

| Question                                                                                                                                                                                                                                            | Options                                                                                                                                                                                                                         | Answer & Explanation                                                                                                                                                                                                                                                                  |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Which workspace role can create reports but CANNOT publish the Power BI app?                                                                                                                                                                        | A. Admin<br>B. Member<br>==**C. Contributor**==<br>D. Viewer                                                                                                                                                                    | **C. Contributor.** This is the core distinction for the Contributor role. They are content creators without publishing rights.                                                                                                                                                       |
| A manager needs to publish a workspace app. They are currently in a security group with the **Contributor** role. What is the most efficient way to grant them the necessary permission without giving extra permissions to their team?             | A. Change the group's role to Member.<br>==B. Add the manager's individual account as a **Member**.==<br>C. Create a new workspace.<br>D. Tell them to share the report instead.                                                | **B. Add the manager's individual account as a Member.** This elevates only their permission. Power BI applies the highest permission level a user has, whether it's assigned individually or through a group.                                                                        |
| An app user reports seeing an old version of a report, even though a workspace **Member** just updated it. What is the most likely cause?                                                                                                           | A. The dataset hasn't been refreshed.<br>B. The user needs to clear their browser cache.<br>==C. The Member forgot to **update the app** after editing the report.==<br>D. The Member does not have permission to edit reports. | **C. The Member forgot to update the app after editing the report.** Changes made in a workspace are not automatically pushed to the published app. The app is a separate package that must be explicitly updated.                                                                    |
| A user has two roles in a workspace: **Viewer** (assigned directly) and **Contributor** (via a security group). What can they do in the workspace?                                                                                                  | A. Only view reports.<br>==B. View and edit reports.==<br>C. Edit reports but not view them.<br>D. Nothing, as the roles are conflicting.                                                                                       | **B. View and edit reports.** Power BI's permission model is additive. It grants the user the _highest_ level of permissions they have from any source. Contributor is higher than Viewer.                                                                                            |
| **Sharing Method**                                                                                                                                                                                                                                  |                                                                                                                                                                                                                                 |                                                                                                                                                                                                                                                                                       |
| You need to provide a set of 10 finalized reports and 3 dashboards to the entire 500-person sales department. They need a simple, centralized place to view this content. Which sharing method should you use?                                      | A. Add all 500 users to the workspace as Viewers.<br>==B. Publish a Power BI app.==<br>C. Share a link to each of the 13 items individually.<br>D. Put the files in a shared SharePoint folder.                                 | **B. Publish a Power BI app.** This is the classic use case for an app. It's designed to distribute a collection of content to a large audience in a controlled, user-friendly way. Adding 500 users to a workspace is unmanageable.                                                  |
| A colleague in the finance department asks for access to a single, specific report you are working on so they can provide feedback. They are not part of your development team. What is the quickest and most appropriate way to grant them access? | A. Add them to your workspace as a Viewer.<br>B. Publish an app containing only that report.<br>==C. Use the **Share** button on the report to send them a direct link.==<br>D. Export the report to PowerPoint and email it.   | **C. Use the Share button on the report to send them a direct link.** This is perfect for ad-hoc, one-off sharing with an individual. It's fast, simple, and doesn't grant them access to the entire workspace or require the formality of publishing an app.                         |
| **Prerequisites**                                                                                                                                                                                                                                   |                                                                                                                                                                                                                                 |                                                                                                                                                                                                                                                                                       |
| You have a Power BI Pro license and have built a set of reports in a standard workspace (not in Premium capacity). You need to share a dashboard with a group of colleagues so they can view it. What license must your colleagues have?            | A. They do not need any license.<br>B. A Power BI Free license.<br>==C. A Power BI Pro or PPU license.==<br>D. A Microsoft 365 license.                                                                                         | **C. A Power BI Pro or PPU license.** To view content shared from a standard (non-Premium) workspace, the recipient must have a paid Power BI license (Pro or PPU). The sharer's license is not enough on its own.                                                                    |

---
## Publishing Reports 
### Publishing from Power BI Desktop
This is the primary and most common method.
1. In Power BI Desktop, select **Publish** from the **Home** ribbon.
2. If prompted, sign in with your work or school account.
3. In the dialog box, select the destination **workspace** for your report.

**What Gets Published:** When you publish, both the **report** (the visuals) and its associated **semantic model** (the data, relationships, and measures) are sent to the Power BI service. ==This allows the semantic model to be reused to create new reports directly in the service.==

**Republishing:** When you make changes and republish an existing report, Power BI will ask you to confirm that you want to **replace** the version currently in the service.
### Uploading a `.pbix` File Directly
You can also add a report by uploading the file directly in the Power BI service.
- **How:** In a workspace, use the **Upload** menu to browse for a file on your computer, or connect to a file stored in OneDrive for Business or SharePoint.
- **Syncing with OneDrive/SharePoint:** If you connect to a `.pbix` file stored in OneDrive for Business or SharePoint, Power BI creates a connection to it. Any changes you save to the file in that location will be **automatically synced** to the Power BI service approximately every hour.

---
## Organizing Content in a Workspace

### Folders (Preview Feature)
You can create **folders** inside a workspace to better organize and manage your content (reports, datasets, etc.).
- You can create nested subfolders up to 10 levels deep.
- To publish a report from Power BI Desktop directly into a specific folder, you must first enable the **"Publish dialogs support folder selection"** setting in the **Preview features** tab of the options menu.
---
## Setting Up and Managing Refreshes

### How to Schedule a Refresh
Before scheduling, you must have a gateway connection configured if your data source is on-premises.
1. In the Power BI service, go to your workspace and hover over the semantic model you want to refresh.
2. Select the **Schedule refresh** icon (a clock with a refresh arrow).
3. On the settings page, turn on the **Scheduled refresh** toggle.
4. Configure the settings:
    - **Refresh frequency:** Daily or Weekly.
    - **Time zone:** Ensure the correct time zone is selected.
    - **Time:** Add the specific time slots for the refresh to occur.
5. Select **Apply**.

**Important Considerations:**
- **Refresh Limits:** You can configure up to **8** daily time slots on a shared capacity (Pro) or up to **48** time slots on a Premium capacity.
- **Timing:** Power BI initiates refreshes on a "best effort" basis. The goal is to start within 15 minutes of the scheduled time, but a delay of up to one hour can occur.
### On-Demand Refresh
In addition to scheduled refreshes, you can trigger a manual refresh at any time. This is called an **on-demand refresh**.
- **Purpose:** Useful for testing your configuration or when you need the absolute latest data immediately and can't wait for the next scheduled time.
- **How to Use:** In the workspace, hover over the semantic model and select the **Refresh now** icon (a circular arrow). This action does not affect the next scheduled refresh time.
## Monitoring Refreshes
It is a good practice to occasionally check the status of your refreshes to ensure they are running successfully.
### Refresh Status and History
- **Status:** A quick way to check the status is in the workspace list view. A small **warning icon** next to a semantic model indicates a problem.
- **History:** To see a detailed log, go to the semantic model's **Settings** page and select **Refresh history**. This shows a list of past refreshes and whether they succeeded or failed.
## Why a Refresh Schedule Might Be Disabled ⚠️
Power BI can automatically disable a refresh schedule under certain conditions:
- After **four consecutive failures**.
- After **two months of inactivity** (meaning no user has viewed any report or dashboard built on the semantic model).
- When the service detects an unrecoverable error, such as **invalid or expired credentials**.

---
## Incremental refresh
Incremental refresh allows you to refresh large semantic models faster and more reliably by only updating the most recent data, instead of reloading the entire historical dataset each time.
**Key Benefits:**
- **Quicker refreshes:** Only a small subset of recent data is refreshed.
- **More reliable refreshes:** Avoids long-running, timeout-prone connections.
- **Reduced resource consumption:** Less data is processed, saving memory and other resources.
### Critical Prerequisite: Query Folding ⚠️
Incremental refresh should **only be used on data sources that support query folding**. Query folding is the process where Power Query translates your filter steps into a native query (like SQL) that is executed directly by the data source. If folding isn't supported, Power BI will be forced to download the entire table first and then apply the filters, which defeats the purpose of incremental refresh and leads to very poor performance.
### How to Configure Incremental Refresh
The process involves creating parameters in Power Query, applying a filter, and then defining the refresh policy.
#### Step 1: Define Filter Parameters
You must create two specific, case-sensitive parameters in the Power Query Editor to filter your data.
1. On the **Home** tab, select **Manage Parameters > New Parameter**.
2. Create a parameter named **`RangeStart`**. Set the **Type** to `Date/Time`.
3. Create a second parameter named **`RangeEnd`**. Set the **Type** to `Date/Time`.
4. Set the **Current Value** for these parameters to define a small window of data to load into Power BI Desktop (e.g., the last month).
#### Step 2: Apply the Filter
Use the `RangeStart` and `RangeEnd` parameters to filter the main data table in Power Query
1. Select the date column you want to filter (e.g., `OrderDate`).
2. Click the filter dropdown and select **Date/Time Filters > Custom Filter...**.
3. Set the filter conditions to be:
    - `is after or equal to` the **`RangeStart`** parameter.
    - **AND**
    - `is before` the **`RangeEnd`** parameter. (Using "is before" and not "is before or equal to" prevents rows from being counted in two partitions).
4. Select **Close & Apply**. Your Power BI Desktop model will now only contain the small subset of data you defined.
#### Step 3: Define the Incremental Refresh Policy
After applying the filter, you define the refresh policy in Power BI Desktop's main interface.
1. In the **Data** or **Model** view, right-click the table you want to configure.
2. Select **Incremental refresh**.
3. In the dialog box, turn on the incremental refresh toggle.
4. Configure the **Archive** (store) and **Refresh** (incrementally refresh) periods. For example:
    - **Store data from the last:** `5` `Years`
    - **Incrementally refresh data from the last:** `10` `Days`
#### Step 4: Publish to the Power BI Service
The incremental refresh policy does nothing in Power BI Desktop. It is only **activated after you publish** the report to the Power BI service.
Upon the first refresh in the service, Power BI will load all 5 years of historical data. All subsequent refreshes will be much faster, only reloading the last 10 days of data.

---
## Sematic model Endorsement 
### The Two Levels of Endorsement in Power BI
Power BI provides two ways to endorse your semantic models, each with a different level of authority.

| Feature                | Promotion 🥈                                                                                       | Certification 🥇                                                                                                                      |
| ---------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Purpose / Meaning**  | A peer-to-peer recommendation. It highlights content that is valuable and ready for others to use. | The official "stamp of approval." It marks content as the authoritative and reliable **single source of truth** for the organization. |
| **Who Can Perform It** | Workspace members with write permissions (Admin, Member, or Contributor).                          | Only a select group of users authorized by a Power BI administrator or a permission from the sematic model owner                      |
| **Process**            | Can be directly applied by users with the required permissions in the workspace settings.          | A controlled, and often request-based, process. Most users can only _request_ certification.                                          |
| **Required License**   | A **Power BI Pro** or **PPU** license is required for the user applying the endorsement.           | A **Power BI Pro** or **PPU** license is required for the authorized user who is applying the certification.                          |
| **Analogy**            | A skilled chef recommending their own dish.                                                        | The restaurant owner declaring a dish the "Signature Special."                                                                        |

## Query Caching

**Query Caching** is a feature for workspaces in **Microsoft Fabric or Premium capacity** that improves report performance by using cloud resources to store, or cache, query results. This reduces the load on your semantic model and speeds up the initial load time for frequently accessed reports.
### How Query Caching Works
- **Scope:** The cache is created on a **per-user** and **per-report** basis. This means the cache respects all security rules, RLS, bookmarks, and default filters for that specific user.
- **Timing:** Caching is performed the **first time a user opens the report**.
- **Limitation:** The service only caches queries for the **initial page** that the user lands on. Queries generated by subsequent user interactions (like clicking a slicer or cross-filtering) are **not cached**.

**Key Benefits:**
- Improves the initial load performance of reports and dashboards.
- Reduces the query load on your dedicated capacity.
## How to Configure Query Caching
1. In your workspace, go to the **Settings** page for the semantic model you want to configure.
2. Expand the **Query Caching** section.
3. Select one of the three options:
    - **Off:** (Default) Query caching is disabled.
    - **On:** Query caching is enabled for this specific semantic model.
    - **Auto:** The service decides whether to use query caching.
## Key Considerations and Warnings ⚠️
- **Clearing the Cache:** Switching the setting from **On** back to **Off** will clear all previously saved query results for that semantic model.
- **Refresh Performance:** If you enable query caching on many semantic models, you might see a temporary reduction in performance immediately after a data refresh. This is because a large number of queries are being processed at once to rebuild all the caches.
---
## Lineage and Impact Analysis 
**Lineage view** in the Power BI service helps you understand the flow of data and the relationships between all the items (artifacts) in a workspace. It's a visual map that helps you answer questions like "What happens if I change this dataset?" or "Why isn't this report up to date?"
To see it, you need at least a **Contributor** role in the workspace.
### What You Can See in Lineage View
Lineage view shows all workspace artifacts and how data flows between them. On each "card" in the view, you can see key information:
- **Data Sources:** Where your semantic models get their data. Gateway information is shown if the source is on-premises.
- **Semantic Models:** The last refresh time and any endorsement status (**Certified** or **Promoted**).
- **Reports and Dashboards:** The final outputs that are connected to the semantic models.
### Performing Impact Analysis
**Impact analysis** is a key feature within lineage view that helps you understand the dependencies of your data.
#### Semantic Model Impact Analysis
- **Purpose:** To see all the downstream **reports and dashboards** that depend on a specific semantic model.
- **Why it's useful:** This is critical before you make changes to a semantic model. It allows you to assess the potential impact on other users and reports, especially when the model is shared across different workspaces.
- **How to use:** Select the impact analysis button on a semantic model card.
#### Data Source Impact Analysis
- **Purpose:** To see where a specific data source is being used throughout your organization.
- **Why it's useful:** If a data source needs to be taken offline for maintenance or permanently retired, this helps you identify everyone who will be impacted.
- **How to use:** Select the impact analysis button on a data source card.