

การใช้งาน _Azure AI Translator_ ต้องเข้าถึงผ่าน **REST API** และต้องมี **Azure Cognitive Services subscription** พร้อมกับ **Translation service subscription**

การสมัครใช้งานมีทั้งแบบ **ฟรี (free tier)** และ **แบบชำระเงิน (standard pricing tier)** ซึ่งหลังจากสมัครแล้วคุณจะได้รับ _endpoint_ และ _subscription key_ สำหรับใช้เรียกบริการ

## Translating text

บริการแปลข้อความของ _Translator_ ใช้ _Web API_ แบบ _JSON_ โดยส่งข้อความในรูปแบบ _string_ นักพัฒนาสามารถระบุให้แปลเป็น _หลายภาษาพร้อมกัน_ ได้ เนื้อหาที่ส่งในคำขอ (_request body_) จะอยู่ในรูปแบบ _array_ ซึ่งแต่ละรายการเป็น _JSON object_ ที่มีข้อความที่ต้องการแปล ตัวอย่างเช่น:


```json
[
    {"Text":"I would really like to go to the theatre."},
    {"Text":"Let's go out for lunch!"}
]
```

ภาษาปลายทางที่ต้องการให้แปลข้อความไป จะต้องระบุไว้ใน _URL_ ของคำขอ ตัวอย่างเช่น URL ด้านล่างนี้ใช้สำหรับส่งคำขอแบบ _POST_ เพื่อแปลข้อความเป็น _ภาษาเยอรมัน_:


```http
https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&to=de
```

## Translating documents

**Document Translation API** ช่วยให้สามารถ _แปลเอกสารจำนวนมาก_ ได้พร้อมกัน โดยยังคง _โครงสร้างเอกสาร_ และ _รูปแบบข้อมูล_ เดิมไว้ทั้งหมด การแปลนี้ไม่เกิดขึ้นแบบ _เรียลไทม์_ แต่จะเป็นการส่งคำขอที่ระบุ _ตำแหน่งของไฟล์ต้นทางและปลายทาง_ รวมถึง _รายการภาษาที่ต้องการให้แปล_ กระบวนการแปลแบบแบตช์นี้ทำผ่าน _Azure Blob Storage containers_ โดยมีการจัดเก็บไฟล์ต้นฉบับ, ไฟล์ปลายทาง, และไฟล์ glossary แยกไว้ในแต่ละ container

ตัวอย่างคำขอด้านล่างนี้คือการแปลเอกสารทั้งหมดใน container ชื่อ `source-en-location` เป็น _ภาษาฝรั่งเศส_:

```json
{
    "inputs": [
        {
            "source": {
                "sourceUrl": https://my.blob.core.windows.net/source-en-location
            },
            "targets": [
                {
                    "targetUrl": https://my.blob.core.windows.net/target-fr-location,
                    "language": "fr"
                }
            ]
        }
    ]
}
```

## Custom Translator

ผ่าน _Custom Translator Portal_ คุณสามารถใช้เอกสารที่เคยแปลไว้ก่อนแล้วเพื่อ _สร้างระบบแปลภาษาที่ปรับแต่งเอง_ (_customized translation system_) เอกสารที่นำมาใช้งานสามารถอยู่ในหลายรูปแบบ เช่น _PDF_, _TXT_, _DOCX_, _XLSX_, และ _HTML_ ในการใช้งานผ่านพอร์ทัลนี้ คุณต้องอัปโหลดเอกสาร 2 ชุด:

- ชุดแรกเป็นเอกสารใน _ภาษาต้นทาง_
- อีกชุดเป็นเอกสารใน _ภาษาปลายทาง_ ที่แปลไว้แล้ว

จากนั้นระบบจะนำข้อมูลจากทั้งสองชุดมาใช้ในการฝึกโมเดลแปลที่เหมาะสมกับบริบทของคุณโดยเฉพาะ

![Custom Translator portal upload documents.](https://learn.microsoft.com/en-us/training/modules/intro-to-translator/media/3-how-to-upload.png)

เมื่อคุณอัปโหลดเอกสารเรียบร้อยแล้ว ก็สามารถสร้าง _custom translation model_ ได้ทันที

โมเดลนี้จะเรียนรู้จากคู่เอกสาร _ต้นฉบับ_ และ _คำแปล_ เพื่อให้สามารถแปลข้อความใหม่ได้อย่าง _แม่นยำ_ และ _สอดคล้องกับบริบทเฉพาะของคุณ_ มากยิ่งขึ้น

![Custom Translator portal train model.](https://learn.microsoft.com/en-us/training/modules/intro-to-translator/media/3-how-to-train.png)

เมื่อ _โมเดลถูกฝึกเสร็จแล้ว_ คุณสามารถดู _ผลการทดสอบ_ ของโมเดลได้ หากต้องการผลลัพธ์ที่ _แม่นยำยิ่งขึ้น_ คุณสามารถอัปโหลดเอกสารเพิ่มเติมและ _ฝึกโมเดลซ้ำ_ ได้ แอปพลิเคชันที่ใช้ _Translator Text API V3_ สามารถเรียกใช้งาน _custom translation model_ เหล่านี้ได้โดยตรง

## More functionalities

**Dictionary look-up** ช่วยให้สามารถดู _คำแปลทางเลือก_ สำหรับคำหรือสำนวนต่าง ๆ ได้ คำขอแบบนี้จะแสดงรายการคำแปลหลายแบบของคำหรือวลีเดิม เพื่อให้เข้าใจความหมายใน _บริบท_ ได้ชัดเจนยิ่งขึ้น คำแปลต้นฉบับหรือทางเลือกเหล่านี้สามารถใช้กับฟีเจอร์ _Dictionary example_ เพื่อแสดง _ประโยคตัวอย่าง_ ที่ใช้คำแปลคู่นั้นในทั้งสองภาษา ช่วยให้ผู้ใช้เข้าใจได้ว่า _คำแปลไหนเหมาะสมที่สุด_

**Dynamic Dictionary** เหมาะสำหรับกรณีที่คุณทราบคำแปลที่ต้องการใช้แล้ว เช่น การแปลชื่อเฉพาะ หรือชื่อผลิตภัณฑ์ _Dynamic Dictionary_ ช่วยให้สามารถระบุคำแปลเฉพาะสำหรับคำหรือวลีที่ต้องการได้โดยตรง

**Profanity filters** มีให้เลือกใช้เมื่อขอแปลข้อความ โดยค่าเริ่มต้น Translator จะคง _คำหยาบ_ ไว้ในการแปล เนื่องจากสิ่งที่ถือว่าเป็นคำหยาบนั้น _แตกต่างกันในแต่ละวัฒนธรรม_ หากคุณต้องการลบหรือ _แท็กคำหยาบ_ ในข้อความแปล คุณสามารถใช้ตัวเลือก _profanity filtering_ เพื่อปรับพฤติกรรมนี้ได้

