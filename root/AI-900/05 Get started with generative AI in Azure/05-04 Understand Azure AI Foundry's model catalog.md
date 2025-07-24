_Azure AI Foundry_ มี _marketplace_ ที่ครบถ้วนและยืดหยุ่น ภายในมีโมเดลให้เลือกใช้ทั้งจาก _Microsoft โดยตรง_ และจาก _พาร์ตเนอร์_ รวมถึง _ชุมชนนักพัฒนา_

ผู้ใช้สามารถค้นหา เลือกเปรียบเทียบ และนำโมเดลเหล่านี้มาใช้งานกับโซลูชัน generative AI ของตนเองได้อย่างคล่องตัว

![Screenshot of Azure AI Foundry's model catalog.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-generative-ai-azure/media/foundry-model-catalog.png)

โมเดล _Azure OpenAI_ ใน Foundry ถือเป็น _โมเดลกลุ่มแรกจาก Microsoft (first-party)_ และถูกจัดอยู่ในกลุ่ม _foundation models_

_foundation models_ คือโมเดลที่ได้รับการฝึกจาก _ข้อมูลขนาดใหญ่_ และสามารถนำมา _fine-tune_ เพิ่มเติมด้วย _ข้อมูลจำนวนน้อย_ เพื่อให้เหมาะกับงานเฉพาะทาง

คุณสามารถ _deploy_ โมเดลจาก _Azure AI Foundry model catalog_ ไปยัง endpoint ได้ทันที _โดยไม่ต้องฝึกเพิ่ม_ แต่หากต้องการให้โมเดล _เชี่ยวชาญเฉพาะด้าน_ หรือ _ทำงานได้ดีขึ้นกับความรู้เฉพาะโดเมน_ ก็สามารถเลือก _customize_ ได้

เพื่อหาโมเดลที่เหมาะสมที่สุดกับงานของคุณ คุณสามารถ:

- ทดลองโมเดลต่าง ๆ ใน _playground_
- ใช้ _model leaderboard (preview)_ เพื่อดูว่าโมเดลไหนทำผลงานได้ดีในเกณฑ์ต่าง ๆ เช่น  
  - _คุณภาพ (quality)_  
  - _ต้นทุน (cost)_  
  - _ปริมาณการประมวลผล (throughput)_

นอกจากนี้ยังสามารถดู _กราฟเปรียบเทียบโมเดล_ ตาม _metrics_ เฉพาะ เพื่อช่วยในการตัดสินใจ

![Screenshot of comparison of models in Azure AI Foundry portal.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-generative-ai-azure/media/model-benchmarks-comparision.png)
