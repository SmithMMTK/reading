
_ดัชนี_ (_index_) คือโครงสร้างที่อยู่บน _disk_ ซึ่งเกี่ยวข้องกับ _table_ หรือ _view_ เพื่อช่วยให้การค้นหาแถว (row) ใน _table_ หรือ _view_ เร็วขึ้น โดยดัชนีจะสร้างจาก _key_ ที่มาจากหนึ่งหรือหลายคอลัมน์ แล้วจัดเก็บในโครงสร้างแบบ _B-tree_ เพื่อให้ SQL Server สามารถค้นหาแถวที่ตรงกับ _key value_ ได้อย่างมีประสิทธิภาพ

_SQL Server_ ใช้คำว่า _B-tree_ โดยทั่วไปเพื่อหมายถึงดัชนีในแบบ _rowstore_ ซึ่งจริง ๆ แล้วใช้ _B+ tree_ (ไม่ได้ใช้ใน _columnstore_ หรือ _memory-optimized tables_)

มี _index_ หลัก ๆ อยู่ 2 แบบคือ

- _Clustered index_:  ดัชนีแบบนี้จะจัดเรียงและจัดเก็บแถวข้อมูลใน _table_ หรือ _view_ ตามค่า _key_ ที่กำหนดไว้ใน _index_  
	- มีได้เพียง 1 อันต่อ 1 _table_ เพราะข้อมูลสามารถเรียงลำดับได้เพียงแบบเดียว  
	- ถ้า _table_ มี _clustered index_ เราเรียกว่า _clustered table_  
	- ถ้าไม่มี _clustered index_ ข้อมูลจะเก็บแบบไม่เรียงลำดับ เรียกว่า _heap_  

- _Non-clustered index_:  ดัชนีนี้จะมีโครงสร้างแยกออกจากแถวข้อมูล โดยจะเก็บ _key_ ไว้ในดัชนี และมีตัวชี้ (_pointer_) ไปยังแถวข้อมูลที่เกี่ยวข้อง  
	- ตัวชี้นี้เรียกว่า _row locator_ ซึ่งมี 2 แบบ ขึ้นอยู่กับว่าแถวข้อมูลเก็บแบบไหน  
	  - ถ้าเก็บแบบ _heap_ ตัวชี้จะชี้ตรงไปยังตำแหน่งแถว  
	  - ถ้าเก็บแบบ _clustered_ ตัวชี้จะใช้ _clustered index key_  
	- สามารถเพิ่ม _nonkey columns_ ลงไปในระดับล่างของ _nonclustered index_ เพื่อทำให้ _query_ ทำงานได้ครอบคลุมมากขึ้น (_fully covered query_)  
	- มีประโยชน์เมื่อมีข้อจำกัดด้านจำนวนคอลัมน์ใน _index key_  

ทั้ง _clustered_ และ _nonclustered index_ สามารถเป็นแบบ _unique_ ได้ ซึ่งหมายความว่าแถวจะต้องไม่ซ้ำกันใน _key_ ที่กำหนด  ถ้าไม่กำหนดแบบ _unique_ หลายแถวสามารถมีค่า _key_ ซ้ำกันได้  

ทุกครั้งที่ข้อมูลใน _table_ เปลี่ยนแปลง ไม่ว่าจะเป็น _insert_, _update_ หรือ _delete_ ระบบจะปรับปรุง _index_ ให้อัตโนมัติ

เกี่ยวกับ _constraints_:  
- ถ้ามีการสร้าง _PRIMARY KEY_ หรือ _UNIQUE_ constraint ระบบจะสร้าง _index_ ให้อัตโนมัติ  
  - _UNIQUE constraint_ → สร้าง _non-clustered index_  
  - _PRIMARY KEY constraint_ → สร้าง _clustered index_ (ถ้ายังไม่มีอยู่)  
  - ถ้ามี _clustered index_ อยู่แล้ว ระบบจะใช้ _non-clustered index_ แทนเพื่อบังคับใช้ _PRIMARY KEY_  

การออกแบบ _index_ ที่ดีจะช่วยลดการอ่าน _disk I/O_ และเพิ่มประสิทธิภาพของ _query optimizer_ ในการเลือกแผนการทำงานที่ดีที่สุด
