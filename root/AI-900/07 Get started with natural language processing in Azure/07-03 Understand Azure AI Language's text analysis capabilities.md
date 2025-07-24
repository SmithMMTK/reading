
_Azure AI Language_ เป็นส่วนหนึ่งของบริการ _Azure AI_ ที่สามารถประมวลผล _natural language processing_ ขั้นสูงบนข้อความที่ไม่มีโครงสร้าง (_unstructured text_) ได้

ความสามารถในการวิเคราะห์ข้อความของ _Azure AI Language_ รวมถึง:

- _named entity recognition_ – ตรวจจับชื่อของ _บุคคล_, _สถานที่_, _เหตุการณ์_ และอื่น ๆ อีกมาก และยังสามารถปรับแต่งให้ตรวจจับ _หมวดหมู่เฉพาะ_ ที่เราต้องการได้  
- _entity linking_ – ระบุ _เอนทิตี_ ที่รู้จักพร้อมลิงก์ไปยังแหล่งข้อมูล เช่น Wikipedia  
- _personal identifying information (PII) detection_ – ตรวจจับข้อมูลส่วนบุคคลที่อ่อนไหว เช่น _ข้อมูลสุขภาพส่วนบุคคล (PHI)_  
- _language detection_ – ตรวจจับภาษาในข้อความ พร้อมคืนค่ารหัสภาษา เช่น `"en"` สำหรับภาษาอังกฤษ  
- _sentiment analysis_ และ _opinion mining_ – วิเคราะห์ว่าเนื้อความมีอารมณ์ _แง่บวก_, _แง่ลบ_ หรือเป็นกลาง  
- _summarization_ – สรุปข้อความโดยดึงสาระสำคัญที่สำคัญที่สุด  
- _key phrase extraction_ – ดึงแนวคิดหลักหรือคำสำคัญจากข้อความที่ไม่มีโครงสร้าง

ต่อไปเราจะมาดูรายละเอียดของแต่ละฟีเจอร์อย่างใกล้ชิดมากขึ้น

## Entity recognition and linking

คุณสามารถส่ง _ข้อความที่ไม่มีโครงสร้าง_ (_unstructured text_) ให้กับ _Azure AI Language_ และมันจะส่งกลับมาเป็น _รายการของ entity_ ที่มันสามารถตรวจจับได้จากข้อความนั้น

_entity_ คือ _สิ่งของ_ หรือ _รายการ_ ที่อยู่ในประเภทหนึ่ง ๆ หรือ _หมวดหมู่_ ที่เฉพาะเจาะจง และในบางกรณีอาจมี _ประเภทย่อย_ ด้วย เช่น:

| Type                  | SubType     | Example                         |
| --------------------- | ----------- | ------------------------------- |
| Person                |             | "Bill Gates", "John"            |
| Location              |             | "Paris", "New York"             |
| Organization          |             | "Microsoft"                     |
| Quantity              | Number      | "6" or "six"                    |
| Quantity              | Percentage  | "25%" or "fifty percent"        |
| Quantity              | Ordinal     | "1st" or "first"                |
| Quantity              | Age         | "90 day old" or "30 years old"  |
| Quantity              | Currency    | "10.99"                         |
| Quantity              | Dimension   | "10 miles", "40 cm"             |
| Quantity              | Temperature | "45 degrees"                    |
| DateTime              |             | "6:30PM February 4, 2012"       |
| DateTime              | Date        | "May 2nd, 2017" or "05/02/2017" |
| DateTime              | Time        | "8am" or "8:00"                 |
| DateTime              | DateRange   | "May 2nd to May 5th"            |
| DateTime              | TimeRange   | "6pm to 7pm"                    |
| DateTime              | Duration    | "1 minute and 45 seconds"       |
| DateTime              | Set         | "every Tuesday"                 |
| URL                   |             | "`https://www.bing.com`"        |
| Email                 |             | "`support@microsoft.com`"       |
| US-based Phone Number |             | "(312) 555-0176"                |
| IP Address            |             | "10.0.1.125"                    |

_Azure AI Language_ ยังรองรับฟีเจอร์ _entity linking_ ซึ่งช่วยในการ _แยกความหมายของ entity ที่ซ้ำกันหรือคลุมเครือ_ โดยเชื่อมโยงกับแหล่งข้อมูลที่ชัดเจน เช่น Wikipedia

เมื่อระบบตรวจพบ _entity_ ที่รู้จัก มันจะส่งคืน _URL_ ที่อ้างอิงไปยังบทความของ Wikipedia ที่เกี่ยวข้องกับ entity นั้น

ตัวอย่างเช่น สมมุติว่าคุณใช้ Azure AI Language เพื่อตรวจจับ entity จากข้อความรีวิวร้านอาหารดังนี้:

> "_I ate at the restaurant in Seattle last week._"

| Entity    | Type     | SubType   | Wikipedia URL                         |
| --------- | -------- | --------- | ------------------------------------- |
| Seattle   | Location |           | https://en.wikipedia.org/wiki/Seattle |
| last week | DateTime | DateRange |                                       |

## Language detection

คุณสามารถใช้ความสามารถ _language detection_ ของ _Azure AI Language_ เพื่อ _ตรวจจับภาษาของข้อความ_ ได้

สำหรับแต่ละข้อความที่ส่งเข้าไป ระบบจะตรวจจับ:

- _ชื่อภาษา_ เช่น "English"  
- _รหัสภาษาตามมาตรฐาน ISO 639-1_ เช่น `"en"`  
- _คะแนนความมั่นใจ_ (confidence score) ที่บอกว่าระบบมั่นใจแค่ไหนว่าภาษาที่ตรวจพบถูกต้อง

ลองนึกภาพสถานการณ์ที่คุณเป็นเจ้าของร้านอาหาร และลูกค้าสามารถตอบแบบสอบถามหรือแสดงความคิดเห็นเกี่ยวกับอาหาร, การบริการ, พนักงาน และอื่น ๆ ได้

สมมุติว่าคุณได้รับรีวิวจากลูกค้าดังต่อไปนี้:

> **Review 1**: "_A fantastic place for lunch. The soup was delicious._"

> **Review 2**: "_Comida maravillosa y gran servicio._"

> **Review 3**: "_The croque monsieur avec frites was terrific. Bon appetit!_"

คุณสามารถใช้ความสามารถด้าน _text analytics_ ใน _Azure AI Language_ เพื่อตรวจจับภาษาของรีวิวแต่ละรายการได้ โดยระบบอาจตอบกลับผลลัพธ์ในลักษณะดังนี้:

|Document|Language Name|ISO 6391 Code|Score|
|---|---|---|---|
|Review 1|English|en|1.0|
|Review 2|Spanish|es|1.0|
|Review 3|English|en|0.9|

สังเกตว่าในรีวิวที่ 3 ระบบตรวจจับภาษาเป็น _English_ แม้ข้อความจะมีการผสมคำภาษาอังกฤษและภาษาฝรั่งเศสอยู่ด้วย นั่นเป็นเพราะบริการตรวจจับภาษาจะโฟกัสที่ _ภาษาหลัก_ (_predominant language_) ของข้อความ

ระบบจะใช้ _อัลกอริธึม_ ในการวิเคราะห์ว่าเนื้อหาส่วนใหญ่ในข้อความนั้นเป็นภาษาใด เช่น ดูจากความยาวของวลี หรือจำนวนข้อความโดยรวมของแต่ละภาษา แล้วเลือกภาษาที่มีน้ำหนักมากที่สุดมาเป็นผลลัพธ์ที่ส่งกลับ พร้อมกับ _รหัสภาษา_ และ _confidence score_

ในกรณีที่ข้อความมี _หลายภาษา_ หรือ _ไม่ชัดเจน_ ค่าความมั่นใจ (_confidence score_) ที่ระบบส่งกลับมาอาจจะไม่ถึง 1 ได้

ข้อความบางประเภทก็อาจก่อให้เกิดความกำกวม เช่น ข้อความที่สั้นเกินไป หรือประกอบด้วยแค่เครื่องหมายวรรคตอน ตัวอย่างเช่น หากใช้ Azure AI Language วิเคราะห์ข้อความ `":-)"` ระบบจะส่งค่าผลลัพธ์ว่า:

- _language name_: unknown  
- _language identifier_: unknown  
- _confidence score_: NaN (_แปลว่าไม่ใช่ตัวเลข_ ใช้ในกรณีที่ไม่สามารถประเมินได้)

สถานการณ์เช่นนี้แสดงให้เห็นว่าการตรวจจับภาษาก็มี _ข้อจำกัด_ เมื่อเจอกับข้อความที่คลุมเครือหรือผสมหลายภาษา

## Sentiment analysis and opinion mining

ความสามารถด้าน _text analytics_ ของ _Azure AI Language_ สามารถวิเคราะห์ข้อความและส่งคืน _คะแนนอารมณ์_ (_sentiment scores_) พร้อมกับ _ป้ายกำกับ_ (_labels_) สำหรับแต่ละประโยคในข้อความได้

ความสามารถนี้มีประโยชน์มากสำหรับการตรวจจับ _อารมณ์เชิงบวก_ หรือ _เชิงลบ_ ในโพสต์บนโซเชียลมีเดีย, รีวิวของลูกค้า, ฟอรัมสนทนา และอื่น ๆ

Azure AI Language ใช้ _โมเดล machine learning ที่สร้างไว้ล่วงหน้า_ (_prebuilt model_) สำหรับจัดประเภทข้อความโดยอัตโนมัติ ระบบจะส่งคืน _คะแนนอารมณ์_ ใน 3 หมวด:

- _positive_ – อารมณ์เชิงบวก  
- _neutral_ – เป็นกลาง  
- _negative_ – อารมณ์เชิงลบ

ในแต่ละหมวดจะมีคะแนนอยู่ในช่วง 0 ถึง 1 ซึ่งแสดงถึง _ความน่าจะเป็น_ ที่ข้อความนั้นมีอารมณ์แบบนั้น เช่น คะแนน 0.85 ในหมวด _positive_ แปลว่ามีโอกาสสูงที่ข้อความจะเป็น _แง่บวก_

นอกจากนี้ ระบบยังสรุปผลรวมของเอกสารว่าโดยรวมแล้วข้อความนั้นมี _อารมณ์หลัก_ (document sentiment) อยู่ในกลุ่มใด

ตัวอย่างเช่น รีวิวร้านอาหารสองรายการต่อไปนี้สามารถนำมาวิเคราะห์ _sentiment_ ได้:

_Review 1_: "_We had dinner at this restaurant last night and the first thing I noticed was how courteous the staff was. We were greeted in a friendly manner and taken to our table right away. The table was clean, the chairs were comfortable, and the food was amazing._"

_Review 2_: "_Our dining experience at this restaurant was one of the worst I've ever had. The service was slow, and the food was awful. I'll never eat at this establishment again._"

คะแนนอารมณ์ (_sentiment score_) สำหรับรีวิวแรกอาจเป็นดังนี้:

_document sentiment_: _positive_  
_positive score_: 0.90  
_neutral score_: 0.10  
_negative score_: 0.00

แสดงว่ารีวิวนี้มีความเป็น _แง่บวก_ สูงมาก

ส่วนรีวิวที่สองอาจให้ผลลัพธ์ดังนี้:

_document sentiment_: _negative_  
_positive score_: 0.00  
_neutral score_: 0.00  
_negative score_: 0.99

ซึ่งแสดงว่ารีวิวนี้ถูกจัดว่าเป็น _แง่ลบ_ อย่างชัดเจน

การวิเคราะห์แบบนี้ช่วยให้องค์กรสามารถ _ประเมินความพึงพอใจของลูกค้า_ ได้โดยอัตโนมัติ และนำไปใช้ในการปรับปรุงบริการหรือผลิตภัณฑ์ต่อไป

## Key phrase extraction

_key phrase extraction_ คือการดึงข้อความสำคัญหรือ _ประเด็นหลัก_ ออกมาจากข้อความ ลองนึกถึงสถานการณ์ร้านอาหารที่กล่าวถึงก่อนหน้านี้ หากคุณมีแบบสอบถามจากลูกค้าจำนวนมาก การอ่านรีวิวทั้งหมดอาจใช้เวลานาน

แทนที่จะต้องอ่านทีละรายการ คุณสามารถใช้ความสามารถในการ _ดึง key phrase_ ของบริการ _Azure AI Language_ เพื่อ _สรุปประเด็นสำคัญ_ จากรีวิวทั้งหมดได้อย่างรวดเร็ว

ตัวอย่างเช่น คุณอาจได้รับรีวิวลูกค้าดังนี้:

"_We had dinner here for a birthday celebration and had a fantastic experience. We were greeted by a friendly hostess and taken to our table right away. The ambiance was relaxed, the food was amazing, and service was terrific. If you like great food and attentive service, you should try this place._"

_key phrase extraction_ สามารถช่วยสรุป _บริบท_ ของรีวิวนี้ได้ โดยดึงข้อความสำคัญออกมา เช่น:
- birthday celebration
- fantastic experience
- friendly hostess
- great food
- attentive service
- dinner
- table
- ambiance
- place

