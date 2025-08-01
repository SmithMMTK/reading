
[Microsoft Fabric Data Warehouse](https://learn.microsoft.com/en-us/fabric/data-warehouse/) คือแพลตฟอร์มแบบครบวงจรสำหรับงานด้านข้อมูล การวิเคราะห์ และ _AI (Artificial Intelligence)_ โดยมุ่งเน้นการจัดเก็บ จัดระเบียบ และบริหารจัดการข้อมูลขนาดใหญ่ทั้งแบบมีโครงสร้างและกึ่งโครงสร้าง

_**Data warehouse**_ ใน _Microsoft Fabric_ ขับเคลื่อนด้วย _Synapse Analytics_ ซึ่งมีฟีเจอร์หลากหลายที่ช่วยให้การจัดการและวิเคราะห์ข้อมูลเป็นเรื่องง่าย พร้อมรองรับ _T-SQL_ อย่างเต็มรูปแบบในระดับองค์กร

ต่างจาก _dedicated SQL pool_ ใน _Synapse Analytics_ ที่เน้นโครงสร้างฐานข้อมูลเฉพาะ ใน _Microsoft Fabric_ จะเน้นการจัดเก็บข้อมูลใน _data lake_ เดียว โดยใช้ไฟล์รูปแบบ _Parquet_ ทำให้ผู้ใช้สามารถโฟกัสกับงานด้านการเตรียมข้อมูล วิเคราะห์ และการรายงานได้ง่ายขึ้น โดยข้อมูลจะถูกจัดเก็บใน _Microsoft OneLake_ ซึ่งใช้ความสามารถของ _SQL engine_ อย่างเต็มประสิทธิภาพ

[![Diagram showing the function and structure of OneLake.](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/1-access-onelake-data-other-tools.png)](https://learn.microsoft.com/en-us/training/wwl-data-ai/load-data-into-microsoft-fabric-data-warehouse/media/1-access-onelake-data-other-tools.png#lightbox)

## Understand the ETL (Extract, Transform, and Load) process

_ETL_ คือกระบวนการพื้นฐานสำหรับการวิเคราะห์ข้อมูลและการทำงานกับ _data warehouse_ โดยประกอบด้วยขั้นตอนหลัก ๆ ดังนี้:

| Description                 |                                                                                                                                                                                                                                |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Data extraction**         | เป็นขั้นตอนการเชื่อมต่อกับระบบต้นทางและดึงข้อมูลที่จำเป็นมาใช้ในการวิเคราะห์                                                                                                                                                   |
| **Data transformation**     | เป็นการแปลงข้อมูลให้อยู่ในรูปแบบมาตรฐาน รวมถึงการรวมข้อมูลจากหลายตาราง, การทำความสะอาด, การลบค่าซ้ำ และการตรวจสอบความถูกต้องของข้อมูล                                                                                          |
| **Data loading**            | เป็นการโหลดข้อมูลที่ผ่านการแปลงเข้าสู่ _fact table_ และ _dimension table_ ในกรณีที่โหลดแบบเพิ่มขึ้น (_incremental load_) จะมีการอัปเดตข้อมูลใหม่เป็นระยะ โดยอาจต้องมีการจัดรูปแบบข้อมูลให้เข้ากับโครงสร้างของ _data warehouse_ |
| **Post-load optimizations** | หลังจากโหลดข้อมูลแล้ว สามารถทำการปรับแต่งเพื่อเพิ่มประสิทธิภาพของ _data warehouse_ ได้                                                                                                                                         |

ทุกขั้นตอนใน _ETL process_ สามารถรันแบบขนานกัน (_parallel_) ได้ตามลักษณะงาน และเมื่อข้อมูลบางส่วนพร้อมใช้งาน ก็สามารถโหลดเข้าได้ทันทีโดยไม่ต้องรอให้ขั้นตอนก่อนหน้าสิ้นสุดก่อน

ในหน่วยถัดไป เราจะสำรวจวิธีการต่าง ๆ ในการโหลดข้อมูลเข้าสู่ _warehouse_ และดูว่ากระบวนการเหล่านี้ช่วยให้การสร้าง _data warehouse workload_ ง่ายขึ้นได้อย่างไร

---

## Next unit: Explore data load strategies
