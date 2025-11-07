[Get started creating paginated reports in the Power BI service - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/paginated-reports/web-authoring/get-started-paginated-formatted-table)
### 1. What is a Paginated Report?
A **paginated report** is a type of report designed to be printed or shared as a document. Unlike standard Power BI reports, which are optimized for interactive exploration, paginated reports are formatted to fit well on a page, hence the name "paginated."
Power BI paginated reports are descendants of SQL Server Reporting Services.
### 2. Key Characteristics and Use Cases
Understanding when to use a paginated report is crucial for the exam.

| **Characteristic**         | **Description**                                                                                                              |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **Pixel-Perfect Layout**   | The layout is highly controlled and precise. It's designed to look exactly the same when printed or exported as a PDF.       |
| **Optimized for Printing** | The primary purpose is to create documents for printing or static sharing (e.g., invoices, statements, operational reports). |
| **Handles Large Tables**   | Paginated reports excel at displaying long, detailed tables that can span multiple pages with repeating headers and footers. |
| **Common File Format**     | They are saved as `.rdl` (Report Definition Language) files.                                                                 |
**Classic Use Cases:**
- Generating invoices or financial statements.
- Printing detailed inventory lists or operational reports.
- Creating mailing labels or certificates.
- Export data from reports in printing format.
### 3. Authoring Tools
- **Power BI Report Builder:** This is the primary, free, standalone application used to design and author paginated reports.
- **Power BI Service (Online Editor):** You can now also create and edit paginated reports directly in the Power BI service. This online editor does **not** have all the advanced functionality of Report Builder.
### 4. How to Create a Paginated Report
You can start the creation process from several places, most of which will launch the online editor in the Power BI service.
- **From a Workspace:** In the list view, select the **More options (...)** for a Power BI semantic model and choose **Create formatted table** or **Create paginated report**.
	- ![Screenshot of Create paginated report in the Power BI service.](https://learn.microsoft.com/en-us/power-bi/paginated-reports/web-authoring/media/paginated-formatted-table/formatted-table-list-view-1.png)
- **From the Data Hub:** Find a dataset in the Data hub, select its **More options (...)**, and choose **Create paginated report**.
	- ![Screenshot of Create paginated report in the Data hub.](https://learn.microsoft.com/en-us/power-bi/paginated-reports/web-authoring/media/paginated-formatted-table/formatted-table-data-hub-1.png)
- **From Power BI Desktop:** On the **Insert** tab, you can add a **Paginated report visual** to your canvas and then click **"Create paginated report"** to launch the service.
	- Open Power BI Desktop, and on the **Insert** tab, select **Visual gallery**. Scroll down to the **Other** section > select **Paginated report**.
	- ![creating a paginated report in Power BI Desktop.](https://learn.microsoft.com/en-us/power-bi/paginated-reports/web-authoring/media/get-started-paginated-formatted-table/create-paginated-desktop-visual-gallery.png)
	- In the visual, select **Create paginated report**.
	- ![select Create paginated report.](https://learn.microsoft.com/en-us/power-bi/paginated-reports/web-authoring/media/get-started-paginated-formatted-table/create-paginated-report-desktop.png)
	- The Power BI service opens.
	- In the **Choose the data you want to connect**, filter or browse to the dataset you want, and **Connect**.
	- ![Choose the data you want to connect.](https://learn.microsoft.com/en-us/power-bi/paginated-reports/web-authoring/media/get-started-paginated-formatted-table/paginated-choose-data-sevice.png)

### 5. Licensing and Permissions
The licensing requirements for paginated reports (`.rdl` files) are the same as for standard Power BI reports (`.pbix` files).
- **To Download Report Builder:** It is **free** for everyone.
- **To Publish to "My Workspace":** You can do this with a **Free** license.
- **To Publish to a Shared Workspace:** You need a **Power BI Pro** or **PPU** license and at least a **Contributor** role in that workspace.
- **To Build a Report:** You need **Build permission** on the dataset you are connecting to.
### 6. Considerations and Limitations
- **Data Sources:** You can create a paginated report in any workspace.
- **Analysis Services Limitation:** You **cannot** create a paginated report from a Power BI semantic model that is based on a live connection to **SQL Server Analysis Services (SSAS)** or **Azure Analysis Services (AAS)**. In these cases, you should connect your paginated report directly to the underlying SSAS/AAS database instead.