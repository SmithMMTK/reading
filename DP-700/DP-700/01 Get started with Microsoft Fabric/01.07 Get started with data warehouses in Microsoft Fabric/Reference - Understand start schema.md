
บทความนี้มุ่งเน้นที่ _Power BI Desktop data modelers_ โดยอธิบายการออกแบบ _star schema_ และความสำคัญในการพัฒนา _Power BI semantic models_ ที่ปรับแต่งเพื่อให้มีประสิทธิภาพและใช้งานได้ง่าย

> **สำคัญ**
>
> _Power BI semantic models_ ต้องใช้ _[Power Query](https://learn.microsoft.com/en-us/power-query/power-query-what-is-power-query)_ ในการนำเข้าหรือเชื่อมต่อกับข้อมูล หมายความว่าคุณต้องใช้ Power Query เพื่อแปลงและเตรียมข้อมูลต้นทาง ซึ่งอาจเป็นเรื่องท้าทายเมื่อคุณมีข้อมูลปริมาณมากหรือจำเป็นต้องใช้แนวคิดขั้นสูง เช่น _slowly changing dimensions_ (อธิบายไว้ [ภายหลังในบทความนี้](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema#slowly-changing-dimensions))

เมื่อเจอความท้าทายเช่นนี้ ขอแนะนำให้คุณสร้าง _data warehouse_ และกระบวนการ _Extract, Transform, and Load (ETL)_ เพื่อนำข้อมูลเข้าแบบเป็นระยะ จากนั้นโมเดลเชิงความหมายของคุณจะสามารถเชื่อมต่อกับ data warehouse ได้ ดูข้อมูลเพิ่มเติมได้ที่ [Dimensional modeling in Microsoft Fabric Warehouse](https://learn.microsoft.com/en-us/fabric/data-warehouse/dimensional-modeling-overview)

> **เคล็ดลับ**
>
> บทความนี้ไม่ได้ให้คำอธิบายครบถ้วนเกี่ยวกับการออกแบบ _star schema_ หากต้องการศึกษาลึกเพิ่มเติม แนะนำให้ดูหนังสือ _The Data Warehouse Toolkit: The Definitive Guide to Dimensional Modeling_ (ฉบับที่ 3 ปี 2013) โดย Ralph Kimball

## Star schema overview

_star schema_ เป็นแนวทางการออกแบบที่เป็นที่ยอมรับอย่างกว้างขวางในระบบฐานข้อมูลแบบสัมพันธ์ (_relational data warehouses_) ซึ่งจำเป็นต้องจัดประเภท _tables_ ให้เป็น _dimension_ หรือ _fact_

### Dimension tables

_dimension tables_ อธิบาย _business entities_ หรือ _สิ่งต่าง ๆ_ ที่คุณต้องการทำโมเดล เช่น สินค้า บุคคล สถานที่ หรือแนวคิดต่าง ๆ รวมถึง _เวลา_ ซึ่งเป็น table ที่พบได้บ่อยใน star schema โดยแต่ละ _dimension table_ จะมีคอลัมน์ _key_ (หรือหลายคอลัมน์) เพื่อระบุแถวอย่างเฉพาะเจาะจง พร้อมคอลัมน์อื่น ๆ สำหรับการกรองและจัดกลุ่มข้อมูล

### Fact tables

_fact tables_ ใช้เก็บข้อมูลเหตุการณ์หรือ _observations_ เช่น คำสั่งซื้อสินค้า ยอดคงเหลือ อัตราแลกเปลี่ยน หรืออุณหภูมิ ประกอบด้วยคีย์ที่เชื่อมโยงไปยัง _dimension tables_ และคอลัมน์เชิงตัวเลข (_measures_) คีย์ของ dimension ระบุ _dimensionality_ ขณะที่ค่าคีย์เหล่านี้ระบุ _granularity_ เช่น ตารางยอดขายที่มีคอลัมน์ `Date` และ `ProductKey` มี 2 มิติ แต่ _granularity_ จะขึ้นอยู่กับค่าของ `Date` ว่าเก็บรายวันหรือรายเดือน

โดยทั่วไป _dimension tables_ มีจำนวนแถวน้อย ส่วน _fact tables_ มีจำนวนแถวมากและเติบโตต่อเนื่องตามเวลา

![Diagram showing an illustration of a star schema.](https://learn.microsoft.com/en-us/power-bi/guidance/media/star-schema/star-schema-example-1.svg)

## Normalization vs. denormalization

เพื่อให้เข้าใจ _star schema_ จำเป็นต้องรู้ความแตกต่างระหว่าง _normalization_ และ _denormalization_

_normalization_ คือการจัดเก็บข้อมูลเพื่อลดความซ้ำซ้อน เช่น ตารางสินค้าเก็บเฉพาะ `ProductKey` และรายละเอียดสินค้าไว้ในตารางแยก ส่วนตารางยอดขายจะเก็บเฉพาะ `ProductKey`

![Diagram showing a table of data that includes a Product Key column.](https://learn.microsoft.com/en-us/power-bi/guidance/media/star-schema/normalized-data-example.svg)

แต่ถ้าตารางยอดขายเก็บข้อมูลสินค้าไว้เลย (เช่น ชื่อ หมวด สี ขนาด) จะเรียกว่า _denormalized_

![Diagram showing a table of data that includes a Product Key and other product-related columns.](https://learn.microsoft.com/en-us/power-bi/guidance/media/star-schema/denormalized-data-example.svg)

หากคุณได้ข้อมูลจากไฟล์ export ข้อมูลมักจะอยู่ในรูปแบบ _denormalized_ จึงควรใช้ _[Power Query](https://learn.microsoft.com/en-us/training/modules/clean-data-power-bi/)_ เพื่อแปลงเป็นตารางแบบ normalized

แม้ในบทความนี้จะแนะนำให้ใช้ _normalized fact_ และ _dimension tables_ แต่บางกรณีอาจใช้ _[snowflake dimension](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema#snowflake-dimensions)_ ที่ถูก _denormalized_ เพื่อรวมเป็นตารางเดียว

## Star schema relevance to Power BI semantic models

การออกแบบ _star schema_ มีความสำคัญต่อประสิทธิภาพและความสามารถในการใช้งานของ _Power BI semantic model_

แต่ละ visual ใน Power BI จะสร้าง query ที่กรอง จัดกลุ่ม และสรุปข้อมูล ดังนั้น โมเดลที่ออกแบบมาดีควรมีตารางสำหรับ _filtering_ และ _grouping_ (มาจาก _dimension tables_) และตารางสำหรับ _summarizing_ (มาจาก _fact tables_)

ไม่มีการตั้งค่าที่ระบุว่าตารางใดเป็น _dimension_ หรือ _fact_ แต่จะพิจารณาจากความสัมพันธ์ (_model relationships_) โดย _one-to-many_ หมายถึงฝั่ง "one" คือ _dimension table_ และฝั่ง "many" คือ _fact table_

![Diagram showing a conceptual illustration of a star schema.](https://learn.microsoft.com/en-us/power-bi/guidance/media/star-schema/star-schema-example-2.svg)

โมเดลที่ดีควรแยก _dimension_ และ _fact_ ออกจากกัน ไม่ควรผสมอยู่ในตารางเดียว และควรกำหนด _relationships_ อย่างเหมาะสม รวมถึง _fact tables_ ควรมี _granularity_ ที่คงที่

การออกแบบโมเดลที่ดีนั้นผสมผสานระหว่าง _ศาสตร์_ และ _ศิลป์_ บางกรณีสามารถเบี่ยงเบนจากแนวปฏิบัติได้หากเหมาะสม

แนวคิดที่เกี่ยวข้องกับ _star schema_ ที่ใช้กับ Power BI ได้แก่:

- [Measures](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema#measures)
- [Surrogate keys](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema#surrogate-keys)
- [Snowflake dimensions](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema#snowflake-dimensions)
- [Role-playing dimensions](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema#role-playing-dimensions)
- [Slowly changing dimensions](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema#slowly-changing-dimensions)
- [Junk dimensions](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema#junk-dimensions)
- [Degenerate dimensions](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema#degenerate-dimensions)
- [Factless fact tables](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema#factless-fact-tables)
