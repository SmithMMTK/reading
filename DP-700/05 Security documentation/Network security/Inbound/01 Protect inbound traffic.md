https://learn.microsoft.com/en-us/fabric/security/protect-inbound-traffic

การรับส่งข้อมูลขาเข้า (_Inbound traffic_) คือข้อมูลที่เข้ามายัง _Fabric_ จาก _internet_ บทความนี้อธิบายความแตกต่างระหว่างสองวิธีในการป้องกัน _inbound traffic_ ใน _Microsoft Fabric_ ได้แก่ _private links_ และ _Entra Conditional Access_ คุณสามารถใช้บทความนี้เพื่อช่วยตัดสินใจว่าวิธีใดเหมาะสมกับองค์กรของคุณที่สุด

- **Private links (Option 1, Customer Vnet)** - _Fabric_ จะใช้ _private IP address_ ที่มาจาก _virtual network_ ของคุณ โดย _endpoint_ นี้อนุญาตให้ผู้ใช้ภายในเครือข่ายของคุณสามารถสื่อสารกับ _Fabric_ ผ่าน _private IP address_ ได้โดยใช้ _private links_
- **Entra Conditional Access (Option 2, User)** - เมื่อผู้ใช้ทำการ _authenticate_ การเข้าถึงจะถูกกำหนดตามชุดของ _policies_ ที่อาจรวมถึง _IP address_, _location_, และอุปกรณ์ที่อยู่ภายใต้การจัดการ (_managed devices_)

![A diagram showing two authentication methods for inbound traffic into Fabric, Vnets and Microsoft Entra ID.](https://learn.microsoft.com/en-us/fabric/security/media/protect-inbound-traffic/protect-inbound-traffic.png)

เมื่อ _traffic_ เข้ามายัง _Fabric_ ระบบจะทำการ _authenticate_ โดยใช้ _Microsoft Entra ID_ ซึ่งเป็นวิธีการรับรองตัวตนเดียวกันกับที่ใช้ใน _Microsoft 365_, _OneDrive_, และ _Dynamics 365_ การ _authenticate_ ผ่าน _Microsoft Entra ID_ ช่วยให้ผู้ใช้สามารถเชื่อมต่อกับแอปพลิเคชันบนคลาวด์ได้อย่างปลอดภัยจากอุปกรณ์และเครือข่ายใด ๆ ไม่ว่าจะเป็นจากที่บ้าน ระยะไกล หรือสำนักงานขององค์กร

แพลตฟอร์ม _backend_ ของ _Fabric_ ได้รับการป้องกันด้วย _virtual network_ และไม่สามารถเข้าถึงได้โดยตรงจาก _public internet_ ยกเว้นผ่าน _secure endpoints_ หากต้องการเข้าใจว่าการปกป้อง _traffic_ ใน _Fabric_ ทำงานอย่างไร โปรดดู 

[[reading/DP-700/05 Security documentation/Network security/Inbound/Architectural diagram]]

โดยค่าเริ่มต้น _Fabric_ จะสื่อสารระหว่าง [experiences](https://learn.microsoft.com/en-us/fabric/fundamentals/microsoft-fabric-overview#components-of-microsoft-fabric) ต่าง ๆ ผ่านเครือข่ายภายในของ _Microsoft_ (_Microsoft backbone network_) เช่น เมื่อรายงาน _Power BI_ โหลดข้อมูลจาก [OneLake](https://learn.microsoft.com/en-us/fabric/onelake/onelake-overview) ข้อมูลจะถูกส่งผ่านเครือข่ายภายในของ _Microsoft_ ซึ่งต่างจากการต้องตั้งค่าหลายบริการ _Platform as a Service (PaaS)_ ให้เชื่อมต่อกันผ่าน _private network_

การสื่อสารขาเข้าระหว่าง _clients_ เช่น _browser_ หรือ _SQL Server Management Studio (SSMS)_ กับ _Fabric_ จะใช้โปรโตคอล _TLS 1.2_ และจะพยายามอัปเกรดเป็น _TLS 1.3_ เมื่อเป็นไปได้

การตั้งค่าความปลอดภัยเริ่มต้นของ _Fabric_ รวมถึง:

- [Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/fundamentals/whatis) ซึ่งใช้ในการ _authenticate_ ทุกคำขอ
- หลังจาก _authentication_ สำเร็จ คำขอจะถูกส่งต่อไปยังบริการ _backend_ ที่เหมาะสมผ่าน _secure Microsoft managed endpoints_
- การรับส่งข้อมูลภายในระหว่าง _experiences_ ต่าง ๆ ใน _Fabric_ จะถูกส่งผ่าน _Microsoft backbone_
- การรับส่งข้อมูลระหว่าง _clients_ กับ _Fabric_ จะถูกเข้ารหัสอย่างน้อยด้วยโปรโตคอล _Transport Layer Security (TLS) 1.2_


## Private links

เมื่อใช้ _private endpoints_ บริการของคุณจะได้รับ _private IP address_ จาก _virtual network_ ของคุณ _endpoint_ นี้จะช่วยให้ทรัพยากรอื่น ๆ ภายในเครือข่ายสามารถสื่อสารกับบริการผ่าน _private IP address_ ได้โดยตรง

การใช้ _Private links_ จะสร้างอุโมงค์ (_tunnel_) จากบริการเข้าสู่หนึ่งใน _subnet_ ของคุณ เพื่อสร้างช่องทางส่วนตัว (_private channel_) การสื่อสารจากอุปกรณ์ภายนอกจะเริ่มจาก _IP address_ ของผู้ใช้งาน วิ่งเข้าสู่ _private endpoint_ ภายใน _subnet_ นั้น ผ่าน _tunnel_ และเข้าสู่บริการ

เมื่อมีการใช้ _private links_ แล้ว การเข้าถึง _Fabric_ จะไม่สามารถทำผ่าน _public internet_ ได้อีกต่อไป ผู้ใช้ทุกคนต้องเชื่อมต่อผ่าน _private network_ เท่านั้น โดยการสื่อสารทั้งหมดกับ _Fabric_ จะต้องใช้ _private network_ ไม่ว่าจะเป็นการดูรายงาน _Power BI_ ผ่าน _browser_ หรือการใช้ _SQL Server Management Studio (SSMS)_ เพื่อเชื่อมต่อกับ _SQL connection string_ เช่น `<guid_unique_your_item>.datawarehouse.fabric.microsoft.com`

