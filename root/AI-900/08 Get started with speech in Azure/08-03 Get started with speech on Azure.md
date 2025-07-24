
_Microsoft Azure_ ให้บริการ _speech recognition_ และ _speech synthesis_ ผ่าน _Azure AI Speech service_ ซึ่งรองรับความสามารถหลายอย่าง ได้แก่

- _Speech to text_  
- _Text to speech_  

> **หมายเหตุ**: โมดูลนี้จะอธิบายเฉพาะ _speech to text_ และ _text to speech_ ส่วน _speech translation_ จะอยู่ในโมดูลแยกต่างหาก

## Speech to text

คุณสามารถใช้ _Azure AI Speech to text API_ เพื่อถอดเสียงจากไฟล์เสียงหรือเสียงสดให้เป็นข้อความแบบเรียลไทม์ (_real-time_) หรือแบบแบตช์ (_batch_)

โมเดลที่ใช้ใน _Speech to text API_ คือ _Universal Language Model_ ซึ่งได้รับการฝึกโดย _Microsoft_ บนข้อมูลที่ _Microsoft_ เป็นเจ้าของและโฮสต์อยู่บน _Azure_ โมเดลนี้ถูกปรับให้เหมาะกับ 2 สถานการณ์หลักคือ 
1. _Conversational_ 
2. _Dictation_ 

และคุณยังสามารถสร้างโมเดลเฉพาะของคุณเองได้ เช่น โมเดลเสียง (_acoustics_), ภาษา (_language_) และการออกเสียง (_pronunciation_) หากโมเดลที่มีอยู่ยังไม่ตรงกับความต้องการ

_**Real-time transcription**_: การถอดเสียงแบบเรียลไทม์ช่วยให้คุณแปลงเสียงพูดสดให้เป็นข้อความได้ทันที เหมาะสำหรับงานพรีเซนต์ เดโม หรือสถานการณ์ที่มีผู้พูดอยู่ต่อหน้า  
แอปพลิเคชันของคุณจะต้องรับเสียงเข้าจากไมโครโฟนหรือแหล่งเสียงอื่น เช่น ไฟล์เสียง แล้วสตรีมเสียงไปยังบริการ ซึ่งจะส่งข้อความถอดเสียงกลับมาให้ทันที

_**Batch transcription**_: ถ้าคุณมีไฟล์เสียงที่บันทึกไว้ล่วงหน้า (เช่น บนไฟล์แชร์ เซิร์ฟเวอร์ระยะไกล หรือ _Azure Storage_) คุณสามารถใช้ _SAS URI_ ชี้ไปที่ไฟล์ และรอผลการถอดเสียงแบบ _asynchronous_

การถอดเสียงแบบแบตช์จะถูกจัดคิวและดำเนินการตามลำดับความพร้อม ซึ่งโดยปกติงานจะเริ่มภายในไม่กี่นาทีหลังจากส่งคำขอ แต่ไม่มีเวลาที่แน่นอนว่าเมื่อใดจะเริ่มทำงานจริง

## Text to speech

_API_ นี้ช่วยให้คุณแปลงข้อความให้เป็นเสียงพูด ซึ่งสามารถเล่นผ่านลำโพงหรือบันทึกเป็นไฟล์เสียงก็ได้

_**Speech synthesis voices**_: คุณสามารถเลือกเสียงที่จะใช้พูดได้ตามต้องการ ซึ่งช่วยให้คุณปรับแต่งเสียงให้มีบุคลิกเฉพาะตัว บริการมีเสียงสำเร็จรูปหลายแบบที่รองรับหลายภาษาและสำเนียงภูมิภาค รวมถึง _neural voices_ ที่ใช้ _neural networks_ แก้ปัญหาเรื่องเสียงที่ไม่เป็นธรรมชาติ โดยให้เสียงที่ลื่นไหลและสมจริงยิ่งขึ้น

คุณยังสามารถพัฒนาเสียงแบบกำหนดเอง (_custom voices_) แล้วนำมาใช้กับ _text to speech API_ ได้อีกด้วย

## Supported Languages

ทั้ง _speech to text_ และ _text to speech_ รองรับหลายภาษา สามารถดูรายละเอียดภาษาที่รองรับได้จากลิงก์ที่ระบุไว้ในหน้าเอกสารของ Azure
- [Speech to text languages](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/language-support?tabs=stt#speech-to-text?azure-portal=true).
- [Text to speech languages](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/language-support?tabs=tts#text-to-speech?azure-portal=true).