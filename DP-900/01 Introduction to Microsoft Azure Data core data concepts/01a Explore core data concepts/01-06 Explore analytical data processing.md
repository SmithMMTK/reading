
การประมวลผลข้อมูลเชิงวิเคราะห์ (_analytical data processing_) มักใช้ระบบที่เน้นการอ่านข้อมูล (_read-only_ หรือ _read-mostly_) โดยเก็บ _ข้อมูลจำนวนมาก_ ที่เป็นข้อมูลย้อนหลัง หรือ _business metrics_ ที่ใช้สำหรับการวิเคราะห์

การวิเคราะห์สามารถอ้างอิงจาก _snapshot_ ของข้อมูลในช่วงเวลาหนึ่ง หรือชุดของ _snapshot_ หลายช่วงเวลาก็ได้

แม้รายละเอียดของระบบประมวลผลเชิงวิเคราะห์จะแตกต่างกันไปในแต่ละโซลูชัน แต่รูปแบบสถาปัตยกรรมที่พบบ่อยสำหรับระบบวิเคราะห์ในระดับองค์กรมักมีหน้าตาดังนี้:

![Diagram showing an analytical database architecture with the numbered elements described below.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-core-data-concepts/media/analytical-processing.png)

1. ข้อมูลจากระบบปฏิบัติการ (_operational data_) จะถูกดึงมาแปลงรูปแบบ และโหลดเข้าสู่ _data lake_ ในกระบวนการที่เรียกว่า _ETL (Extract, Transform, Load)_ เพื่อเตรียมสำหรับการวิเคราะห์  
2. ข้อมูลจะถูกโหลดเข้าสู่โครงสร้างแบบตาราง (_schema of tables_) ซึ่งอาจอยู่ในระบบ _data lakehouse_ ที่ใช้ _Spark_ ทำหน้าที่เป็นเลเยอร์ตารางเหนือไฟล์ใน _data lake_ หรืออยู่ใน _data warehouse_ ซึ่งเป็นฐานข้อมูลแบบ relational ที่รองรับ _SQL_ เต็มรูปแบบ  
3. ข้อมูลจาก _data warehouse_ อาจถูกประมวลผลเพิ่มเติมและโหลดเข้าสู่โมเดล _OLAP (Online Analytical Processing)_ หรือที่เรียกว่า _cube_ โดยจะคำนวณค่าต่าง ๆ (_measures_) จาก _fact table_ สำหรับแต่ละจุดตัดของ _dimensions_ ที่มาจาก _dimension table_ เช่น ยอดขายรวมแยกตามวัน ลูกค้า และสินค้า  
4. ข้อมูลใน _data lake_, _data warehouse_ และ _analytical model_ สามารถถูกสืบค้นเพื่อสร้าง _report_, _visualization_ และ _dashboard_

_data lake_ เหมาะกับกรณีที่มี _ข้อมูลจำนวนมาก_ ในรูปแบบไฟล์ และต้องเก็บไว้เพื่อการวิเคราะห์ในระยะยาว

_data warehouse_ เป็นรูปแบบที่ใช้กันมานานในการจัดเก็บข้อมูลในรูปแบบตารางสัมพันธ์ (_relational schema_) โดยออกแบบมาให้เหมาะกับการสืบค้น (_read-optimized_) เพื่อรองรับ _reporting_ และ _data visualization_

_data lakehouse_ เป็นนวัตกรรมใหม่ที่รวมข้อดีของ _data lake_ (ความยืดหยุ่นและขนาดที่ขยายได้ง่าย) เข้ากับความสามารถในการสืบค้นแบบตารางของ _data warehouse_ ซึ่งบางครั้งอาจต้อง _denormalize_ ข้อมูลจากแหล่ง _OLTP_ เพื่อให้การสืบค้นทำงานได้รวดเร็วขึ้น

_OLAP model_ เป็นรูปแบบการจัดเก็บข้อมูลแบบรวม (_aggregated_) ที่เหมาะกับการประมวลผลเชิงวิเคราะห์ โดยจะรวมข้อมูลตาม _dimension_ หลายระดับ ทำให้สามารถ _drill up/down_ เพื่อดูยอดรวมตามลำดับชั้น เช่น ยอดขายรวมตามภูมิภาค เมือง หรือที่อยู่เฉพาะเจาะจง การที่ข้อมูลถูก _pre-aggregated_ ทำให้การสืบค้นทำได้เร็วมาก

ผู้ใช้งานแต่ละประเภทจะทำงานกับระบบวิเคราะห์ในระดับต่าง ๆ เช่น

- _Data scientists_ มักจะทำงานกับไฟล์โดยตรงใน _data lake_ เพื่อสำรวจและสร้างแบบจำลองข้อมูล  
- _Data analysts_ มักจะสืบค้นตารางใน _data warehouse_ เพื่อสร้างรายงานและภาพข้อมูลที่ซับซ้อน  
- _Business users_ จะใช้งานข้อมูลที่ถูก _pre-aggregated_ แล้วผ่าน _analytical model_ ในรูปแบบของ _report_ หรือ _dashboard_
