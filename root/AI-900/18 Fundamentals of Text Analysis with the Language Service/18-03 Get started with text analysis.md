
**Azure AI Language** เป็นส่วนหนึ่งของบริการ _Azure AI_ ที่สามารถทำ _natural language processing_ ขั้นสูงบนข้อความที่ไม่มีโครงสร้าง (_unstructured text_) ได้  
ฟีเจอร์ด้าน _text analysis_ ของ Azure AI Language ได้แก่:

- **_Named entity recognition_**: ระบุชื่อบุคคล สถานที่ เหตุการณ์ และอื่น ๆ โดยสามารถปรับแต่งให้ดึงหมวดหมู่เฉพาะ (_custom categories_) ได้ด้วย  
- **_Entity linking_**: ระบุชื่อสิ่งที่รู้จักพร้อมลิงก์ไปยัง _Wikipedia_  
- **_Personal identifying information (PII) detection_**: ตรวจจับข้อมูลส่วนบุคคลที่อ่อนไหว เช่น ข้อมูลสุขภาพ (_PHI_)  
- **_Language detection_**: ตรวจจับภาษาในข้อความ และส่งกลับรหัสภาษา เช่น `"en"` สำหรับภาษาอังกฤษ  
- **_Sentiment analysis_ และ _opinion mining_**: วิเคราะห์ว่าข้อความมีความรู้สึกเชิง _positive_ หรือ _negative_  
- **_Summarization_**: สรุปข้อความโดยดึงสาระสำคัญที่สุดออกมา  
- **_Key phrase extraction_**: แยกรายการแนวคิดหลัก (_main concepts_) จากข้อความที่ไม่มีโครงสร้าง

## Entity recognition and linking

คุณสามารถส่งข้อความที่ไม่มีโครงสร้าง (_unstructured text_) ให้กับ _Azure AI Language_ แล้วระบบจะส่งกลับรายการของ _entities_ ที่มันสามารถตรวจพบได้ _entity_ คือรายการของสิ่งที่จัดอยู่ใน _ประเภท_ หรือ _หมวดหมู่_ ใดหมวดหมู่หนึ่ง และบางกรณีอาจมีการระบุ _subtype_ เพิ่มเติมด้วย

|Type|SubType|Example|
|---|---|---|
|Person||"Bill Gates", "John"|
|Location||"Paris", "New York"|
|Organization||"Microsoft"|
|Quantity|Number|"6" or "six"|
|Quantity|Percentage|"25%" or "fifty percent"|
|Quantity|Ordinal|"1st" or "first"|
|Quantity|Age|"90 day old" or "30 years old"|
|Quantity|Currency|"10.99"|
|Quantity|Dimension|"10 miles", "40 cm"|
|Quantity|Temperature|"45 degrees"|
|DateTime||"6:30PM February 4, 2012"|
|DateTime|Date|"May 2nd, 2017" or "05/02/2017"|
|DateTime|Time|"8am" or "8:00"|
|DateTime|DateRange|"May 2nd to May 5th"|
|DateTime|TimeRange|"6pm to 7pm"|
|DateTime|Duration|"1 minute and 45 seconds"|
|DateTime|Set|"every Tuesday"|
|URL||"`https://www.bing.com`"|
|Email||"`support@microsoft.com`"|
|US-based Phone Number||"(312) 555-0176"|
|IP Address||"10.0.1.125"|

_Azure AI Language_ ยังรองรับฟีเจอร์ _entity linking_ ซึ่งช่วยให้สามารถแยกแยะ _entity_ ที่มีความหมายใกล้เคียงกันได้ โดยการเชื่อมโยงกับแหล่งข้อมูลเฉพาะ เช่น _Wikipedia_  

เมื่อระบบตรวจพบ _entity_ ที่รู้จักได้ มันจะส่งคืน URL ของบทความ _Wikipedia_ ที่เกี่ยวข้องกับ _entity_ นั้น

ตัวอย่างเช่น หากคุณใช้ Azure AI Language วิเคราะห์ข้อความจากรีวิวร้านอาหารดังนี้:

> "_I ate at the restaurant in Seattle last week._"

|Entity|Type|SubType|Wikipedia URL|
|---|---|---|---|
|Seattle|Location||https://en.wikipedia.org/wiki/Seattle|
|last week|DateTime|DateRange||

## Language detection

คุณสามารถใช้ความสามารถ _language detection_ ของ _Azure AI Language_ เพื่อระบุว่าแต่ละข้อความเขียนด้วยภาษาใดโดยคุณสามารถส่งข้อความหลายฉบับพร้อมกันได้ และสำหรับแต่ละข้อความ ระบบจะตรวจจับข้อมูลต่อไปนี้:

- _ชื่อภาษา_ (เช่น `"English"`)  
- _รหัสภาษา ISO 639-1_ (เช่น `"en"`)  
- _คะแนนความมั่นใจ_ ในผลการรวจจับภาษานั้น 

ตัวอย่างเช่น  

สมมติว่าคุณเป็นเจ้าของร้านอาหาร และเปิดให้ลูกค้าให้ _feedback_ ผ่านแบบสอบถามเกี่ยวกับอาหาร การบริการ พนักงาน เป็นต้น  

คุณได้รับรีวิวจากลูกค้าหลายภาษา เช่น:

> **Review 1**: "_A fantastic place for lunch. The soup was delicious._"
> 
> **Review 2**: "_Comida maravillosa y gran servicio._"
> 
> **Review 3**: "_The croque monsieur avec frites was terrific. Bon appetit!_"

คุณสามารถใช้ความสามารถของ _text analytics_ ใน _Azure AI Language_ เพื่อตรวจจับ _ภาษา_ ของแต่ละรีวิวได้ ระบบอาจตอบกลับด้วยผลลัพธ์ในลักษณะดังนี้:

|Document|Language Name|ISO 6391 Code|Score|
|---|---|---|---|
|Review 1|English|en|1.0|
|Review 2|Spanish|es|1.0|
|Review 3|English|en|0.9|

สังเกตว่าในการวิเคราะห์ข้อความที่ 3 ระบบอาจระบุว่าเป็นภาษา _English_ แม้ว่าข้อความจะมีทั้งภาษาอังกฤษและฝรั่งเศสผสมกัน เนื่องจากบริการตรวจจับภาษาจะโฟกัสที่ _**ภาษาหลัก (predominant language)**_ ของข้อความ โดยใช้ _algorithm_ ที่พิจารณาจากความยาวของแต่ละส่วน หรือปริมาณข้อความในแต่ละภาษาเพื่อเปรียบเทียบกัน ค่าที่ระบบส่งกลับจึงเป็น _ภาษาหลัก_ พร้อมกับ _language code_ และคะแนน _confidence score_ ซึ่งอาจไม่ถึง 1.0 หากมีภาษาผสมอยู่

ในบางกรณีอาจมีข้อความที่ _คลุมเครือ_ หรือเป็น _ภาษาผสม_ อย่างชัดเจน ซึ่งทำให้การตรวจจับเป็นเรื่องท้าทาย ตัวอย่างของเนื้อหาคลุมเครือ เช่น ข้อความที่มีเนื้อหาน้อยมาก หรือเป็นเพียงเครื่องหมายวรรคตอน หากเราวิเคราะห์ข้อความ `"🙂"` หรือ `":-)"` ด้วย Azure AI Language ผลลัพธ์จะเป็น:

- _Language name_: **unknown**  
- _Language code_: **unknown**  
- _Confidence score_: **NaN** (_not a number_)  

เนื่องจากไม่มีข้อมูลเพียงพอให้ระบบสามารถสรุปได้ว่าเป็นภาษาใด

## Sentiment analysis and opinion mining

ความสามารถด้าน _text analytics_ ของ _Azure AI Language_ สามารถประเมินข้อความและส่งคืน _คะแนนและป้ายกำกับความรู้สึก (sentiment scores and labels)_ สำหรับแต่ละประโยค ฟีเจอร์นี้มีประโยชน์มากในการตรวจจับ _sentiment_ ทั้ง _positive_ และ _negative_ จากโซเชียลมีเดีย รีวิวจากลูกค้า ฟอรัมสนทนา และอื่น ๆ

Azure AI Language ใช้โมเดล _machine learning_ ที่สร้างไว้ล่วงหน้า (_prebuilt classification model_) ในการประเมินข้อความ ระบบจะส่งคืนคะแนนความรู้สึกใน 3 ประเภทคือ _positive_, _neutral_ และ _negative_ โดยแต่ละประเภทจะให้ _คะแนนระหว่าง 0 ถึง 1_  ซึ่งหมายถึงความน่าจะเป็นที่ข้อความนั้นจะมี _sentiment_ ในประเภทนั้น ๆ  นอกจากนี้ยังมีการสรุป _sentiment โดยรวมของข้อความทั้งฉบับ (document sentiment)_ อีกด้วย
  

ตัวอย่างเช่น รีวิวร้านอาหาร 2 รายการต่อไปนี้สามารถนำมาวิเคราะห์ _sentiment_ ได้:

> _Review 1_: "_We had dinner at this restaurant last night and the first thing I noticed was how courteous the staff was. We were greeted in a friendly manner and taken to our table right away. The table was clean, the chairs were comfortable, and the food was amazing._"

and

> _Review 2_: "_Our dining experience at this restaurant was one of the worst I've ever had. The service was slow, and the food was awful. I'll never eat at this establishment again._"

สำหรับรีวิวแรก ระบบอาจประเมิน _sentiment_ ได้ดังนี้:
- _Document sentiment_: **positive**  
- _Positive score_: 0.90  
- _Neutral score_: 0.10  
- _Negative score_: 0.00

ส่วนรีวิวที่สองอาจได้ผลลัพธ์ดังนี้:
- _Document sentiment_: **negative**  
- _Positive score_: 0.00  
- _Neutral score_: 0.00  
- _Negative score_: 0.99

ผลลัพธ์เหล่านี้ช่วยให้เรามองเห็น _ความรู้สึกโดยรวม_ ที่แฝงอยู่ในข้อความ และนำไปใช้ต่อยอดในงานวิเคราะห์ข้อมูล เช่น การจัดอันดับร้าน การตอบกลับรีวิว หรือการวัดความพึงพอใจของลูกค้าได้อย่างแม่นยำ

## Key phrase extraction

การ _key phrase extraction_ คือการดึง _ประเด็นสำคัญ_ ออกจากข้อความ ในกรณีร้านอาหารที่พูดถึงก่อนหน้านี้ หากคุณมีแบบสอบถามจากลูกค้าจำนวนมาก การอ่านรีวิวทีละรายการอาจใช้เวลานาน แทนที่จะอ่านทั้งหมด คุณสามารถใช้ฟีเจอร์ _key phrase extraction_ ของ _Azure AI Language_ เพื่อสรุป _ประเด็นหลัก_ ได้อย่างรวดเร็ว

ตัวอย่างเช่น คุณอาจได้รับรีวิวจากลูกค้าดังนี้:

> "_We had dinner here for a birthday celebration and had a fantastic experience. We were greeted by a friendly hostess and taken to our table right away. The ambiance was relaxed, the food was amazing, and service was terrific. If you like great food and attentive service, you should try this place._"

การ _key phrase extraction_ สามารถช่วยให้เราเข้าใจบริบทของรีวิวนี้ได้ โดยดึงวลีสำคัญต่อไปนี้ออกมา:

- birthday celebration
- fantastic experience
- friendly hostess
- great food
- attentive service
- dinner
- table
- ambiance
- place

นอกจากการใช้ _sentiment analysis_ เพื่อตรวจสอบว่ารีวิวนี้เป็น _positive review_ แล้ว คุณยังสามารถใช้บริการ _key phrase extraction_ เพื่อระบุ _องค์ประกอบสำคัญ_ ของรีวิวได้ด้วย

## Create a resource for Azure AI Language

หากคุณต้องการใช้งาน _Azure AI Language_ ภายในแอปพลิเคชัน  
คุณต้องมีการ _สร้างทรัพยากร (provision resource)_ ที่เหมาะสมในบัญชี _Azure subscription_ ของคุณก่อน

คุณสามารถเลือกสร้างได้ 2 ประเภท:

- **_Language resource_**: เหมาะสำหรับกรณีที่คุณวางแผนจะใช้แค่บริการ _Azure AI Language_ เท่านั้น หรือหากคุณต้องการแยกการจัดการเรื่อง _สิทธิ์การเข้าถึง_ และ _การเรียกเก็บเงิน_ ออกจากบริการอื่น
- **_Azure AI services resource_**: เหมาะสำหรับกรณีที่คุณจะใช้ _Azure AI Language_ ร่วมกับบริการอื่น ๆ ในกลุ่ม _Azure AI_ และต้องการบริหารจัดการ _การเข้าถึง_ และ _ค่าใช้จ่าย_ รวมกันในทรัพยากรเดียว
