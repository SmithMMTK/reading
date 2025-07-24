_Analytical data store_ มีอยู่ 2 ประเภทหลักที่พบได้บ่อย
## Data warehouses

![Diagram of a data warehouse with a star schema.](https://learn.microsoft.com/en-us/training/wwl-data-ai/examine-components-of-modern-data-warehouse/media/data-warehouse.png)

_data warehouse_ คือฐานข้อมูลแบบ _relational_ ที่มีการจัดเก็บข้อมูลใน _schema_ ซึ่งออกแบบมาเพื่อรองรับการวิเคราะห์ข้อมูล (_data analytics_) มากกว่าการประมวลผลธุรกรรม (_transactional workloads_)

โดยทั่วไป ข้อมูลจาก _transactional store_ จะถูกแปลงให้อยู่ใน _schema_ ที่มีการเก็บค่าตัวเลขไว้ใน _fact table_ และเชื่อมโยงกับ _dimension table_ หนึ่งหรือหลายตาราง ซึ่งใช้แทน _entities_ ที่สามารถนำมาใช้ในการรวมข้อมูล (_aggregation_) ได้  
ตัวอย่างเช่น _fact table_ อาจเก็บข้อมูลคำสั่งซื้อ ซึ่งสามารถรวมยอดตาม _dimension_ เช่น ลูกค้า สินค้า สาขา และช่วงเวลา (ทำให้สามารถดูยอดขายรวมรายเดือนแยกตามสินค้าและแต่ละสาขาได้ง่าย)

โครงสร้างตารางแบบนี้เรียกว่า _star schema_ แต่หากมีการเพิ่มตารางเพิ่มเติมที่เชื่อมโยงกับ _dimension table_ เพื่อแสดงลำดับชั้นของข้อมูล เช่น สินค้าเชื่อมกับประเภทสินค้า จะกลายเป็น _snowflake schema_

_data warehouse_ เป็นตัวเลือกที่ดีหากคุณมีข้อมูลธุรกรรมที่สามารถจัดรูปแบบให้อยู่ใน _structured schema_ ได้ และต้องการใช้ _SQL_ ในการสืบค้นข้อมูลเหล่านั้น

## Data lakes

![Diagram of a data lake in which files are abstracted by tables.](https://learn.microsoft.com/en-us/training/wwl-data-ai/examine-components-of-modern-data-warehouse/media/data-lake.png)

_data lake_ คือที่เก็บข้อมูลแบบไฟล์ (_file store_) ซึ่งมักอยู่บนระบบไฟล์แบบกระจาย (_distributed file system_) เพื่อให้สามารถเข้าถึงข้อมูลได้อย่างมีประสิทธิภาพสูง เทคโนโลยีอย่าง _Spark_ หรือ _Hadoop_ มักถูกใช้ในการประมวลผลคำสั่ง query จากไฟล์ที่จัดเก็บไว้ และส่งข้อมูลกลับมาเพื่อทำ _reporting_ และ _analytics_

ระบบเหล่านี้มักใช้แนวคิด _schema-on-read_ ซึ่งหมายถึงการกำหนด _schema_ แบบตารางให้กับไฟล์ข้อมูลกึ่งโครงสร้าง (_semi-structured data_) เฉพาะตอนที่อ่านข้อมูลเพื่อวิเคราะห์ โดยไม่ได้บังคับให้ข้อมูลต้องมีรูปแบบตอนที่จัดเก็บ  

_data lake_ เหมาะสำหรับรองรับข้อมูลหลากหลายประเภท ทั้งแบบมีโครงสร้าง (_structured_), กึ่งโครงสร้าง (_semi-structured_) และไม่มีโครงสร้าง (_unstructured_) โดยไม่ต้องกำหนด _schema_ ล่วงหน้าเมื่อลงข้อมูล

### Hybrid approaches

คุณสามารถใช้แนวทางแบบผสม (_hybrid_) ที่รวมคุณสมบัติของ _data lake_ และ _data warehouse_ เข้าไว้ด้วยกันในรูปแบบที่เรียกว่า _data lakehouse_ โดยข้อมูลดิบจะถูกจัดเก็บเป็นไฟล์ใน _data lake_ และ _Microsoft Fabric SQL analytics endpoint_ จะเปิดเผยข้อมูลเหล่านั้นให้สามารถเข้าถึงในรูปแบบ _tables_ ซึ่งสามารถสืบค้นด้วย _SQL_ ได้

เมื่อคุณสร้าง _Lakehouse_ ด้วย _Microsoft Fabric_ ระบบจะสร้าง _SQL analytics endpoint_ ให้โดยอัตโนมัติ _data lakehouse_ เป็นแนวทางใหม่ที่เกิดขึ้นในระบบที่ใช้ _Spark_ โดยใช้เทคโนโลยีอย่าง _Delta Lake_ เพื่อเพิ่มความสามารถของการเก็บข้อมูลแบบ _relational_ ลงไปใน _Spark_ ซึ่งหมายความว่าคุณสามารถกำหนด _table_ ที่มีการบังคับใช้ _schema_, มีความสอดคล้องเชิงธุรกรรม (_transactional consistency_), รองรับทั้ง _batch-loaded_ และ _streaming data sources_, และสามารถสืบค้นข้อมูลผ่าน _SQL API_ ได้

## Azure services for analytical stores

บน Azure มีบริการหลายตัวที่สามารถใช้ในการสร้าง _large-scale analytical store_ ได้ เช่น:

![Screenshot of a Microsoft Fabric logo.](https://learn.microsoft.com/en-us/training/wwl-data-ai/examine-components-of-modern-data-warehouse/media/fabric-icon.png)**[Microsoft Fabric](https://www.microsoft.com/microsoft-fabric)** เป็นโซลูชันแบบครบวงจร (_unified, end-to-end_) สำหรับการวิเคราะห์ข้อมูลขนาดใหญ่ (_large scale data analytics_) บริการนี้รวมเอาหลายเทคโนโลยีและความสามารถเข้าไว้ด้วยกัน ช่วยให้คุณสามารถผสานความน่าเชื่อถือและความถูกต้องของ _relational data warehouse_ ที่ใช้ _SQL Server_ ซึ่งมีประสิทธิภาพสูงและสามารถปรับขนาดได้ กับความยืดหยุ่นของ _data lake_ และ _Apache Spark_ แบบโอเพ่นซอร์ส

นอกจากนี้ยังรองรับการวิเคราะห์ _log_ และ _telemetry_ แบบเรียลไทม์โดยตรงผ่าน _Microsoft Fabric Real-Time Intelligence_ และมี _data pipelines_ สำหรับการ _ingest_ และแปลงข้อมูล (_transformation_) ที่ติดตั้งมาในตัว

แต่ละส่วนของ _Microsoft Fabric_ จะมีหน้า _Home_ ของตัวเอง เช่น _Data Factory Home_ ซึ่งจะแสดงรายการที่คุณสร้างไว้หรือมีสิทธิ์เข้าถึงจากทุก _workspace_ ที่คุณใช้งาน _Microsoft Fabric_ เป็นตัวเลือกที่ยอดเยี่ยมหากคุณต้องการสร้างระบบวิเคราะห์ข้อมูลแบบรวมศูนย์ (_unified analytics solution_)

![Screenshot of an Azure Databricks logo.](https://learn.microsoft.com/en-us/training/wwl-data-ai/examine-components-of-modern-data-warehouse/media/azure-databricks.png)**[Azure Databricks](https://azure.microsoft.com/services/databricks)** คือบริการของ Azure ที่ติดตั้งแพลตฟอร์ม _Databricks_ ซึ่งเป็นที่นิยมในการวิเคราะห์ข้อมูล  
Databricks เป็นโซลูชันด้าน _data analytics_ แบบครบวงจรที่พัฒนาบน _Apache Spark_ โดยรองรับทั้งความสามารถของ _SQL_ โดยตรง และมี _Spark clusters_ ที่ถูกปรับแต่งมาเฉพาะสำหรับงานวิเคราะห์ข้อมูลและงานด้าน _data science_

Databricks มี _interactive user interface_ ที่ให้คุณบริหารจัดการระบบ และสำรวจข้อมูลผ่าน _interactive notebooks_ ได้อย่างสะดวก เนื่องจาก Databricks ถูกใช้งานอย่างแพร่หลายในหลายแพลตฟอร์มคลาวด์ หากคุณมีความเชี่ยวชาญในแพลตฟอร์มนี้อยู่แล้ว หรือมีความต้องการใช้งานในสภาพแวดล้อมแบบ _multicloud_ หรือระบบที่ย้ายข้ามคลาวด์ได้ (_cloud-portable_) การใช้ _Azure Databricks_ เป็น _analytical store_ ก็เป็นตัวเลือกที่เหมาะสม

 Note
	บริการแต่ละตัวข้างต้นสามารถมองว่าเป็น _analytical data store_ ได้ เพราะมีทั้ง _schema_ และ _interface_ ที่ใช้ในการสืบค้นข้อมูล อย่างไรก็ตาม ในหลายกรณี ข้อมูลจริง ๆ จะถูกจัดเก็บไว้ใน _data lake_ และบริการเหล่านี้ทำหน้าที่ในการ _process_ ข้อมูลและรันคำสั่ง _query_ แทน บางโซลูชันอาจใช้บริการหลายตัวร่วมกัน เช่น กระบวนการ _ELT (extract, load, and transform)_ อาจคัดลอกข้อมูลเข้า _data lake_ ก่อน แล้วใช้บริการหนึ่งเพื่อแปลงข้อมูล และใช้อีกบริการหนึ่งเพื่อสืบค้นข้อมูล  ตัวอย่างเช่น _pipeline_ อาจใช้ _notebook_ ที่รันอยู่บน _Azure Databricks_ เพื่อประมวลผลข้อมูลปริมาณมากใน _data lake_ แล้วโหลดข้อมูลที่ผ่านการแปลงแล้วเข้าสู่ _Microsoft Fabric Warehouse_ ในรูปแบบ _tables_
