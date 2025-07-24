
คุณสามารถใช้ _Azure AI Translator_ กับภาษาโปรแกรมที่คุณเลือกเอง หรือผ่าน _REST API_ และยังสามารถใช้ฟีเจอร์บางอย่างผ่าน _Language Studio_ ได้

สำหรับ _Azure AI Speech_ ก็สามารถเริ่มใช้งานได้ผ่าน _Speech Studio_ หรือใช้กับภาษาโปรแกรมที่คุณเลือก หรือ _REST API_ เช่นกัน

## Azure resources for Azure AI Translator and Azure AI Speech

ก่อนใช้งาน _Azure AI Translator_ หรือ _Azure AI Speech_ คุณต้องสร้างทรัพยากรในบัญชี Azure ของคุณก่อน โดยมีทางเลือกดังนี้:

- สร้างทรัพยากรแบบแยกกัน (_Translator_ และ _Speech_) เพื่อให้สามารถจัดการการเข้าถึงและการคิดค่าบริการแยกจากกัน
- หรือ สร้างทรัพยากรแบบรวมเป็น _Azure AI services_ เพื่อใช้บริการทั้งสองผ่าน _resource เดียว_ รวมการคิดค่าบริการ และใช้งานผ่าน _endpoint_ และ _authentication key_ เดียวกัน

## Using Azure AI Translator

- _Text translation_: แปลข้อความแบบ _real-time_ ได้อย่างแม่นยำ รองรับทุกภาษา
- _Document translation_: แปลเอกสารจำนวนมาก โดยคงรูปแบบเอกสารต้นฉบับไว้
- _Custom translation_: ให้บริษัท นักพัฒนาแอป และผู้ให้บริการแปลภาษา สร้างระบบ _NMT แบบปรับแต่งเอง_

API ของ Azure AI Translator ยังมีตัวเลือกปรับแต่งผลลัพธ์ เช่น:

- _Profanity filtering_: หากไม่ตั้งค่า ระบบจะไม่กรองคำหยาบโดยอัตโนมัติ คุณสามารถเลือกให้แสดง, แทนที่ หรือไม่รวมคำหยาบไว้ก็ได้ โดยขึ้นอยู่กับ _วัฒนธรรมของภาษา_
- _Selective translation_: สามารถแท็กข้อความบางส่วนเพื่อไม่ให้แปล เช่น โค้ด ชื่อแบรนด์ หรือคำเฉพาะที่ไม่ควรแปล

Azure AI Translator ยังสามารถใช้ร่วมกับ _Azure AI Foundry_ ซึ่งเป็นแพลตฟอร์มรวมสำหรับการจัดการ AI ในองค์กร และยังมีให้ใช้ผ่าน _Microsoft Translator Pro_ ซึ่งเป็นแอปมือถือสำหรับองค์กร รองรับการแปลเสียงแบบ _real-time speech-to-speech_

## Speech translation with Azure AI Speech

- _Speech to text_: แปลงเสียงเป็นข้อความ
- _Text to speech_: แปลงข้อความเป็นเสียง
- _Speech translation_: แปลเสียงจากภาษาหนึ่งเป็นข้อความหรือเสียงในอีกภาษา
