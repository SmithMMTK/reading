
## Medallion architecture (bronze, silver and gold)

**Medallion Architecture** คือ แนวทางการจัดชั้นข้อมูลใน **Data Lakehouse** ให้เป็นลำดับขั้นตอนเพื่อการจัดการข้อมูลที่มีคุณภาพ โดยแบ่งออกเป็น 3 ชั้นหลัก ๆ ได้แก่ **Bronze**, **Silver**, และ **Gold** ซึ่งแนวคิดนี้นิยมใช้กับแพลตฟอร์มที่รองรับ **Delta Lake** เช่น **Databricks**, **Microsoft Fabric** และ **Azure Synapse**

```text
[Raw IoT Data]        [Sales CSVs]        [Web Logs]
      │                   │                   │
      ▼                   ▼                   ▼
  -----------        ------------        -------------
 |  Bronze   |      |   Bronze   |      |   Bronze    |
 |  Raw IoT  |◄────►|  Raw Sales |◄────►|  Raw Logs   |
  -----------        ------------        -------------
      │ (clean, filter, join)
      ▼
  ----------------------------
 |         Silver             |
 | IoT with timestamps,       |
 | Sales with customer info, |
 | Logs joined with users     |
  ----------------------------
      │ (aggregate, calculate KPIs)
      ▼
  --------------------------
 |         Gold             |
 | Daily KPIs, Revenue,     |
 | Customer Segmentation    |
  --------------------------
```

### **🏅 Medallion Architecture Overview**

| **ชั้นข้อมูล** | **ชื่อ**                 | **ลักษณะ**                                             | **วัตถุประสงค์**                                                                 |
| -------------- | ------------------------ | ------------------------------------------------------ | -------------------------------------------------------------------------------- |
| 🥉 **Bronze**  | Raw Layer                | ข้อมูลดิบจากแหล่งต่าง ๆ เช่น Logs, IoT, APIs           | จัดเก็บข้อมูล **แบบไม่เปลี่ยนแปลง** เพื่อเป็นจุดอ้างอิงต้นฉบับ (source of truth) |
| 🥈 **Silver**  | Cleaned / Refined Layer  | ข้อมูลที่ผ่านการแปลง เช่น การทำความสะอาด, join, enrich | เตรียมข้อมูลให้เหมาะกับการวิเคราะห์หรือใช้งานต่อได้โดยง่าย                       |
| 🥇 **Gold**    | Business / Curated Layer | ข้อมูลระดับธุรกิจ เช่น metrics, KPIs                   | ใช้สำหรับการ **วิเคราะห์เชิงธุรกิจ, dashboard, ML models**                       |

## **🛡️** **Fabric Permission Matrix – Focus on Lakehouse Access**

| **Permission / Role**                      | **ใช้กับ**     | **เข้าถึง SQL Endpoint (Delta)** | **เข้าถึง Spark (Notebooks)** | **เห็น Bronze/Silver** | **เหมาะกับ**                                   |
| ------------------------------------------ | -------------- | -------------------------------- | ----------------------------- | ---------------------- | ---------------------------------------------- |
| **Workspace Viewer**                       | Workspace      | ✅ ได้ทั้งหมด                     | ✅ ได้ทั้งหมด                  | ✅ ได้ทั้งหมด           | 🔥 ขัดกับ RLS หรือ Isolation Requirement       |
| **Lakehouse Viewer (default)**             | Lakehouse      | ❌                                | ❌                             | ❌                      | ยังต้องตั้งสิทธิ์เพิ่ม                         |
| **Read all SQL Endpoint data**             | Lakehouse      | ✅ **อ่าน Delta เท่านั้น**        | ❌                             | ❌                      | ✅ เหมาะกับ Data Analysts ที่ต้องเห็นเฉพาะ Gold |
| **Read all Apache Spark data**             | Lakehouse      | ✅                                | ✅                             | ✅                      | ❌ ขัดกับ policy ไม่ให้แตะ Bronze/Silver        |
| **Build reports on semantic model**        | Semantic Model | ❌                                | ❌                             | ❌                      | ใช้กับ Power BI ไม่ใช่ Lakehouse               |
| **Contributor / Member (Workspace Level)** | Workspace      | ✅                                | ✅                             | ✅                      | ✅ สำหรับ Data Engineers เท่านั้น               |

## **✅ Keyword จำง่าย:**

- **SQL Endpoint = ปลอดภัย อ่านอย่างเดียว**
- **Spark = แรงและอันตรายสำหรับ Analysts**
- **Workspace Viewer = เห็นหมดทุกอย่าง (ไม่ควรให้ Data Analysts)**


## Data store properties

https://learn.microsoft.com/en-us/fabric/fundamentals/decision-guide-data-store

| Table 1 of 2                      | **[Lakehouse](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-overview)**                                       | **[Warehouse](https://learn.microsoft.com/en-us/fabric/data-warehouse/data-warehousing)**                                                                                                                                                                                                                                                                                                   | **[Eventhouse](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/eventhouse)**                                                                                                           |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Data volume**                   | Unlimited                                                                                                                           | Unlimited                                                                                                                                                                                                                                                                                                                                                                                   | Unlimited                                                                                                                                                                                              |
| **Type of data**                  | Unstructured,  <br>semi-structured,  <br>structured                                                                                 | Structured,  <br>semi-structured (JSON)                                                                                                                                                                                                                                                                                                                                                     | Unstructured,  <br>semi-structured,  <br>structured                                                                                                                                                    |
| **Primary developer persona**     | Data engineer, data scientist                                                                                                       | Data warehouse developer, data architect, data engineer, database developer                                                                                                                                                                                                                                                                                                                 | App developer, data scientist, data engineer                                                                                                                                                           |
| **Primary dev skill**             | Spark (Scala, PySpark, Spark SQL, R)                                                                                                | SQL                                                                                                                                                                                                                                                                                                                                                                                         | No code, KQL, SQL                                                                                                                                                                                      |
| **Data organized by**             | Folders and files, databases, and tables                                                                                            | Databases, schemas, and tables                                                                                                                                                                                                                                                                                                                                                              | Databases, schemas, and tables                                                                                                                                                                         |
| **Read operations**               | Spark, T-SQL                                                                                                                        | T-SQL, Spark*                                                                                                                                                                                                                                                                                                                                                                               | KQL, T-SQL, Spark                                                                                                                                                                                      |
| **Write operations**              | Spark (Scala, PySpark, Spark SQL, R)                                                                                                | T-SQL                                                                                                                                                                                                                                                                                                                                                                                       | KQL, Spark, connector ecosystem                                                                                                                                                                        |
| **Multi-table transactions**      | No                                                                                                                                  | Yes                                                                                                                                                                                                                                                                                                                                                                                         | Yes, for [multi-table ingestion](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/management/updatepolicy?context=%2Ffabric%2Fcontext%2Fcontext-rta&pivots=fabric#the-update-policy-object) |
| **Primary development interface** | Spark notebooks, Spark job definitions                                                                                              | SQL scripts                                                                                                                                                                                                                                                                                                                                                                                 | KQL Queryset, KQL Database                                                                                                                                                                             |
| **Security**                      | RLS, CLS**, [table level](https://learn.microsoft.com/en-us/fabric/data-warehouse/sql-granular-permissions) (T-SQL), none for Spark | [Object level](https://learn.microsoft.com/en-us/fabric/data-warehouse/sql-granular-permissions), [RLS](https://learn.microsoft.com/en-us/fabric/data-warehouse/column-level-security), [CLS](https://learn.microsoft.com/en-us/fabric/data-warehouse/column-level-security), DDL/DML, [dynamic data masking](https://learn.microsoft.com/en-us/fabric/data-warehouse/dynamic-data-masking) | RLS                                                                                                                                                                                                    |
| **Access data via shortcuts**     | Yes                                                                                                                                 | Yes, via SQL analytics endpoint                                                                                                                                                                                                                                                                                                                                                             | Yes                                                                                                                                                                                                    |
| **Can be a source for shortcuts** | Yes (files and tables)                                                                                                              | Yes (tables)                                                                                                                                                                                                                                                                                                                                                                                | Yes                                                                                                                                                                                                    |
| **Query across items**            | Yes                                                                                                                                 | Yes                                                                                                                                                                                                                                                                                                                                                                                         | Yes                                                                                                                                                                                                    |
| **Advanced analytics**            | Interface for large-scale data processing, built-in data parallelism, and fault tolerance                                           | Interface for large-scale data processing, built-in data parallelism, and fault tolerance                                                                                                                                                                                                                                                                                                   | Time Series native elements, full geo-spatial and query capabilities                                                                                                                                   |
| **Advanced formatting support**   | Tables defined using PARQUET, CSV, AVRO, JSON, and any Apache Hive compatible file format                                           | Tables defined using PARQUET, CSV, AVRO, JSON, and any Apache Hive compatible file format                                                                                                                                                                                                                                                                                                   | Full indexing for free text and semi-structured data like JSON                                                                                                                                         |
| **Ingestion latency**             | Available instantly for querying                                                                                                    | Available instantly for querying                                                                                                                                                                                                                                                                                                                                                            | Queued ingestion, streaming ingestion has a couple of seconds latency                                                                                                                                  |

---

## Group By Cheat Sheet

| **คำสั่ง**                           | **ใช้เมื่อ…**      | **ได้ผลลัพธ์อะไรบ้าง**                          | **ตรงกับโจทย์แบบไหน**            |
| ------------------------------------ | ------------------ | ----------------------------------------------- | -------------------------------- |
| ROLLUP(col1, col2)                   | รวมแบบลำดับชั้น    | ✅ col1+col2✅ col1 only✅ Grand total (null,null) | ❌ รวมมากเกินไป                   |
| CUBE(col1, col2)                     | ทุก combination    | ✅ col1+col2✅ col1 only✅ col2 only✅ Grand total  | ❌ เกินความต้องการ                |
| GROUPING SETS ((col1, col2), (col1)) | คุมได้ว่าจะรวมอะไร | ✅ col1+col2✅ col1 only                          | ✅ ตรงโจทย์ที่ให้รวมตามปีเท่านั้น |
## **🧠 วิธีจำแบบเร็ว:**

- **ROLLUP** = **R**oll ขึ้นทีละชั้น → ปี ➜ ปีรวม ➜ รวมทั้งหมด
- **CUBE** = รูปทรงลูกบาศก์ ➜ ทุกมุม ทุกมิติ
- **GROUPING SETS** = ระบุเอง อยากได้อะไรบ้าง
    → ใช้ในข้อสอบที่บอกว่า:
    > “ต้องมีรวมตามปีด้วย” (แต่ไม่พูดถึง total)
    

---
## High concurrency mode in Apache Spark for Fabric

https://learn.microsoft.com/en-us/fabric/data-engineering/high-concurrency-overview

---

### **Fabric Security Cheat Sheet – Warehouse vs Lakehouse**

| **Feature / Security Control**        | **Warehouse** **🏢**              | **Lakehouse** **🧪**                | **Notes**                                                      |
| ------------------------------------- | --------------------------------- | ----------------------------------- | -------------------------------------------------------------- |
| **DDM** (Dynamic Data Masking)        | ✅ รองรับ                          | ❌ ไม่รองรับ                         | ใช้ MASKED WITH (FUNCTION = '...') เพื่อปิดบังข้อมูลบาง column |
| **RLS** (Row-Level Security)          | ✅ รองรับ                          | ❌ ไม่รองรับ                         | ใช้ CREATE SECURITY POLICY ควบคุมการเข้าถึงระดับแถว            |
| **OLS** (Object-Level Security)       | ✅ รองรับ                          | ❌ ไม่รองรับ                         | จำกัดการเข้าถึง table/view ตาม user/role                       |
| **Column-Level Security**             | ✅ รองรับ                          | ❌ ไม่รองรับ                         | ซ่อนหรือแสดง column บางอันให้ user บางคนได้                    |
| **Fine-grained Access Control**       | ✅ มี                              | ❌ ไม่มี                             | Lakehouse ต้องใช้วิธีแยก workspace/lakehouse                   |
| **Permission Granularity**            | Table, Column, Row                | All-or-nothing (at lakehouse level) | Lakehouse ใช้ role ที่ workspace เท่านั้น                      |
| **T-SQL Security Features**           | ✅ เต็มรูปแบบ                      | ❌ ไม่รองรับ                         | เช่น GRANT, DENY, REVOKE                                       |
| **Data Sensitivity Labels (Purview)** | ✅ (integrated)                    | ⏳ ไม่รองรับ (อาจมาในอนาคต)          | Warehouse รองรับ data governance ดีกว่า                        |
| **เหมาะสำหรับ**                       | Analytics + Security + Compliance | Data Engineering + ML + Big Data    | ขึ้นกับ use case                                               |

---

## Row-Level Security in Fabric DW

การ implement **RLS** ใน Fabric Warehouse (เช่นเดียวกับ Azure SQL / Synapse DW) ใช้ 2 องค์ประกอบหลัก:

1. **Inline Table-Valued Function (TVF)**
    ใช้สำหรับระบุ logic การตรวจสอบว่า user แต่ละคนควรเห็นแถวไหน
2. **Security Policy**
    ใช้ CREATE SECURITY POLICY เพื่อผูก function เข้ากับ table ที่ต้องการควบคุม

---

## Supported items on Deployment Pipelines

https://learn.microsoft.com/en-us/fabric/cicd/deployment-pipelines/intro-to-deployment-pipelines?tabs=new-ui#supported-items

When you deploy content from one pipeline stage to another, the copied content can contain the following items:

- Data Engineering items:
    - [Environment](https://learn.microsoft.com/en-us/fabric/data-engineering/environment-git-and-deployment-pipeline#set-up-a-deployment-pipeline-for-an-environment)
    - [GraphQL](https://learn.microsoft.com/en-us/fabric/data-engineering/graphql-source-control-and-deployment#api-for-graphql-in-deployment-pipeline) _(preview)_
    - [Lakehouse](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-git-deployment-pipelines#lakehouse-in-deployment-pipelines) _(preview)_
    - [Notebook](https://learn.microsoft.com/en-us/fabric/data-engineering/notebook-source-control-deployment#notebook-in-deployment-pipelines)
    - Spark Job Definitions _(preview)_
    - User Data Functions _(preview)_
- Data Factory items:
    - [Copy Job](https://learn.microsoft.com/en-us/fabric/data-factory/cicd-copy-job#deployment-pipelines-for-git) _(preview)_
    - [Dataflows gen2](https://learn.microsoft.com/en-us/fabric/data-factory/dataflow-gen2-cicd-and-git-integration)
    - [Data pipeline](https://learn.microsoft.com/en-us/fabric/data-factory/cicd-pipelines)
    - [Mirrored database](https://learn.microsoft.com/en-us/fabric/database/mirrored-database/mirrored-database-cicd#mirrored-database-in-deployment-pipelines)
    - Mount ADF _(preview)_
    - [Variable library](https://learn.microsoft.com/en-us/fabric/cicd/variable-library/variable-library-cicd#variable-libraries-and-deployment-pipelines) _(preview)_
- Real-time Intelligence items:
    - [Activator](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/git-deployment-pipelines) _(preview)_
    - [Digital twin builder](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/digital-twin-builder/overview) _(preview)_
    - [Eventhouse](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/git-deployment-pipelines)
    - [EventStream](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/event-streams/eventstream-cicd#deploy-eventstream-items-from-one-stage-to-another)
    - [KQL database](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/git-deployment-pipelines)
    - [KQL Queryset](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/git-deployment-pipelines)
    - [Real-time Dashboard](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/git-deployment-pipelines)
- Data Warehouse items:
    - [Warehouse](https://learn.microsoft.com/en-us/fabric/data-warehouse/source-control#deployment-pipelines) _(preview)_
    - Mirrored Azure Databricks Catalog _(preview)_
- Power BI items:
    - Dashboard _(preview)_
    - Dataflow _(preview)_
    - Datamart _(preview)_
    - [Org app](https://learn.microsoft.com/en-us/power-bi/consumer/org-app-items/org-app-cicd) _(preview)_
    - Paginated report _(preview)_
    - Report (based on supported semantic models) _(preview)_
    - Semantic model (that originates from a .pbix file and isn't a PUSH dataset) _(preview)_
- Database items:
    - [SQL database](https://learn.microsoft.com/en-us/fabric/database/sql/deployment-pipelines) _(preview)_
- Industry solutions:
    - [Healthcare](https://learn.microsoft.com/en-us/industry/healthcare/healthcare-data-solutions/application-lifecycle-management) _(preview)_
    - HealthCare Cohort _(preview)_

---

## Eventhouse OneLake Availability

https://learn.microsoft.com/en-us/fabric/real-time-intelligence/event-house-onelake-availability#turn-on-onelake-availability

### How it works

You can turn on **OneLake availability** at the database or table level. When enabled at the database level, all new tables and their data are made available in OneLake. When turning on the feature, you can also choose to apply this option to existing tables by selecting the _Apply to existing tables_ option, to include historic backfill.

```python
delta_table_path = "abfss://`<workspaceGuid>`@onelake.dfs.fabric.microsoft.com/`<eventhouseGuid>`/Tables/`<tableName>`"

df = spark.read.format("delta").load(delta_table_path)

df.show()
```

### Adaptive behavior

Eventhouse offers a robust mechanism that intelligently batches incoming data streams into one or more Parquet files, structured for analysis. Batching data streams is important when dealing with trickling data. Writing many small Parquet files into the lake can be inefficient resulting in higher costs and poor performance.

Eventhouse's adaptive mechanism can delay write operations if there isn't enough data to create optimal Parquet files. This behavior ensures Parquet files are optimal in size and adhere to Delta Lake best practices. The Eventhouse adaptive mechanism ensures that the Parquet files are primed for analysis and balances the need for prompt data availability with cost and performance considerations.

---

## Caching

https://learn.microsoft.com/en-us/fabric/onelake/onelake-shortcuts#caching

|**หัวข้อ**|**รายละเอียด**|
|---|---|
|🔄 **หน้าที่ของ Shortcut Caching**|ช่วยลด **egress cost** (ค่าใช้จ่ายในการดึงข้อมูลข้ามคลาวด์) โดยเก็บไฟล์ที่อ่านจาก shortcut ไว้ใน cache|
|🧠 **การทำงานของ Cache**|- เมื่อมีการอ่านไฟล์ผ่าน shortcut → ระบบจะ **เก็บไฟล์ไว้ใน cache**- การอ่านครั้งต่อไปจะใช้ไฟล์จาก cache แทน remote|
|🕓 **Retention Period**|- ตั้งได้ระหว่าง **1-28 วัน**- **ถูก reset ทุกครั้งที่มีการเข้าถึงไฟล์**|
|🔄 **ไฟล์อัปเดต**|ถ้า remote storage มีไฟล์ใหม่กว่า cache → จะใช้ไฟล์จาก remote และ **อัปเดต cache ด้วยไฟล์ใหม่**|
|🧹 **การลบ Cache**|- หากไฟล์ไม่ได้ถูกอ่านเกินช่วง retention → **จะถูกลบอัตโนมัติ**- ไฟล์ที่ใหญ่เกิน **1 GB จะไม่ถูก cache**|
|📦 **รองรับ Shortcut จาก**|- GCS- S3- S3-compatible- On-premises data gateway|
|⚙️ **เปิดใช้งาน**|- ที่ **Workspace settings > OneLake tab**- เปิด toggle และตั้ง retention period|
|🧼 **Reset Cache**|- มีปุ่มให้กด **ล้าง cache ทั้งหมดใน workspace**|
### **🎯 จำให้แม่นก่อนสอบ**

- ✔ Shortcut caching = ลดต้นทุน + เพิ่ม performance
- ✔ ใช้ได้เฉพาะ shortcut ที่มาจาก S3, GCS, etc.
- ✔ ไฟล์ที่ใหญ่เกิน 1 GB ไม่เข้า cache
- ✔ Reset retention ทุกครั้งที่มีคนอ่านไฟล์
- ✔ ถ้าไฟล์ต้นทางใหม่กว่า → cache จะถูกอัปเดตตาม
- ✔ Clear cache ได้เองผ่าน UI


