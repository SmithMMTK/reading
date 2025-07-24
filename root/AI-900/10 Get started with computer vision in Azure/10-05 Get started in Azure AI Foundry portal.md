
Azure AI Vision ให้ _เครื่องมือพื้นฐาน_ สำหรับนำความสามารถด้านภาพเข้ามาใช้ในแอปพลิเคชันต่าง ๆ ซึ่งเป็นหนึ่งในบริการของ _Azure AI Services_ ที่สามารถนำมาใช้สร้างโซลูชันได้หลายวิธี เช่น

- ผ่าน _Azure AI Foundry portal_ ที่มีอินเทอร์เฟซให้ใช้งานง่าย
- ผ่าน _SDK_ หรือ _REST API_ สำหรับนักพัฒนาโปรแกรมที่ต้องการควบคุมด้วยโค้ด

## Azure resources for Azure AI Vision service

ในการใช้งาน _Azure AI Vision_ คุณต้องสร้าง _resource_ สำหรับบริการนี้ใน _Azure subscription_ ของคุณ โดยสามารถเลือกใช้ resource ได้ 2 ประเภท:

- **Azure AI Vision**: เป็น resource ที่ออกแบบมาสำหรับบริการ _Azure AI Vision_ โดยเฉพาะ เหมาะสำหรับกรณีที่คุณใช้แค่บริการนี้ หรืออยากแยกดู _การใช้งาน_ และ _ค่าใช้จ่าย_ ของ Azure AI Vision โดยไม่รวมกับบริการอื่น

- **Azure AI services**: เป็น resource แบบรวม ที่ครอบคลุมบริการ AI หลายตัว เช่น _Azure AI Language_, _Azure AI Custom Vision_, _Azure AI Translator_ และอื่น ๆ เหมาะกับผู้ที่วางแผนจะใช้หลายบริการร่วมกัน เพื่อให้การ _ดูแลระบบ_ และ _พัฒนาแอป_ ง่ายขึ้น

> _หมายเหตุ_ 
> มีหลายวิธีในการสร้าง _resources_ บน Azure คุณสามารถใช้ _หน้าจออินเทอร์เฟซ_ เพื่อสร้าง resource หรือใช้ _สคริปต์_ ก็ได้ โดยทั้ง _Azure portal_ และ _Azure AI Foundry portal_ ต่างก็มีอินเทอร์เฟซให้สร้าง resource ได้สะดวก
> 
> แนะนำให้ใช้ _Azure AI Foundry portal_ หากคุณต้องการดู _ตัวอย่างการใช้งานจริง_ ของบริการ _Azure AI Services_ ไปพร้อมกัน

## Get started in Azure AI Foundry portal

![Screenshot of the Azure AI Foundry portal.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-computer-vision-azure/media/azure-ai-foundry-portal.png)

_Azure AI Foundry_ เป็นแพลตฟอร์มรวมสำหรับการดำเนินงานด้าน _AI ขององค์กร_, การสร้าง _โมเดล_, และการพัฒนา _แอปพลิเคชัน_ โดยใน _Azure AI Foundry portal_ จะมีอินเทอร์เฟซที่ออกแบบมาโดยใช้แนวคิดของ _hubs_ และ _projects_

การใช้งานบริการ _Azure AI Services_ เช่น _Azure AI Vision_ จำเป็นต้องสร้าง _project_ ซึ่งจะทำให้ระบบสร้าง resource ของ _Azure AI Services_ ให้คุณโดยอัตโนมัติ

_project_ ใน Azure AI Foundry จะช่วยให้คุณ _จัดระเบียบงาน_ และ _resource_ ได้อย่างมีประสิทธิภาพ โดย acting เป็นเหมือน _กล่องรวมข้อมูล_ เช่น _datasets_, _models_, และ resource อื่น ๆ ทำให้จัดการและทำงานร่วมกันได้ง่ายขึ้น

ภายใน _Azure AI Foundry portal_ คุณสามารถลองใช้งานฟีเจอร์ต่าง ๆ ของบริการได้ทันที ไม่ว่าจะเป็นการทดสอบกับ _ภาพตัวอย่าง_ หรือ _อัปโหลดภาพของคุณเอง_

![Screenshot of Azure AI Foundry's Vision page.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-computer-vision-azure/media/azure-ai-foundry-portal-vision-example.png)

