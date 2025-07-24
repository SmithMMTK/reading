
_Microsoft Azure_ คือแพลตฟอร์มคลาวด์ที่ขับเคลื่อนแอปพลิเคชันและโครงสร้างพื้นฐาน IT ขององค์กรขนาดใหญ่ทั่วโลก โดยมีบริการมากมายที่รองรับ _transactional_ และ _analytical data workloads_

_หมายเหตุ_  
เนื้อหานี้ครอบคลุมเฉพาะบริการจัดการข้อมูลที่ใช้กันอย่างแพร่หลายในโซลูชันสมัยใหม่ ยังมีบริการอื่นอีกมากใน Azure ที่เกี่ยวข้อง

## _Azure SQL_

![Azure SQL](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-roles-responsibilities-world-of-data/media/azure-sql.png)  
กลุ่มบริการฐานข้อมูลแบบ _relational_ ที่ใช้เอนจินของ _SQL Server_ โดยรวมถึง:
- _Azure SQL Database_: ฐานข้อมูลแบบ _PaaS_ ที่ Azure ดูแลให้ทั้งหมด
- _Azure SQL Managed Instance_: ให้ความยืดหยุ่นมากขึ้นแต่เจ้าของมีภาระดูแลบางส่วน
- _Azure SQL VM_: ติดตั้ง SQL Server บน VM พร้อมความสามารถในการปรับแต่งสูงสุด

_DBAs_ ใช้เพื่อรองรับ _LOB applications_  
_Data engineers_ ใช้เป็นแหล่งข้อมูลใน _ETL pipelines_  
_Data analysts_ อาจสืบค้นข้อมูลโดยตรง หรือผสานกับแหล่งข้อมูลอื่นใน _analytical store_

## _Open-source databases in Azure_

![Open-source DB](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-roles-responsibilities-world-of-data/media/azure-database.png)  
Azure มีบริการฐานข้อมูล _open-source_ ยอดนิยมแบบที่ดูแลให้เสร็จสรรพ:
- _Azure Database for MySQL_: ใช้งานง่าย เหมาะกับแอป LAMP stack
- _Azure Database for MariaDB_: สร้างโดยทีมพัฒนา MySQL ดั้งเดิม ปรับปรุงประสิทธิภาพ
- _Azure Database for PostgreSQL_: รองรับ _relational_ และ _custom object types_

## _Azure Cosmos DB_

![Cosmos DB](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-roles-responsibilities-world-of-data/media/cosmos-db.png)  
ระบบฐานข้อมูล _NoSQL_ ที่รองรับ _JSON_, _key-value_, _column-family_, และ _graph_ ที่ขยายข้ามภูมิภาคได้  
ผู้ดูแลอาจเป็น _DBA_ หรือ _developer_ ขึ้นกับบริบท  
_Data engineers_ นำไปเชื่อมกับ _analytics system_  
_Data analysts_ ใช้งานข้อมูลผ่านระบบวิเคราะห์

## _Azure Storage_

![Azure Storage](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-roles-responsibilities-world-of-data/media/azure-storage.png)  
บริการเก็บข้อมูลหลักของ Azure:
- _Blob containers_: สำหรับไฟล์ไบนารี
- _File shares_: พื้นที่แชร์ไฟล์เหมือนในองค์กร
- _Tables_: สำหรับจัดเก็บข้อมูล _key-value_

_Data engineers_ ใช้สร้าง _data lake_ โดยใช้ blob storage ที่รองรับโฟลเดอร์ (_hierarchical namespace_)

## _Azure Data Factory_

![ADF](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-roles-responsibilities-world-of-data/media/azure-data-factory.png)  
บริการสร้างและจัดตารางการทำงานของ _data pipeline_ สำหรับการ _extract_, _transform_, และ _load_  
ใช้เชื่อมต่อกับบริการอื่นของ Azure ได้  
_Data engineers_ ใช้เพื่อสร้าง _ETL solutions_ ที่โหลดข้อมูลไปยัง _analytical store_

## _Microsoft Fabric_

![Fabric](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-roles-responsibilities-world-of-data/media/3-fabric-icon.png)  
แพลตฟอร์ม _SaaS_ แบบรวมศูนย์สำหรับ:
- _Data ingestion & ETL_
- _Data lakehouse / warehouse analytics_
- _Machine learning_
- _Realtime analytics_
- _Visualization & AI insights_
- _Governance_

_Data engineers_ ใช้สร้างโซลูชันวิเคราะห์แบบรวมศูนย์ทั้งหมดในแพลตฟอร์มเดียวภายใต้ _OneLake_

## _Azure Databricks_

![Databricks](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-roles-responsibilities-world-of-data/media/azure-databricks.png)  
แพลตฟอร์มวิเคราะห์ที่รวม _Apache Spark_ กับ SQL และอินเทอร์เฟซจัดการ  
_Data engineers_ ใช้ทักษะ Spark/Databricks สร้าง analytical store  
_Data analysts_ ใช้ _notebook_ วิเคราะห์และสร้าง visualization ผ่านเว็บ

## _Azure Stream Analytics_

![Stream Analytics](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-roles-responsibilities-world-of-data/media/stream-analytics.png)  
เครื่องมือประมวลผลข้อมูลแบบ _streaming_ แบบเรียลไทม์  
รับข้อมูลเข้า ใช้ _query_ เพื่อแยกและจัดการข้อมูล แล้วส่งออกเพื่อวิเคราะห์หรือประมวลผลต่อ  
_Data engineers_ ใช้เชื่อมสถาปัตยกรรมวิเคราะห์กับ _real-time data_

## _Azure Data Explorer_

![Data Explorer](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-roles-responsibilities-world-of-data/media/azure-data-explorer.png)  
แพลตฟอร์มวิเคราะห์ข้อมูลขนาดใหญ่ (_big data_) ที่เหมาะกับ _log_ และ _IoT telemetry_  
_Data analysts_ ใช้สืบค้นข้อมูลที่มี _timestamp_ เพื่อทำการวิเคราะห์เชิงเวลา

## _Microsoft Purview_

![Purview](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-roles-responsibilities-world-of-data/media/azure-purview.png)  
บริการสำหรับ _data governance_ และการค้นหาแหล่งข้อมูลในระดับองค์กร  
ช่วยติดตาม _data lineage_ และสร้างแผนที่ข้อมูลข้ามหลายระบบ  
_Data engineers_ ใช้เพื่อควบคุมคุณภาพและความน่าเชื่อถือของข้อมูลที่ใช้ใน _analytical workloads_