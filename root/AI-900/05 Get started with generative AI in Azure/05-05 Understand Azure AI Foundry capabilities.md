
_Azure AI Foundry portal_ มีส่วนติดต่อผู้ใช้ (UI) ที่ออกแบบมาโดยใช้แนวคิดของ _hubs_ และ _projects_

โดยทั่วไป การสร้าง _hub_ จะให้คุณเข้าถึงบริการต่าง ๆ ของ _Azure AI_ และ _Azure Machine Learning_ ได้แบบครอบคลุมมากขึ้น ภายในแต่ละ hub คุณสามารถสร้าง _projects_ ซึ่งให้การเข้าถึงที่เฉพาะเจาะจงยิ่งขึ้น เช่น การจัดการ _models_ หรือ _agent development_ คุณสามารถจัดการ projects ของคุณได้จากหน้า _overview_ ใน Azure AI Foundry portal ได้โดยตรง

![Screenshot of Azure AI Foundry overview page](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-generative-ai-azure/media/foundry-overview-page.png)

เมื่อคุณสร้าง _Azure AI Hub_ จะมี _ทรัพยากรอื่น ๆ_ ถูกสร้างขึ้นพร้อมกันโดยอัตโนมัติ เช่น _Azure AI services resource_

ภายใน _Azure AI Foundry portal_ คุณสามารถทดลองใช้บริการต่าง ๆ ของ Azure AI ได้หลากหลาย เช่น:

- _Azure AI Speech_: สำหรับการรู้จำเสียงพูด และแปลงข้อความเป็นเสียง  
- _Azure AI Language_: สำหรับการเข้าใจและวิเคราะห์ภาษาธรรมชาติ  
- _Azure AI Vision_: สำหรับการประมวลผลและเข้าใจภาพ  
- _Azure AI Foundry Content Safety_: สำหรับตรวจสอบและจัดการเนื้อหาที่อาจไม่ปลอดภัย

![Screenshot of Azure AI services on Azure AI Foundry portal.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-generative-ai-azure/media/foundry-ai-services-home-page.png)

นอกจาก _demos_ แล้ว _Azure AI Foundry portal_ ยังมี _playgrounds_ สำหรับให้คุณ _ทดลองใช้งานบริการ Azure AI_ และ _ทดสอบโมเดล_ จาก _model catalog_ ได้โดยตรง

_playgrounds_ ช่วยให้คุณสามารถลองใช้งานโมเดลหรือบริการต่าง ๆ อย่างรวดเร็ว โดยไม่ต้องเขียนโค้ดหรือสร้างแอปก่อน  
เหมาะสำหรับการ _สำรวจความสามารถ_ และ _เปรียบเทียบผลลัพธ์_ ของโมเดลต่าง ๆ

![Screenshot of playgrounds on Azure AI Foundry portal](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-generative-ai-azure/media/foundry-playgrounds-page.png)

![Screenshot of the chat playground on Azure AI Foundry portal.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-generative-ai-azure/media/foundry-chat-playground.png)

## Customizing models

มีหลายวิธีในการ _ปรับแต่งโมเดล_ ที่ใช้ในแอปพลิเคชัน _generative AI_ เป้าหมายของการปรับแต่งคือเพื่อ _เพิ่มประสิทธิภาพ_ ของโมเดลในด้านต่าง ๆ เช่น _คุณภาพของคำตอบ_ และ _ความปลอดภัยในการใช้งาน_

ต่อไปเราจะไปดู _4 วิธีหลัก_ ที่คุณสามารถใช้เพื่อ _customize โมเดล_ ใน _Azure AI Foundry_

| _Method_ | _Description_ |
|----------|----------------|
| _Using grounding data_ | _Grounding_ คือการเชื่อมคำตอบของโมเดลกับแหล่งข้อมูลที่ _น่าเชื่อถือ มีบริบท และตรงตามข้อเท็จจริง_ เช่น ฐานข้อมูล การค้นหาแบบเรียลไทม์ หรือแหล่งความรู้เฉพาะทาง เพื่อเพิ่ม _ความถูกต้องและความน่าเชื่อถือ_ ของคำตอบ |
| _Implementing Retrieval-Augmented Generation (RAG)_ | เทคนิค _RAG_ คือการเชื่อม language model กับ _ฐานข้อมูลขององค์กร_ โดยดึงข้อมูลที่เกี่ยวข้องจากชุดข้อมูลเฉพาะ และใช้ในการสร้างคำตอบที่ _ตรงบริบทและอัปเดต_ เหมาะกับงานที่ต้องใช้ข้อมูลล่าสุด เช่น _customer support_ หรือ _knowledge management_ |
| _Fine-tuning_ | คือการนำโมเดลที่ผ่านการฝึกมาแล้ว (pretrained model) มาฝึกเพิ่มด้วยชุดข้อมูลขนาดเล็กที่เจาะจงเฉพาะงาน เพื่อให้โมเดล _เชี่ยวชาญในเรื่องเฉพาะ_ และ _เพิ่มความแม่นยำ_ ลดโอกาสเกิดคำตอบที่ไม่ตรงประเด็น |
| _Managing security and governance controls_ | การจัดการด้าน _ความปลอดภัยและธรรมาภิบาล_ มีความสำคัญในการควบคุม _สิทธิ์การเข้าถึง การยืนยันตัวตน และการใช้ข้อมูล_ เพื่อป้องกันไม่ให้เกิดการเผยแพร่ข้อมูลที่ผิดหรือไม่เหมาะสม |
ต่อไปเราจะมาทำความเข้าใจว่า Azure AI Foundry มีเครื่องมืออะไรบ้างที่ช่วยประเมิน _ประสิทธิภาพ (performance)_ ของแอปพลิเคชันที่ใช้ _generative AI_
