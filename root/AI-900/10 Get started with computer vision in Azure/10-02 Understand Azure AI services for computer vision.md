
_Azure AI_ มีบริการคลาวด์หลากหลายสำหรับงาน _AI_ หลายประเภท รวมถึง _computer vision_ บริการที่ชื่อว่า **Azure AI Vision** ของ _Microsoft_ ให้ทั้งโมเดลที่สร้างไว้ล่วงหน้า (_prebuilt_) และโมเดลที่สามารถปรับแต่งได้ (_customizable_)  
โดยใช้ _deep learning_ เป็นพื้นฐาน เพื่อรองรับความสามารถที่หลากหลาย

_Azure AI Vision_ มีฟังก์ชันแบบ "พร้อมใช้งาน" (_off-the-shelf_) สำหรับสถานการณ์ _computer vision_ ที่พบได้ทั่วไป  
และยังเปิดโอกาสให้สร้างโมเดลที่ปรับให้เหมาะกับภาพของคุณเองได้อีกด้วย

บริการ _Azure AI Vision_ ประกอบด้วยผลิตภัณฑ์ย่อยหลายตัว ซึ่งแต่ละตัวออกแบบมาสำหรับจัดการกับชุดงานเฉพาะ ได้แก่:

- **Azure AI Vision Image Analysis service**: ตรวจจับวัตถุทั่วไปในภาพ (_detects common objects_), ใส่แท็กให้กับคุณลักษณะของภาพ (_tags visual features_), สร้างคำบรรยาย (_generates captions_) และรองรับการแยกข้อความจากภาพ (_optical character recognition: OCR_) ![Screenshot of image captioning example from Azure AI Foundry.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-computer-vision-azure/media/image-captioning-example.png)
    
- **Azure AI Face service**: ตรวจจับ รู้จำ และวิเคราะห์ใบหน้าของมนุษย์ในภาพ (_detects, recognizes, and analyzes human faces_) โดยมีโมเดลเฉพาะสำหรับการวิเคราะห์ใบหน้า (_facial analysis_) ซึ่งครอบคลุมมากกว่าความสามารถที่มีใน _image analysis_ ทั่วไป ![Screenshot of face detection example from Azure AI Foundry.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-computer-vision-azure/media/face-detection-example.png)
ความสามารถด้าน _image analysis_ และ _face detection_, _analysis_, และ _recognition_ ของ _Azure AI Vision_  
สามารถนำไปประยุกต์ใช้งานได้หลากหลาย ตัวอย่างเช่น:

- _search engine optimization_ – ใช้ _image tagging_ และ _captioning_ เพื่อปรับปรุงอันดับการค้นหา  
- _content moderation_ – ใช้ _image detection_ ช่วยตรวจสอบความปลอดภัยของภาพที่เผยแพร่ออนไลน์  
- _security_ – ใช้ _facial recognition_ ในระบบรักษาความปลอดภัยอาคาร หรือปลดล็อกอุปกรณ์ในระบบปฏิบัติการ  
- _social media_ – ใช้ _facial recognition_ เพื่อติดแท็กเพื่อนอัตโนมัติในภาพถ่าย  
- _missing persons_ – ใช้กล้องวงจรปิดร่วมกับ _facial recognition_ เพื่อช่วยระบุบุคคลสูญหาย  
- _identity validation_ – ใช้ตรวจสอบตัวตนที่ตู้ตรวจคนเข้าเมือง เมื่อมีใบอนุญาตพิเศษ  
- _museum archive management_ – ใช้ _optical character recognition_ เพื่อเก็บข้อมูลจากเอกสารกระดาษ

> **หมายเหตุ**  
> โซลูชัน _vision_ สมัยใหม่หลายตัวมักสร้างขึ้นโดยใช้ความสามารถหลายอย่างร่วมกัน  ตัวอย่างเช่น ความสามารถในการวิเคราะห์วิดีโอ (_video analysis_) นั้นรองรับโดยบริการ _Azure AI Video Indexer_

> _Azure AI Video Indexer_ สร้างขึ้นจากการรวมบริการ _Azure AI_ หลายตัว  
> เช่น _Face_, _Translator_, _Image Analysis_, และ _Speech_

