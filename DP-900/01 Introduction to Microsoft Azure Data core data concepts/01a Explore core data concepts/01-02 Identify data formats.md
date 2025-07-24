
_ข้อมูล_ คือการรวบรวมข้อเท็จจริง เช่น ตัวเลข คำบรรยาย หรือสิ่งที่สังเกตได้ ซึ่งถูกใช้เพื่อบันทึกข้อมูลต่าง ๆ โครงสร้างของ _ข้อมูล_ มักจะถูกจัดเรียงในรูปแบบที่แสดงถึง _entities_ หรือสิ่งที่มีความสำคัญต่อองค์กร (เช่น _ลูกค้า_, _สินค้า_, _คำสั่งซื้อ_ เป็นต้น) แต่ละ _entity_ จะมี _attributes_ หรือคุณลักษณะ เช่น ลูกค้าอาจมีชื่อ ที่อยู่ และเบอร์โทรศัพท์

เราสามารถแบ่งประเภทของ _ข้อมูล_ ได้เป็น 3 ประเภท ได้แก่ _structured_, _semi-structured_ และ _unstructured_

## Structured data

_structured data_ คือ _ข้อมูล_ ที่มีโครงสร้างตายตัวหรือมี _schema_ กำหนดไว้ล่วงหน้า ซึ่งหมายความว่า _ข้อมูล_ ทุกชุดจะมีฟิลด์หรือคุณสมบัติที่เหมือนกันเสมอ โดยทั่วไปแล้ว _schema_ ของ _structured data_ มักอยู่ในรูปแบบ _tabular_ หรือ ตาราง กล่าวคือ _ข้อมูล_ จะถูกจัดเก็บในตารางที่มีแถว (rows) เพื่อแทนแต่ละรายการของ _data entity_ และมีคอลัมน์ (columns) เพื่อแทน _attributes_ ของ entity นั้น

ตัวอย่างเช่น ตาราง _Customer_ และ _Product_ ที่แสดง _ข้อมูล_ แต่ละรายการพร้อมคุณลักษณะต่าง ๆ

![Diagram showing how structured data is represented in tables.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-core-data-concepts/media/2-tabular-diagram.png)

_structured data_ มักถูกจัดเก็บใน _database_ ซึ่งสามารถมีหลายตาราง และแต่ละตารางสามารถเชื่อมโยงกันได้โดยใช้ค่า _key_ ตามรูปแบบที่เรียกว่า _relational model_ ซึ่งเราจะเรียนรู้เพิ่มเติมในหัวข้อต่อไป

## Semi-structured data

_semi-structured data_ คือ _ข้อมูล_ ที่มีโครงสร้างบางส่วน แต่ยืดหยุ่นให้มีความแตกต่างกันได้ในแต่ละ _entity instance_ เช่น ลูกค้าส่วนใหญ่อาจมี _email address_ แต่บางคนอาจมีหลายอีเมล หรือบางคนอาจไม่มีเลยก็ได้

รูปแบบที่พบได้บ่อยสำหรับ _semi-structured data_ คือ _JavaScript Object Notation_ หรือ _JSON_ ตัวอย่างด้านล่างเป็นเอกสาร JSON สองรายการที่แสดงข้อมูลของลูกค้า ซึ่งแต่ละรายการจะมีข้อมูลที่อยู่และการติดต่อ แต่ฟิลด์ที่ใช้ในแต่ละคนอาจแตกต่างกัน


```json
// Customer 1
{
  "firstName": "Joe",
  "lastName": "Jones",
  "address":
  {
    "streetAddress": "1 Main St.",
    "city": "New York",
    "state": "NY",
    "postalCode": "10099"
  },
  "contact":
  [
    {
      "type": "home",
      "number": "555 123-1234"
    },
    {
      "type": "email",
      "address": "joe@litware.com"
    }
  ]
}

// Customer 2
{
  "firstName": "Samir",
  "lastName": "Nadoy",
  "address":
  {
    "streetAddress": "123 Elm Pl.",
    "unit": "500",
    "city": "Seattle",
    "state": "WA",
    "postalCode": "98999"
  },
  "contact":
  [
    {
      "type": "email",
      "address": "samir@northwind.com"
    }
  ]
}

```

 _หมายเหตุ_

_JSON_ เป็นเพียงหนึ่งในหลายวิธีที่ใช้ในการแสดง _semi-structured data_ จุดสำคัญของเนื้อหานี้ไม่ใช่การลงรายละเอียดเรื่องไวยากรณ์ของ JSON แต่ต้องการแสดงให้เห็นว่า _semi-structured data_ มีความยืดหยุ่นในการจัดเก็บและแสดงข้อมูลอย่างไร

## Unstructured data

ไม่ใช่ทุก _ข้อมูล_ จะเป็น _structured_ หรือแม้แต่ _semi-structured_ เช่น เอกสาร รูปภาพ ไฟล์เสียง วิดีโอ และไฟล์ไบนารี มักจะไม่มีโครงสร้างที่ชัดเจน _ข้อมูล_ ประเภทนี้เรียกว่า _unstructured data_

![Diagram showing unstructured data in documents.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-core-data-concepts/media/2-unstructured-data.png)

## Data stores

องค์กรส่วนใหญ่จะจัดเก็บ _ข้อมูล_ ในรูปแบบ _structured_, _semi-structured_ หรือ _unstructured_ เพื่อใช้บันทึกรายละเอียดของ _entities_ เช่น _ลูกค้า_ หรือ _สินค้า_ รวมถึงเหตุการณ์ต่าง ๆ เช่น _ธุรกรรมการขาย_ หรือข้อมูลอื่น ๆ ที่อยู่ในรูปแบบเอกสาร รูปภาพ และไฟล์ประเภทอื่น ๆ โดย _ข้อมูล_ เหล่านี้สามารถนำกลับมาใช้งานเพื่อการ _วิเคราะห์_ และ _รายงานผล_ ได้ในภายหลัง

รูปแบบการจัดเก็บข้อมูลหลักที่ใช้งานทั่วไปมีอยู่ 2 ประเภทคือ

- _file stores_
- _databases_

เราจะเรียนรู้เพิ่มเติมเกี่ยวกับรูปแบบการจัดเก็บข้อมูลทั้งสองประเภทนี้ในหัวข้อถัดไป