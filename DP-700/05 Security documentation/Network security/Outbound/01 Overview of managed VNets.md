
_Managed virtual networks_ คือ _virtual networks_ ที่ถูกสร้างและจัดการโดย _Microsoft Fabric_ สำหรับแต่ละ _Fabric workspace_ โดยให้การแยกเครือข่าย (_network isolation_) สำหรับการประมวลผล _Spark workloads_ ซึ่งหมายความว่า _compute clusters_ จะถูกสร้างขึ้นในเครือข่ายที่แยกเฉพาะ และจะไม่อยู่ในเครือข่ายที่แชร์ร่วมกันอีกต่อไป

_Managed virtual networks_ ยังเปิดใช้งานคุณสมบัติด้านความปลอดภัยของเครือข่าย เช่น _managed private endpoints_ และรองรับ _private link_ สำหรับ _Data Engineering_ และ _Data Science_ ที่ใช้ _Apache Spark_ ภายใน _Microsoft Fabric_

![Animated illustration of how managed virtual networks work.](https://learn.microsoft.com/en-us/fabric/security/media/security-managed-vnets-fabric-overview/managed-vnets-overview.gif)

การใช้ _Fabric workspace_ ที่สร้างขึ้นพร้อมกับ _dedicated virtual network_ ให้คุณค่าใน 3 ด้านดังนี้:

- คุณจะได้รับการแยกเครือข่ายอย่างสมบูรณ์สำหรับ _Spark clusters_ ที่ใช้รันงาน _Spark_ (ซึ่งรันโค้ดที่ผู้ใช้กำหนดได้เอง) โดยไม่ต้องดูแลจัดการเครือข่ายเอง เพราะ _Microsoft Fabric_ จัดการให้ทั้งหมด
- คุณไม่จำเป็นต้องสร้าง _subnet_ สำหรับ _Spark clusters_ ตามโหลดสูงสุด เพราะ _Microsoft Fabric_ จะจัดสรรให้โดยอัตโนมัติ
- _Managed virtual network_ พร้อมกับ _managed private endpoints_ สำหรับ _workspace_ ของคุณ ช่วยให้สามารถเข้าถึงแหล่งข้อมูลที่อยู่หลัง _firewall_ หรือไม่สามารถเข้าถึงผ่าน _public access_ ได้

> **หมายเหตุ**  
> ปัจจุบัน _Managed virtual networks_ **ยังไม่รองรับ** ในภูมิภาค **Switzerland West** และ **West Central US**

**Outbound:** _Managed Private Endpoints_ ไม่สามารถใช้งานได้ใน _Fabric workspaces_ ที่ผูกกับ _capacity_ ในภูมิภาค **Switzerland West** และ **West Central US**

**Inbound:** หาก _workspaces_ ผูกกับ _Fabric capacities_ ในภูมิภาคเหล่านี้ และ _tenant_ มีการเปิดใช้งาน _Private Link setting_ งาน _Data Engineering_ ที่เริ่มจาก _notebooks_, _Spark job definitions_ และ _Lakehouse operations_ จะเกิดข้อผิดพลาด

## How to enable managed virtual networks for a Fabric workspace

_Managed virtual networks_ จะถูกสร้างขึ้นอัตโนมัติให้กับ _Fabric workspace_ เมื่อเกิดเหตุการณ์ใดเหตุการณ์หนึ่งต่อไปนี้:

- มีการเพิ่ม **Managed private endpoints** เพื่อให้สามารถเข้าถึงระบบภายนอก (_outbound_) ได้อย่างปลอดภัย  
  ผู้ดูแล _workspace_ สามารถสร้างหรือลบ _managed private endpoint connections_ ได้จากเมนู _workspace settings_ ภายใน _Fabric workspace_

  ![Animated illustration of the process of creating a private endpoint in Microsoft Fabric.](https://learn.microsoft.com/en-us/fabric/security/media/security-managed-vnets-fabric-overview/creating-private-endpoint-animation.gif)

  อ่านเพิ่มเติมได้ที่ [About managed private endpoints in Fabric](https://learn.microsoft.com/en-us/fabric/security/security-managed-private-endpoints-overview)

- มีการเปิดใช้ **Private Link** ซึ่งให้การป้องกันเครือข่ายขาเข้า (_inbound_) และมีการรัน _Spark job_ ภายใน _Fabric workspace_  
  ผู้ดูแล _tenant_ สามารถเปิดใช้ _Private Link setting_ ได้จาก [Admin portal](https://learn.microsoft.com/en-us/fabric/admin/tenant-settings-index#advanced-networking)

  เมื่อเปิดใช้ _Private Link setting_ แล้ว การรัน _Spark job_ ครั้งแรก (ไม่ว่าจะเป็น _Notebook_ หรือ _Spark job definition_) หรือการดำเนินการบน _Lakehouse_ เช่น _Load to Table_, _Optimize_ หรือ _Vacuum_ จะทำให้ระบบสร้าง _managed virtual network_ สำหรับ _workspace_ โดยอัตโนมัติ

  อ่านเพิ่มเติมได้ที่ [configuring Private Links for Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/security/security-private-links-overview)

> **หมายเหตุ**  
> _Managed virtual network_ จะถูกสร้างโดยอัตโนมัติในขั้นตอนการส่งงาน _Spark_ ครั้งแรกใน _workspace_  
> เมื่อมีการสร้าง _managed virtual network_ แล้ว ตัวเลือก _starter pools_ (คลัสเตอร์แบบ _default compute_ ที่พร้อมใช้งานทันที) จะถูกปิดใช้งาน  
> งาน _Spark_ จะรันบน _custom pools_ ที่สร้างขึ้นแบบ _on-demand_ ภายใน _dedicated managed virtual network_ ของ _workspace_ ซึ่งอาจใช้เวลาประมาณ 3 ถึง 5 นาทีในการเริ่มต้น _Spark session_