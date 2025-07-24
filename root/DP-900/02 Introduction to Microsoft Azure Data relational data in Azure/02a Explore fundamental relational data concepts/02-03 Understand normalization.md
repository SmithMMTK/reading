_normalization_ คือคำที่ผู้เชี่ยวชาญด้านฐานข้อมูลใช้เรียกกระบวนการออกแบบ _schema_ เพื่อช่วยลดการซ้ำซ้อนของข้อมูล (_data duplication_) และทำให้ข้อมูลมีความถูกต้องสม่ำเสมอ (_data integrity_)

แม้ว่ากระบวนการนี้จะมีระดับต่าง ๆ (_forms_) ที่ซับซ้อน แต่ในทางปฏิบัติสามารถสรุปได้ง่าย ๆ ว่า:

1. แยกแต่ละ _entity_ ออกเป็น _table_ ของตัวเอง  
2. แยกแต่ละ _attribute_ ที่แตกต่างกันออกเป็น _column_ ของตัวเอง  
3. ใช้ _primary key_ เพื่อระบุแต่ละ _row_ อย่างไม่ซ้ำกัน  
4. ใช้ _foreign key_ เพื่อเชื่อมโยง _entities_ ที่เกี่ยวข้องกัน

เพื่อให้เข้าใจหลักการของ _normalization_ สมมุติว่ามีตารางที่ใช้ในรูปแบบ _spreadsheet_ สำหรับติดตามการขายของบริษัท

![Diagram showing an order data in a single, un-normalized table.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-relational-data-offerings/media/unnormalized-data.png)

สังเกตว่าใน _spreadsheet_ ตัวอย่าง ข้อมูลของลูกค้าและสินค้า _ถูกทำซ้ำ_ สำหรับแต่ละรายการสินค้าที่ขาย เช่น ชื่อลูกค้าและที่อยู่, ชื่อสินค้าและราคาถูกใส่ซ้ำ ๆ ในทุกแถว และยังถูกรวมอยู่ในช่องเดียวกัน

เมื่อใช้ _normalization_ การจัดเก็บข้อมูลจะเปลี่ยนไปอย่างมีระเบียบมากขึ้น โดยแต่ละ _entity_ เช่น _customer_, _product_, _sales order_, และ _line item_ จะถูกแยกออกมาเก็บใน _table_ ของตัวเอง และแต่ละ _attribute_ ก็จะอยู่ใน _column_ แยกเฉพาะ

การออกแบบแบบนี้ช่วยลดการซ้ำของข้อมูล และทำให้สามารถจัดการ แก้ไข และค้นหาข้อมูลได้ง่ายและแม่นยำมากขึ้น

![Diagram showing an order data in a normalized tabular schema.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-relational-data-offerings/media/normalized-data.png)

แต่ละ _entity_ ที่อยู่ในข้อมูล เช่น _customer_, _product_, _sales order_, และ _line item_ จะถูกเก็บไว้ใน _table_ แยกของตัวเอง และแต่ละ _attribute_ ของ _entity_ นั้นจะอยู่ใน _column_ แยกต่างหาก

การเก็บแต่ละ _instance_ ของ _entity_ เป็น _row_ ใน _table_ ของตัวเองช่วยลดการซ้ำซ้อนของข้อมูล เช่น ถ้าต้องการเปลี่ยนที่อยู่ของลูกค้า ก็เพียงแค่แก้ค่าใน _row_ เดียว

การแยก _attribute_ ออกเป็น _columns_ เฉพาะ ช่วยให้แต่ละค่าถูกจำกัดอยู่ใน _datatype_ ที่เหมาะสม เช่น ราคาสินค้าต้องเป็น _decimal_ และจำนวนสินค้าในแต่ละรายการต้องเป็น _integer_ นอกจากนี้ยังช่วยให้สามารถ _query_ ข้อมูลได้ละเอียด เช่น ค้นหาลูกค้าที่อยู่ในเมืองใดเมืองหนึ่ง

แต่ละ _entity_ จะถูกระบุแบบเฉพาะด้วยค่า _primary key_ ซึ่งมักเป็น ID หรือรหัสอื่น ๆ และเมื่อ _entity_ หนึ่งอ้างถึงอีก _entity_ หนึ่ง เช่น คำสั่งซื้อ (_order_) มีลูกค้า (_customer_) ที่เกี่ยวข้อง ก็จะเก็บ _primary key_ ของ _customer_ ไว้ในรูปของ _foreign key_ ใน _Order table_

ตัวอย่างเช่น เราสามารถดูที่อยู่ของลูกค้า (ซึ่งถูกเก็บไว้แค่ครั้งเดียว) จากแต่ละคำสั่งซื้อได้โดยการอ้างอิง _CustomerID_ จาก _Order table_ ไปยัง _Customer table_

ระบบบริหารจัดการฐานข้อมูล (_RDBMS_) มักสามารถบังคับใช้ _referential integrity_ ได้ เช่น ตรวจสอบว่า _foreign key_ ที่กรอกมี _primary key_ ที่ตรงกันใน _table_ ปลายทาง เพื่อป้องกันไม่ให้เกิดคำสั่งซื้อของลูกค้าที่ไม่มีอยู่จริง

ในบางกรณี _key_ (ทั้ง _primary_ และ _foreign_) อาจถูกกำหนดให้เป็น _composite key_ โดยใช้การรวมกันของหลาย _columns_ ที่ไม่ซ้ำกัน เช่น _LineItem table_ ใช้ _OrderNo_ + _ItemNo_ เป็นรหัสเฉพาะของแต่ละรายการสินค้าในคำสั่งซื้อนั้น

---
## Normalization Concept

| **Normal Form** | **Description (English - DBA Terms)**                                                                            | **คำอธิบาย (ภาษาไทย)**                                                                                                                                              |
| --------------- | ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1NF**         | Eliminate repeating groups. Ensure each cell holds atomic (indivisible) values.                                  | กำจัดข้อมูลซ้ำในคอลัมน์ ให้ทุกคอลัมน์เก็บแค่ค่าหนึ่งค่า (Atomic)                                                                                                    |
| **2NF**         | Must be in 1NF. Remove partial dependency — every non-key attribute must depend on the whole primary key.        | อยู่ในรูป 1NF แล้ว และต้องไม่มีการพึ่งพาบางส่วนของ Primary Key (เฉพาะกรณีที่มี composite key)                                                                       |
| **3NF**         | Must be in 2NF. Remove transitive dependency — non-key attributes should not depend on other non-key attributes. | อยู่ในรูป 2NF แล้ว และไม่มีความสัมพันธ์แบบลูกโซ่ระหว่าง Non-key กับ Non-key<br><br>ตารางที่ “ทุกคอลัมน์ต้องขึ้นกับคีย์โดยตรงเท่านั้น” ห้ามมีคอลัมน์ไหนขึ้นต่อกันเอง |

### **Unnormalized Form**
| StudentID | Name  | Courses                    | Instructors                | Phones                     |
|-----------|-------|----------------------------|----------------------------|----------------------------|
| 1001      | Alice | Database, Data Structures  | Dr. Smith, Dr. John        | 081-111-1111,081-222-2222  |
| 1002      | Bob   | Database                   | Dr. Smith                  | 081-111-1111               |

### **After 1NF (Remove repeating groups)**
| StudentID | Name  | Course           | Instructor | InstructorPhone |
|-----------|-------|------------------|------------|-----------------|
| 1001      | Alice | Database         | Dr. Smith  | 081-111-1111    |
| 1001      | Alice | Data Structures  | Dr. John   | 081-222-2222    |
| 1002      | Bob   | Database         | Dr. Smith  | 081-111-1111    |

### **After 2NF (Split student info to its own table)**

| StudentID | Name  |
| --------- | ----- |
| 1001      | Alice |
| 1002      | Bob   |

| StudentID | Course          | Instructor | InstructorPhone |
| --------- | --------------- | ---------- | --------------- |
| 1001      | Database        | Dr. Smith  | 081-111-1111    |
| 1001      | Data Structures | Dr. John   | 081-222-2222    |
| 1002      | Database        | Dr. Smith  | 081-111-1111    |

##  **3NF: Remove Transitive Dependencies**

| StudentID | Name  |
| --------- | ----- |
| 1001      | Alice |
| 1002      | Bob   |

| StudentID | Course          | Instructor |
| --------- | --------------- | ---------- |
| 1001      | Database        | Dr. Smith  |
| 1001      | Data Structures | Dr. John   |
| 1002      | Database        | Dr. Smith  |

| Instructor   | InstructorPhone |
|--------------|-----------------|
| Dr. Smith    | 081-111-1111    |
| Dr. John     | 081-222-2222    |
