
**_Generative AI_** ช่วยให้ซอฟต์แวร์สามารถสร้าง _เนื้อหา_ เช่น ข้อความ รูปภาพ และโค้ด ได้โดยใช้ _language models_ ขนาดใหญ่หรือเล็กที่ผ่านการฝึกด้วยชุดข้อมูลจำนวนมหาศาล

**_Computer vision_** คือความสามารถของ AI ในการเข้าใจภาพ โดยใช้เทคนิคอย่าง _image classification_, _object detection_ และ _semantic segmentation_

**_Speech technologies_** รวมถึง _speech recognition_ (แปงเสียงพูดเป็นข้อความ) และ _speech synthesis_ (แปลงข้อความเป็นเสียงพูด) เพื่อให้สามารถโต้ตอบกับ AI ด้วยเสียงได้

**_Natural Language Processing (NLP)_** สนับสนุนงานต่าง ๆ เช่น การแยกข้อมูลสำคัญ (_entity extraction_), วิเคราะห์อารมณ์ (_sentiment analysis_) และตรวจจับภาษา (_language detection_) ซึ่ง _generative models_ ก็ช่วยยกระดับความสามารถในด้านนี้ได้อีกขั้น

**_Data extraction_** มักใช้เทคโนโลยี **_OCR_** เพื่ออ่านและแปลข้อความจากภาพและเอกสาร และตอนนี้ก็ขยายไปถึงเสียงและวิดีโอด้วย

**_Responsible AI_** คือการออกแบบและใช้งาน AI อย่างมีจริยธรรม โดยให้ความสำคัญกับ _fairness_, _privacy_, _inclusiveness_, _transparency_ และ _accountability_ เพื่อให้แน่ใจว่า AI ถูกใช้และพัฒนาอย่างปลอดภัยและเท่าเทียม

## Generative AI
---
- _Generative AI_ เป็นสาขาหนึ่งของ AI ที่ช่วยให้ซอฟต์แวร์สามารถ _สร้างเนื้อหาใหม่_ ได้ เช่น การสนทนาด้วยภาษาธรรมชาติ รูปภาพ วิดีโอ โค้ด และรูปแบบอื่น ๆ
- ความสามารถในการสร้างเนื้อหาเกิดจาก _language model_ ที่ได้รับการฝึกจากข้อมูลปริมาณมหาศาล ซึ่งมักมาจากเอกสารในอินเทอร์เน็ตหรือแหล่งข้อมูลสาธารณะอื่น ๆ
- โมเดล _generative AI_ สามารถเข้าใจ _ความสัมพันธ์เชิงความหมาย (semantic)_ ระหว่างคำต่าง ๆ (พูดง่าย ๆ คือโมเดล “รู้” ว่าคำต่าง ๆ มีความเชื่อมโยงกันอย่างไร) ซึ่งทำให้สามารถสร้างข้อความที่มีความหมายได้
- _Large language models (LLMs)_ และ _small language models (SLMs)_ ต่างกันที่ขนาดของข้อมูลที่ใช้ฝึก และจำนวนตัวแปรในโมเดล โดย _LLMs_ มีพลังสูงและสามารถประมวลผลได้กว้าง แต่ใช้ทรัพยากรมากกว่า ส่วน _SLMs_ มักเหมาะกับงานเฉพาะทาง และมีต้นทุนที่ต่ำกว่า

## Computer vision
---
- _Computer vision_ ทำงานโดยการฝึกโมเดลด้วยรูปภาพจำนวนมาก
- _Image classification_ เป็นรูปแบบหนึ่งของ _computer vision_ โดยโมเดลจะถูกฝึกด้วยภาพที่มีการระบุว่า "ภาพนี้คืออะไร" เพื่อให้สามารถทำนายป้ายกำกับของภาพที่ยังไม่มีการระบุได้ ว่าเป็นภาพของอะไร 
- _Object detection_ เป็นอีกหนึ่งรูปแบบของ _computer vision_ ที่ฝึกให้โมเดลสามารถระบุตำแหน่งของวัตถุในภาพได้
- ยังมีรูปแบบที่ซับซ้อนมากขึ้น เช่น _semantic segmentation_ ซึ่งเป็นการพัฒนาจาก _object detection_ โดยไม่ใช่แค่ล้อมกรอบวัตถุ แต่สามารถระบุได้เลยว่า "พิกเซล" ไหนในภาพที่เป็นส่วนหนึ่งของวัตถุนั้น
- เรายังสามารถผสาน _computer vision_ เข้ากับ _language models_ เพื่อสร้างโมเดลแบบ _multi-modal_ ที่รวมความสามารถของ _computer vision_ และ _generative AI_ ไว้ด้วยกัน

## Speech
---
- _Speech recognition_ คือความสามารถของ AI ในการ “ฟัง” และตีความคำพูด โดยทั่วไปจะอยู่ในรูปแบบของ _speech-to-text_ ซึ่งเป็นการแปลงเสียงพูดให้กลายเป็นข้อความ
- _Speech synthesis_ คือความสามารถของ AI ในการเปล่งเสียงพูด โดยมักอยู่ในรูปแบบของ _text-to-speech_ ซึ่งคือการแปลงข้อความให้กลายเป็นเสียงที่ฟังได้
- เทคโนโลยีเสียงของ AI กำลังพัฒนาอย่างรวดเร็ว เพื่อรับมือกับความท้าทาย เช่น การตัดเสียงรบกวน การตรวจจับการพูดแทรก และการสร้างเสียงพูดที่ _เป็นธรรมชาติและมีอารมณ์_ มากขึ้นเหมือนมนุษย์

## Natural language processing
---
- ความสามารถของ _NLP_ มาจากโมเดลที่ถูกฝึกมาเพื่อวิเคราะห์ข้อความในรูปแบบต่าง ๆ
- แม้ว่า _generative AI_ จะสามารถจัดการกับหลายงานด้าน _natural language processing_ ได้ในปัจจุบัน แต่ในหลายกรณีก็สามารถใช้ _NLP_ แบบดั้งเดิมที่ง่ายกว่าและประหยัดกว่าได้เช่นกัน
- ตัวอย่างงานทั่วไปของ _NLP_ ได้แก่:
  - _Entity extraction_ คือการระบุชื่อคน สถานที่ หรือองค์กรในเอกสาร
  - _Text classification_ คือการจัดประเภทเอกสารให้อยู่ในหมวดหมู่ที่เหมาะสม
  - _Sentiment analysis_ คือการวิเคราะห์ว่าเนื้อหามี _อารมณ์_ เชิงบวก ลบ หรือเป็นกลาง และสื่อถึงความคิดเห็นอย่างไร
  - _Language detection_ คือการตรวจจับว่าเนื้อหานั้นเขียนด้วยภาษาอะไร

## Extract data and insights
---
- พื้นฐานของการวิเคราะห์เอกสารส่วนใหญ่มาจากเทคโนโลยี _computer vision_ ที่เรียกว่า _optical character recognition (OCR)_
- แม้ว่าโมเดล _OCR_ จะสามารถระบุตำแหน่งของข้อความในภาพได้ แต่โมเดลที่ล้ำหน้ากว่านั้นสามารถ _ตีความ_ ค่าต่าง ๆ ในเอกสาร และดึงข้อมูลในฟิลด์เฉพาะออกมาได้
- ในอดีต _data extraction_ มักเน้นการดึงข้อมูลจากแบบฟอร์มที่เป็นข้อความ แต่ปัจจุบันมีโมเดลที่สามารถดึงข้อมูลจาก _เสียง_ _ภาพ_ และ _วิดีโอ_ ได้อย่างมีประสิทธิภาพมากขึ้น

## Responsible AI
---
- **_Fairness_**: โมเดล AI ถูกฝึกจากข้อมูลที่คัดเลือกโดยมนุษย์ ซึ่งอาจมี _bias_ หรืออคติโดยไม่ตั้งใจ ทำให้โมเดลสร้างผลลัพธ์ที่ไม่เป็นธรรมได้ นักพัฒนา AI ต้องใส่ใจในการลดอคติในข้อมูลฝึก และทดสอบระบบเพื่อให้แน่ใจว่า _fair_
- **_Reliability and safety_**: AI ทำงานบนพื้นฐานของ _probabilistic models_ ซึ่งไม่สามารถให้คำตอบที่ถูกต้อง 100% ได้เสมอ ดังนั้นแอปพลิเคชันที่ใช้ AI ต้องมีวิธีจัดการความเสี่ยงและป้องกันข้อผิดพลาด
- **_Privacy and security_**: ข้อมูลฝึกอาจมีข้อมูลส่วนตัว ดังนั้นนักพัฒนา AI ต้องรักษาความปลอดภัยของข้อมูลและมั่นใจว่าโมเดลที่ฝึกแล้วจะไม่สามารถเปิดเผยข้อมูลส่วนบุคคลหรือข้อมูลองค์กรได้
- **_Inclusiveness_**: ประโยชน์ของ AI ควรเข้าถึงทุกคน นักพัฒนา AI ควรพยายามไม่ให้โซลูชันของตน _กีดกันหรือทำให้ผู้ใช้บางกลุ่มเข้าถึงไม่ได้_
- **_Transparency_**: แม้ AI จะดูเหมือน “เวทมนตร์” แต่ผู้ใช้ควร _เข้าใจวิธีทำงาน_ ของระบบ และทราบถึงข้อจำกัดของมัน
- **_Accountability_**: คนหรือองค์กรที่พัฒนาและใช้งาน AI ต้องมีความ _รับผิดชอบ_ ต่อการกระทำของตนเอง จำเป็นต้องมี _framework_ ด้านการกำกับดูแลเพื่อให้มั่นใจว่าหลักการของ _Responsible AI_ ถูกนำไปใช้อย่างจริงจัง

## 4 Guiding Principles
### **1. Fairness**

- **Goal**: Avoid bias and ensure AI systems treat all people and groups equitably.
- **Example**: A facial recognition system should not perform worse on people of color or women compared to others.
- **Why it matters**: Biased AI can perpetuate discrimination or cause harm to certain communities.
    
---

### **2. Reliability and Safety**

- **Goal**: AI systems should work as intended, even in unpredictable or adversarial situations.
- **Example**: An AI used in healthcare must provide consistently accurate diagnoses, even across diverse datasets.
- **Why it matters**: Malfunctioning AI can lead to real-world harm, including loss of life or financial damage.  

---

### **3. Privacy and Security**

- **Goal**: Protect user data and ensure AI systems cannot be easily exploited.
- **Example**: A voice assistant should not store or leak private conversations.
- **Why it matters**: Users must trust that AI respects their personal information and is protected from misuse.

---

### **4. Transparency and Accountability**

- **Goal**: AI systems should be understandable and there should be clear responsibility when things go wrong.
- **Example**: A bank using AI to approve loans should be able to explain why an applicant was rejected.
- **Why it matters**: Without transparency, it’s difficult to build trust or address failures.