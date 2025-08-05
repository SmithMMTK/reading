https://learn.microsoft.com/en-us/fabric/security/security-fundamentals#architectural-diagram

แผนภาพสถาปัตยกรรมด้านล่างแสดงภาพรวมในระดับสูงของสถาปัตยกรรมด้านความปลอดภัยของ _Fabric_

![Diagram shows a high-level representation of the Fabric security architecture.](https://learn.microsoft.com/en-us/fabric/security/media/security-fundamentals/fabric-security-architectural-diagram.svg)

แผนภาพนี้แสดงแนวคิดหลักต่อไปนี้:

1. ผู้ใช้เชื่อมต่อกับบริการ _Fabric_ โดยใช้ _browser_ หรือแอปพลิเคชันของ _client_ เช่น _Power BI Desktop_
2. การ _authenticate_ จัดการโดย _Microsoft Entra ID_ ([ชื่อเดิมคือ Azure Active Directory](https://learn.microsoft.com/en-us/entra/fundamentals/new-name)) ซึ่งเป็นบริการ _identity and access management_ บนคลาวด์ที่ทำหน้าที่ _authenticate_ ผู้ใช้หรือ [service principal](https://learn.microsoft.com/en-us/entra/identity-platform/app-objects-and-service-principals?tabs=browser#service-principal-object) และจัดการการเข้าถึง _Fabric_
3. _Web front end_ รับคำขอจากผู้ใช้และอำนวยความสะดวกในการ _sign-in_ รวมถึงกำหนดเส้นทางคำขอและแสดงเนื้อหาส่วนหน้าให้กับผู้ใช้
4. _Metadata platform_ ทำหน้าที่จัดเก็บข้อมูล _metadata_ ของ _tenant_ ซึ่งอาจรวมถึงข้อมูลของลูกค้า _Fabric services_ จะเรียกใช้งาน _platform_ นี้ตามคำขอเพื่อดึงข้อมูลการอนุญาต และทำการตรวจสอบความถูกต้องของคำขอจากผู้ใช้ โดย _metadata platform_ ตั้งอยู่ในภูมิภาคหลักของ _tenant_
5. _Back-end capacity platform_ รับผิดชอบในการดำเนินการประมวลผล (_compute operations_) และการจัดเก็บข้อมูลของลูกค้า โดยตั้งอยู่ใน _capacity region_ และใช้บริการหลักของ _Azure_ ภายในภูมิภาคนั้นเพื่อสนับสนุน _Fabric experiences_ เฉพาะ

โครงสร้างพื้นฐานของ _Fabric platform services_ เป็นแบบ _multitenant_ โดยมีการแยก _logical isolation_ ระหว่าง _tenants_ บริการเหล่านี้ไม่ได้ประมวลผลข้อมูลที่ซับซ้อนจากผู้ใช้ และเขียนด้วย _managed code_ ทั้งหมด โดยไม่มีการรันโค้ดที่เขียนโดยผู้ใช้เลย

ทั้ง _metadata platform_ และ _back-end capacity platform_ ทำงานภายใน _secured virtual networks_ ซึ่งเปิดเผยเพียงบาง _secure endpoints_ สู่ _internet_ เพื่อให้สามารถรับคำขอจากลูกค้าและบริการอื่น ๆ ได้ นอกเหนือจาก _endpoints_ เหล่านี้ ระบบจะได้รับการปกป้องด้วยกฎความปลอดภัยของเครือข่าย (_network security rules_) ที่บล็อกการเข้าถึงจาก _public internet_ และการสื่อสารภายใน _virtual networks_ จะถูกจำกัดตามสิทธิ (_privilege_) ของแต่ละบริการภายใน

เลเยอร์แอปพลิเคชันทำหน้าที่รับรองว่าแต่ละ _tenant_ สามารถเข้าถึงเฉพาะข้อมูลของตนเองได้เท่านั้น
