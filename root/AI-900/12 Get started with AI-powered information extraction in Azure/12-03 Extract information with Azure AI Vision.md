
บริการ _Azure AI Vision Image Analysis_ เหมาะอย่างยิ่งเมื่อคุณต้องการ _ดึงข้อมูลเชิงลึกจากภาพถ่าย_ หรือ _เอกสารขนาดเล็กที่สแกนไว้_ เช่น _นามบัตร_ หรือ _เมนูอาหาร_

## _การสร้างคำบรรยายและแท็กอัตโนมัติ (Automated caption and tag generation)_

คุณสามารถใช้บริการนี้เพื่อสร้าง _ข้อความบรรยายภาพ_ โดยระบบจะวิเคราะห์ภาพและสร้าง:

- **_caption_**: ข้อความบรรยายภาพโดยรวม
- **_dense captions_**: คำอธิบายสำหรับวัตถุสำคัญแต่ละชิ้นในภาพ
- **_tags_**: คำหลักที่ใช้จัดหมวดหมู่ภาพ

ตัวอย่างเช่น หากคุณต้องการดึงข้อมูลสำคัญจากภาพภาพหนึ่ง ระบบสามารถช่วยสรุปเนื้อหาของภาพนั้นให้ได้ทันที

![Photograph of a man walking a dog in a busy street.](https://learn.microsoft.com/en-us/training/wwl-data-ai/ai-information-extraction/media/street.png)

บริการ _AI Vision Image Analysis_ จะสร้าง _ข้อความอธิบาย_ ภาพในรูปแบบต่าง ๆ ดังนี้:

- **Caption**: A man walking a dog on a leash
- **Dense captions**:
    - A man walking a dog on a leash
    - A man walking on the street
    - A yellow car on the street
    - A yellow car on the street
    - A green telephone booth with a green sign
- **Tags**:
    - outdoor
    - land vehicle
    - vehicle
    - building
    - road
    - street
    - wheel
    - taxi
    - person
    - clothing
    - car
    - dog
    - yellow
    - walking
    - city

## Object detection

Azure AI Vision Image Analysis can also detect common objects and people in an image.

For example, consider the following image:

![Photograph of an apple, a banana, and an orange.](https://learn.microsoft.com/en-us/training/wwl-data-ai/ai-information-extraction/media/produce.png)

Azure AI Vision Image Analysis detects the types and locations of objects in this image, as shown here:

![Photograph of fruit with the the locations of an apple, a banana, and an orange highlighted.](https://learn.microsoft.com/en-us/training/wwl-data-ai/ai-information-extraction/media/object-detection.png)

## Optical character recognition (OCR)

เมื่อภาพมี _ข้อความที่พิมพ์_ หรือ _ข้อความลายมือ_ อยู่ ระบบ _Azure AI Vision Image Analysis_ สามารถใช้เทคนิคที่เรียกว่า _optical character recognition (OCR)_ เพื่อระบุตำแหน่งและเนื้อหาของแต่ละ _บรรทัด (line)_ และ _แต่ละคำ (word)_

ความสามารถของ _OCR_ เหล่านี้มีประโยชน์มากเมื่อคุณต้องการ _อ่านข้อความในภาพเพื่อนำไปประมวลผลต่อ_ เช่น:

- _แปลเมนูอาหาร_ ด้วยแอปมือถือ
- _ดึงข้อมูลติดต่อ_ จากนามบัตรที่ถ่ายภาพไว้

_Azure AI Vision Image Analysis_ เหมาะกับการ _ดึงข้อความอิสระปริมาณไม่มาก_ จากเอกสารง่าย ๆ ได้อย่างรวดเร็วและแม่นยำ

Consider the following scanned business card:

![Photograph of a business card.](https://learn.microsoft.com/en-us/training/wwl-data-ai/ai-information-extraction/media/business-card.png)

You could use Azure AI Vision Image Analysis to locate and extract the text from this card, with the following results:

![Photograph of a business card with text highlighted.](https://learn.microsoft.com/en-us/training/wwl-data-ai/ai-information-extraction/media/extracted-text.png)


```text
Adventure Works Cycles
Roberto Tamburello
Engineering Manager
roberto@adventure-works.com
555-123-4567
```

