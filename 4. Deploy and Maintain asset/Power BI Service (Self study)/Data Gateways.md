### What is a Power BI Gateway?
- A **Power BI Gateway** is a secure application that acts as a **bridge** between the cloud-based **Power BI service** and **on-premises data sources** (data not directly accessible over the internet, like local SQL Servers or files).
- It is **required** whenever Power BI needs to access data that resides within your organization's private network.
- The gateway creates the connection and securely **passes data through** without storing it.
### Key Gateway Functions
Gateways enable two primary interactions with on-premises data:
- **Data Refresh:** Facilitates the **scheduled** or **incremental refresh** of datasets in Import mode, pulling the latest data from the on-premises source into the Power BI service.
- **Query Execution:** Enables **DirectQuery** or **Live Connection** reports to send live queries to the on-premises data source and retrieve real-time results.
### Types of Gateways
Power BI offers three types of gateways:
- **On-Premises Data Gateway (Standard Mode):** Enterprise solution for multiple users and sources.
- **On-Premises Data Gateway (Personal Mode):** Simplified solution for a single user.
- **Virtual Network (VNet) Data Gateway:** Managed service for connecting to data within Azure VNets.
	- **Who It's For:** Best for complex organizational setups that use **Azure Virtual Networks** and require enhanced security.
	- **Capabilities:**
	    - It's a managed service, which reduces the overhead of installing and monitoring on-premises gateways.
	    - It virtually bridges Power BI to supported Azure data services within a VNet.
	    - It provides a secure pathway for data that adheres to organizational security policies.
	- **Use Case:** A growing organization that requires better security and data management for their Azure-based data sources, keeping communication within their virtual network.

| Gateway Type                          | Purpose                                                                                                   | Primary Use Case                                                                                                    |
| ------------------------------------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **On-Premises Gateway (Standard)** 🏢 | Securely connects the Power BI service to **local, on-premises** data sources.                            | The standard, enterprise-grade solution for teams connecting to company databases and files behind a firewall.      |
| **On-Premises Gateway (Personal)** 👤 | Connects a **single user's** Power BI content to on-premises data.                                        | An individual analyst needs to refresh reports from their local files without using the central IT-managed gateway. |
| **VNet Data Gateway** ☁️              | Securely connects the Power BI service to data sources inside a **private Azure Virtual Network (VNet)**. | For highly secure Azure data sources that are isolated from the public internet.                                    |
##### Comparison of the two on-premises gateway modes:

|**Feature**|**Standard (On-Premises) Mode 🏢**|**Personal Mode 👤**|
|---|---|---|
|**Who is it for?**|**Multiple users**/teams|**Single user** (individual)|
|**Data Sources**|Multiple on-premises sources|Local sources (SQL, Excel...)|
|**Sharing with Others**|✅ Yes|❌ No|
|**Supported Connections**|Import, Scheduled Refresh, **DirectQuery, Live Connection**|Import, Scheduled Refresh **ONLY**|
|**Data Management**|**Centralized** (by Admin)|**User manages** their own|
|**Data Supervision**|**Central system** to oversee|**No central supervision**|
|**Compatibility**|Power BI, Power Apps, Power Automate, etc.|**Power BI only**|
### How Gateways Work (Security)
- The gateway is installed on a server within the local domain.
- Credentials for data sources are entered in Power BI, **encrypted**, stored in the cloud, and can **only be decrypted by the gateway**.
- When the Power BI service needs data, it sends an encrypted request to the gateway.
- The gateway decrypts the credentials, connects to the on-premises source, executes the query, and sends the results back securely to the Power BI service.
- The connection is **outbound**, minimizing security vulnerabilities.
### Business Use Cases
- **Centralized Access:** Ensures teams across different locations or departments have uniform, secure access to the same on-premises data sources.
- **Up-to-Date Data:** Enables scheduled refreshes and DirectQuery, ensuring reports and analyses in the Power BI service reflect the latest on-premises data.
- **Enhanced Security:** Minimizes direct connections to on-premises sources; only the gateway communicates directly with the data, providing an added layer of security.
### Gateway Configuration in the Power BI Service
After the gateway software is installed, an administrator must configure it in the Power BI service before it can be used for scheduled refreshes.
- **Add a Data Source to the Gateway:**
    1. In the Power BI Service, go to **Settings > Manage connections and gateways**.
    2. Select the gateway cluster.
    3. Add a new **connection** (data source), providing the server name, database name, and authentication method.
### Key Considerations
- **Credentials:** A common cause of refresh failures with a gateway is out-of-date credentials for the data source. These must be kept updated in the connection settings.
- **Cloud Sources:** You do **not** need a gateway to connect to cloud services like SharePoint, OneDrive, OneDrive for Business or Azure SQL Database, as the data is already in the cloud.
### Setting Up a Personal Gateway and Scheduled Refresh
This note outlines the steps to install the Personal Mode gateway on your computer and configure a dataset for scheduled refresh using that gateway.
[Install an on-premises data gateway | Microsoft Learn](https://learn.microsoft.com/en-us/data-integration/gateway/service-gateway-install)
#### 1. Download and Install the Gateway (Personal Mode)
1. **Download:** Get the **personal mode** gateway installer from the Power BI gateway download page.
2. **Install:** Run the installer. When prompted, sign in using your Power BI service account email and password.
3. **Verify:** Confirm the gateway application shows it is running and online. Keep this application running on your computer for refreshes to work.
#### 2. Connect Dataset to Gateway in Power BI Service
After publishing a report that uses an on-premises data source to the Power BI service:
1. **Go to Dataset Settings:** In your workspace, find the dataset, hover over it, and select the **Schedule refresh** icon.
2. **Check Gateway Connection:** Scroll down to the **Gateway and cloud connections** section. Your personal gateway should be listed and running.
3. **Edit Credentials:**
    - Go to the **Data source credentials** section.
    - Select **Edit credentials**.
    - In the configuration pop-up, choose the appropriate **Authentication method** (e.g., `Windows without Impersonation`).
    - Set the **Privacy level** (typically `Organizational`).
    - Select **Sign In** and provide the necessary credentials for the _data source itself_.
#### 3. Configure the Scheduled Refresh
Once the gateway connection and credentials are set:
1. Scroll down to the **Refresh** section in the dataset settings.
2. Turn the **Scheduled refresh** toggle to **On**.
3. Select the desired **Refresh frequency** (e.g., `Daily`).
4. Choose the correct **Time zone**.
5. Add the specific **Time(s)** you want the refresh to run.
6. Select **Apply**.
The dataset is now configured to automatically refresh using your personal gateway according to the schedule you set. Remember, your computer with the personal gateway installed must be turned on and connected to the internet at the scheduled refresh times.

> [!Note]
> - You can configure up to **8 daily time** slots, if your semantic model is on shared capacity, or **48 time** slots on Power BI Premium. 
> - If there are **4 consecutive semantic model refresh failures**, the refresh schedule will be automatically disabled.
