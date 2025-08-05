
คุณสามารถใช้ _Private Links_ เพื่อให้การเข้าถึงข้อมูลใน _Fabric_ มีความปลอดภัย โดยใช้ _Azure Private Link_ และ _Azure Networking private endpoints_ ในการส่งข้อมูลผ่านโครงสร้างพื้นฐานเครือข่ายของ _Microsoft_ (_Microsoft backbone network_) แทนการส่งผ่าน _internet_

เมื่อมีการใช้ _private link_ การเชื่อมต่อของผู้ใช้ _Fabric_ จะผ่าน _Microsoft private network backbone_ เท่านั้น

## What is a private endpoint?

_private endpoint_ รับประกันว่าการส่งข้อมูลเข้า (_into_) ไปยังทรัพยากรของ _Fabric_ (เช่น การอัปโหลดไฟล์ไปยัง _OneLake_) จะต้องเป็นไปตามเส้นทาง _private link_ ที่องค์กรกำหนดเท่านั้น โดยคุณสามารถตั้งค่าให้ _Fabric_ ปฏิเสธคำขอทั้งหมดที่ไม่ได้มาจากเส้นทางนี้

อย่างไรก็ตาม _private endpoint_ ไม่ได้รับประกันความปลอดภัยของข้อมูลที่ออกจาก _Fabric_ ไปยังแหล่งข้อมูลภายนอก (ทั้งบนคลาวด์หรือภายในองค์กร) คุณควรตั้งค่า _firewall rules_ และ _virtual networks_ เพิ่มเติมเพื่อความปลอดภัยของแหล่งข้อมูล

_private endpoint_ เป็นเทคโนโลยีแบบทางเดียว ที่อนุญาตให้ _client_ เชื่อมต่อกับบริการ แต่ไม่อนุญาตให้บริการเชื่อมต่อกลับเข้าไปยังเครือข่ายลูกค้า รูปแบบนี้ช่วยแยกการจัดการระหว่างบริการและนโยบายของลูกค้า โดยเฉพาะในบริการแบบ _multitenant_ ที่สามารถแยกการเข้าถึงระหว่างลูกค้าแต่ละรายได้ด้วย _link identifiers_

_Fabric_ ใช้ _private endpoints_ เท่านั้น ไม่ได้ใช้ _service endpoints_

**ข้อดีของการใช้ private endpoints กับ Fabric:**

- จำกัดการเข้าถึงจาก _internet_ และเปลี่ยนเส้นทางไปยัง _Microsoft backbone_
- รับประกันว่าเฉพาะเครื่องลูกค้าที่ได้รับอนุญาตเท่านั้นที่เข้าถึง _Fabric_ ได้
- รองรับข้อกำหนดด้านกฎระเบียบและความปลอดภัยที่ต้องการการเข้าถึงแบบส่วนตัว

## Understand private endpoint configuration

มี 2 ค่าการตั้งค่าใน _Fabric admin portal_ สำหรับกำหนดค่า _Private Link_ ได้แก่:

- **Azure Private Links**
- **Block Public Internet Access**

**กรณีที่เปิดใช้งาน Azure Private Link และเปิด Block Public Internet Access:**

- _Fabric items_ ที่รองรับจะเข้าถึงได้เฉพาะผ่าน _private endpoints_ ภายในองค์กรเท่านั้น
- การรับส่งข้อมูลจาก _virtual network_ ไปยัง _endpoints_ ที่รองรับ _private link_ จะใช้เส้นทาง _private link_
- _Endpoints_ หรือ _scenarios_ ที่ไม่รองรับ _private link_ จะถูกบล็อกโดย _Fabric service_

**กรณีที่เปิดใช้งาน Azure Private Link และไม่เปิด Block Public Internet Access:**

- _Fabric_ จะอนุญาตการเข้าถึงจาก _internet_
- การเชื่อมต่อจาก _virtual network_ ที่รองรับ _private link_ จะวิ่งผ่าน _private link_
- การเชื่อมต่อที่ไม่รองรับ _private link_ จะใช้ _internet_ และยังสามารถใช้งานได้
- หาก _virtual network_ ถูกตั้งค่าให้บล็อก _internet_ อยู่แล้ว กรณีที่ไม่รองรับ _private link_ จะใช้งานไม่ได้

## Private Link in Fabric experiences

### OneLake

_OneLake_ รองรับ _Private Link_ คุณสามารถใช้งานผ่าน _Fabric portal_, _OneLake File Explorer_, _Azure Storage Explorer_, _PowerShell_ และอื่น ๆ ภายใน _virtual network_ ที่ตั้งค่าไว้

**หมายเหตุ:** การเรียกผ่าน _OneLake regional endpoints_ จะไม่ทำงานผ่าน _private link_

### Warehouse และ Lakehouse SQL analytics endpoint

รองรับ _private link_ ทั้งในการเข้าถึงผ่าน _portal_ และ _TDS endpoint_ (เช่น _SSMS_, _Azure Data Studio_)

**Visual query ใน Warehouse จะไม่ทำงาน** หากเปิดใช้ **Block Public Internet Access**

### SQL database

รองรับ _private link_ ทั้งใน _portal_ และ _TDS endpoint_ เช่น _SSMS_, _VS Code_

### Lakehouse, Notebook, Spark job definition, Environment

การรัน _Spark job_ หรือการใช้งาน _Lakehouse operations_ จะสร้าง _managed virtual network_ และยกเลิก _starter pool_ (คลัสเตอร์ที่แชร์กันล่วงหน้า) โดย _Spark job_ จะใช้ _custom pool_ ที่สร้างขึ้นในขณะรันงาน

หากภูมิภาคของ _tenant_ ไม่รองรับ _Fabric Data Engineering_ งาน _Spark_ จะไม่สามารถทำงานได้

### Dataflow Gen2

สามารถใช้งาน _Dataflow gen2_ ผ่าน _private link_ และเชื่อมต่อแหล่งข้อมูลหลัง _firewall_ ด้วย _VNet data gateway_

### Pipeline

สามารถโหลดข้อมูลจากแหล่งข้อมูลที่มี _public endpoint_ เข้า _lakehouse_ ได้ และสามารถใช้งานกิจกรรมต่าง ๆ เช่น _Notebook_, _Dataflow_ ผ่าน _private link_

**แต่ไม่สามารถ copy ข้อมูลจากหรือไปยัง Data Warehouse ได้**

### ML Model, Experiment, Data agent

รองรับ _private link_

### Power BI

- _Publish to Web_, _Email subscriptions_, _Export เป็น PDF/PowerPoint_ ไม่รองรับ
- หากมีการเปิดใช้งาน _Azure Private Link_ รายงานการใช้งาน (_usage metrics_) จะแสดงผลได้เพียงบางส่วน
- _Copilot_ ยังไม่รองรับ _Private Link_

### Eventhouse

รองรับการ ingest และ query ข้อมูลอย่างปลอดภัยผ่าน _private link_

**ข้อจำกัด:**

- ingest จาก _OneLake_ ไม่ได้
- สร้าง _shortcut_, ใช้งานกับ _pipeline_, หรือ _T-SQL_ ไม่ได้
- ไม่รองรับการ ingest แบบ _queued_

### Healthcare data solutions (preview)

สามารถใช้งานผ่าน _Private Link_ ได้เต็มรูปแบบภายใน _tenant_ ที่เปิดใช้งาน

**หมายเหตุ:** บริการบางอย่าง เช่น _Eventstream_ จะถูกปิดใช้งานโดยอัตโนมัติหากเปิด Block Public Internet Access

### Microsoft Purview Information Protection

ยังไม่รองรับ _Private Link_

- ปุ่ม _Sensitivity_ ใน _Power BI Desktop_ จะใช้งานไม่ได้
- _Label_ ไม่แสดง และ _pbix_ ถอดรหัสไม่ได้

ผู้ดูแลระบบสามารถใช้ _service tags_ เพื่อเปิดการเข้าถึงบริการเบื้องหลังได้ เช่น _EOP_, _AIP_

## Other considerations and limitations

- รองรับสูงสุด 450 _capacities_ ต่อ _tenant_
- _Capacity_ ใหม่อาจใช้เวลา 24 ชม. กว่าจะรองรับ _private link_
- ไม่สามารถ _tenant migration_ ได้หากเปิด _Private Link_
- ไม่สามารถเชื่อมต่อหลาย _tenants_ จาก _network location_ เดียวกันได้
- ไม่รองรับ _trial capacity_
- ไม่สามารถใช้ภาพหรือธีมจากภายนอก
- _private endpoint_ เชื่อมได้กับ _tenant_ เดียวเท่านั้น
- **สำหรับ Fabric users:** _on-premises data gateway_ ไม่รองรับ ต้องใช้ _VNet data gateway_
- ไม่รองรับ _diagnostics_ ของ _VNet Data Gateway_
- _Capacity Metrics app_ ไม่รองรับ
- _REST APIs_ ของ _Private Links_ ไม่รองรับ _tags_

**URLs ที่ต้องเปิดให้เข้าถึงได้จาก browser:**

_สำหรับ auth:_
- `login.microsoftonline.com`
- `aadcdn.msauth.net`
- `msauth.net`
- `msftauth.net`
- `graph.microsoft.com`
- `login.live.com`

_สำหรับ Data Engineering / Data Science:_
- `http://res.cdn.office.net/`
- `https://aznbcdn.notebooks.azure.net/`
- `https://pypi.org/*`
- _local static endpoints สำหรับ condaPackages_
- `https://cdn.jsdelivr.net/npm/monaco-editor*`