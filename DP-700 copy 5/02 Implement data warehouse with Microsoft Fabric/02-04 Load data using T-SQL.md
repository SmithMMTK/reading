

นักพัฒนา SQL หรือ _citizen developers_ ที่มีความเชี่ยวชาญในการใช้ _SQL engine_ และ _T-SQL_ จะพบว่า _Warehouse_ ใน _Microsoft Fabric_ นั้นใช้งานได้อย่างคุ้นเคย

เนื่องจาก _Warehouse_ ใช้ _SQL engine_ ตัวเดียวกับที่นักพัฒนาเคยใช้ จึงสามารถทำงานขั้นสูง เช่น การกรอง เรียงลำดับ การรวมกลุ่ม และ _join_ ตารางต่าง ๆ ได้ง่าย อีกทั้งยังรองรับฟังก์ชันและโอเปอเรเตอร์หลากหลายที่ช่วยในการวิเคราะห์และแปลงข้อมูลในระดับฐานข้อมูล

## Use COPY statement

คำสั่ง [`COPY`](https://learn.microsoft.com/en-us/sql/t-sql/statements/copy-into-transact-sql) คือวิธีหลักในการนำเข้าข้อมูลเข้าสู่ _Warehouse_ โดยช่วยให้สามารถ _ingest_ ข้อมูลจาก _Azure Storage_ ภายนอกได้อย่างมีประสิทธิภาพ

คำสั่งนี้ยืดหยุ่น เช่น สามารถระบุรูปแบบไฟล์ต้นทาง, ตำแหน่งเก็บข้อมูลที่ถูกปฏิเสธ, ข้ามแถวหัวตาราง และตัวเลือกอื่น ๆ

การระบุ _rejected row location_ แยกต่างหากช่วยให้สามารถตรวจสอบคุณภาพของข้อมูลได้ง่ายขึ้น โดยสามารถวิเคราะห์แถวที่นำเข้าไม่สำเร็จได้โดยตรง

การเชื่อมต่อกับ _Azure Storage_ ต้องใช้ _Shared Access Signature (SAS)_ หรือ _Storage Account Key (SAK)_

### Handle error

สามารถกำหนด _REJECTED_ROW_LOCATION_ ให้ชี้ไปยัง _storage account_ อื่น เพื่อจัดการและแยกปัญหาได้ง่ายขึ้น ตัวเลือกนี้ใช้ได้กับไฟล์แบบ _CSV_ เท่านั้น

### Load multiple files

สามารถใช้ _wildcard_ และระบุไฟล์หลายรายการใน path เพื่อโหลดข้อมูลจำนวนมากได้ในคราวเดียว โดยทั้งหมดต้องอยู่ใน _storage account_ และ _container_ เดียวกัน ใช้เครื่องหมายจุลภาคเพื่อแยกรายการ

```sql
COPY INTO my_table
FROM 'https://myaccount.blob.core.windows.net/myblobcontainer/folder0/*.csv, 
    https://myaccount.blob.core.windows.net/myblobcontainer/folder1/'
WITH (
    FILE_TYPE = 'CSV',
    CREDENTIAL=(IDENTITY= 'Shared Access Signature', SECRET='<Your_SAS_Token>'),
    FIELDTERMINATOR = '|'
)
````

ตัวอย่างการโหลดไฟล์ _PARQUET_:

```
COPY INTO test_parquet
FROM 'https://myaccount.blob.core.windows.net/myblobcontainer/folder1/*.parquet'
WITH (
    CREDENTIAL=(IDENTITY= 'Shared Access Signature', SECRET='<Your_SAS_Token>')
)
```

**ข้อควรระวัง** ไฟล์ทั้งหมดต้องมีโครงสร้างเหมือนกัน (จำนวนคอลัมน์ ลำดับ ฯลฯ) และต้องตรงกับโครงสร้างของ _target table_
 
## **Load table from other warehouses and lakehouses**

สามารถโหลดข้อมูลจาก _data assets_ อื่นใน _workspace_ เช่น _warehouse_ หรือ _lakehouse_ ได้

ต้องอ้างอิงด้วยชื่อแบบ [three-part naming](https://learn.microsoft.com/en-us/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql) แล้วใช้ CREATE TABLE AS SELECT (_CTAS_) หรือ INSERT...SELECT เพื่อโหลดข้อมูล

|**SQL Statement**|**Description**|
|---|---|
|[CREATE TABLE AS SELECT](https://learn.microsoft.com/en-us/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)|สร้างตารางใหม่จากผลลัพธ์ของ SELECT มักใช้สำหรับสร้างสำเนา หรือโหลดผลลัพธ์ที่ผ่านการแปลง|
|[INSERT...SELECT](https://learn.microsoft.com/en-us/sql/t-sql/statements/insert-transact-sql)|โหลดข้อมูลจากตารางหนึ่งไปอีกตารางหนึ่งโดยไม่ต้องสร้างตารางใหม่|

เช่น นักวิเคราะห์ต้องการรวมข้อมูลจาก _warehouse_ และ _lakehouse_ ก็สามารถใช้ product_id เป็น _join key_ แล้วโหลดผลลัพธ์เข้าสู่ _warehouse_ ใหม่:

```
CREATE TABLE [analysis_warehouse].[dbo].[combined_data]
AS
SELECT *
FROM [sales_warehouse].[dbo].[sales_data] sales
INNER JOIN [social_lakehouse].[dbo].[social_data] social
ON sales.[product_id] = social.[product_id];
```

ทุก _warehouse_ ที่อยู่ใน _workspace_ เดียวกันจะอยู่บน _logical SQL server_ เดียวกัน หากใช้เครื่องมือเช่น [SQL Server Management Studio](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) ก็สามารถ _query ข้ามฐาน_ ได้เช่นเดียวกับใน SQL Server

![Animated GIF showing how to reference other Warehouses in a workspace from SQL Server Management Studio.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/4-load-using-ssms.gif)

_MyWarehouse_ และ _Sales_ เป็นตัวอย่างของ _warehouse assets_ ที่แชร์ _workspace_ เดียวกัน

![Animated GIF showing how to query other Warehouses in a workspace from the Fabric workspace.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/4-query-using-workspace.gif)

หากใช้ _Object Explorer_ จากใน _workspace_ จะต้องเพิ่ม _warehouse_ ที่ต้องการใช้ก่อน ซึ่งจะสามารถเข้าถึงได้จาก _Visual query editor_ ด้วย

การโหลดข้อมูลเข้าสู่ _warehouse_ ใน Microsoft Fabric สามารถทำได้อย่างมีประสิทธิภาพผ่านคำสั่ง COPY หรือโหลดจาก _warehouse_ และ _lakehouse_ อื่นภายใน _workspace_ เดียวกัน เพื่อการจัดการข้อมูลและวิเคราะห์ที่ราบรื่น

---

## **Next unit: Load and transform data with Dataflow Gen2**
