

---

![[reading/DP-900/Exam Prep/attachments/Pasted image 20250717221752.png]]

> **JSON + Schema ยืดหยุ่น + เขียนเยอะ → Document store**
> 👉 เหมาะสุดสำหรับการเขียนข้อมูลแบบ flexible ที่ไม่รู้ล่วงหน้าว่าจะมี field อะไรบ้าง

|**ประเภท**|**โครงสร้างข้อมูล**|**เหมาะกับงาน**|**จุดเด่น**|**จุดอ่อน**|**ตัวอย่างฐานข้อมูล**|
|---|---|---|---|---|---|
|🗂️ **Document**|JSON, BSON, XML|- แอปที่ข้อมูลมี schema ยืดหยุ่น- เก็บข้อมูลแบบเอกสาร (user profile, order, etc.)- รองรับ query แบบเจาะ field ได้|- รองรับ semi-structured data- Flexible schema- Query ได้ละเอียด|- ช้ากว่า key/valueถ้า query บ่อย ๆ บน field ซับซ้อนอาจช้า|- **Azure Cosmos DB (MongoDB API)**- **MongoDB**, Couchbase|
|🔑 **Key/Value**|Key → Value blob|- Session store- Cache- Lookup ตาม key อย่างเดียว|- เร็วมาก (low latency)- Simple API|- Query field ย่อยใน value ไม่ได้- No secondary index|- **Azure Table Storage**- Redis, DynamoDB (mode)|
|📊 **Columnar**|Column-based tables|- Analytics, BI workload- อ่านข้อมูลจำนวนมาก (OLAP)- Query คอลัมน์เฉพาะ|- อ่านเฉพาะ column ได้เร็วมาก- เหมาะกับการ Aggregate|- เขียนช้ากว่า row store- ไม่เหมาะกับ transaction|- **Azure Synapse**, **Apache Parquet**, BigQuery|
|🔗 **Graph**|Node + Edge (ความสัมพันธ์)|- ระบบความสัมพันธ์ซับซ้อน (เช่น social graph)- ระบบ recommendation- Network traversal|- Query ความสัมพันธ์ซับซ้อนได้ดี- เหมาะกับ “เชื่อมโยงหลาย hop”|- ไม่เหมาะกับ data ปกติที่ไม่เชื่อมกัน|- **Azure Cosmos DB (Gremlin API)**- Neo4j, Amazon Neptune|

| **รูปแบบ**    | **คำจำ**                          |
| ------------- | --------------------------------- |
| **Document**  | “เก็บ JSON, schema ยืดหยุ่น”      |
| **Key/Value** | “เร็วสุด, คีย์เดียว, ไม่มี query” |
| **Columnar**  | “อ่านเร็ว, วิเคราะห์, BI”         |
| **Graph**     | “เน้นความสัมพันธ์, hop ไป hop มา” |

---

![[reading/DP-900/Exam Prep/attachments/Pasted image 20250717222149.png]]

---

![[reading/DP-900/Exam Prep/attachments/Pasted image 20250717222324.png]]

---
![[reading/DP-900/Exam Prep/attachments/Pasted image 20250717222422.png]]

![[reading/DP-900/Exam Prep/attachments/Pasted image 20250718084038.png]]

### OLTP characteristic 

| **ตัวเลือก**                           | **✔/✘** | **คำอธิบาย**                                                             |
| -------------------------------------- | ------- | ------------------------------------------------------------------------ |
| **A. denormalized data**               | ❌       | Denormalized ใช้ใน OLAP (data warehouse) เพื่อให้อ่านเร็ว, ไม่ใช่ OLTP   |
| **B. heavy writes and moderate reads** | ✅       | OLTP = เขียนบ่อย เช่น insert, update (คำสั่ง transaction แบบ real-time)  |
| **C. light writes and heavy reads**    | ❌       | อธิบายลักษณะของ OLAP (เช่น BI tools, report) ไม่ใช่ OLTP                 |
| **D. schema on write**                 | ✅       | OLTP ต้องกำหนด schema ชัดเจนก่อนเขียน (SQL/relational DB)                |
| **E. schema on read**                  | ❌       | ใช้ใน NoSQL/document DB เช่น MongoDB → OLAP หรือ flexible storage        |
| **F. normalized data**                 | ✅       | OLTP ต้อง normalized เพื่อ **ลด duplication, เพิ่มความถูกต้องของข้อมูล** |

---


