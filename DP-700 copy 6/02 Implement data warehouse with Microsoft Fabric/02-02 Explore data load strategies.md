
ใน Microsoft Fabric มีหลายวิธีในการโหลดข้อมูลเข้าสู่ _data warehouse_ ซึ่งเป็นขั้นตอนพื้นฐานที่สำคัญ เพราะช่วยให้สามารถรวมข้อมูลที่มีคุณภาพสูงผ่านการ _transform_ หรือ _process_ มาไว้ในที่เดียว

อีกทั้ง ประสิทธิภาพของการโหลดข้อมูลมีผลโดยตรงต่อความถูกต้องและความทันเวลาในการวิเคราะห์ข้อมูล ซึ่งมีความสำคัญต่อการตัดสินใจแบบ _real-time_ ดังนั้นการลงทุนเวลาและทรัพยากรในการออกแบบและดำเนินการกลยุทธ์การโหลดข้อมูลที่แข็งแกร่งจึงเป็นสิ่งจำเป็นต่อความสำเร็จของ _data warehouse project_

## Understand data ingestion and data load operations

แม้ว่าทั้งสองกระบวนการจะเป็นส่วนหนึ่งของ _ETL (Extract, Transform, Load)_ สำหรับ _data warehouse_ แต่มีวัตถุประสงค์ต่างกัน:

- **Data ingestion/extract** คือการย้ายข้อมูลดิบจากแหล่งต่าง ๆ มาสู่ศูนย์กลาง
- **Data loading** คือการนำข้อมูลที่ผ่านการ _transform_ หรือ _process_ แล้วไปโหลดเข้าสู่ปลายทางที่ใช้สำหรับการวิเคราะห์และรายงาน

ทั้ง _Fabric data warehouses_ และ _lakehouses_ จะเก็บข้อมูลใน _OneLake_ โดยใช้รูปแบบ _Delta Parquet_

## Stage your data

คุณอาจต้องสร้างและทำงานกับวัตถุเสริม เช่น _tables_, _stored procedures_, และ _functions_ ที่เกี่ยวข้องกับกระบวนการโหลด ซึ่งวัตถุเหล่านี้เรียกว่า **staging**

วัตถุ _staging_ ทำหน้าที่เป็นพื้นที่จัดเก็บและแปลงข้อมูลชั่วคราว โดยอาจแชร์ทรัพยากรร่วมกับ _data warehouse_ หรือมีพื้นที่จัดเก็บแยกต่างหาก

_staging_ ทำหน้าที่เป็น _abstraction layer_ เพื่อช่วยให้การโหลดข้อมูลไปยังตารางสุดท้ายใน _data warehouse_ ทำได้ง่ายขึ้น

![Diagram of sequential steps in the data science process.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/1-data-warehouse-process.png)

นอกจากนี้ _staging area_ ยังช่วยลดผลกระทบของการโหลดข้อมูลต่อประสิทธิภาพของ _data warehouse_ ซึ่งเป็นสิ่งสำคัญหากต้องการให้ระบบยังคงใช้งานได้ต่อเนื่องระหว่างการโหลด

## Review type of data loads

มีสองประเภทของการโหลดข้อมูลที่ควรพิจารณา:

|Load Type|Description|Operation|Duration|Complexity|Best used|
|---|---|---|---|---|---|
|**Full (initial) load**|กระบวนการโหลดข้อมูลทั้งหมดครั้งแรก|ตารางทั้งหมดจะถูกลบและโหลดใหม่ ข้อมูลเดิมจะหายไป|ใช้เวลานานกว่าเพราะมีข้อมูลจำนวนมาก|ง่ายต่อการดำเนินการ ไม่มีการเก็บประวัติ|เหมาะกับการตั้งค่า _data warehouse_ ใหม่ หรือรีเฟรชข้อมูลทั้งหมด|
|**Incremental load**|การอัปเดตเฉพาะข้อมูลที่เปลี่ยนแปลงตั้งแต่รอบที่แล้ว|เก็บประวัติไว้ และอัปเดตข้อมูลใหม่ลงตาราง|ใช้เวลาน้อยกว่าการโหลดเต็ม|ซับซ้อนกว่าการโหลดเต็ม|เหมาะกับการอัปเดตประจำ เช่น รายวันหรือรายชั่วโมง ต้องมีระบบติดตามการเปลี่ยนแปลงของข้อมูลต้นทาง|

กระบวนการ _ETL_ สำหรับ _data warehouse_ ไม่จำเป็นต้องใช้ทั้ง _full load_ และ _incremental load_ เสมอไป บางกรณีอาจใช้ร่วมกัน โดยขึ้นอยู่กับปริมาณข้อมูล ลักษณะข้อมูล และความต้องการของ _data warehouse_

## Understand business key and surrogate key

ใน _data warehouse_, ทั้ง _surrogate keys_ และ _business keys_ มีความสำคัญแต่ใช้งานต่างกัน:

- **Surrogate key:** เป็นรหัสที่ระบบสร้างขึ้นเพื่อระบุแถวในตารางของ _data warehouse_ อย่างไม่ซ้ำกัน ไม่มีความหมายเชิงธุรกิจ มักเป็นเลขจำนวนเต็ม ใช้เพื่อคงความแม่นยำเมื่อรวมข้อมูลจากหลายแหล่ง และป้องกันปัญหาเรื่องการเปลี่ยนแปลงของ _business key_ ในระบบต้นทาง

- **Business Key:** หรือ _natural key_ เป็นรหัสที่มีความหมายทางธุรกิจ เช่น รหัสลูกค้า รหัสสินค้า ใช้เพื่อระบุแถวในระบบต้นทาง และช่วยในการเชื่อมโยงข้อมูลระหว่าง _data warehouse_ กับระบบต้นทาง

## Load a dimension table

ให้มอง _dimension table_ เป็นคำตอบของคำถาม _"ใคร ทำอะไร ที่ไหน เมื่อไร ทำไม"_ ซึ่งเป็นบริบทที่อธิบายข้อมูลใน _fact table_

ตัวอย่างเช่น ในร้านค้าออนไลน์ _fact table_ อาจเก็บข้อมูลยอดขายสินค้า แต่หากไม่มี _dimension table_ ก็จะไม่รู้ว่าลูกค้าคือใคร ซื้อเมื่อไร และอยู่ที่ไหน

### Slowly changing dimensions (SCD)

_Slowly Changing Dimensions_ คือข้อมูลที่เปลี่ยนแปลงช้าและไม่แน่นอน เช่น ที่อยู่ของลูกค้า ถ้าเขาย้ายบ้านและเราเขียนทับข้อมูลเดิม จะสูญเสียประวัติ ซึ่งจะเป็นปัญหาถ้าต้องวิเคราะห์ข้อมูลย้อนหลัง

ประเภทของ _SCD_ ที่ใช้บ่อยคือ _type 1_ และ _type 2_:

- **Type 0 SCD:** ไม่เปลี่ยนค่าเลย
- **Type 1 SCD**: แก้ไขข้อมูลทับ ไม่เก็บประวัติ
- **Type 2 SCD**: เพิ่มเรคอร์ดใหม่ เก็บประวัติทั้งหมดตาม _natural key_
- **Type 3 SCD:** เพิ่มคอลัมน์สำหรับเก็บประวัติ
- **Type 4 SCD**: สร้าง _dimension table_ ใหม่
- **Type 5 SCD**: ใช้เมื่อ _dimension_ ใหญ่มากและไม่สามารถใช้ _type 2_ ได้
- **Type 6 SCD**: ผสมระหว่าง _type 2_ และ _type 3_

ใน _Type 2_, เมื่อมีข้อมูลใหม่เข้ามา เวอร์ชันเก่าจะหมดอายุ และเวอร์ชันใหม่จะถูกเปิดใช้งาน

[![Diagram showing the function and structure of OneLake.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/2-slowly-changing-dimension.png)](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/2-slowly-changing-dimension.png#lightbox)

ตัวอย่างโค้ดสำหรับจัดการ _Type 2 SCD_ ในตาราง _Dim_Products_ ด้วย _T-SQL_:

```sql
IF EXISTS (SELECT 1 FROM Dim_Products WHERE SourceKey = @ProductID AND IsActive = 'True')
BEGIN
    -- Existing product record
    UPDATE Dim_Products
    SET ValidTo = GETDATE(), IsActive = 'False'
    WHERE SourceKey = @ProductID 
        AND IsActive = 'True';
END
ELSE
BEGIN
    -- New product record
    INSERT INTO Dim_Products (SourceKey, ProductName, StartDate, EndDate, IsActive)
    VALUES (@ProductID, @ProductName, GETDATE(), '9999-12-31', 'True');
END
````

กลไกในการตรวจจับการเปลี่ยนแปลงในระบบต้นทางมีความสำคัญ เช่น:

- [Change Data Capture (CDC)](https://learn.microsoft.com/en-us/sql/relational-databases/track-changes/about-change-data-capture-sql-server)
- [Change Tracking](https://learn.microsoft.com/en-us/sql/relational-databases/track-changes/about-change-tracking-sql-server)
- [Triggers](https://learn.microsoft.com/en-us/sql/relational-databases/triggers/dml-triggers)

## **Load a fact table**

โดยทั่วไปการโหลด _fact table_ จะทำหลังจากโหลด _dimension tables_ เพื่อให้ _surrogate keys_ ที่ใช้ในการเชื่อมโยงพร้อมใช้งาน

ข้อมูลที่โหลดเข้า _fact table_ มักจะมี _business key_ ของ _dimension_ ที่เกี่ยวข้อง ดังนั้นต้องมีขั้นตอนการแปลงเป็น _surrogate key_ ที่ถูกต้อง โดยอาจต้องพิจารณาช่วงเวลาที่ข้อมูลมีผล

ในบางกรณีสามารถใช้เวอร์ชันล่าสุด (_current version_) ของ _dimension_ ได้ แต่บางครั้งต้องใช้ตามช่วงเวลา (_DateTime_) ที่ตรงกับเหตุการณ์ใน _fact table_

ตัวอย่างโค้ดการโหลด _fact table_ จากข้อมูลใน _staging table_ โดยใช้การค้นหา _surrogate keys_:

```
-- Lookup keys in dimension tables
INSERT INTO dbo.FactSales
SELECT  (SELECT MAX(DateKey)
         FROM dbo.DimDate
         WHERE FullDateAlternateKey = stg.OrderDate) AS OrderDateKey,
        (SELECT MAX(CustomerKey)
         FROM dbo.DimCustomer
         WHERE CustomerAlternateKey = stg.CustNo) AS CustomerKey,
        (SELECT MAX(ProductKey)
         FROM dbo.DimProduct
         WHERE ProductAlternateKey = stg.ProductID) AS ProductKey,
        (SELECT MAX(StoreKey)
         FROM dbo.DimStore
         WHERE StoreAlternateKey = stg.StoreID) AS StoreKey,
        OrderNumber,
        OrderLineItem,
        OrderQuantity,
        UnitPrice,
        Discount,
        Tax,
        SalesAmount
FROM dbo.StageSales AS stg
```

---