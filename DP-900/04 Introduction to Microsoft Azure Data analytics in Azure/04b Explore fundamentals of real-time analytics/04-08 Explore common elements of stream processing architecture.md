
มีเทคโนโลยีมากมายที่สามารถใช้ในการสร้างโซลูชัน _stream processing_ ได้ แม้ว่ารายละเอียดการใช้งานจะต่างกันไปในแต่ละกรณี แต่สถาปัตยกรรม _streaming_ ส่วนใหญ่จะมี _องค์ประกอบพื้นฐานที่คล้ายกัน_

## A general architecture for stream processing

ในรูปแบบง่ายที่สุด _สถาปัตยกรรมระดับสูงของ stream processing_ จะมีหน้าตาประมาณนี้:

![Diagram of an event generating data, which is captured in a queue before being processed, and the results are written to a data store or visualization.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-fundamentals-stream-processing/media/stream-architecture.png)

1. มีเหตุการณ์หนึ่งเกิดขึ้นและสร้าง _ข้อมูล_ ขึ้นมา เช่น สัญญาณจากเซนเซอร์, ข้อความในโซเชียลมีเดีย, รายการในไฟล์ล็อก หรือเหตุการณ์ใด ๆ ที่ส่งผลให้เกิด _ข้อมูลดิจิทัล_
2. ข้อมูลที่สร้างขึ้นจะถูก _เก็บไว้ในแหล่งข้อมูลแบบสตรีม (streaming source)_ เพื่อรอการประมวลผล กรณีง่าย ๆ source อาจเป็น _โฟลเดอร์บน cloud_ หรือ _ตารางในฐานข้อมูล_ ส่วนในโซลูชันที่มีความซับซ้อนมากขึ้น source อาจเป็น _queue_ ที่มี _ตรรกะควบคุมลำดับของข้อมูล_ และช่วยให้มั่นใจว่าแต่ละเหตุการณ์จะถูกประมวลผล _ครั้งเดียวและตามลำดับ_
3. ข้อมูลเหตุการณ์จะถูกประมวลผล โดยใช้ _query ที่ทำงานต่อเนื่องตลอดเวลา_ เพื่อเลือกเหตุการณ์บางประเภท, ดึงเฉพาะค่าที่ต้องการ, หรือคำนวณข้อมูลแบบรวม (_aggregate_) ตามช่วงเวลา (_temporal windows_) เช่น นับจำนวนสัญญาณจากเซนเซอร์ในแต่ละนาที
4. ผลลัพธ์จากการประมวลผล _stream_ จะถูก _เขียนไปยังปลายทาง (sink)_ เช่น ไฟล์, ตารางในฐานข้อมูล, แดชบอร์ดแบบเรียลไทม์ หรือ queue อื่น ๆ เพื่อใช้ใน query ขั้นถัดไป

## Real-time analytics services

Microsoft มีเทคโนโลยีหลากหลายที่สามารถใช้สร้างโซลูชัน _real-time analytics_ สำหรับ _streaming data_ ได้แก่:

- **Azure Stream Analytics**: เป็นบริการแบบ _PaaS (platform-as-a-service)_ ที่ให้คุณสามารถสร้าง _streaming jobs_ เพื่อรับข้อมูลจาก _streaming source_ ใช้ _perpetual query_ เพื่อประมวลผล และ _เขียนผลลัพธ์_ ไปยังปลายทางที่ต้องการได้
- **Spark Structured Streaming**: เป็นไลบรารีแบบโอเพ่นซอร์สที่ช่วยให้คุณพัฒนา _streaming solutions ที่ซับซ้อน_ ได้บนบริการที่ใช้ Apache Spark เช่น **Microsoft Fabric** และ **Azure Databricks**
- **Microsoft Fabric**: เป็นแพลตฟอร์มสำหรับ _ฐานข้อมูลและการวิเคราะห์ประสิทธิภาพสูง_ ซึ่งรวมฟีเจอร์หลายด้าน เช่น _Data Engineering_, _Data Factory_, _Data Science_, _Real-Time Analytics_, _Data Warehouse_ และ _Databases_

### _Sources_ for stream processing

บริการต่อไปนี้มักถูกใช้ในการ _ingest data_ สำหรับ _stream processing_ บน Azure:

- **Azure Event Hubs**: บริการรับข้อมูลที่ช่วยจัดการ _queue ของ event data_ เพื่อให้มั่นใจว่าเหตุการณ์แต่ละรายการจะถูก _ประมวลผลตามลำดับ_ และ _ครั้งเดียว_
- **Azure IoT Hub**: บริการรับข้อมูลคล้ายกับ Event Hubs แต่ถูกออกแบบให้เหมาะกับการจัดการ _ข้อมูลเหตุการณ์จากอุปกรณ์ IoT (Internet-of-things)_
- **Azure Data Lake Store Gen 2**: บริการจัดเก็บข้อมูลที่ _ขยายขนาดได้สูงมาก_ มักใช้ในกรณี _batch processing_ แต่ก็สามารถใช้เป็น _แหล่งข้อมูลสตรีม_ ได้เช่นกัน
- **Apache Kafka**: โซลูชันรับข้อมูลแบบโอเพ่นซอร์ส ที่นิยมใช้ร่วมกับ Apache Spark สำหรับระบบ ingest และ stream processing

### _Sinks_ for stream processing

ผลลัพธ์จากการ _stream processing_ มักถูกส่งไปยังบริการต่อไปนี้:

- **Azure Event Hubs**: ใช้ในการ _จัดคิวข้อมูลที่ผ่านการประมวลผล_ เพื่อใช้ในกระบวนการต่อเนื่องขั้นถัดไป
- **Azure Data Lake Store Gen 2**, **Microsoft OneLake**, หรือ **Azure blob storage**: ใช้เพื่อ _จัดเก็บผลลัพธ์ที่ประมวลผลแล้วในรูปแบบไฟล์_
- **Azure SQL Database**, **Azure Databricks**, หรือ **Microsoft Fabric**: ใช้เพื่อ _เก็บผลลัพธ์ที่ประมวลผลแล้วในรูปแบบตาราง_ สำหรับการ query และการวิเคราะห์ต่อ
- **Microsoft Power BI**: ใช้ในการ _แสดงผลข้อมูลแบบเรียลไทม์_ ผ่าน _รายงาน_ และ _แดชบอร์ด_