
_database_ คือระบบศูนย์กลางที่ใช้ในการ _จัดเก็บ_ และ _สืบค้นข้อมูล_ หากมองในมุมที่เรียบง่าย ระบบ _file system_ ที่เราใช้เก็บไฟล์ก็ถือเป็นฐานข้อมูลรูปแบบหนึ่งเช่นกัน

แต่ในการใช้งานระดับมืออาชีพ คำว่า _database_ มักหมายถึงระบบเฉพาะที่ใช้ในการจัดการ _data records_ ไม่ใช่แค่ไฟล์ธรรมดา

## Relational databases

_relational databases_ ถูกใช้อย่างแพร่หลายในการจัดเก็บและสืบค้น _structured data_ โดยข้อมูลจะถูกจัดเก็บในรูปแบบ _ตาราง_ ซึ่งแต่ละตารางแทน _entity_ เช่น _ลูกค้า_, _สินค้า_, หรือ _คำสั่งซื้อ_

แต่ละ _entity instance_ จะมี _primary key_ ที่ใช้ระบุเอกลักษณ์ของรายการนั้น และ _key_ นี้จะถูกใช้เพื่ออ้างอิงถึง _entity_ ในตารางอื่น ตัวอย่างเช่น _primary key_ ของลูกค้าสามารถใช้ใน _sales order_ เพื่อระบุว่าคำสั่งซื้อนั้นมาจากลูกค้าคนใด

การใช้ _key_ เพื่ออ้างอิงข้อมูลแบบนี้ทำให้ฐานข้อมูลสามารถ _normalized_ ได้ ซึ่งหมายถึงการลดการซ้ำซ้อนของข้อมูล เช่น รายละเอียดของลูกค้าจะถูกจัดเก็บเพียงครั้งเดียว ไม่ต้องทำซ้ำในทุกคำสั่งซื้อที่ลูกค้ารายนั้นสร้างขึ้น

การจัดการและสืบค้นข้อมูลในตารางเหล่านี้จะทำผ่าน _SQL (Structured Query Language)_ ซึ่งเป็นภาษามาตรฐานตาม ANSI ทำให้มีรูปแบบที่คล้ายกันในหลายระบบฐานข้อมูล

![Diagram showing a relational database schema.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-core-data-concepts/media/relational-database.png)

## Non-relational databases

_non-relational databases_ คือระบบจัดการข้อมูลที่ไม่ใช้ _relational schema_ ในการจัดโครงสร้าง _ข้อมูล_ ฐานข้อมูลประเภทนี้มักถูกเรียกรวมว่า _NoSQL database_ แม้ว่าบางระบบจะรองรับการใช้งานภาษาที่คล้ายกับ _SQL_ ก็ตาม

_non-relational database_ ที่ใช้กันอย่างแพร่หลายมีอยู่ 4 ประเภทหลัก

**Key-value databases**  
ประเภทแรกคือ _key-value store_ ซึ่งแต่ละเรกคอร์ดจะประกอบด้วย _key_ ที่ไม่ซ้ำกัน และ _value_ ที่เชื่อมโยงกับ key นั้น โดย _value_ สามารถอยู่ในรูปแบบใดก็ได้  
![Diagram showing a key-value database.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-core-data-concepts/media/key-value-store.png)

**Document databases**  
_document database_ เป็นรูปแบบหนึ่งของ _key-value store_ โดยที่ _value_ จะเป็น _JSON document_ ซึ่งระบบสามารถ _parse_ และ _query_ ได้อย่างมีประสิทธิภาพ  
![Diagram showing a document database.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-core-data-concepts/media/document-store.png)

**Column family databases**  
ฐานข้อมูลแบบ _column family_ ใช้การจัดเก็บข้อมูลในรูปแบบตารางที่ประกอบด้วยแถวและคอลัมน์ โดยสามารถแบ่งคอลัมน์ออกเป็นกลุ่มที่เรียกว่า _column-families_ ซึ่งแต่ละกลุ่มจะเก็บชุดของคอลัมน์ที่มีความเกี่ยวข้องกัน  
![Diagram showing a column family database.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-core-data-concepts/media/column-family-store.png)

**Graph databases**  
_graph database_ จัดเก็บ _entities_ ในรูปแบบ _nodes_ และใช้ _links_ เพื่อระบุความสัมพันธ์ระหว่างกัน เหมาะกับข้อมูลที่มีโครงสร้างเชิงความสัมพันธ์ซับซ้อน  
![Diagram showing a graph database.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-core-data-concepts/media/graph.png)

