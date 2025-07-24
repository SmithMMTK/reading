
_Azure AI Content Understanding_ ใช้ _โมเดล AI ขั้นสูง_ เพื่อวิเคราะห์เนื้อหาหลายรูปแบบ ได้แก่:

- _เอกสาร_ และ _ฟอร์มที่เป็นข้อความ_
- _เสียง (audio)_
- _ภาพ (images)_
- _วิดีโอ (video)_


## Analyzing forms and documents

ความสามารถในการวิเคราะห์เอกสารของ _Azure AI Content Understanding_ ไม่ได้หยุดแค่การดึงข้อความด้วย _OCR_ แต่ยังสามารถ _ดึงข้อมูลตามโครงสร้าง (schema-based extraction)_ โดยระบุ _field_ และ _value_ ได้อย่างแม่นยำ

ตัวอย่างเช่น หากคุณกำหนด _schema_ ที่มีฟิลด์ทั่วไปที่มักพบใน _ใบแจ้งหนี้ (invoice)_ เช่น:
- Vendor name
- Invoice number
- Invoice date
- Customer name
- Custom address
- Items - the items ordered, each of which includes:
    - Item description
    - Unit price
    - Quantity ordered
    - Line item total
- Invoice subtotal
- Tax
- Shipping Charge
- Invoice total

คราวนี้สมมติว่าคุณต้องการ _ดึงข้อมูล_ ตาม schema ที่กำหนดจาก _ใบแจ้งหนี้ (invoice)_ ด้านล่างนี้

![Photograph of an invoice.](https://learn.microsoft.com/en-us/training/wwl-data-ai/ai-information-extraction/media/invoice.png)

_Azure AI Content Understanding_ สามารถใช้ _schema ของใบแจ้งหนี้_ ที่คุณกำหนด แล้วนำไปจับคู่กับข้อมูลในเอกสารจริงได้อย่างชาญฉลาด แม้ว่า:
- ชื่อฟิลด์จะไม่ตรงกับที่กำหนดไว้
- หรือบางฟิลด์อาจ ไม่มีฉลากกำกับ (unlabeled)

![Photograph of an analyzed invoice with detected fields highlighted.](https://learn.microsoft.com/en-us/training/wwl-data-ai/ai-information-extraction/media/analyzed-invoice.png)

สำหรับแต่ละ _field_ ที่ตรวจพบ ระบบจะทำการ _ดึงค่า (value)_ จากใบแจ้งหนี้โดยอัตโนมัติ

- **Vendor name**: Adventure Works Cycles
- **Invoice number**: 1234
- **Invoice date**: 03/07/2025
- **Customer name**: John Smith
- **Custom address**: 123 River Street, Marshtown, England, GL1 234
- **Items**:
    - Item 1:
        - **Item description**: 38" Racing Bike (Red)
        - **Unit price**: 1299.00
        - **Quantity ordered**: 1
        - **Line item total**: 1299.00
    - Item 2:
        - **Item description**: Cycling helmet (Black)
        - **Unit price**: 25.99
        - **Quantity ordered**: 1
        - **Line item total**: 25.99
    - Item 3:
        - **Item description**: Cycling shirt (L)
        - **Unit price**: 42.50
        - **Quantity ordered**: 2
        - **Line item total**: 85.00
- **Invoice subtotal**: 1409.99
- **Tax**: 140.99
- **Shipping Charge**: 35.00
- **Invoice total**: 1585.98

## Analyzing audio

นอกจากจะวิเคราะห์เอกสารที่เป็นข้อความได้แล้ว _Azure AI Content Understanding_ ยังสามารถวิเคราะห์ _ไฟล์เสียง_ เพื่อให้ผลลัพธ์เป็น _การถอดความ (transcription)_, _บทสรุป_, และ _ข้อมูลสำคัญอื่น ๆ_

สมมติว่าคุณต้องการให้ AI สรุปข้อความเสียงจาก _voice mail_ โดยคุณกำหนด _schema_ สำหรับสิ่งที่ต้องดึงจากแต่ละข้อความเสียงไว้ดังนี้:

- _Caller_: ใครเป็นคนโทรมา
- _Message summary_: สาระสำคัญของข้อความ
- _Requested actions_: สิ่งที่ผู้โทรต้องการให้คุณทำ
- _Callback number_: หมายเลขที่ให้ติดต่อกลับ
- _Alternative contact details_: ช่องทางการติดต่ออื่น (ถ้ามี)

ตอนนี้ลองสมมติว่า _มีผู้โทรฝากข้อความเสียงไว้_ ดังนี้:


```text
Hi, this is Ava from Contoso.

Just calling to follow up on our meeting last week.

I wanted to let you know that I've run the numbers and I think we can meet your price expectations.

Please call me back on 555-12345 or send me an e-mail at Ava@contoso.com and we'll discuss next steps.

Thanks, bye!
```

เมื่อใช้ _Azure AI Content Understanding_ วิเคราะห์ข้อความเสียงและใช้ schema ที่กำหนดไว้ ระบบจะสามารถ _ดึงข้อมูล_ ออกมาได้ดังนี้:

- **_Caller_**: Ava จาก Contoso  
- **_Message summary_**: Ava จาก Contoso โทรมาเพื่อติดตามผลการประชุม และแจ้งว่าสามารถตอบโจทย์ด้านราคาที่คาดหวังได้ พร้อมขอให้ติดต่อกลับทางโทรศัพท์หรืออีเมลเพื่อพูดคุยขั้นตอนถัดไป  
- **_Requested actions_**: โทรกลับหรือส่งอีเมลเพื่อหารือขั้นตอนถัดไป  
- **_Callback number_**: 555-12345  
- **_Alternative contact details_**: Ava@contoso.com  

ผลลัพธ์นี้สามารถนำไปใช้ใน _ระบบ CRM_, _อัตโนมัติการติดตามลูกค้า_, หรือ _จัดการการติดต่อธุรกิจ_ ได้อย่างมีประสิทธิภาพ

## Analyzing images and video

_Azure AI Content Understanding_ ยังรองรับการวิเคราะห์ _ภาพ_ และ _วิดีโอ_ เพื่อดึงข้อมูลตาม _schema ที่กำหนดเอง_

ตัวอย่างเช่น คุณอาจต้องการวิเคราะห์ _ภาพจากการประชุมทางวิดีโอ_ เพื่อดึงข้อมูลเกี่ยวกับ _สถานที่_, _ผู้เข้าร่วมในห้อง_, _ผู้เข้าร่วมทางไกล_, และ _จำนวนผู้เข้าร่วมทั้งหมด_

สมมติว่าคุณกำหนด schema สำหรับภาพจากระบบประชุมที่รวมทั้งผู้เข้าร่วมในห้องและทางไกลไว้ดังนี้:

- _Location_: สถานที่ของห้องประชุม
- _In-person attendees_: รายชื่อหรือจำนวนผู้ที่อยู่ในห้อง
- _Remote attendees_: รายชื่อหรือจำนวนผู้ที่เข้าร่วมจากระยะไกล
- _Total attendees_: จำนวนรวมของผู้เข้าร่วมทั้งหมด

จากนั้นคุณสามารถใช้ _Azure AI Content Understanding_ เพื่อวิเคราะห์ _ภาพนิ่งที่ถ่ายจากกล้องห้องประชุม_ เพื่อดึงข้อมูลตาม schema นี้โดยอัตโนมัติ

![Photograph of a person in a conference room on a call with three remote attendees.](https://learn.microsoft.com/en-us/training/wwl-data-ai/ai-information-extraction/media/conference-call.jpg)

เมื่อใช้ schema ข้างต้นกับภาพประชุม ระบบ _Azure AI Content Understanding_ จะให้ผลลัพธ์ดังนี้:
- **_Location_**: ห้องประชุม  
- **_In-person attendees_**: 1  
- **_Remote attendees_**: 3  
- **_Total attendees_**: 4  

การวิเคราะห์แบบนี้ช่วยให้สามารถ _ติดตามผลการประชุม_, _สรุปประเด็นสำคัญ_, และ _วางแผนงานต่อไปได้อย่างมีประสิทธิภาพ_