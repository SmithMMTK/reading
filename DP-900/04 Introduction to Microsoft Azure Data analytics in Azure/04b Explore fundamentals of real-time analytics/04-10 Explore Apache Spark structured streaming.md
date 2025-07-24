
**Apache Spark** คือ _เฟรมเวิร์กสำหรับการประมวลผลแบบกระจาย_ (_distributed processing_) ที่ออกแบบมาสำหรับการวิเคราะห์ข้อมูลขนาดใหญ่ (_large scale data analytics_)

คุณสามารถใช้งาน Spark บน Microsoft Azure ได้ผ่านบริการต่อไปนี้:

- Microsoft Fabric
- Azure Databricks

_Spark_ สามารถใช้ในการรันโค้ด (มักเขียนด้วย _Python_, _Scala_, หรือ _Java_) แบบ _ขนาน (parallel)_ บนหลายโหนดในคลัสเตอร์ ซึ่งช่วยให้สามารถ _ประมวลผลข้อมูลปริมาณมหาศาลได้อย่างมีประสิทธิภาพ_

_Spark_ รองรับทั้ง _batch processing_ และ _stream processing_ ในระบบเดียวกัน

## Spark Structured Streaming

ในการประมวลผล _streaming data_ บน Spark คุณสามารถใช้ไลบรารี _Spark Structured Streaming_ ซึ่งมี _API สำหรับการ ingest, ประมวลผล, และส่งออกผลลัพธ์_ จากข้อมูลสตรีมที่ไหลเข้ามาอย่างต่อเนื่อง (_perpetual streams_)

_Spark Structured Streaming_ ทำงานบนโครงสร้างหลักของ Spark ที่เรียกว่า _dataframe_ ซึ่งเป็นการห่อหุ้มข้อมูลในรูปแบบตาราง คุณจะใช้ API นี้เพื่อ _อ่านข้อมูลจากแหล่งแบบเรียลไทม์_ เช่น _Kafka hub_, _file store_, หรือ _network port_ เข้ามาใน _dataframe แบบไม่สิ้นสุด (boundless dataframe)_ ซึ่งจะถูกเติมข้อมูลใหม่เข้ามาเรื่อย ๆ จาก stream

จากนั้นคุณสามารถกำหนด _query_ บน dataframe เพื่อ _เลือกข้อมูล (select)_, _แสดงเฉพาะบางค่า (project)_, หรือ _รวมข้อมูล (aggregate)_ ซึ่งมักจะใช้ _temporal windows_ เพื่อแบ่งช่วงเวลา

ผลลัพธ์จาก query จะกลายเป็น _dataframe ใหม่_ ซึ่งสามารถ _จัดเก็บไว้เพื่อวิเคราะห์_ หรือใช้ในกระบวนการประมวลผลต่อไปได้

![Diagram of streaming data is written to a dataframe, which is being queried to create another dataframe for analysis.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-fundamentals-stream-processing/media/spark-streaming.png)

_Spark Structured Streaming_ เป็นตัวเลือกที่ยอดเยี่ยมสำหรับการทำ _real-time analytics_ โดยเฉพาะเมื่อคุณต้องการ _ผนวกข้อมูลสตรีม_ เข้ากับ _data lake_ หรือ _analytical data store_ ที่ใช้พื้นฐานจาก Spark

_หมายเหตุ_

หากต้องการข้อมูลเพิ่มเติมเกี่ยวกับ _Spark Structured Streaming_ ดูได้ที่ [Spark Structured Streaming programming guide](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html)

## Delta Lake

**Delta Lake** เป็น _ชั้นจัดเก็บข้อมูลแบบโอเพ่นซอร์ส_ ที่เพิ่มความสามารถในการ _จัดการธุรกรรมแบบสอดคล้อง (transactional consistency)_, _ควบคุม schema_, และฟีเจอร์อื่น ๆ ที่พบได้ใน _data warehouse_ ลงในระบบจัดเก็บแบบ _data lake_

Delta Lake ยังช่วย _รวมการจัดเก็บข้อมูลทั้งแบบ streaming และ batch_ เข้าไว้ด้วยกัน และสามารถใช้ร่วมกับ _Spark_ เพื่อ _สร้างตารางเชิงสัมพันธ์_ ที่ใช้ได้ทั้งใน _batch processing_ และ _stream processing_

เมื่อนำมาใช้ในงาน _streaming_ ตาราง Delta Lake สามารถทำหน้าที่เป็นทั้ง _source_ สำหรับ query ข้อมูลเรียลไทม์ หรือ _sink_ สำหรับเขียนข้อมูลสตรีมลงในตาราง

_Spark runtimes_ ในทั้ง **Microsoft Fabric** และ **Azure Databricks** รองรับการทำงานกับ Delta Lake โดยตรง

การผสานระหว่าง _Delta Lake_ กับ _Spark Structured Streaming_ เป็นโซลูชันที่เหมาะสมเมื่อคุณต้องการ _แปลงข้อมูลที่ประมวลผลแบบ batch และ stream ใน data lake_ ให้สามารถ _เข้าถึงผ่าน schema เชิงสัมพันธ์_ เพื่อรองรับการ _query และวิเคราะห์ด้วย SQL_

_หมายเหตุ_

หากต้องการข้อมูลเพิ่มเติมเกี่ยวกับ **Delta Lake** ดูได้ที่  
[Lakehouse and Delta Lake tables](https://learn.microsoft.com/en-us/fabric/data-engineering/lakehouse-and-delta-tables)