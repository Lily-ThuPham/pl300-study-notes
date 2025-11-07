[Read this discussion of the app publishing process.](https://learn.microsoft.com/en-us/power-bi/collaborate-share/service-create-distribute-apps)
A **Power BI App** is used to distribute a collection of related content (reports, dashboards, etc.) to a broad but selected audience securely and efficiently. You can manage the app's lifecycle and even customize the content that different groups of users see within the same app.

---
## Managing a Power BI App
### Create an App
1. **Set up:** In a workspace, select **Create app**. Provide a name, description, and optional theme color.
2. **Add content:** On the **Content** tab, select the reports and dashboards from the workspace that you want to include in the app.
3. **Publish:** Click **Publish app** to finalize and generate a shareable link.

> [!Note] Publishing an app will grant access to reports and dashboards, not datasets. Further app publishing grants access only to the included Power BI content. It does not allow users to see all the datasets available in the organization and request access.
### Update an App
If you want to update an existing content in your workspace, simply upload the updated file.
1. In the workspace, select the **Update app** button (or **Edit app** pencil icon).
2. Make your changes to the app's content or settings. These changes are saved in the workspace but are **not visible to users yet**.
3. Select **Update app** again to republish. Users will automatically see the new version.
**Automatic updates**: If your data source is set up with a scheduled refresh in Power BI Service, the reports and dashboards linked to it will be updated automatically based on the refresh frequency.
### Unpublish an App
- In the workspace, select **More options (...) > Unpublish app**.
- **Impact:** This action permanently removes the app for all users and **deletes their personal customizations** like bookmarks and comments. The content in the workspace itself is not affected.

---
## Using Audiences to Customize Content
**Audiences** allow you to show a different subset of content to different groups of users, all within a single app. This is useful for tailoring content to various departments without creating multiple apps.
### How to Configure Audiences
1. During app creation or editing, go to the **Audience** tab.
2. **Create an Audience Group:** Select **New Audience** and give it a name (e.g., "Sales Team," "Marketing Team").
3. **Customize Content Visibility:** Use the **hide/show icons** next to each report or dashboard to control what this specific audience group can see.
4. **Assign Users:** In the **Manage audience access** pane, specify the users or security groups who belong to this audience.
5. **Publish or Update** the app. Users will now only see the content you made visible for the audience they belong to.
## Licensing Requirements for Apps 🔑
- **For Creators:** To create or update an app, you need a **Power BI Pro** or **Premium Per User (PPU)** license.
	- You must have an **Admin** or **Member** role in the workspace containing the content. _(Note: An Admin can optionally allow users with the **Contributor** role to update an existing app, but Contributors cannot create or publish it initially.)_
- **For Consumers (Viewers):**
    - If the workspace is **not** in a Premium capacity, all viewers need a **Pro** or **PPU** license.
    - If the workspace **is** in a Premium capacity, users with a **Free** license can view the app.

---
Power BI provides two essential data governance practices to ensure your data is high-quality, trusted, and secure: **endorsing your content** and **applying sensitivity labels**.
## Endorse Your Content ✅
Endorsing content helps users easily find and trust high-quality, authoritative data sources, which is crucial for creating a healthy data culture. Endorsed content is marked with a badge and is prioritized in searches in both Power BI Desktop and the service.

There are two levels of endorsement:
- **Promotion 🥈:** A collaborative, peer-to-peer recommendation. Content owners or workspace members with write permissions can **promote** content they believe is valuable and ready for broader use.
- **Certification 🥇:** The official "stamp of approval" from your organization. **Certification** signifies that the content has undergone a comprehensive vetting process, aligns with the highest organizational standards and is deemed authoritative and reliable for critical decision-making. Only a select group of authorized reviewers, defined by a Power BI administrator, can certify content.
#### Four aspects of Certification
When content is certified, it means it has passed through a rigorous scrutiny process, adhering to the standards set by the organization.
1. Review process: expert validation of data quality and adherence to best practices.
2. Governance: implementing strict organization standards while certifying contents; 
3. Visibility: certified content is marked with a badge for easy recognition.
4. Trust: indicates high level approval and reliability for all users in the organization.
##### Comparison of Power BI Endorsement: Promotion vs. Certification

| Feature                 | Promotion 🥈                                                                                                                                                     | Certification 🥇                                                                                                                            |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **Primary Aim**         | To **highlight valuable content** that is ready for wider use within the organization.                                                                           | To signify that content meets official **organizational quality standards** and is a reliable, authoritative source of truth.               |
| **Level of trust**      | Creator / peer approval                                                                                                                                          | Organizational approve by qualified team                                                                                                    |
| **Who Can Perform It**  | **Content owners** or anyone with **write permissions** in the workspace (Admin, Member, Contributor).<br>_Peer review_                                          | A select group of **authorized reviewers**, defined by a Power BI administrator in the tenant settings.<br>_Expert review_                  |
| **Visibility & Impact** | Shared and recommend sections.<br>Content is marked with a "Promoted" badge for easy identification. It can also be **"Featured on Home"** for added visibility. | Content is marked with a distinct "Certified" badge and is **prioritized in search results**, helping users find official data sources.     |
| **Governance**          | Decentralized                                                                                                                                                    | Centralized                                                                                                                                 |
| **Who should use it**   | Team-level or Department sharing                                                                                                                                 | Organization sharing                                                                                                                        |
| **Use Case Example**    | A data analyst promotes a newly created sales dataset to make it easily accessible and recommended for their immediate team.                                     | An organization's finance department certifies a financial dashboard, marking it as the single, official source for all financial analysis. |
Endorsing an app or a report by promoting it automatically checks the **Feature on Home** checkbox.

---
[[Sensitivity Labels in Power BI]]
[[Data Subscription & Alerts in Power BI]]
