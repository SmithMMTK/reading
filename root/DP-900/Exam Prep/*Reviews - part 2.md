
![[Pasted image 20250718083210.png]]

https://learn.microsoft.com/en-us/power-bi/paginated-reports/paginated-reports-report-builder-power-bi

![Paginated](https://learn.microsoft.com/en-us/power-bi/paginated-reports/media/paginated-reports-report-builder-power-bi/power-bi-paginated-wwi-report-page.png)

**Required Power BI Report Builder**

---

|**คำศัพท์**|**คำอธิบายแบบง่าย**|**ตัวอย่าง**|**เทคนิคจำ**|
|---|---|---|---|
|**Dimension**|เป็น “มิติ” เช่น เวลา, สินค้า, พื้นที่|ปี, เดือน, วัน  ประเทศ, จังหวัด, อำเภอ|เป็น “ข้อมูลอ้างอิง” สำหรับการวิเคราะห์|
|**Hierarchy**|เป็น “ลำดับชั้นในมิติ”|ปี → ไตรมาส → เดือน → วัน|ใช้สำหรับ **drill down** และ **drill up**|
|**Fact table**|ตารางหลักที่เก็บค่าตัวเลข|ยอดขาย, ปริมาณ|ใช้คำนวณ ไม่ใช้สำหรับ drill|
|**Cube**|โครงสร้างรวมมิติ + ข้อมูล|OLAP Cube|ใหญ่เกินไป ใช้ในระดับรวม|
### **🎯 สรุปสั้น:**
- ถ้าโจทย์พูดถึงการ **drill up/down → ตอบ Hierarchy**
- ถ้าโจทย์พูดถึง **การจำแนกหรือกลุ่มมิติ → ตอบ Dimension**

```text
[ Dimension: "เวลา" ]
┌───────────────┐
│ ปี             │
│ เดือน          │
│ วัน            │
└───────────────┘
```

```text
[ Hierachy: "ลำดับขั้น = บันได" ]
ปี  
│
├──> ไตรมาส
│    └──> เดือน
│         └──> วัน
```

---

|**Workload Type**|**เน้นเรื่อง**|**ใช้ในงานแบบไหน**|**จำง่ายๆ**|
|---|---|---|---|
|**Transactional**|✅ Update, insert, delete|ระบบธุรกรรม เช่น การโอนเงิน, ซื้อสินค้า|“Transaction = การเปลี่ยนข้อมูลบ่อย”|
|**Graph**|❌ ไม่เน้น update แต่เน้น query ความสัมพันธ์|Friend-of-friend, recommendation, social graph|“Graph = ความสัมพันธ์เชิงลึก”|
|**Analytical**|วิเคราะห์ข้อมูลสรุป|BI, Dashboard|“Analytics = คิดย้อน ดูภาพรวม”|
|**Time Series**|ข้อมูลตามเวลา|IoT, เซ็นเซอร์, stock|“Time = ตามเส้นเวลา ไม่เน้นความสัมพันธ์”|

---

|**API Name**|**เหมาะกับข้อมูลแบบ**|**จำง่าย ๆ ว่า**|
|---|---|---|
|**Cassandra**|✅ Column-family|“Cassandra = Column-based”|
|**MongoDB**|Document (JSON-like)|“Mongo = JSON”|
|**Gremlin**|Graph (Vertex/Edge)|“Gremlin = Graph”|
|**Table**|Key-value|“Table API = Azure Table Storage, ไม่ใช่ column family”|

|**API**|**Query Language**|**SQL-based?**|**คำช่วยจำ**|
|---|---|---|---|
|**Cassandra**|✅ CQL|✅ ใช่|“Cassandra ≈ SQL แบบ NoSQL”|
|**MongoDB**|❌ JSON-style|❌ ไม่ใช่|“Mongo = Mongo-style ไม่ใช่ SQL”|
|**Table**|REST or SDK|❌ ไม่ใช่|“Table = Key-value (ไม่ใช่ SQL)”|
|**Gremlin**|Gremlin|❌ ไม่ใช่|“Graph = Gremlin (เดินกราฟ)”|

---

|**ตัวเลือก**|**ย้าย “ทั้งเซิร์ฟเวอร์” ได้ไหม**|**ต้องดูแล infra เองไหม**|**เหมาะกับ**|**สรุป**|
|---|---|---|---|---|
|**Azure SQL Database**|❌ เฉพาะ DB เดี่ยว|❌ (PaaS)|App ใหม่, SaaS|“เบาแต่ไม่ย้ายได้ทั้ง server”|
|**SQL Managed Instance**|✅ ย้ายทั้ง instance (หลาย DB, agent, login ฯลฯ)|❌ (PaaS)|Modernize ระบบเก่า|✅ ใช่ในคำถามนี้|
|**SQL on Azure VM**|✅ ย้ายได้หมด|✅ ต้องดูแล OS, patch|ต้องการฟีเจอร์พิเศษ|ไม่ตรงคำถาม เพราะยังต้องดูแล|

---

![[Pasted image 20250718093046.png]]

|**คำอธิบาย**|**บริการที่ตรง**|
|---|---|
|**Output data to Parquet format**|✅ **Azure Synapse Analytics**|
|**Store data that is in Parquet format**|✅ **Azure Data Lake Storage**|
|**Persist a tabular representation of data that is stored in Parquet format**|✅ **Azure SQL Database**|

---

|**แพลตฟอร์ม**|**คำอธิบายโดยย่อ**|
|---|---|
|**Microsoft Fabric**|แพลตฟอร์ม All-in-One สำหรับการทำ Data Engineering, BI, Real-time analytics บน Power BI ecosystem|
|**Azure Databricks**|แพลตฟอร์ม Big Data & AI analytics ที่สร้างบน Apache Spark เหมาะกับ Machine Learning, Data Science, และ ETL ที่ต้องการประสิทธิภาพสูง|
|**Azure Synapse**|แพลตฟอร์มสำหรับ Enterprise Data Warehousing และ Analytics ที่รองรับ SQL, Spark และการทำ BI pipeline|

| **หมวดหมู่**                 | **Microsoft Fabric**                       | **Azure Databricks**                         | **Azure Synapse Analytics**                     |
| ---------------------------- | ------------------------------------------ | -------------------------------------------- | ----------------------------------------------- |
| **แนวคิดหลัก**               | Unified SaaS data platform (BI-first)      | Unified big data & AI workspace (code-first) | Enterprise analytics integration platform       |
| **ใช้กับใครดี?**             | BI Analyst, Citizen Data Scientist         | Data Engineer, Data Scientist, ML Engineer   | BI, SQL Analyst, Data Engineer                  |
| **Data Engine**              | OneLake + DirectLake (delta-based)         | Apache Spark / Delta Lake                    | SQL Pool + Spark Pool                           |
| **UI/UX**                    | Low-code / Power BI-style interface        | Notebook-based (Jupyter/Databricks UI)       | Mixed: SQL Studio + Notebooks                   |
| **เหมาะกับงานประเภทใด**      | Reporting, Real-time dashboard, Light ML   | Large-scale data engineering, ML, AI         | Big SQL analytics, batch ETL, data integration  |
| **Language Support**         | Mostly DAX, Power Query (some Python, SQL) | Scala, Python, SQL, R                        | SQL, Spark (Python/Scala), T-SQL                |
| **Machine Learning**         | Basic ML in Power BI or Copilot            | Advanced ML + MLOps + AutoML                 | Integration with Azure ML                       |
| **Pricing Model**            | Capacity-based (Power BI Premium capacity) | DBU (Databricks Unit) + Azure infra          | Pay-per-query (serverless) or reserved capacity |
| **Integration กับ Power BI** | Native และแน่นมาก                          | มี แต่ต้องเชื่อมต่อ                          | มี แต่บางส่วนต้องใช้ connector                  |
| **Real-time Analytics**      | รองรับผ่าน KQL + Eventstream ใน Fabric     | รองรับ Structured Streaming                  | รองรับผ่าน Synapse Real-time Analytics (KQL)    |
If your focus is on data warehousing with high daily ingestion and the need for complex data processing, Azure Synapse Analytics would likely be a better fit. However, if your goal is to have a more streamlined analytics pipeline with a focus on self-service BI and Power BI integration, Microsoft Fabric could be a more efficient choice.

---

![[Pasted image 20250718100522.png]]

**Batch workloads** คือรูปแบบการประมวลผลข้อมูลที่:

- ไม่จำเป็นต้องเกิดขึ้นทันที
- ข้อมูลจะถูกสะสมไว้ในช่วงระยะเวลาหนึ่ง หรือจนกว่า “เงื่อนไข” บางอย่างจะสำเร็จ เช่น ถึงเวลา, จำนวนข้อมูลเพียงพอ, หรือทริกเกอร์จากเหตุการณ์ภายนอก
- แล้วค่อยนำข้อมูลทั้งหมดมาประมวลผลในชุดเดียว (batch)
---
### **❌ ตัวเลือกที่ไม่ถูกต้อง:**
- **“process data in memory, row-by-row.”** → อธิบายลักษณะงานแบบ _streaming_ หรือ _OLTP_ มากกว่า
- **“collect and process data at most once a day.”** → ข้อจำกัดที่ไม่จำเป็นของ batch; batch อาจทำได้บ่อยกว่านั้น เช่นทุก 10 นาที
- **“process data as new data is received in near real-time.”** → นี่เป็นลักษณะของ _streaming workloads_

---
![[Pasted image 20250718101913.png]]

![Diagram showing how the change feed works to provide an ordered log of changes to blobs](https://learn.microsoft.com/en-us/azure/storage/blobs/media/storage-blob-change-feed/change-feed-diagram.png)

https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-change-feed?tabs=azure-portal
---

![[Pasted image 20250718102355.png]]

| **คำศัพท์**      | **ความหมาย (จำง่าย ๆ)**                                                                   |
| ---------------- | ----------------------------------------------------------------------------------------- |
| **Attributes**   | คือ **คุณลักษณะ** ของ entity เช่น “ชื่อ”, “อายุ”, “อีเมล” → เป็น **columns** ในตาราง      |
| **Entities**     | คือ **สิ่งที่ต้องเก็บข้อมูล** เช่น “ลูกค้า”, “สินค้า” → แต่ละ entity จะกลายเป็น **table** |
| **Foreign keys** | คือ **กุญแจเชื่อมโยงระหว่างตาราง** เช่น CustomerId ใน Order → ใช้ **link ระหว่าง entity** |

---

https://learn.microsoft.com/en-us/azure/synapse-analytics/spark/apache-spark-what-is-delta-lake

Delta Lake is an open-source storage layer that brings ACID (atomicity, consistency, isolation, and durability) transactions to Apache Spark and big data workloads.

![[Pasted image 20250718102904.png]]

---

![[Pasted image 20250718144804.png]]

---

![[Pasted image 20250718150521.png]]

> จุดตัดของ “หลายมิติ” = จุดที่ได้ “ค่ารวม”
> ❌ ไม่ใช่ตัวมิติ (dimension)
> ✅ แต่คือค่าที่วัดได้ เช่นยอดขาย = “an aggregated measure”

---

![[Pasted image 20250718151830.png]]

---

![[Pasted image 20250718152253.png]]

---

![[Pasted image 20250718153824.png]]


---

![[Pasted image 20250718154537.png]]

|**Data storage option**|**Match with**|
|---|---|
|**Azure Blob Storage**|🎵 **Audio files**|
|**Azure Cosmos DB for NoSQL**|📄 **JSON documents**|
|**Azure SQL Database**|📊 **Tabular datasets**|

---

![[Pasted image 20250718154819.png]]

[[03-10 Identify Azure Cosmos DB APIs]]

---
![[Pasted image 20250718155012.png]]

---
![[Pasted image 20250718155102.png]]

