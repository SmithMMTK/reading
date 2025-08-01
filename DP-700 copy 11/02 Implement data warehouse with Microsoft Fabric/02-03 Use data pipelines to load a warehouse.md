
_Warehouse_ ของ _Microsoft Fabric_ มีเครื่องมือสำหรับการ _ingest_ ข้อมูลแบบในตัว ซึ่งช่วยให้ผู้ใช้สามารถโหลดข้อมูลเข้า _warehouse_ ได้ในขนาดใหญ่ ทั้งแบบเขียนโค้ดและไม่ต้องเขียนโค้ด

_data pipeline_ คือบริการแบบ _cloud-based_ สำหรับ _data integration_ ที่ช่วยให้สามารถสร้าง _workflow_ สำหรับการเคลื่อนย้ายและแปลงข้อมูลในระดับขนาดใหญ่ ผู้ใช้สามารถสร้างและตั้งเวลาให้ _data pipeline_ ทำงานเพื่อ _ingest_ และโหลดข้อมูลจากแหล่งข้อมูลต่าง ๆ ได้ และสามารถสร้างกระบวนการ _ETL_ หรือ _ELT_ ที่ซับซ้อน โดยใช้ _data flow_ เพื่อแปลงข้อมูลแบบ _visual_

ฟีเจอร์ส่วนใหญ่ของ _data pipeline_ ใน _Microsoft Fabric_ ได้มาจาก _Azure Data Factory_ ทำให้สามารถเชื่อมต่อและใช้งานร่วมกันได้อย่างไร้รอยต่อภายในระบบของ _Microsoft Fabric_

> **Note**  
> ข้อมูลทั้งหมดใน _Warehouse_ จะถูกจัดเก็บโดยอัตโนมัติในรูปแบบ _Delta Parquet_ ภายใน _OneLake_

## Create a data pipeline

มีหลายวิธีในการเปิดตัวแก้ไข _data pipeline_:

- จากหน้า _workspace_: เลือก **+ New** จากนั้นเลือก **Data pipeline** (หากไม่พบในรายการ ให้เลือก **More options** แล้วหาที่หัวข้อ **Get data**)
- จาก _warehouse asset_: เลือก **Get Data** แล้วเลือก **New data pipeline**

![Screenshot showing the shortcuts for a few features in the Warehouse asset.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/3-create-data-pipeline.png)

เมื่อสร้าง _pipeline_ จะมีให้เลือก 3 ตัวเลือก:

![Screenshot showing the options available when creating a pipeline.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/3-build-pipeline.png)

|Option|Description|
|---|---|
|**Add pipeline activity**|เปิดตัวแก้ไข _pipeline_ เพื่อให้คุณสร้าง _pipeline_ เอง|
|**Copy data**|เปิดตัวช่วย (_assistant_) สำหรับการคัดลอกข้อมูลจากหลายแหล่งไปยังปลายทาง พร้อมสร้าง _Copy Data task_ ที่ถูกตั้งค่าล่วงหน้า|
|**Choose a task to start**|เลือกจากชุด _template_ ที่เตรียมไว้สำหรับการเริ่ม _pipeline_ จากสถานการณ์ต่าง ๆ|

## Configure the copy data assistant

ตัวช่วยในการคัดลอกข้อมูล (_copy data assistant_) จะให้ประสบการณ์แบบเป็นขั้นตอน เพื่อช่วยกำหนดค่าการทำงานของ _Copy Data task_

![Screenshot showing the copy data assistant.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/3-copy-data-assistant.png)

ขั้นตอนประกอบด้วย:

1. **Choose data source**: เลือกตัวเชื่อมต่อ (_connector_) และให้ข้อมูลการเชื่อมต่อ
2. **Connect to a data source**: เลือกและดูตัวอย่างข้อมูล เลือกตารางหรือ _view_ หรือใช้คำสั่ง _query_ แบบกำหนดเอง
3. **Choose data destination**: เลือกแหล่งปลายทางของข้อมูล
4. **Connect to data destination**: เลือกและแมปคอลัมน์ระหว่างต้นทางและปลายทาง สามารถโหลดเข้าสู่ตารางใหม่หรือที่มีอยู่แล้ว
5. **Settings**: ตั้งค่าเพิ่มเติม เช่น การใช้ staging, ค่าปริยาย (_default values_)

หลังจากคัดลอกข้อมูลแล้ว คุณสามารถใช้ _task_ อื่นเพื่อแปลงและวิเคราะห์ข้อมูลต่อได้ และยังสามารถใช้ _Copy Data task_ เพื่อเผยแพร่ผลลัพธ์สำหรับ _BI_ และการใช้งานในแอปพลิเคชัน

## Schedule a data pipeline

คุณสามารถตั้งเวลาให้ _data pipeline_ ทำงานได้โดยเลือก **Schedule** จากตัวแก้ไข _data pipeline_

![Screenshot showing where to schedule a data pipeline from the pipeline designer.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/3-schedule-data-pipeline.png)

หรือสามารถตั้งค่าตารางเวลาได้ผ่านเมนู **Settings** ที่อยู่ในแถบ **Home** ของตัวแก้ไข _pipeline_

![Screenshot showing the configuration properties when you schedule a data pipeline.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/3-schedule-configuration.png)

แนะนำให้ใช้ _data pipeline_ หากต้องการประสบการณ์แบบไม่ต้องเขียนโค้ดหรือเขียนโค้ดน้อย (_code-free/low-code_) โดยเฉพาะกับ _workflow_ ที่มีตารางเวลา หรือต้องเชื่อมต่อกับแหล่งข้อมูลหลายประเภท

[เรียนรู้เพิ่มเติมเกี่ยวกับ data pipeline →](https://learn.microsoft.com/en-us/fabric/data-factory/ingest-data-warehouse)

## Next unit: Load data using T-SQL