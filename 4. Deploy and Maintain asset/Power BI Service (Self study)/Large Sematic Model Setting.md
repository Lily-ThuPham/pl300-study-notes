The **Large semantic model storage format** is a setting for workspaces in a **Premium or Fabric capacity** that allows a Power BI semantic model to grow beyond the default size limits, up to the size of the capacity itself.

**Key Benefits:**
- Enables semantic models to grow beyond 10 GB.
- Improves write performance when using **XMLA-based tools**, even for smaller models.

---
## How to Enable the Large Model Format

This setting can be enabled in several ways. The most common is on a per-model basis.
- **For an Existing Model (in the Service):** Go to the semantic model's **Settings**, expand the **Large semantic model storage format** section, and turn the slider to **On**.
- **As a Workspace Default:** In the workspace **Settings > Premium** tab, an admin can set the **Default storage format** to "Large semantic model storage format" for all _new_ models created in that workspace.
- **Using PowerShell:** Admins can use the `Set-PowerBIDataset` cmdlet to change a model's storage mode to `PremiumFiles`.

**Important Note:** Enabling this format does not change the 10 GB upload limit for a `.pbix` file from Power BI Desktop. The model grows beyond this limit in the service during subsequent data refreshes, often in conjunction with **incremental refresh**.

---
## Key Features of the Large Model Format

Enabling this format also turns on other advanced memory management features.
- **Semantic Model Eviction:** A Premium feature where Power BI can temporarily unload inactive semantic models from memory to make room for models that are being actively queried. When a user later queries an evicted model, they may experience a short delay as it is reloaded into memory.
- **On-Demand Load:** An enhancement to eviction. When an evicted model is queried, Power BI doesn't have to reload the entire model. Instead, it loads only the relevant data pages needed for that query, significantly improving the load time.

---

## Considerations and Limitations

- **Region Availability:** This feature is only available in Azure regions that support Azure Premium Files Storage.
- **Refresh Memory Requirements:** A full data refresh can require up to twice the memory of the semantic model's final size. A 12 GB model on a 25 GB capacity might fail a full refresh. Fine-grained refreshes using the **XMLA endpoint** are recommended in these cases.
- **Push Datasets:** Push semantic models do not support the large model format.