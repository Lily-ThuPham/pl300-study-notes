[Real-time streaming in Power BI - Power BI | Microsoft Learn](https://learn.microsoft.com/en-us/power-bi/connect-data/service-real-time-streaming#push-dataset)
Power BI allows you to stream live data and update visuals in real-time. This is used for monitoring time-sensitive data, such as factory sensors, social media feeds, or service metrics.
_(Note: The creation of new streaming models is scheduled for retirement in October 2027, but the concepts and existing models are still relevant.)_

---

### 1. Types of Real-Time Semantic Models

Power BI offers three types of real-time semantic models. The main difference between them is **where the data is stored**.

| **Capability**                          | **Push Semantic Model**                                                | **Streaming Semantic Model**                                               | **PubNub Streaming Model**                                                 |
| --------------------------------------- | ---------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| **Data Storage**                        | Data is **stored permanently** in a database in the Power BI service.  | Data is stored **temporarily** in a cache (e.g., for one hour).            | **No data is stored** in Power BI at all.                                  |
| **Build Reports (Historical Analysis)** | ✅ **Yes**. You can build full Power BI reports on the historical data. | ❌ **No**. You cannot build reports as there is no underlying database.     | ❌ **No**. You cannot build reports.                                        |
| **How to Visualize**                    | 1. Report visuals (which can be pinned to a dashboard). 2. Q&A.        | **Only** by adding a "Custom Streaming Data" tile directly to a dashboard. | **Only** by adding a "Custom Streaming Data" tile directly to a dashboard. |
| **Dashboard Tile Updates**              | Updates in real-time when data is pushed.                              | Updates in real-time with smooth animations.                               | Updates in real-time with smooth animations.                               |
| **Data Ingestion**                      | Max 16 MB per request; 1 million rows/hour.                            | Max 15 KB per request (5 requests/sec).                                    | N/A (Data is not pushed to Power BI).                                      |

---
### 2. The "pushStreaming" Model (The Best of Both)
When you create a new streaming dataset in the Power BI service UI, you are given a critical option:
**"Historic data analysis"**
- **If turned OFF (default):** You create a standard **Streaming semantic model**. Data is only stored in a temporary cache. You _cannot_ build reports on it.
- **If turned ON:** You create a hybrid model that is **both a streaming model AND a push model**.
    - You get the benefit of **low-latency streaming tiles** on a dashboard.
    - You also get the benefit of a **permanent database** storing all the data, allowing you to build standard Power BI reports on the history.  
- **Azure Stream Analytics** automatically creates this hybrid `pushStreaming` model when it outputs to Power BI.
### 3. How to Push Data to a Semantic Model
There are three primary methods to get data into a real-time model:
1. **Power BI REST APIs:** The most flexible method for developers to create and send data to push and streaming models.
2. **Streaming Semantic Model UI:** In the Power BI service, select **New > Streaming dataset** and choose **API**, **Azure Stream**, or **PubNub**. This UI is where you find the "Historic data analysis" toggle.
3. **Azure Stream Analytics:** You can add Power BI as an output within an Azure Stream Analytics job to visualize data streams in real-time.
### 4. How to Visualize Streaming Data
There are two distinct ways to visualize this data, which are often confused:
- **For True Real-Time (Streaming):**
    1. Go to a **Dashboard** (this does not work in a Report).
    2. Select **Edit > Add a tile**.
    3. Choose **Custom Streaming Data**.
    4. Select your streaming dataset and configure the visual (e.g., a line chart, card, or gauge).
    5. This tile will now update instantly as new data is pushed.
- **For Historical Analysis (Reporting):**
    1. This is only possible if you enabled **"Historic data analysis"** (creating a push model).
    2. Open **Power BI Desktop** and connect to the Power BI semantic model you created.
    3. Build a standard report with any visuals you want.
    4. **Note:** These report visuals **do not** update in real-time. To make them refresh automatically, you must also configure **Automatic Page Refresh (APR)**, which runs on a set interval (e.g., every 1 second).

### 5. Key Limitations
- **No Filtering:** You cannot filter a pure **streaming** semantic model. You can only filter **push** semantic models (in a report, which you then pin to a dashboard).
- **No Modeling:** You cannot create relationships or DAX measures on a pure **streaming** semantic model, as the data is not stored.
- **Q&A:** Q&A is only supported for **push** semantic models, as it requires a database to query.