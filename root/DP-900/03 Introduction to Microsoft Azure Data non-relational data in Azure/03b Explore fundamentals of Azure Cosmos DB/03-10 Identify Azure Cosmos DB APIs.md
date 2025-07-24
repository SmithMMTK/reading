
_Azure Cosmos DB_ เป็นบริการฐานข้อมูลแบบ _fully managed_ และ _serverless_ ของ Microsoft ที่ออกแบบมาสำหรับแอปพลิเคชันทุกขนาด ไม่ว่าจะเล็กหรือใหญ่ และรองรับทั้ง _relational_ และ _non-relational workloads_

นักพัฒนาสามารถสร้างหรือย้ายแอปพลิเคชันมายัง _Cosmos DB_ ได้อย่างรวดเร็ว โดยใช้ _open source database engine_ ที่คุ้นเคย เช่น _PostgreSQL_, _MongoDB_, และ _Apache Cassandra_

เมื่อคุณสร้าง _Cosmos DB instance_ ใหม่ จะต้องเลือก _database engine_ ที่ต้องการใช้ โดยการเลือกขึ้นอยู่กับหลายปัจจัย เช่น ประเภทของข้อมูลที่จะจัดเก็บ ความจำเป็นในการรองรับแอปเดิมที่มีอยู่ และทักษะของนักพัฒนาที่จะทำงานกับระบบฐานข้อมูลนั้น

## Azure Cosmos DB for NoSQL

_Azure Cosmos DB for NoSQL_ เป็นบริการ _non-relational_ แบบดั้งเดิมของ Microsoft ที่ใช้สำหรับจัดการข้อมูลในรูปแบบ _document model_ โดยข้อมูลจะถูกจัดเก็บในรูปแบบ _JSON document_

แม้จะเป็นระบบจัดเก็บข้อมูลแบบ _NoSQL_ แต่ _Cosmos DB_ ก็สามารถใช้คำสั่งที่มีลักษณะเหมือน _SQL_ เพื่อ _query_ ข้อมูลได้
#dp-900-key 

ตัวอย่าง _SQL query_ สำหรับ _Cosmos DB_ ที่เก็บข้อมูลลูกค้า อาจมีหน้าตาแบบนี้:

```sql
SELECT *
FROM customers c
WHERE c.id = "joe@litware.com"
```

ผลลัพธ์จาก _query_ นี้จะอยู่ในรูปแบบของ _JSON documents_ หนึ่งฉบับหรือมากกว่านั้น เช่น:

```json
{
   "id": "joe@litware.com",
   "name": "Joe Jones",
   "address": {
        "street": "1 Main St.",
        "city": "Seattle"
    }
}
```

## Azure Cosmos DB for MongoDB

_MongoDB_ เป็นฐานข้อมูลแบบ _open source_ ที่ได้รับความนิยมสูง ซึ่งจัดเก็บข้อมูลในรูปแบบ _Binary JSON (BSON)_

_Azure Cosmos DB for MongoDB_ ช่วยให้นักพัฒนาสามารถใช้ไลบรารีและโค้ดของ MongoDB ที่คุ้นเคยในการทำงานกับข้อมูลบน _Cosmos DB_ ได้โดยไม่ต้องเปลี่ยนแปลงมาก

_MongoDB Query Language (MQL)_ ใช้ไวยากรณ์ที่กระชับและมีลักษณะเชิงวัตถุ (_object-oriented_) โดยนักพัฒนาจะใช้ _object_ เรียกใช้ _method_ เช่นคำสั่งนี้ใช้ _method_ **find** เพื่อค้นหาข้อมูลจาก _collection_ ชื่อ **products** ใน _object_ ชื่อ **db**:

```javascript
db.products.find({id: 123})
```

ผลลัพธ์จาก _query_ นี้จะอยู่ในรูปแบบ _JSON documents_ คล้ายตัวอย่างต่อไปนี้:

```json
{
   "id": 123,
   "name": "Hammer",
   "price": 2.99
}
```

## Azure Cosmos DB for PostgreSQL

_Azure Cosmos DB for PostgreSQL_ เป็นตัวเลือก _PostgreSQL_ แบบกระจาย (distributed) บน _Azure_ ซึ่งรองรับการทำงานแบบ _relational_ และถูกออกแบบให้สามารถกระจายข้อมูล (_shard_) ได้โดยอัตโนมัติ เพื่อช่วยให้คุณสร้างแอปที่ _scalable_ ได้อย่างง่ายดาย

คุณสามารถเริ่มต้นพัฒนาแอปบน _single node server group_ ได้เหมือนกับการใช้งาน _PostgreSQL_ ปกติ และเมื่อแอปของคุณต้องการขยายประสิทธิภาพหรือรองรับผู้ใช้จำนวนมากขึ้น ก็สามารถขยายไปยัง _multiple nodes_ ได้โดยการกระจาย _table_ แบบโปร่งใส (_transparently_)

_PostgreSQL_ เป็นระบบ _relational database management system (RDBMS)_ ที่ให้คุณนิยาม _relational table_ เช่น ถ้าคุณต้องการเก็บข้อมูลสินค้า ก็อาจสร้าง _table_ แบบนี้:

|ProductID|ProductName|Price|
|---|---|---|
|123|Hammer|2.99|
|162|Screwdriver|3.49|

คุณสามารถใช้ _SQL query_ เพื่อดึงข้อมูลชื่อและราคาของสินค้ารายการใดรายการหนึ่งจาก _table_ นี้ได้ เช่น:

```sql
SELECT ProductName, Price 
FROM Products
WHERE ProductID = 123;
```

ผลลัพธ์ของ _query_ นี้จะมีหนึ่งแถวสำหรับสินค้าที่มี _id_ เท่ากับ 123 โดยแสดงในรูปแบบตาราง เช่น:

|ProductName|Price|
|---|---|
|Hammer|2.99|

## Azure Cosmos DB for Table

_Azure Cosmos DB for Table_ ใช้สำหรับทำงานกับข้อมูลในรูปแบบ _key-value table_ ซึ่งคล้ายกับการใช้งาน _Azure Table Storage_ แต่ให้ _scalability_ และ _performance_ ที่ดีกว่าอย่างชัดเจน

ตัวอย่างเช่น คุณอาจนิยาม _table_ ชื่อว่า **Customers** โดยแต่ละแถวจะมีคีย์หลัก (_primary key_) ซึ่งประกอบด้วย _PartitionKey_ และ _RowKey_ พร้อมกับฟิลด์ข้อมูลอื่น ๆ เช่น:

|PartitionKey|RowKey|Name|Email|
|---|---|---|---|
|1|123|Joe Jones|joe@litware.com|
|1|124|Samir Nadoy|samir@northwind.com|

You can then use the Table API through one of the language-specific SDKs to make calls to your service endpoint to retrieve data from the table. For example, the following request returns the row containing the record for _Samir Nadoy_ in the previous table:

คุณสามารถใช้ _Table API_ ผ่าน _SDK_ ที่รองรับภาษาต่าง ๆ เพื่อเรียกข้อมูลจาก _table_ ผ่าน _service endpoint_ ได้โดยตรง

ตัวอย่างเช่น หากต้องการดึงแถวของ _Samir Nadoy_ จาก _table_ ที่มีโครงสร้างคล้ายตัวอย่างก่อนหน้า

```text
https://endpoint/Customers(PartitionKey='1',RowKey='124')
```

## Azure Cosmos DB for Apache Cassandra

_Azure Cosmos DB for Apache Cassandra_ รองรับการทำงานร่วมกับ _Apache Cassandra_ ซึ่งเป็นฐานข้อมูล _open source_ ที่ได้รับความนิยม และใช้โครงสร้างแบบ _column-family storage_

_Column family_ คือ _table_ ที่คล้ายกับในระบบ _relational_ แต่มีความยืดหยุ่นมากกว่า เพราะแต่ละแถวไม่จำเป็นต้องมีคอลัมน์เหมือนกันทั้งหมด

ตัวอย่างเช่น คุณอาจสร้าง _table_ ชื่อ **Employees** ได้แบบนี้:

|ID|Name|Manager|
|---|---|---|
|1|Sue Smith||
|2|Ben Chan|Sue Smith|

_Cassandra_ รองรับไวยากรณ์ที่คล้ายกับ _SQL_ ดังนั้นแอปพลิเคชันฝั่งลูกข่ายสามารถใช้คำสั่งเพื่อดึงข้อมูลของ _Ben Chan_ ได้แบบนี้:

```sql
SELECT * FROM Employees WHERE ID = 2
```

## Azure Cosmos DB for Apache Gremlin

_Azure Cosmos DB for Apache Gremlin_ ใช้สำหรับจัดการข้อมูลในรูปแบบ _graph structure_ ซึ่งเหมาะกับข้อมูลที่มีความสัมพันธ์กันซับซ้อน

ใน _graph_ ข้อมูลจะถูกจัดเก็บเป็น _vertices_ (จุดยอด) ซึ่งเป็น _node_ หรือสิ่งที่มีตัวตน เช่น คน สินค้า หรือสถานที่ และเชื่อมต่อกันด้วย _edges_ ซึ่งแทนความสัมพันธ์ระหว่าง _node_ เช่น “เป็นเพื่อนกับ” หรือ “ซื้อ”

ตัวอย่างเช่น:

![A graph showing employees and departments and the connections between them](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-non-relational-data-stores-azure/media/graph.png)

ตัวอย่างในภาพแสดงให้เห็น _vertex_ สองประเภท ได้แก่ _employee_ และ _department_ พร้อมกับ _edge_ ที่เชื่อมโยงพวกเขา เช่น พนักงานชื่อ "Ben" รายงานต่อพนักงานชื่อ "Sue" และทั้งคู่ทำงานอยู่ในแผนก "Hardware" 

ไวยากรณ์ของ _Gremlin_ มีฟังก์ชันที่ใช้จัดการกับ _vertex_ และ _edge_ เช่น การ _insert_, _update_, _delete_ และ _query_ ข้อมูลใน _graph_

ตัวอย่างเช่น ถ้าต้องการเพิ่มพนักงานใหม่ชื่อ _Alice_ ที่รายงานต่อพนักงานที่มี _id_ เป็น **1** (ซึ่งคือ _Sue_) สามารถใช้คำสั่งแบบนี้:

```apache
g.addV('employee').property('id', '3').property('firstName', 'Alice')
g.V('3').addE('reports to').to(g.V('1'))
```

คำสั่ง _Gremlin_ ต่อไปนี้จะ _query_ ข้อมูลพนักงานทั้งหมด (_employee vertices_) และเรียงตาม _id_:

```apache
 g.V().hasLabel('employee').order().by('id')
```
