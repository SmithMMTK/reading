
https://learn.microsoft.com/en-us/training/modules/explore-non-relational-data-stores-azure/1-introduction

ฐานข้อมูลแบบ _relational_ จะจัดเก็บข้อมูลในรูปแบบ _table_ ที่มีโครงสร้างแน่นอน แต่บางครั้งโครงสร้างที่ตายตัวแบบนี้อาจทำให้ยืดหยุ่นน้อย และถ้าไม่ได้ปรับแต่ง (_tuning_) รายละเอียดให้ดี ก็อาจทำให้ _performance_ แย่ลงได้

จึงมีฐานข้อมูลอีกกลุ่มหนึ่งที่เรียกรวม ๆ ว่า _NoSQL_ ซึ่งออกแบบมาเพื่อจัดเก็บข้อมูลในรูปแบบที่ยืดหยุ่นกว่า เช่น _document_, _graph_, _key-value store_ และ _column family store_

_Azure Cosmos DB_ เป็นบริการฐานข้อมูลบนคลาวด์ที่รองรับข้อมูลแบบ _NoSQL_ และสามารถขยายตัว (_scalable_) ได้สูงมาก เหมาะกับระบบที่ต้องการความยืดหยุ่นและประสิทธิภาพสูง