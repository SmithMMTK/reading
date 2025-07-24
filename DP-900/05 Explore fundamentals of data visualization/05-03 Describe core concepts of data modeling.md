
_Analytical models_ ช่วยให้คุณสามารถ _จัดโครงสร้างข้อมูล_ เพื่อรองรับการวิเคราะห์ โดยโมเดลจะประกอบด้วย _ตารางข้อมูลที่มีความสัมพันธ์กัน_ และกำหนดค่าเชิงตัวเลขที่ต้องการวิเคราะห์หรือรายงาน ซึ่งเรียกว่า _measures_ และองค์ประกอบที่ต้องการใช้ในการรวมกลุ่มข้อมูล ซึ่งเรียกว่า _dimensions_

ตัวอย่างเช่น โมเดลหนึ่งอาจมีตารางที่เก็บ _measures_ เช่น _ยอดขาย (revenue)_ หรือ _จำนวนที่ขายไป (quantity)_ และมี _dimensions_ เช่น _สินค้า_, _ลูกค้า_, และ _เวลา_ ซึ่งช่วยให้สามารถรวมยอดขายตามมุมมองต่าง ๆ ได้ เช่น _รวมยอดขายทั้งหมดตามลูกค้า_ หรือ _รวมจำนวนสินค้าที่ขายได้รายเดือนตามประเภทสินค้า_

ในเชิงแนวคิด โมเดลนี้จะมีโครงสร้างแบบ _multidimensional_ ซึ่งมักเรียกว่า _cube_ โดยแต่ละจุดตัดของมิติ (_dimensions_) จะเป็นค่ารวมเชิงตัวเลข (_aggregated measure_) สำหรับชุดของมิตินั้น ๆ

![Diagram of a data model.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-fundamentals-data-visualization/media/cube.png)

_หมายเหตุ_

แม้ว่าเราจะเรียก _analytical model_ ว่าเป็น _cube_ แต่ในความเป็นจริงแล้ว _อาจมีมากกว่าหรือน้อยกว่า 3 มิติ_ ก็ได้ — เพียงแต่มนุษย์เรามัก _นึกภาพเกิน 3 มิติได้ยากเท่านั้น!_

## Tables and schema

ตาราง _dimension_ ใช้แทน _หน่วยข้อมูลที่ต้องการใช้ในการรวมค่าตัวเลข_ เช่น _สินค้า_ หรือ _ลูกค้า_ โดยแต่ละแถวใน dimension table จะแทนหนึ่ง entity ที่มี _key เฉพาะตัว_ และคอลัมน์อื่น ๆ จะแสดง _attribute_ ของ entity นั้น เช่น สินค้ามี _ชื่อ_ และ _หมวดหมู่_, ลูกค้ามี _ที่อยู่_ และ _เมือง_

ในโมเดลวิเคราะห์ส่วนใหญ่ มักจะมีการเพิ่ม _dimension ของเวลา (Time dimension)_ เพื่อให้สามารถรวมค่าตัวเลขตามช่วงเวลาได้ เช่น การดูยอดขายรายเดือนหรือรายปี

ส่วน _ค่าตัวเลข (numeric measures)_ ที่จะถูกนำมารวมตามมิติต่าง ๆ จะถูกเก็บในตารางที่เรียกว่า _fact table_ โดยแต่ละแถวใน fact table แสดงถึง _เหตุการณ์ที่เกิดขึ้นจริง_ ซึ่งมีค่าตัวเลขผูกกับมัน

ตัวอย่างเช่น ตาราง **Sales** ด้านล่างนี้คือ fact table ที่แทน _รายการขายสินค้าแต่ละชิ้น_ โดยมีข้อมูลเช่น _จำนวนที่ขายไป (quantity)_ และ _รายได้ (revenue)_

![Diagram of a star schema.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-fundamentals-data-visualization/media/star-schema.png)

โครงสร้างแบบนี้ ซึ่งมี _fact table_ เชื่อมโยงกับ _dimension tables_ หนึ่งหรือหลายตาราง จะเรียกว่า _star schema_ (ลองจินตนาการว่ามี 5 มิติ เชื่อมกับ fact table เดียว — โครงสร้างจะดูเหมือนดาว 5 แฉก!)

นอกจากนี้ยังสามารถออกแบบโครงสร้างที่ซับซ้อนขึ้นได้ เช่น _dimension table_ เชื่อมกับ _ตารางอื่นที่เก็บรายละเอียดเพิ่มเติม_ เช่น การแยก attribute ของประเภทสินค้าออกมาในตาราง **Category** ซึ่งเชื่อมกับตาราง **Product** แบบนี้จะเรียกว่า _snowflake schema_

_โครงสร้างของ fact และ dimension tables_ เหล่านี้ถูกนำมาใช้สร้าง _analytical model_ ซึ่งมีการ _คำนวณค่ารวม (aggregations) ล่วงหน้า_ ตามทุกมิติ ช่วยให้การวิเคราะห์และการสร้างรายงาน _มีประสิทธิภาพสูงขึ้นมาก_ เมื่อเทียบกับการคำนวณค่ารวมใหม่ทุกครั้ง

## Attribute hierarchies

#dp-900-key 

สิ่งสุดท้ายที่ควรพิจารณาเกี่ยวกับ _analytical models_ คือการสร้าง _attribute hierarchies_ ซึ่งช่วยให้คุณสามารถ _drill-up_ หรือ _drill-down_ เพื่อดูค่ารวม (_aggregated values_) ในระดับต่าง ๆ ของมิติที่มีโครงสร้างแบบลำดับขั้น (_hierarchical dimension_)

ตัวอย่างเช่น ในตาราง **Product** สามารถสร้าง _hierarchy_ ที่ให้ _แต่ละหมวดหมู่ (category)_ มี _สินค้าหลายรายการ_ อยู่ภายใน ในตาราง **Customer** ก็สามารถสร้าง _hierarchy_ ที่ให้ _แต่ละเมืองมีลูกค้าหลายคน_  และในตาราง **Time** สามารถสร้าง _hierarchy_ ที่ประกอบด้วย _ปี → เดือน → วัน_

โมเดลสามารถถูกสร้างให้มีการ _คำนวณค่ารวมไว้ล่วงหน้า_ สำหรับแต่ละระดับใน hierarchy เหล่านี้ ทำให้คุณสามารถ _เปลี่ยนมุมมองการวิเคราะห์ได้อย่างรวดเร็ว_ เช่น ดูยอดขายรวมรายปี แล้ว _drill down_ เพื่อดูรายละเอียดรายเดือนต่อได้ทันที

![Diagram of a data hierarchy.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-fundamentals-data-visualization/media/hierarchy.png)

## Analytical modeling in Microsoft Power BI

คุณสามารถใช้ **Power BI** เพื่อสร้าง _analytical model_ จากตารางข้อมูลที่นำเข้ามาจากหนึ่งหรือหลายแหล่งข้อมูล จากนั้นสามารถใช้ _data modeling interface_ บนแท็บ **Model** ใน Power BI Desktop เพื่อ:

- สร้าง _ความสัมพันธ์ระหว่าง fact และ dimension tables_
- กำหนด _hierarchies_ ภายในมิติ
- ตั้งค่า _ชนิดข้อมูล (data types)_ และ _รูปแบบการแสดงผล (display formats)_ ของแต่ละฟิลด์ในตาราง
- จัดการ _คุณสมบัติอื่น ๆ_ ที่ช่วยเสริมให้โมเดลมีความสมบูรณ์ในการวิเคราะห์

ทั้งหมดนี้ช่วยให้คุณสร้าง _model ที่มีโครงสร้างชัดเจนและพร้อมใช้งาน_ สำหรับการสำรวจและวิเคราะห์ข้อมูลเชิงลึก

![Screenshot of the Model tab in Power BI Desktop.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-fundamentals-data-visualization/media/power-bi-model.png)