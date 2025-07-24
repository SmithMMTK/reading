
โซลูชัน _knowledge mining_ ช่วยให้สามารถ _ดึงข้อมูลโดยอัตโนมัติ_ จากข้อมูลจำนวนมากที่มักจะเป็น _ข้อมูลไม่มีโครงสร้าง_ หนึ่งในพื้นฐานของ knowledge mining คือ _search_ ซึ่งเป็นกระบวนการดึงข้อมูลที่เกี่ยวข้องจากชุดข้อมูลขนาดใหญ่เพื่อตอบสนองต่อคำค้นของผู้ใช้

การใช้ _AI-powered information extraction_ ช่วยให้ _สิ่งที่ค้นหาได้ใน search index_ มีความหลากหลายและแม่นยำมากขึ้น

ในกระบวนการค้นหาด้วย AI ข้อมูลจะผ่านขั้นตอนหลัก ๆ ดังนี้:
- **Document cracking** คือขั้นตอนการ _เปิดไฟล์เอกสาร_ เช่น PDF เพื่อแปลงเนื้อหาออกมาในรูปแบบ _ASCII text_ เพื่อวิเคราะห์และนำไปทำ index ต่อ
- ต่อมาคือ **AI enrichment** ซึ่งจะใช้ AI วิเคราะห์เนื้อหาต้นฉบับเพื่อ _ดึงข้อมูลเพิ่มเติม_ เช่น _ใส่คำบรรยายให้ภาพ_ หรือ _วิเคราะห์อารมณ์ของข้อความ_

ข้อมูลที่ผ่านการ enrichment จะถูกส่งไปยัง _knowledge store_ เพื่อ _เก็บผลลัพธ์_ ของ pipeline สำหรับการวิเคราะห์หรือใช้งานต่อ ผลลัพธ์สุดท้ายจะถูกจัดเก็บในรูปแบบ _JSON_ ซึ่งใช้ในการเติมข้อมูลเข้าสู่ _search index_ เมื่อ _search index_ ได้รับการเติมข้อมูลแล้ว ผู้ใช้สามารถค้นหาด้วยคำ เช่น "coffee" และระบบจะค้นข้อมูลนั้นจากใน index

_search index_ มีโครงสร้างคล้ายตาราง ซึ่งเรียกว่า _index schema_ โดยใน schema จะมี:

- _fields_: ช่องเก็บข้อมูลที่ใช้ในการค้นหา เช่น ชื่อสินค้า
- _field data type_: ประเภทข้อมูล เช่น _string_
- _field attributes_: คุณสมบัติเพิ่มเติมของ field เช่น _filter_ หรือ _sort_

ตัวอย่าง schema ที่ใช้ใน search index จะถูกแสดงด้านล่าง

![A screenshot of the structure of an index schema in json including key phrases and image tags.](https://learn.microsoft.com/en-us/training/wwl-data-ai/introduction-information-extraction/media/json-index-example.png)

ผลลัพธ์ที่ได้คือ _search solution_ ซึ่งโดยทั่วไปจะประกอบด้วยองค์ประกอบหลัก ๆ ดังนี้:

| **Component**        | **Function (หน้าที่)**                                                                                           |
| -------------------- | ---------------------------------------------------------------------------------------------------------------- |
| _API Layer_          | รับคำค้นจากผู้ใช้ (_user query_) และส่งคำค้นไปยัง _search engine_                                                |
| _Query Processor_    | วิเคราะห์และตีความคำค้น (_parse & interpret_)                                                                    |
| _Search Strategies_  | กำหนดกลยุทธ์ในการค้นหา เช่น _keyword search_, _semantic search_, _vector search_ หรือ _hybrid_                   |
| _Execution Engine_   | ประมวลผลคำค้นกับ _search index_ โดยมี _AI-powered information extraction_ ช่วยเพิ่มปริมาณข้อมูลที่สามารถค้นหาได้ |
| _Result Aggregator_  | รวมผลลัพธ์จากหลายแหล่งให้เป็นรายการเดียว                                                                         |
| _Ranking Engine_     | เรียงลำดับผลลัพธ์ตาม _ความเกี่ยวข้อง_, _ความสดใหม่_, _ความนิยม_, หรือ _สัญญาณจาก AI_                             |
| _Response Formatter_ | จัดรูปแบบผลลัพธ์เพื่อแสดงผลใน _user interface_                                                                   |
