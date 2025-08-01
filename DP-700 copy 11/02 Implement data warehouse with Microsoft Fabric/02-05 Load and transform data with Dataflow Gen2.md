
[Dataflow Gen2](https://learn.microsoft.com/en-us/fabric/data-factory/dataflows-gen2-overview) คือรุ่นใหม่ของ _dataflows_ ที่มอบประสบการณ์การใช้งาน _Power Query_ อย่างครบถ้วน โดยช่วยนำทางผู้ใช้ในแต่ละขั้นตอนของการนำเข้าข้อมูล ทำให้กระบวนการสร้าง _dataflows_ ง่ายขึ้นและลดจำนวนขั้นตอนที่ต้องทำ

คุณสามารถใช้ _dataflows_ ภายใน _data pipeline_ เพื่อ _ingest_ ข้อมูลเข้าสู่ _lakehouse_ หรือ _warehouse_ รวมถึงกำหนดชุดข้อมูล (_dataset_) สำหรับรายงาน _Power BI_

## Create a dataflow

ในการสร้าง _dataflow_ ใหม่ ให้ไปที่ _workspace_ แล้วเลือก **+ New** หากไม่พบ **Dataflow Gen2** ให้เลือก **More options** แล้วหาในหัวข้อ **Data Factory**

![Animated GIF showing how to launch Dataflow Gen2 from the workspace.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/5-load-using-dataflow.gif)

## Import data

เมื่อเปิด _Dataflow Gen2_ ขึ้นมา คุณจะสามารถเลือกวิธีโหลดข้อมูลได้หลายแบบ

![Screenshot showing how to launch Data Pipeline from the Warehouse asset.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/5-import-options.png)

สามารถโหลดไฟล์ได้หลายประเภทด้วยขั้นตอนที่ง่าย เช่น การโหลดไฟล์ _text_ หรือ _CSV_ จากเครื่องของคุณ

![Screenshot showing how to load a text or CSV file.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/5-load-file.png)

เมื่อข้อมูลถูกนำเข้าแล้ว คุณสามารถเริ่มเขียน _dataflow_ ได้ทันที เช่น การล้างข้อมูล แปลงโครงสร้าง ลบหรือสร้างคอลัมน์ใหม่ โดยทุกขั้นตอนที่ทำจะถูกบันทึกไว้

## Transform data with Copilot

_Copilot_ เป็นผู้ช่วยสำคัญสำหรับการแปลงข้อมูลใน _dataflow_ ยกตัวอย่างเช่น หากคุณมีคอลัมน์ _Gender_ ที่มีค่า 'Male' และ 'Female' และต้องการแปลงค่าเหล่านี้

เริ่มจากเปิดใช้งาน _Copilot_ ภายใน _dataflow_ แล้วระบุคำสั่ง เช่น:  
_"Transform the Gender column. If Male 0, if Female 1. Then convert it to integer."_

![Screenshot showing how to use Copilot to apply transformation in a dataflow.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/5-copilot.png)

_Copilot_ จะเพิ่มขั้นตอนใหม่โดยอัตโนมัติ คุณสามารถย้อนกลับหรือเพิ่มขั้นตอนอื่นต่อได้

## Add a data destination

ฟีเจอร์ **Add data destination** ช่วยให้แยกขั้นตอน _ETL_ ออกจากพื้นที่เก็บข้อมูลปลายทาง ซึ่งทำให้โค้ดดูสะอาด เป็นระเบียบ และปรับเปลี่ยนได้ง่ายโดยไม่กระทบต่ออีกฝ่าย

หลังจากแปลงข้อมูลแล้ว ให้ไปที่แท็บ **Query settings** แล้วเลือก **+** เพื่อเพิ่มขั้นตอนปลายทางใน _dataflow_

![Screenshot showing the option to add a data destination in a dataflow.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/5-add-destination.png)

ตัวเลือกปลายทางที่รองรับ:

- Azure SQL Database
- Lakehouse
- Azure Data Explorer (Kusto)
- Azure Synapse Analytics (SQL DW)
- Warehouse

ข้อมูลที่โหลดเข้าสู่ปลายทาง เช่น _warehouse_ สามารถเข้าถึงและวิเคราะห์ได้ง่ายผ่านเครื่องมือต่าง ๆ ซึ่งเพิ่มความยืดหยุ่นและความสามารถในการวิเคราะห์ข้อมูล

เมื่อเลือก _warehouse_ เป็นปลายทาง จะสามารถเลือกวิธีอัปเดตข้อมูลได้สองแบบ:

![Diagram showing visually the difference between the append and replace methods to update a row.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/5-update-table-options.png)

- **Append:** เพิ่มข้อมูลแถวใหม่ลงในตารางที่มีอยู่
- **Replace:** แทนที่ข้อมูลทั้งหมดในตารางด้วยข้อมูลชุดใหม่

## Publish a dataflow

เมื่อเลือกวิธีอัปเดตแล้ว ขั้นตอนสุดท้ายคือการ **Publish** _dataflow_

การ _publish_ จะทำให้การแปลงข้อมูลและการโหลดมีผลใช้งานจริง ซึ่งสามารถเรียกใช้แบบแมนนวลหรือแบบตั้งเวลาได้ กระบวนการนี้ช่วยรวบรวมขั้นตอน _ETL_ ไว้ในหน่วยเดียวที่นำกลับมาใช้ได้ซ้ำ ช่วยให้การจัดการข้อมูลมีประสิทธิภาพมากขึ้น

ทุกการเปลี่ยนแปลงใน _dataflow_ จะมีผลหลังจากที่คุณ _publish_ ดังนั้นควรตรวจสอบและ _publish_ ทุกครั้งหลังการแก้ไข


---
## Next unit: Exercise: Load data into a warehouse in Microsoft Fabric