
เทคนิคการ _ดึงข้อมูลด้วย AI_ สามารถนำมาผสมผสานกันเพื่อดึงข้อมูลจาก _หลายรูปแบบเนื้อหา (multiple modalities)_ เช่น เอกสาร วิดีโอ และเสียง การใช้ _multimodal data extraction_ ช่วยให้สามารถจัดการ _ทรัพย์สินดิจิทัล_, _ทำงานอัตโนมัติ_, และ _สร้างข้อมูลเชิงลึกเพิ่มเติม_ ได้

การประสานการทำงาน (_orchestration_) ของเทคนิคเหล่านี้อาจรวมถึง _computer vision_, _document intelligence_, และเทคนิคอื่น ๆ เช่น

- _Natural language processing (NLP)_ ใช้ในการวิเคราะห์ภาษาที่เขียนหรือพูด เช่น _ค้นหาวลีสำคัญ_, _ระบุหน่วยข้อมูลสำคัญ (entities)_, _วิเคราะห์อารมณ์ (sentiment)_ และอื่น ๆ

	 _หมายเหตุ_ 
		แนวคิดด้าน _machine learning_ ที่เกี่ยวข้องกับ _NLP_ มีอธิบายอย่างละเอียดในหัวข้อ [Introduction to natural language processing concepts](https://learn.microsoft.com/en-us/training/modules/analyze-text-with-text-analytics-service)

- _Speech recognition_ คือการแปลงคำพูดให้อยู่ในรูปแบบข้อมูลที่สามารถประมวลผลได้ โดยมักจะถูกแปลงเป็นข้อความ (_transcription_) ซึ่งสามารถมาจาก _ไฟล์เสียง_ หรือ _เสียงสดจากไมโครโฟน_

	_หมายเหตุ_
		การรู้จำเสียงมีอธิบายเพิ่มเติมใน [Get started with speech on Azure](https://learn.microsoft.com/en-us/training/modules/recognize-synthesize-speech)

- _Generative AI_ ช่วยเสริมกระบวนการดึงข้อมูล โดยเปิดโอกาสให้ผู้ใช้งานสามารถ _กำหนด field และ field description_ ได้เอง ซึ่งมีประโยชน์มากกับข้อมูลแบบ _unstructured_ เช่น ถ้าผู้ใช้เพิ่ม field ว่า "summary" ระบบจะต้อง _สร้าง value ขึ้นมา_ โดยอิงจากข้อมูลภายในเนื้อหา

	_หมายเหตุ_
		แนวคิดเกี่ยวกับ Generative AI มีอธิบายอย่างละเอียดใน [Introduction to generative AI on Azure](https://learn.microsoft.com/en-us/training/modules/fundamentals-azure-ai-services/)

การประมวลผลเนื้อหาหลายรูปแบบ (_multimodal information extraction pipeline_) สามารถรวมหลายชั้นของเทคนิคเหล่านี้ไว้ด้วยกัน

หนึ่งในผลลัพธ์ที่ได้จาก pipeline นี้คือ _ข้อมูลเชิงโครงสร้าง (structured insights)_ และ _เนื้อหาที่ถูกสร้างขึ้นเพิ่มเติม_

![Screenshot of the possible components of multimodal information extraction.](https://learn.microsoft.com/en-us/training/wwl-data-ai/introduction-information-extraction/media/component-overview.png)