
_Azure Data Lake Store (Gen1)_ เป็นบริการแยกต่างหากที่ออกแบบมาเพื่อเก็บข้อมูลแบบมีลำดับชั้น (_hierarchical data_) สำหรับ _analytical data lakes_ โดยเฉพาะ เหมาะกับระบบวิเคราะห์ _big data_ ที่ทำงานกับข้อมูลแบบ _structured_, _semi-structured_ และ _unstructured_ ที่ถูกจัดเก็บในรูปแบบไฟล์

_Azure Data Lake Storage Gen2_ เป็นรุ่นใหม่ของบริการนี้ ซึ่งถูกรวมอยู่ภายใน _Azure Storage_ โดยตรง ช่วยให้คุณสามารถใช้ประโยชน์จากความสามารถในการปรับขนาด (_scalability_) ของ _blob storage_ ร่วมกับการควบคุมต้นทุนผ่าน _storage tiers_ ได้ อีกทั้งยังรองรับ _hierarchical file system_ และสามารถใช้งานร่วมกับระบบวิเคราะห์ข้อมูลหลัก ๆ ได้เหมือนกับ _Gen1_

การรวมข้อดีของทั้ง _blob storage_ และ _data lake_ ใน _Gen2_ ทำให้เหมาะกับการใช้งานในระบบวิเคราะห์ข้อมูลขนาดใหญ่ที่ต้องการทั้งความยืดหยุ่นและประสิทธิภาพ

![Screenshot of an Azure blob storage container with a hierarchical namespace.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-provision-deploy-non-relational-data-services-azure/media/azure-data-lake.png)


ระบบอย่าง _Azure Databricks_ สามารถเชื่อมต่อ (_mount_) กับ _distributed file system_ ที่โฮสต์อยู่บน _Azure Data Lake Store Gen2_ และใช้เพื่อประมวลผลข้อมูลปริมาณมหาศาลได้

สำหรับผู้ใช้งาน _Microsoft Fabric_ จะได้รับการสร้าง _OneLake_ โดยอัตโนมัติ ซึ่งอยู่บนพื้นฐานของ _Azure Data Lake Storage Gen2_

หากต้องการสร้าง _file system_ สำหรับ _Azure Data Lake Store Gen2_ ต้องเปิดใช้งานตัวเลือก _**Hierarchical Namespace**_ ในตอนสร้าง _Azure Storage account_ หรือสามารถอัปเกรด _storage account_ ที่มีอยู่เดิมให้รองรับ _Data Lake Gen2_ ได้

แต่ต้องระวังว่า การอัปเกรดไปใช้ _hierarchical namespace_ จะเป็นกระบวนการทางเดียว (_one-way process_) คือ เมื่ออัปเกรดแล้วจะไม่สามารถย้อนกลับมาใช้แบบ _flat namespace_ ได้อีก