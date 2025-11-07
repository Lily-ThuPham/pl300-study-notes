#### **Key Concepts 💡**

**Sensitivity labels** from Microsoft Purview Information Protection provide a way to classify and protect data according to its sensitivity or confidentiality, ensuring that it is handled appropriately and securely. Sensitivity labels can be used to ensure that only authorized people can access your data, and they can enforce protection settings that are appropriate for the sensitivity of that data.
In the Power BI service, sensitivity labels can be applied to _**semantic models, reports, dashboards, and dataflows**_.

The primary goal is to help your organization comply with data protection and governance requirements. When you apply a sensitivity label to a Power BI asset, that classification is visible, acts as a _**digital watermark**_, and its protection rules are enforced. For example, a "Highly Confidential" label might be configured to encrypt data upon export to Excel or prevent unauthorized users from accessing it.

This feature ensures that data protection is not just confined to the Power BI service but **travels with the data**, providing end-to-end security.
#### **Types of Sensitive labels**
- **Personal**: This label is used for data that is not sensitive and can be freely shared with anyone. Personal data sensitivity labels don't impose any restrictions on sharing or access.
- **Public**: Public data sensitivity labels are for information that can be shared publicly. While it's still considered non-sensitive, using this label indicates that it's suitable for public consumption. It can be helpful for compliance or transparency purposes.
- **General**: This label is for data that has some sensitivity but can still be shared relatively broadly within the organization. It might contain data that is not confidential but should be handled with care.
- **Confidential**: Confidential labels are used for sensitive data that should be accessed and shared only with authorized individuals or teams within the organization. It typically includes data that, if exposed or mishandled, could cause harm or legal issues.
- **Highly Confidential:** Highly confidential sensitivity labels are reserved for the most sensitive data within an organization. This label is applied to data that requires the highest level of protection and should be accessible only to a limited group of individuals with explicit permissions.
- **Restricted**: The Restricted sensitivity label is used for data that is sensitive and has strict access restrictions. This label is typically applied to information that should only be accessed by a specific group of authorized personnel, often with the highest level of security clearance. Data labeled as "Restricted" should be handled with the utmost care, and access is tightly controlled to prevent any unauthorized use or exposure.
#### **How It Works**
- **Label Application:** Users can apply sensitivity labels to reports, dashboards, datasets, and dataflows in the Power BI service and to PBIX files in Power BI Desktop. When opened, and the sensitivity label will be located beside the artifact's name.
- **Inheritance:** Labels applied to datasets or dataflows are automatically inherited by the downstream content built from them. For instance, if you label a dataset as "Confidential," any new report created from that dataset will automatically inherit the "Confidential" label.
- **Protection Enforcement:** The policies associated with a label are enforced. This can include:
    - **Content Marking:** Applying watermarks or headers/footers to content.
    - **Export Protection:** Encrypting files (Excel, PDF, PowerPoint) when data is exported from the Power BI service.
- **Data Loss Prevention (DLP):** Power BI integrates with Microsoft Purview Data Loss Prevention. DLP policies can detect the upload of sensitive data (like credit card numbers or PII) to a dataset and trigger real-time alerts and policy tips for users.
---
#### **Definitions of Important Terms**

| Term                                         | Definition                                                                                                                                                         | Relevance to Sensitivity Labels                                                                                                                          |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Microsoft Purview Information Protection** | A Microsoft 365 cloud-based solution that allows organizations to discover, classify, and protect sensitive information wherever it lives or travels.              | This is the framework that provides and manages the sensitivity labels that are used in Power BI.                                                        |
| **Sensitivity Label**                        | A digital tag that you apply to content. The label applies a specific classification (e.g., Public, Confidential) and its associated protection policies.          | This is the core component. Applying a label to a Power BI asset is how you classify and protect it.                                                     |
| **Inheritance**                              | The automatic application of a sensitivity label from a parent asset to its child assets.                                                                          | This ensures that protection is consistently applied across the data lineage (e.g., from a dataflow to a dataset to a report).                           |
| **Data Loss Prevention (DLP) Policies**      | Policies configured in Microsoft Purview to identify and protect sensitive information. They can detect sensitive info types using deep content analysis.          | DLP policies for Power BI can detect when a user tries to publish a dataset containing sensitive information and can block the action or show a warning. |
| **Downstream Inheritance**                   | A type of inheritance where labels applied to assets like datasets and dataflows are passed down to connected reports and dashboards.                              | This is the most common form of inheritance in Power BI, ensuring new content gets the same protection as its source.                                    |
| **Upstream Inheritance**                     | A type of inheritance where a label from a data source (like Azure Synapse Analytics or SQL Server) is automatically applied to the connected dataset in Power BI. | This extends protection from the original data source into the Power BI environment automatically.                                                       |

---
#### **Apply sensitivity labels in the Power BI service**
You can apply sensitivity labels to reports, dashboards, semantic models, and dataflows.
##### Requirements
- You must have a **Power BI Pro or Premium Per User (PPU)** license and Edit permissions on the content.
- Sensitivity labels must be enabled for your organization.
- You must belong to a security group that has permissions to apply labels.
##### How to Apply
1. Go to the **Settings** for the report, dashboard, semantic model, or dataflow.
2. Find the **Sensitivity label** section.
3. Select the appropriate label from the list. The setting is applied automatically.
#### **Apply sensitivity labels in Power BI Desktop**
##### Requirements
- You must have a **Power BI Pro or Premium Per User (PPU)** license.
- Sensitivity labels must be enabled for your organization.
- You must belong to a security group with permissions to apply labels.
- You must be signed in.
##### How to Apply
1. In the **Home** ribbon, select the **Sensitivity** option.
2. Choose the appropriate label from the dropdown list.
3. The applied label will be visible in the status bar at the bottom of the window.
#### **Label Behavior When Publishing and Downloading**
- **Publishing to Service:** When you publish a labeled `.pbix` file to the Power BI service, the report and semantic model created in the service **inherit** the file's label.
- **Downloading from Service:** When you download a `.pbix` file, if the report and its semantic model have different labels, the **most restrictive** of the two labels is applied to the downloaded file.
#### **Remove sensitivity labels**
You can only remove sensitivity labels in **Power BI Desktop**. To do so, select the **Sensitivity** option in the toolbar and click the currently selected label to deselect it.

---
#### **Enabling Sensitivity label for Power BI Fabric** (for **Fabric/Power BI administrators**)
This is a prerequisite step that must be completed before users can apply labels to their content, to enable sensitivity labels from Microsoft Purview Information protection for the entire organization.
##### Licensing and Prerequisites
Before enabling the feature, several requirements must be met
- **Azure Licensing:** Users who will apply labels must have an **Azure Information Protection Premium P1 or P2** license.
- **Power BI Licensing:** The same users must also have a **Power BI Pro or Premium Per User (PPU)** license.
- **Labels Must Be Defined:** Sensitivity labels must already be created and published for the relevant users and groups in the Microsoft Purview compliance portal.
- **Desktop Version:** Users must have the December 2020 (or later) version of Power BI Desktop.
##### How to Enable Sensitivity Labels (Admin Steps)
This is a tenant-wide setting configured in the Admin portal.
1. Navigate to the **Fabric admin portal**.
2. Go to **Tenant settings** and find the **Information protection** section.
3. Expand the setting **"Allow users to apply sensitivity labels for content"** and turn the toggle **On**.
4. Define who can apply and change labels:
    - **The entire organization:** (Default) Allows everyone to apply labels.
    - **Specific security groups:** Restricts the ability to apply labels to only the members of the specified security group(s). You can also add exceptions.
5. Select **Apply**.
##### Troubleshooting
If you encounter an error when trying to enable the feature, it is likely due to one of two reasons:
- Sensitivity labels have not been defined yet in the Microsoft Purview compliance portal.
- Older Azure Information Protection labels have not been migrated to the newer, unified Purview Information Protection platform.

---
#### **Sample Exam Questions 📝**

| No. | Question                                                                                                                                                                                                                                                                    | Options                                                                                                                                                                                                                                                                                                                                                | Explanation                                                                                                                                                                                                                                                                                                |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | A data analyst applies a "Highly Confidential" sensitivity label to a dataset in the Power BI service. This label is configured to encrypt files on export. What happens when a business user creates a new report from this dataset and then exports it to Excel?          | A. The report cannot be exported.<br>B. The Excel file will be unencrypted because the label was on the dataset, not the report.<br>==**C. The new report automatically inherits the "Highly Confidential" label, and the exported Excel file will be encrypted.**==<br>D. The user must manually apply the same label to the report before exporting. | Power BI enforces **downstream inheritance**. The new report automatically inherits the sensitivity label from its parent dataset. Consequently, the protection policy (file encryption) associated with that label is applied when the data is exported.                                                  |
| 2   | Your organization wants to prevent users from accidentally publishing PBIX files that contain personally identifiable information (PII) like national ID numbers. Which feature should be configured to detect this specific type of sensitive information within datasets? | A. Power BI workspace access roles.<br>==**B. Data Loss Prevention (DLP) policies.**==<br>C. Power BI data alerts.<br>D. Sensitivity label inheritance.                                                                                                                                                                                                | **Data Loss Prevention (DLP) policies** are designed for this exact purpose. They use content inspection to identify specific sensitive information types (like ID numbers) within a dataset and can provide warnings to users or block the publish action.                                                |
| 3   | You apply a sensitivity label to a Power BI report in the service. Which of the following is **NOT** a direct capability of sensitivity labels in Power BI?                                                                                                                 | A. Encrypting an exported PDF file.<br>B. Applying a watermark to the report pages.<br>==**C. Restricting access to the report to a specific security group.**==<br>D. Classifying the report as "Internal Use Only".                                                                                                                                  | While sensitivity labels classify and protect data _within_ and _exported from_ Power BI, they do not manage access permissions to the content _inside_ the Power BI service. Access control is managed separately through workspace roles (Admin, Member, Viewer) and report/dataset sharing permissions. |
| 4   | Where must sensitivity labels and their associated policies be created and configured before they can be applied to content in Power BI?                                                                                                                                    | A. In the Power BI Admin portal.<br>==**B. In the Microsoft Purview compliance portal.**==<br>C. Directly within a Power BI workspace's settings.<br>D. In Power BI Desktop's options.                                                                                                                                                                 | Sensitivity labels are a centralized feature of Microsoft's compliance offerings. They are created and managed in the **Microsoft Purview compliance portal**, and then they become available to be used across various Microsoft services, including Power BI.                                            |
