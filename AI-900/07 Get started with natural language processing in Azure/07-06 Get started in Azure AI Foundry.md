
_Azure AI Language_ และ _Azure AI Translator_ เป็นส่วนประกอบสำคัญในการเพิ่ม _ความสามารถด้านภาษา_ ให้กับแอปพลิเคชันของคุณ ในฐานะที่เป็นหนึ่งในบริการของ _Azure AI_ คุณสามารถสร้างโซลูชันได้หลายรูปแบบ เช่น:

- ผ่าน _Azure AI Foundry portal_  
- ผ่าน _software development kit (SDK)_ หรือ _REST API_

ในการใช้งาน _Azure AI Language_ หรือ _Azure AI Translator_ ในแอปพลิเคชัน คุณต้องมีการ _สร้าง resource ที่เหมาะสม_ ไว้ใน _Azure subscription_ ของคุณก่อน โดยสามารถเลือกได้ดังนี้:

- _Language resource_: เลือกตัวนี้ถ้าคุณวางแผนจะใช้แค่บริการ _Azure AI Language_ หรือหากคุณต้องการแยกการจัดการเรื่องการเข้าถึงและการคิดค่าใช้จ่ายออกจากบริการอื่น ๆ  
- _Translator resource_: เลือกตัวนี้ถ้าคุณต้องการจัดการเรื่องการเข้าถึงและการคิดค่าใช้จ่ายสำหรับบริการ _translation_ โดยเฉพาะ  
- _Azure AI services resource_: เลือกตัวนี้หากคุณวางแผนจะใช้ _Azure AI Language_ ร่วมกับบริการอื่น ๆ ของ Azure AI และต้องการจัดการทุกอย่างรวมกันใน resource เดียว

คุณสามารถสร้าง _resource_ บน Azure ได้หลายวิธี โดยสามารถใช้ _หน้าจอแบบกราฟิก (UI)_ หรือเขียน _script_ ก็ได้ ทั้ง _Azure portal_ และ _Azure AI Foundry portal_ ต่างก็มี _อินเทอร์เฟซสำหรับสร้าง resource_ ที่ใช้งานง่าย หากคุณต้องการเห็น _ตัวอย่างการใช้งานจริง_ ของบริการ _Azure AI_ พร้อมไปกับการสร้าง resource ขอแนะนำให้เลือกใช้ _Azure AI Foundry portal_ พอร์ทัลนี้เหมาะสำหรับผู้ที่ต้องการเรียนรู้และทดลอง _ความสามารถของ AI_ พร้อมกับการตั้งค่าระบบไปในตัว

## Get started in Azure AI Foundry portal

![Screenshot of Azure AI Language page in Azure AI Foundry portal.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-language-azure/media/ai-foundry-language-1.png)

_Azure AI Foundry_ เป็นแพลตฟอร์มแบบรวมศูนย์สำหรับการดำเนินงานด้าน AI ในระดับองค์กร, การสร้างโมเดล, และการพัฒนาแอปพลิเคชัน

พอร์ทัลของ _Azure AI Foundry_ มีอินเทอร์เฟซที่ออกแบบตามแนวคิดของ _hubs_ และ _projects_

หากคุณต้องการใช้งานบริการต่าง ๆ ของ _Azure AI_ เช่น _Azure AI Language_ หรือ _Azure AI Translator_ คุณจะต้องสร้าง _project_ ใน Azure AI Foundry ซึ่งจะมีการสร้าง _Azure AI services resource_ ให้คุณโดยอัตโนมัติ

_project_ ใน Azure AI Foundry ช่วยให้คุณสามารถจัดระเบียบงานและ resource ได้อย่างมีประสิทธิภาพ โดย project จะทำหน้าที่เป็นเหมือน _กล่องเก็บข้อมูล_ สำหรับ _datasets_, _โมเดล_, และ resource อื่น ๆ ซึ่งช่วยให้สามารถบริหารจัดการและทำงานร่วมกันได้สะดวกขึ้น

ภายในพอร์ทัลของ Azure AI Foundry คุณยังสามารถทดลองใช้ฟีเจอร์ต่าง ๆ ของบริการได้ในรูปแบบ _playground_ เช่น:

- _language playground_ – ทดลองความสามารถของ Azure AI Language  
- _translator playground_ – ทดลองความสามารถของ Azure AI Translator

การใช้งาน playground เหล่านี้เหมาะสำหรับการเรียนรู้และทดสอบโดยไม่ต้องเขียนโค้ดในทันที

![Screenshot of Azure AI Language playground in Azure AI Foundry portal with an example of sentiment analaysis.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-language-azure/media/ai-foundry-language-sentiment.png)

![Screenshot of Azure AI Translator playground in Azure AI Foundry portal with an example of text translation.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-language-azure/media/ai-foundry-translator-playground.png)
