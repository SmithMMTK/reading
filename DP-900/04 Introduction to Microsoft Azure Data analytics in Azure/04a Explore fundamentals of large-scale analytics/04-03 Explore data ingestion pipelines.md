
ตอนนี้คุณได้เข้าใจพื้นฐานของสถาปัตยกรรม _large-scale data warehousing solution_ และรู้จักเทคโนโลยีการประมวลผลแบบกระจาย (_distributed processing_) ที่ใช้จัดการข้อมูลปริมาณมากแล้ว ถึงเวลาไปดูขั้นตอนการ _ingest_ หรือการรับข้อมูลเข้าสู่ _analytical data store_ จากแหล่งข้อมูลหนึ่งหรือหลายแหล่ง

![Diagram of a pipeline.](https://learn.microsoft.com/en-us/training/wwl-data-ai/examine-components-of-modern-data-warehouse/media/pipeline.png)

บน Azure การ _ingest_ ข้อมูลขนาดใหญ่ควรทำผ่านการสร้าง _pipelines_ ที่ควบคุมกระบวนการ _ETL_ คุณสามารถสร้างและรัน _pipeline_ ได้ด้วย [Azure Data Factory](https://azure.microsoft.com/services/data-factory) หรือใช้ความสามารถของ _pipeline_ ที่มีอยู่ใน [Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/) หากต้องการจัดการทุกองค์ประกอบของ _data warehousing solution_ ในพื้นที่ทำงานเดียวกัน (_unified workspace_)

ไม่ว่าจะใช้เครื่องมือใด _pipeline_ จะประกอบด้วยหนึ่งกิจกรรมขึ้นไป (_activities_) ที่ทำงานกับข้อมูล โดยจะมี _input dataset_ เป็นข้อมูลต้นทาง และกิจกรรมต่าง ๆ จะเป็นเหมือน _data flow_ ที่ค่อย ๆ แปลงข้อมูลไปเรื่อย ๆ จนได้ _output dataset_  

_Pipeline_ จะใช้ _linked services_ เพื่อโหลดและประมวลผลข้อมูล ซึ่งช่วยให้คุณเลือกใช้เทคโนโลยีที่เหมาะสมกับแต่ละขั้นตอนใน _workflow_ ตัวอย่างเช่น คุณอาจใช้ _Azure Blob Store_ เป็น _linked service_ สำหรับรับข้อมูลเข้ามา จากนั้นใช้ _Azure SQL Database_ เพื่อรัน _stored procedure_ ที่ค้นหาค่าข้อมูลที่เกี่ยวข้อง ต่อด้วยการประมวลผลข้อมูลใน _Azure Databricks_ หรือใส่ _custom logic_ ด้วย _Azure Function_ สุดท้ายสามารถจัดเก็บผลลัพธ์ (_output dataset_) ไว้ใน _linked service_ อย่างเช่น _Microsoft Fabric_ นอกจากนี้ _pipeline_ ยังสามารถใช้ _built-in activities_ บางอย่างที่ไม่จำเป็นต้องมี _linked service_ ได้เช่นกัน