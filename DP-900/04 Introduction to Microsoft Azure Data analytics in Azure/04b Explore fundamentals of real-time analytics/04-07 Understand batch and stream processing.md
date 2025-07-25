
การประมวลผลข้อมูล (Data processing) คือการแปลงข้อมูลดิบให้กลายเป็นข้อมูลที่มีความหมาย โดยผ่านกระบวนการหนึ่ง ซึ่งแบ่งได้เป็น 2 วิธีหลัก ๆ ในการ _ประมวลผลข้อมูล_:

- _Batch processing_: คือการรวบรวม _ข้อมูลหลายรายการ_ ไว้ก่อน แล้วค่อยนำมาประมวลผลพร้อมกันในครั้งเดียว
- _Stream processing_: คือการเฝ้าดู _แหล่งข้อมูล_ อย่างต่อเนื่อง และประมวลผลแบบ _เรียลไทม์_ ทันทีที่มีข้อมูลใหม่เข้ามา

## Understand batch processing

ใน _batch processing_ ข้อมูลใหม่ที่เข้ามาจะถูก _รวบรวมและจัดเก็บไว้ก่อน_ แล้วจึงนำมาประมวลผลทีละกลุ่ม (_batch_) พร้อมกัน โดยเวลาที่จะประมวลผลแต่ละกลุ่มนั้นสามารถกำหนดได้หลายแบบ เช่น ประมวลผลตาม _ช่วงเวลาที่ตั้งไว้ล่วงหน้า_ (เช่น ทุก 1 ชั่วโมง), ประมวลผลเมื่อ _ข้อมูลถึงจำนวนที่กำหนด_, หรือเกิดจาก _เหตุการณ์บางอย่าง_ ที่กระตุ้นให้เริ่มการประมวลผล

ยกตัวอย่างเช่น ถ้าคุณต้องการวิเคราะห์การจราจรด้วยการนับจำนวนรถบนถนน วิธีแบบ _batch processing_ จะหมายถึงการ _รวบรวมรถทั้งหมดไว้ในลานจอด_ ก่อน แล้วจึงนับรถทั้งหมดในครั้งเดียว ขณะที่รถจอดนิ่งอยู่

![Diagram of cars being counted in a parking lot.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-fundamentals-stream-processing/media/batch.png)

หากถนนมีรถจำนวนมากวิ่งผ่านอยู่ตลอดเวลา วิธีแบบ _batch processing_ อาจ _ไม่เหมาะสม_ เพราะต้องรอให้จอดรถจำนวนหนึ่งก่อนจึงค่อยนับ และนั่นหมายความว่า _คุณจะไม่ได้ผลลัพธ์เลย_ จนกว่าจะเก็บรถครบหนึ่งชุดและนับเสร็จ

ตัวอย่างจริงของ _batch processing_ คือระบบเรียกเก็บเงินของบริษัทบัตรเครดิต ลูกค้า _จะไม่ได้รับบิลแยกสำหรับแต่ละรายการ_ ที่ใช้บัตร แต่จะได้รับบิลรวมรายเดือนที่สรุปการใช้จ่ายทั้งหมดในเดือนนั้น

_ข้อดี_ ของ _batch processing_ ได้แก่:
- สามารถประมวลผล _ข้อมูลปริมาณมาก_ ได้ในเวลาที่เหมาะสม
- สามารถตั้งเวลาให้ทำงานช่วงที่ระบบหรือคอมพิวเตอร์ไม่ได้ใช้งาน เช่น _ตอนกลางคืน_ หรือ _นอกเวลาทำการ_

_ข้อเสีย_ ของ _batch processing_ ได้แก่:
- มี _ความล่าช้า_ ระหว่างเวลาที่ข้อมูลถูกป้อนเข้า กับเวลาที่ได้ผลลัพธ์
- ข้อมูลของงานแต่ละชุด (_batch job_) ต้อง _ครบถ้วนและถูกต้อง_ ก่อนจึงจะประมวลผลได้ ซึ่งหากข้อมูลผิดพลาด หรือโปรแกรมล่มระหว่างกระบวนการ จะทำให้ _งานทั้งหมดหยุดชะงัก_ และต้องตรวจสอบข้อมูลใหม่ก่อนเริ่มประมวลผลอีกครั้ง แม้แต่ _ข้อผิดพลาดเล็กน้อย_ ก็อาจทำให้ batch job ทำงานไม่ได้

## Understand stream processing

ใน _stream processing_ ข้อมูลแต่ละชิ้นจะถูก _ประมวลผลทันทีเมื่อมาถึง_ ต่างจาก _batch processing_ ที่ต้องรอให้ครบชุดก่อน จึงจะประมวลผลได้ วิธีนี้ไม่ต้องรอช่วงเวลาใด ๆ แต่จะ _ประมวลผลข้อมูลแบบแยกรายตัว_ และ _แบบเรียลไทม์_

การประมวลผลแบบ _stream_ เหมาะกับสถานการณ์ที่มี _ข้อมูลใหม่เกิดขึ้นอย่างต่อเนื่อง_ และมีความเปลี่ยนแปลงตลอดเวลา

ยกตัวอย่างในกรณีการนับจำนวนรถ วิธีที่ดีกว่าแบบเดิมคือการใช้ _stream processing_ โดย _นับรถแบบเรียลไทม์ขณะรถวิ่งผ่าน_ โดยไม่ต้องจอดรถรวบรวมไว้ก่อน

![Diagram of cars being counted as they pass.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-fundamentals-stream-processing/media/stream.gif)

ด้วยวิธีนี้ คุณ _ไม่จำเป็นต้องรอให้รถทุกคันจอดก่อน_ ถึงจะเริ่มประมวลผล แต่สามารถ _นับรถแบบเรียลไทม์_ และ _สรุปข้อมูลตามช่วงเวลา_ ได้ เช่น นับจำนวนรถที่ผ่านในแต่ละนาที

ตัวอย่าง _streaming data_ ในโลกจริง ได้แก่:

- สถาบันการเงินติดตาม _การเปลี่ยนแปลงของตลาดหุ้นแบบเรียลไทม์_ คำนวณ _value-at-risk_ และปรับสมดุลพอร์ตโดยอัตโนมัติตามราคาหุ้นที่เปลี่ยนแปลง
- บริษัทเกมออนไลน์เก็บข้อมูล _การโต้ตอบของผู้เล่นกับเกมแบบเรียลไทม์_ แล้วนำไปวิเคราะห์เพื่อเสนอ _สิ่งจูงใจ_ และ _ประสบการณ์แบบไดนามิก_ เพื่อดึงดูดผู้เล่น
- เว็บไซต์อสังหาริมทรัพย์ติดตาม _ข้อมูลบางส่วนจากอุปกรณ์มือถือ_ และแนะนำ _อสังหาริมทรัพย์ที่เหมาะสม_ ให้ผู้ใช้แบบเรียลไทม์ตาม _พิกัด GPS_

_stream processing_ เหมาะกับงานที่ต้องการ _การตอบสนองแบบทันที_ เช่น ระบบเฝ้าระวังอาคารที่ตรวจจับ _ควันหรือความร้อน_ หากเกิดเพลิงไหม้ ระบบต้อง _สั่งเตือนภัย_ และ _ปลดล็อกประตู_ ทันที เพื่อให้ผู้อยู่อาศัยสามารถหนีออกมาได้อย่างปลอดภัย

## Understand differences between batch and streaming data

นอกจากความแตกต่างในวิธีจัดการข้อมูลแล้ว _batch processing_ และ _stream processing_ ยังมีความแตกต่างอื่น ๆ ดังนี้:

- _data scope_: _batch processing_ สามารถเข้าถึงและประมวลผล _ข้อมูลทั้งหมด_ ในชุดข้อมูลได้ ส่วน _stream processing_ มักจะเห็นเฉพาะ _ข้อมูลล่าสุด_ ที่เพิ่งได้รับ หรือข้อมูลใน _ช่วงเวลาที่เลื่อนผ่านไป_ เช่น ภายใน 30 วินาทีล่าสุด

- _data size_: _batch processing_ เหมาะกับการจัดการกับ _ชุดข้อมูลขนาดใหญ่_ อย่างมีประสิทธิภาพ ส่วน _stream processing_ มักใช้กับ _ข้อมูลรายตัว_ หรือ _micro batches_ ที่มีข้อมูลเพียงไม่กี่รายการ

- _performance_: ค่าความหน่วง (_latency_) คือเวลาที่ใช้ตั้งแต่รับข้อมูลจนถึงประมวลผลเสร็จ สำหรับ _batch processing_ มักจะมี latency หลายชั่วโมง ขณะที่ _stream processing_ มักจะเกิดขึ้นทันที มี latency ระดับ _วินาที_ หรือ _มิลลิวินาที_

- _analysis_: โดยทั่วไป _batch processing_ จะใช้สำหรับ _การวิเคราะห์ที่ซับซ้อน_ ส่วน _stream processing_ ใช้กับฟังก์ชันตอบสนองง่าย ๆ เช่น _การรวมข้อมูล_ หรือ _การคำนวณค่าเฉลี่ยแบบต่อเนื่อง (rolling average)_


## Combine batch and stream processing

โซลูชันวิเคราะห์ข้อมูลขนาดใหญ่มักจะรวม _batch processing_ และ _stream processing_ เข้าด้วยกัน เพื่อรองรับทั้ง _การวิเคราะห์ข้อมูลย้อนหลัง_ และ _ข้อมูลเรียลไทม์_ ได้พร้อมกัน

เป็นเรื่องปกติที่ _stream processing_ จะใช้เพื่อ _ดึงข้อมูลแบบเรียลไทม์_ แล้วทำการ _กรอง_ หรือ _รวมข้อมูล_ จากนั้นแสดงผลผ่าน _แดชบอร์ด_ หรือ _กราฟแบบเรียลไทม์_ (เช่น แสดงยอดรวมของรถที่วิ่งผ่านในช่วงชั่วโมงปัจจุบัน) ขณะเดียวกันก็ _จัดเก็บผลลัพธ์_ ที่ประมวลผลไว้ใน _data store_ เพื่อใช้ในการ _วิเคราะห์ย้อนหลัง_ ควบคู่กับข้อมูลที่ได้จาก _batch processing_ (เช่น การวิเคราะห์ปริมาณการจราจรย้อนหลัง 1 ปี)

แม้ในกรณีที่ไม่จำเป็นต้องวิเคราะห์หรือแสดงผลแบบเรียลไทม์ _streaming_ ก็ยังมีประโยชน์ในการ _เก็บข้อมูลแบบทันที_ แล้วส่งไปเก็บไว้ใน _data store_ เพื่อใช้ประมวลผลแบบ batch ภายหลัง (เปรียบได้กับการส่งรถทุกคันที่วิ่งผ่านถนนไปเก็บไว้ในลานจอด ก่อนจะนับภายหลัง)

แผนภาพต่อไปนี้แสดงให้เห็นวิธีต่าง ๆ ที่สามารถผสาน _batch_ และ _stream processing_ เข้าด้วยกันในสถาปัตยกรรมการวิเคราะห์ข้อมูลขนาดใหญ่

![Diagram of a data analytics architecture that includes batch and stream processing.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-fundamentals-stream-processing/media/lambda-architecture.png)

1. เหตุการณ์ข้อมูล (_data events_) จาก _แหล่งข้อมูลแบบสตรีม_ จะถูก _จับแบบเรียลไทม์_
2. ข้อมูลจากแหล่งอื่น ๆ จะถูก _นำเข้ามายัง data store_ (มักเป็น _data lake_) เพื่อใช้ใน _batch processing_
3. หากไม่ต้องการวิเคราะห์แบบเรียลไทม์ ข้อมูลจาก _streaming_ ที่จับไว้จะถูก _เขียนลงใน data store_ เพื่อใช้ประมวลผลแบบ batch ในภายหลัง
4. หากต้องการวิเคราะห์แบบเรียลไทม์ จะใช้เทคโนโลยี _stream processing_ เพื่อเตรียมข้อมูลสำหรับการวิเคราะห์หรือแสดงผลทันที เช่น การ _กรอง_ หรือ _รวมข้อมูล_ ตาม _ช่วงเวลา (temporal windows)_
5. ข้อมูลที่ไม่ใช่แบบสตรีมจะถูก _ประมวลผลเป็น batch ตามช่วงเวลา_ และ _จัดเก็บผลลัพธ์_ ไว้ใน _analytical data store_ (มักเรียกว่า _data warehouse_) เพื่อใช้ในการ _วิเคราะห์ย้อนหลัง_
6. ผลลัพธ์จาก _stream processing_ ก็สามารถ _จัดเก็บไว้ใน analytical data store_ เพื่อรองรับการวิเคราะห์ย้อนหลังได้เช่นกัน
7. เครื่องมือด้าน _analytics_ และ _visualization_ จะถูกใช้เพื่อ _แสดงผล_ และ _สำรวจข้อมูลทั้งเรียลไทม์และย้อนหลัง_

_หมายเหตุ_

สถาปัตยกรรมที่นิยมใช้ในการผสาน _batch_ และ _stream processing_ เข้าด้วยกัน ได้แก่ _lambda_ และ _delta architectures_ แม้ว่ารายละเอียดเชิงลึกจะอยู่นอกขอบเขตของคอร์สนี้ แต่ทั้งสองแบบล้วนใช้เทคโนโลยีสำหรับ _ประมวลผลข้อมูล batch ขนาดใหญ่_ และ _stream แบบเรียลไทม์_ เพื่อสร้างโซลูชันวิเคราะห์ข้อมูลแบบครบวงจร (_end-to-end analytical solution_)