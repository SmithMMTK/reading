
## What are Managed Private Endpoints?

_Managed private endpoints_ คือฟีเจอร์ที่ช่วยให้ _Fabric workloads_ สามารถเข้าถึงแหล่งข้อมูล (_data sources_) ที่อยู่หลัง _firewall_ หรือถูกบล็อกจากการเข้าถึงผ่าน _public internet_ ได้อย่างปลอดภัยและเป็นส่วนตัว

- _Workspace admins_ สามารถสร้าง _managed private endpoints_ เพื่อเข้าถึงแหล่งข้อมูลที่ถูกปิดจากภายนอก
- _Managed private endpoints_ ช่วยให้ _Fabric workloads_ เข้าถึงข้อมูลได้โดยไม่ต้องเปิดเผยสู่เครือข่ายสาธารณะ และไม่ต้องตั้งค่าเครือข่ายที่ซับซ้อน
- _Microsoft Fabric_ จะทำการสร้างและจัดการ _managed private endpoints_ โดยอิงจากข้อมูลที่ผู้ดูแล _workspace_ กำหนดไว้  
  ผู้ดูแลสามารถตั้งค่า _managed private endpoints_ ได้จากเมนู _workspace settings_ โดยระบุ _resource ID_ ของแหล่งข้อมูล, ระบุ _subresource_ เป้าหมาย และให้เหตุผลประกอบการขอใช้ _private endpoint_
- _Managed private endpoints_ รองรับหลายแหล่งข้อมูล เช่น _Azure Storage_, _Azure SQL Database_ และอื่น ๆ

![Animated illustration showing the process of creating a managed private endpoint in Microsoft Fabric.](https://learn.microsoft.com/en-us/fabric/security/media/security-managed-private-endpoints-overview/managed_private_endpoint.gif)

> **หมายเหตุ**  
> _Managed private endpoints_ รองรับทั้งใน _Fabric trial capacity_ และ _Fabric F SKU capacities_

ดูข้อมูลเพิ่มเติมเกี่ยวกับแหล่งข้อมูลที่รองรับได้ที่ [Supported data sources](https://learn.microsoft.com/en-us/fabric/security/security-managed-private-endpoints-create#supported-data-sources)