_Delta Lake_ เป็นระบบจัดเก็บข้อมูลแบบโอเพ่นซอร์สที่เพิ่มความสามารถแบบ _relational database_ ให้กับการประมวลผลข้อมูลใน _Spark-based data lake_ ตารางใน _Microsoft Fabric lakehouse_ เป็น _Delta tables_ ซึ่งสังเกตได้จากไอคอนรูปสามเหลี่ยม **Δ** บนหน้าต่างผู้ใช้

![Screenshot of the salesorders table viewed in the Lakehouse explorer in Microsoft Fabric.](https://learn.microsoft.com/en-us/training/wwl/work-delta-lake-tables-fabric/media/delta-table.png)


_Delta table_ เป็น _schema abstraction_ ที่ครอบอยู่บนไฟล์ข้อมูลที่จัดเก็บในรูปแบบ _Delta format_ โดยในแต่ละตารางจะมีโฟลเดอร์ที่เก็บไฟล์ข้อมูลแบบ _Parquet_ และโฟลเดอร์ชื่อ **_delta_log** ที่ใช้เก็บบันทึกรายการธุรกรรม (_transactions_) ในรูปแบบไฟล์ _JSON_

![Screenshot of the files view of the parquet files in the salesorders table viewed through Lakehouse explorer.](https://learn.microsoft.com/en-us/training/wwl/work-delta-lake-tables-fabric/media/delta-files.png)

ข้อดีของการใช้ _Delta tables_ ได้แก่

- เป็น _relational table_ ที่สามารถสั่ง _query_ และปรับปรุงข้อมูลได้ เช่นเดียวกับระบบฐานข้อมูลแบบดั้งเดิม เราสามารถใช้ _CRUD_ (สร้าง อ่าน แก้ไข ลบ) ได้ผ่านคำสั่ง _select_, _insert_, _update_, และ _delete_

- รองรับ _ACID transactions_ หมายถึงมี _atomicity_ (ธุรกรรมสำเร็จหรือยกเลิกทั้งชุด), _consistency_ (ผลลัพธ์ยังคงถูกต้องตามกฎ), _isolation_ (ธุรกรรมที่กำลังทำอยู่จะไม่ถูกรบกวน), และ _durability_ (ข้อมูลไม่สูญหายหลังธุรกรรมจบ)

- มีระบบ _data versioning_ และ _time travel_ คือสามารถย้อนดูเวอร์ชันก่อนหน้าได้จาก _transaction log_

- รองรับทั้งข้อมูลแบบ _batch_ และ _streaming_ โดยสามารถใช้ _Delta table_ เป็นทั้ง _source_ และ _sink_ สำหรับ _streaming data_ ผ่าน _Spark Structured Streaming API_

- ใช้ _standard format_ คือ _Parquet_ ซึ่งใช้กันทั่วไปใน _data lake_ และสามารถใช้ _SQL analytics endpoint_ เพื่อ _query_ ตารางใน _Fabric lakehouse_ ได้ด้วย SQL โดยตรง