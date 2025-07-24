
ข้อมูลเป็นรากฐานของ _machine learning_ โดยทั้ง _ปริมาณของข้อมูล_ และ _คุณภาพของข้อมูล_ ต่างก็ส่งผลต่อ _accuracy_ ของโมเดล

ในการฝึก _machine learning model_ เราต้อง:

- ระบุ _แหล่งข้อมูล_ และ _รูปแบบข้อมูล_ ที่ต้องการใช้  
- เลือกวิธีที่จะ _ให้บริการข้อมูล (serve data)_  
- ออกแบบ _โซลูชันการนำเข้าข้อมูล (data ingestion)_

เพื่อให้ได้ข้อมูลที่พร้อมสำหรับฝึกโมเดล เราจำเป็นต้อง _ดึงข้อมูล (extract)_ จากแหล่งที่มา และจัดให้พร้อมใช้งานในบริการของ Azure ที่ใช้ในการฝึกหรือทำนายด้วยโมเดล

## Identify data source and format

ขั้นแรกคือการระบุว่า _แหล่งข้อมูล (data source)_ ของคุณคืออะไร และมี _รูปแบบข้อมูล (data format)_ เป็นแบบใดในปัจจุบัน

| Identify the | Examples                                                                                                        |
| ------------ | --------------------------------------------------------------------------------------------------------------- |
| Data source  | ข้อมูลอาจเก็บไว้ในระบบ _CRM_, ฐานข้อมูลเชิงธุรกรรม เช่น _SQL database_, หรือมาจาก _อุปกรณ์ IoT_                 |
| Data format  | ต้องเข้าใจว่าข้อมูลปัจจุบันอยู่ในรูปแบบใด เช่น _structured_ (เชิงตาราง), _semi-structured_, หรือ _unstructured_ |

หลังจากนั้น คุณต้องตัดสินใจว่า _ต้องใช้ข้อมูลประเภทใด_ ในการฝึกโมเดล และต้องการให้ข้อมูลนั้นอยู่ใน _รูปแบบแบบไหน_ เพื่อให้โมเดลสามารถใช้งานได้

## Design a data ingestion solution

โดยทั่วไป _แนวทางปฏิบัติที่ดีที่สุด_ คือการ _ดึงข้อมูล (extract)_ ออกจากแหล่งที่มาก่อนที่จะนำไปวิเคราะห์ ไม่ว่าจะใช้สำหรับ _data engineering_, _data analysis_ หรือ _data science_ ก็ตาม

กระบวนการนี้จะประกอบด้วย  
- _Extract_: ดึงข้อมูลออกจากแหล่ง  
- _Transform_: แปลงข้อมูลให้อยู่ในรูปแบบที่ต้องการ  
- _Load_: โหลดข้อมูลเข้าสู่ _serving layer_  

เรียกรวมกันว่า _ETL (Extract, Transform, Load)_ หรือ _ELT (Extract, Load, Transform)_

_serving layer_ คือส่วนที่ทำให้ข้อมูลพร้อมสำหรับใช้กับบริการต่าง ๆ เช่นการ _ฝึก machine learning model_

ในการเคลื่อนย้ายและแปลงข้อมูล สามารถใช้ _data ingestion pipeline_ ซึ่งคือชุดของงานที่ทำหน้าที่ดึงและแปลงข้อมูลตามลำดับ เราสามารถตั้งค่าให้ pipeline นี้ _ทำงานแบบแมนนวล_ หรือ _ตั้งเวลาให้ทำงานอัตโนมัติ_ ก็ได้

บริการของ Azure ที่สามารถใช้สร้าง pipeline ได้ เช่น _Azure Synapse Analytics_, _Azure Databricks และ _Azure Machine Learning_

แนวทางที่นิยมสำหรับ _data ingestion solution_ มีขั้นตอนดังนี้:

1. _Extract_ ข้อมูลดิบจากแหล่งที่มา เช่น _CRM system_ หรือ _อุปกรณ์ IoT_  
2. คัดลอกและ _แปลงข้อมูล_ ด้วย _Azure Synapse Analytics_  
3. จัดเก็บข้อมูลที่เตรียมไว้แล้วลงใน _Azure Blob Storage_  
4. ใช้ _Azure Machine Learning_ ในการ _ฝึกโมเดล (train the model)_

![Diagram showing an example of a data ingestion pipeline.](https://learn.microsoft.com/en-us/training/wwl-data-ai/design-machine-learning-model-training-solution/media/data-ingestion-pipeline.png)

## Explore an example

ลองจินตนาการว่าคุณต้องการฝึก _โมเดลพยากรณ์อากาศ_

คุณต้องการใช้ _ตารางเดียว_ ที่รวมข้อมูล _อุณหภูมิที่วัดได้ในแต่ละนาที_ ทั้งหมดเข้าไว้ด้วยกัน จากนั้นต้องการ _คำนวณค่าเฉลี่ย_ เพื่อให้ได้ _ตารางที่แสดงอุณหภูมิเฉลี่ยต่อชั่วโมง_

เพื่อสร้างตารางนี้ คุณจำเป็นต้อง _แปลงข้อมูลแบบกึ่งโครงสร้าง (semi-structured data)_ ที่ได้จาก _อุปกรณ์ IoT_ ซึ่งวัดอุณหภูมิเป็นช่วง ๆ ให้กลายเป็น _ข้อมูลแบบตาราง (tabular data)_

![Diagram showing an example of JSON data converted to a table.](https://learn.microsoft.com/en-us/training/wwl-data-ai/design-machine-learning-model-training-solution/media/json-to-table.png)

