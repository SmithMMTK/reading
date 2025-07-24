
นอกจาก _tables_ แล้ว ฐานข้อมูลเชิงสัมพันธ์ (_relational database_) ยังสามารถมีโครงสร้างอื่น ๆ  
ที่ช่วยให้การจัดเก็บข้อมูลเป็นระบบมากขึ้น รองรับการทำงานแบบโปรแกรม และเพิ่มความเร็วในการเข้าถึงข้อมูลได้

ในหัวข้อนี้คุณจะได้เรียนรู้เพิ่มเติมเกี่ยวกับโครงสร้าง 3 แบบที่สำคัญ ได้แก่  
- _views_  
- _stored procedures_  
- _indexes_
## What is a view?

_view_ คือ _virtual table_ ที่สร้างขึ้นจากผลลัพธ์ของคำสั่ง _SELECT_  คุณสามารถนึกถึง _view_ ได้เหมือนกับ "หน้าต่าง" ที่มองเห็นข้อมูลบางส่วนจาก _rows_ ของหนึ่งหรือหลาย _tables_ ที่อยู่เบื้องหลัง ตัวอย่างเช่น คุณสามารถสร้าง _view_ ที่ดึงข้อมูลจาก _Order_ และ _Customer_ เพื่อรวมคำสั่งซื้อและข้อมูลลูกค้าไว้ใน _object_ เดียว ซึ่งจะช่วยให้สามารถดูที่อยู่จัดส่งของคำสั่งซื้อได้อย่างง่ายดาย

```sql
CREATE VIEW Deliveries
AS
SELECT o.OrderNo, o.OrderDate,
       c.FirstName, c.LastName, c.Address, c.City
FROM Order AS o JOIN Customer AS c
ON o.Customer = c.ID;
```

คุณสามารถ _query_ ข้อมูลจาก _view_ ได้เหมือนกับการ _query_ จาก _table_ โดยสามารถใส่เงื่อนไขกรองข้อมูล (_filter_) ได้เช่นเดียวกัน ตัวอย่างคำสั่งด้านล่างนี้ใช้ค้นหารายละเอียดของคำสั่งซื้อ (_orders_) สำหรับลูกค้าที่อาศัยอยู่ในเมือง _Seattle_:

```sql
SELECT OrderNo, OrderDate, LastName, Address
FROM Deliveries
WHERE City = 'Seattle';
```

## What is a stored procedure?

_stored procedure_ คือชุดของคำสั่ง _SQL_ ที่ถูกกำหนดไว้ล่วงหน้า และสามารถเรียกใช้งานได้ตามต้องการ ใช้สำหรับรวมตรรกะการทำงานแบบโปรแกรม (_programmatic logic_) ไว้ในฐานข้อมูล เพื่อให้ง่ายต่อการใช้งานซ้ำโดยแอปพลิเคชัน

คุณสามารถกำหนด _stored procedure_ ให้รับพารามิเตอร์ (_parameters_) เพื่อให้สามารถนำไปใช้กับข้อมูลตามรหัสหรือเงื่อนไขที่ต้องการได้

ตัวอย่างด้านล่างเป็น _stored procedure_ ที่ใช้เปลี่ยนชื่อสินค้า โดยอ้างอิงจากรหัส _ProductID_ ที่ระบุ:

```sql
CREATE PROCEDURE RenameProduct
	@ProductID INT,
	@NewName VARCHAR(20)
AS
UPDATE Product
SET Name = @NewName
WHERE ID = @ProductID;
```

เมื่อต้องการเปลี่ยนชื่อสินค้า คุณสามารถเรียกใช้ _stored procedure_ โดยส่งค่ารหัสสินค้า (_ID_)  และชื่อใหม่ (_NewName_) ที่ต้องการกำหนดเข้าไปเป็นพารามิเตอร์

```sql
EXEC RenameProduct 201, 'Spanner';
```

## What is an index?

_index_ ช่วยให้คุณสามารถค้นหาข้อมูลใน _table_ ได้รวดเร็วขึ้น สามารถนึกถึง _index_ ของ _table_ ได้เหมือนกับดัชนีท้ายเล่มหนังสือ ซึ่งจะเรียงลำดับคำสำคัญพร้อมหน้าที่อ้างอิง ทำให้สามารถเปิดไปยังเนื้อหานั้นได้โดยตรง หากไม่มีดัชนี คุณอาจต้องอ่านทั้งเล่มเพื่อหาสิ่งที่ต้องการ

เมื่อคุณสร้าง _index_ ในฐานข้อมูล จะต้องระบุ _column_ ที่ต้องการทำ _index_ ระบบจะเก็บข้อมูลของคอลัมน์นั้นในรูปแบบที่เรียงลำดับไว้ พร้อมกับตัวชี้ (_pointer_) ไปยังแถวที่เกี่ยวข้องใน _table_

เมื่อมีการรัน _query_ ที่มีเงื่อนไข _WHERE_ ระบุคอลัมน์ที่มี _index_ อยู่ ระบบฐานข้อมูลสามารถใช้ _index_ เพื่อเข้าถึงข้อมูลได้เร็วขึ้น แทนที่จะต้องไล่ดูทุกแถวใน _table_ ทีละรายการ

For example, you could use the following code to create an index on the **Name** column of the **Product** table:

```sql
CREATE INDEX idx_ProductName
ON Product(Name);
```

ตัวอย่างต่อไปนี้เป็นการสร้าง _index_ บน _Name column_ ของ _Product table_ เพื่อให้สามารถค้นหาข้อมูลตามชื่อสินค้าได้รวดเร็วยิ่งขึ้น:

![Screenshot of an example index that creates a tree-based structure.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-relational-data-offerings/media/index.png)

สำหรับ _table_ ที่มีแถวจำนวนน้อย การใช้ _index_ อาจไม่ช่วยให้ _query_ เร็วขึ้นมากนัก เพราะการอ่านทั้ง _table_ เพื่อหาข้อมูลอาจเร็วพออยู่แล้ว ในกรณีแบบนี้ _query optimizer_ อาจเลือกไม่ใช้ _index_ แต่ถ้า _table_ มีข้อมูลจำนวนมาก _index_ จะช่วยเพิ่ม _performance_ ของ _query_ ได้อย่างชัดเจน คุณสามารถสร้าง _indexes_ หลายตัวบน _table_ เดียวกันได้ เช่น หากต้องการค้นหาสินค้าจาก _price_ ก็สามารถสร้าง _index_ บน _Price column_ เพิ่มได้ 

แต่อย่าลืมว่า _index_ มีต้นทุน ทั้งในด้าน _storage_ และการดูแล ทุกครั้งที่มีการ _insert_, _update_, หรือ _delete_ ข้อมูล ระบบต้องอัปเดต _index_ ด้วย ซึ่งอาจทำให้กระบวนการเหล่านี้ช้าลง

ดังนั้นต้องหาจุดสมดุลระหว่างการสร้าง _index_ เพื่อให้ _query_ เร็วขึ้น กับต้นทุนที่เกิดขึ้นในการจัดการข้อมูล
