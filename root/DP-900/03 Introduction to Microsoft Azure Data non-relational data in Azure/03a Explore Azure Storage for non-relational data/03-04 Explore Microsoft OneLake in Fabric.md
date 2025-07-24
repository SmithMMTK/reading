
#microsoftfabric

_Microsoft Fabric_ จะสร้าง _OneLake_ ให้โดยอัตโนมัติ ซึ่ง _OneLake_ นี้ถูกสร้างขึ้นบนพื้นฐานของ _Azure Data Lake Storage Gen2_

![Diagram showing the function and structure of OneLake.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-provision-deploy-non-relational-data-services-azure/media/onelake-foundation-for-fabric.png)

_OneLake_ คือ _logical data lake_ แบบรวมศูนย์ที่ออกแบบมาเพื่อรองรับการใช้งานของทั้งองค์กร เป็นที่จัดเก็บข้อมูลวิเคราะห์ (_analytics data_) ทั้งหมด ไม่ว่าจะเป็นข้อมูลแบบ _structured_ หรือ _unstructured_

เมื่อคุณใช้งาน _Microsoft Fabric_ จะได้รับ _OneLake_ โดยอัตโนมัติ ซึ่งทำหน้าที่เป็นศูนย์กลางในการจัดเก็บข้อมูลจากทุกแหล่ง โดยสามารถใช้ข้อมูลเดียวกันร่วมกันได้ในหลาย _analytical engines_ โดยไม่ต้องคัดลอกหรือย้ายข้อมูลเลย ช่วยลดความซ้ำซ้อนและเพิ่มประสิทธิภาพในการทำงานกับข้อมูลหลากหลายรูปแบบ

## Key Benefits of OneLake

- _**Organization-wide data lake**_ ก่อนที่จะมี _OneLake_ แต่ละหน่วยงานในองค์กรมักสร้าง _data lake_ แยกกัน แต่ _OneLake_ มอบทางออกที่ทำให้ทุกส่วนขององค์กรสามารถใช้งาน _data lake_ เดียวร่วมกันได้อย่างมีประสิทธิภาพ

- _**Distributed ownership and collaboration**_ ภายใน _tenant_ สามารถสร้าง _workspaces_ ให้แต่ละแผนกหรือทีมบริหารจัดการข้อมูลของตนเองได้ ทำให้เกิดการทำงานร่วมกันโดยยังรักษาขอบเขตด้าน _governance_

- _**Open and Compatible**_ เนื่องจาก _OneLake_ ถูกสร้างบน _Azure Data Lake Storage (ADLS) Gen2_ และใช้รูปแบบไฟล์ _Delta Parquet_ จึงสามารถใช้ร่วมกับ API และ SDK ของ ADLS Gen2 เดิมได้ ทำให้สามารถใช้งานร่วมกับแอปพลิเคชันที่มีอยู่ได้ทันที

- _**Easy to navigate**_ ผู้ใช้สามารถเข้าถึงและเรียกดูข้อมูลใน _OneLake_ ได้อย่างง่ายดายผ่าน _[OneLake file explorer](https://learn.microsoft.com/en-us/fabric/onelake/onelake-file-explorer)_ บนระบบปฏิบัติการ Windows

For more information, see [OneLake, the OneDrive for data](https://learn.microsoft.com/en-us/fabric/onelake/onelake-overview).