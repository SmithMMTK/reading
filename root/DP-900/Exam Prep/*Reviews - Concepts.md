
![[Pasted image 20250717152206.png]]

> **Normalization improves data integrity by** ensuring data consistency, minimizing duplication, maintaining valid relationships, and enforcing rules through well-structured tables.

---


![[Pasted image 20250717154759.png]]

https://learn.microsoft.com/en-us/sql/relational-databases/indexes/clustered-and-nonclustered-indexes-described?view=sql-server-ver15

[[Clustered and non-clustered indexes]]

---

| **Role**         | **ทำอะไรหลัก ๆ**      | **คำจำง่าย ๆ**         |
| ---------------- | --------------------- | ---------------------- |
| 🧠 **Analyst**   | ตีความข้อมูล + ธุรกิจ | “**วิเคราะห์** ธุรกิจ” |
| 🔧 **Engineer**  | สร้างระบบจัดการข้อมูล | “**เตรียม** ข้อมูล”    |
| 🧪 **Scientist** | ทำนาย/ทดลองกับข้อมูล  | “**ทำนาย** อนาคต”      |
### **❗สรุปเคล็ดลับป้องกันโดนหลอก:**

- ถ้าโจทย์มีคำว่า **“business rule”**, **“apply rule”**, **“understand business meaning”** → มักเป็น **data analyst** 
- ถ้าคำว่า **“build pipeline”**, **“ingest data”** → คือ **data engineer**
- ถ้าเจอคำว่า **“predict”**, **“model”**, **“machine learning”** → คือ **data scientist**

---

![[Pasted image 20250717221359.png]]

| **ตัวเลือก**     | **เหมาะกับ**                                        | **ใช้กรณีนี้ไหม?** | **เหตุผล**                          |
| ---------------- | --------------------------------------------------- | ------------------ | ----------------------------------- |
| **A. key/value** | อ่านข้อมูลเร็วมากตาม sessionID                      | ✅ ใช่              | session data = key/value ชัดเจน     |
| **B. graph**     | โจทย์ที่มีความสัมพันธ์ซับซ้อน (เช่น social network) | ❌ ไม่ใช่           | ไม่มีความสัมพันธ์ที่ซับซ้อน         |
| **C. columnar**  | วิเคราะห์เชิงสถิติ, BI, read-heavy                  | ❌ ไม่เหมาะ         | columnar ช้าเมื่อโหลดข้อมูลทั้งแถว  |
| **D. document**  | Semi-structured JSON, query ได้บางส่วน              | ✅ ทางเลือกได้      | แต่ latency ยังไม่ต่ำเท่า key/value |

---

![[Pasted image 20250717221103.png]]


![[Pasted image 20250717221601.png]]

|**ข้อที่**|**คำตอบ**|**เหตุผล**|
|---|---|---|
|1|❌ No|API เลือกตอนสร้าง account ไม่ใช่แยกตาม database|
|2|✅ Yes|Partition key ช่วยเพิ่มประสิทธิภาพการ query|
|3|❌ No|ข้อมูลใน logical partition เดียวกัน ต้องมี partition key เดียวกัน|

---

