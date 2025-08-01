
ไม่มีวิธีการโหลดข้อมูลแบบใดที่เหมาะกับทุกกรณี วิธีที่ดีที่สุดขึ้นอยู่กับความต้องการทางธุรกิจเฉพาะของคุณและคำถามที่ต้องการคำตอบจากข้อมูล

เมื่อพูดถึงการโหลดข้อมูลเข้าสู่ _data warehouse_ มีหลายปัจจัยที่ควรพิจารณา:

|Description|
|---|---|
|**Load volume & frequency**|ประเมินปริมาณข้อมูลและความถี่ในการโหลดเพื่อให้ปรับแต่งประสิทธิภาพได้เหมาะสม|
|**Governance**|ข้อมูลที่โหลดเข้าสู่ _OneLake_ จะถูกควบคุมตามนโยบายของระบบโดยอัตโนมัติ|
|**Data mapping**|จัดการการแมปข้อมูลจากต้นทาง ไปยัง _staging_ และเข้าสู่ _warehouse_|
|**Dependencies**|ทำความเข้าใจการพึ่งพากันใน _data model_ โดยเฉพาะการโหลด _dimension_|
|**Script design**|ออกแบบสคริปต์การนำเข้าอย่างมีประสิทธิภาพ โดยพิจารณาชื่อคอลัมน์ กฎการกรอง การแมปค่า และการทำดัชนีฐานข้อมูล (_indexing_)|

อ่านเพิ่มเติมได้ที่:

- [Create a Warehouse in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-warehouse/create-warehouse)
- [Ingest data into the Warehouse](https://learn.microsoft.com/en-us/fabric/data-warehouse/ingest-data)
- [Compare the Warehouse and the SQL analytics endpoint of the Lakehouse](https://learn.microsoft.com/en-us/fabric/data-warehouse/data-warehousing#compare-the-warehouse-and-the-sql-endpoint-of-the-lakehouse?azure-portal=true)