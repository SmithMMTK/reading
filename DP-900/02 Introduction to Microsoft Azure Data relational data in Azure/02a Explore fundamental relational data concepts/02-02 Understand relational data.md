
ในฐานข้อมูลแบบเชิงสัมพันธ์ (_relational database_) เราจะใช้ _tables_ เพื่อจำลองกลุ่มของ _entities_ ที่มาจากโลกจริง โดยที่ _entity_ หมายถึงสิ่งที่เราต้องการเก็บข้อมูล เช่น วัตถุหรือเหตุการณ์ที่สำคัญ

ตัวอย่างเช่นในระบบร้านค้า คุณอาจสร้าง _tables_ สำหรับ _customers_, _products_, _orders_ และ _line items_ ที่อยู่ในแต่ละคำสั่งซื้อ

ใน _table_ หนึ่ง ๆ จะมีหลาย _rows_ โดยแต่ละ _row_ คือข้อมูลของ _entity_ หนึ่งตัว เช่น  
- แต่ละ _row_ ใน _customer table_ แทนลูกค้าหนึ่งคน  
- แต่ละ _row_ ใน _product table_ แทนสินค้าหนึ่งชิ้น  
- แต่ละ _row_ ใน _order table_ แทนคำสั่งซื้อของลูกค้าหนึ่งรายการ  
- แต่ละ _row_ ใน _line item table_ แทนสินค้าที่อยู่ในคำสั่งซื้อนั้น ๆ


![Diagram showing an example of a relational model, showing tables for customers, products, orders, and line items.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-relational-data-offerings/media/relational-tables.png)

_table_ แบบเชิงสัมพันธ์ (_relational tables_) เป็นรูปแบบการจัดเก็บข้อมูลที่มีโครงสร้าง (_structured data_) โดยที่แต่ละ _row_ ใน _table_ จะมี _columns_ เหมือนกันทั้งหมด แม้ว่าในบางกรณีบาง _column_ อาจไม่มีค่า เช่น ใน _customer table_ อาจมี _MiddleName column_ ซึ่งสามารถเว้นว่างไว้ได้ (_NULL_) สำหรับลูกค้าที่ไม่มีชื่อกลางหรือไม่ทราบชื่อกลาง

แต่ละ _column_ จะเก็บข้อมูลตาม _datatype_ ที่ระบุไว้ ตัวอย่างเช่น  
- _Email column_ ใน _Customer table_ มักจะเก็บข้อมูลประเภทตัวอักษร (ข้อความ) ซึ่งอาจมีความยาวคงที่หรือเปลี่ยนแปลงได้  
- _Price column_ ใน _Product table_ มักจะเก็บข้อมูลตัวเลขทศนิยม  
- _Quantity column_ ใน _Order table_ มักจะจำกัดให้เก็บเฉพาะตัวเลขจำนวนเต็ม  
- _OrderDate column_ ใน _Order table_ จะใช้เก็บค่าวันที่และเวลา  

ชนิดของ _datatype_ ที่สามารถใช้ได้ขึ้นอยู่กับระบบฐานข้อมูล (_database system_) ที่คุณใช้ แต่โดยทั่วไปจะมีมาตรฐาน _datatypes_ จาก ANSI (_American National Standards Institute_) ที่ระบบส่วนใหญ่มักจะรองรับ