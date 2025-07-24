
พื้นฐานของ _Azure AI Search_ คือบริการบนคลาวด์สำหรับ _สร้างดัชนี (indexing)_ และ _ค้นหาข้อมูล_ แต่สิ่งที่ทำให้บริการนี้ทรงพลังมากขึ้นคือ:

- การใช้ _AI skills_ เพื่อ _ดึงข้อมูลเชิงลึกจากข้อมูลหลายรูปแบบ_ ไม่ว่าจะเป็นข้อความ รูปภาพ หรือเอกสาร
- ความสามารถในการ _เชื่อมต่อกับบริการ AI อื่น ๆ_ เช่น _Azure AI Vision_ และ _Azure AI Document Intelligence_

สิ่งเหล่านี้ทำให้ _Azure AI Search_ เป็น _แพลตฟอร์มที่แข็งแกร่ง_ สำหรับการสร้างโซลูชันด้าน _การจัดการทรัพย์สินดิจิทัล (digital asset management)_ และ _การขุดความรู้ (knowledge mining)_

## Indexers, indexes, and skills

หัวใจสำคัญของโซลูชัน _Azure AI Search_ คือ _indexer_ ซึ่งเป็นกระบวนการแบบทำซ้ำได้ (_repeatable process_) เพื่อ:

1. _ดึงข้อมูลจากแหล่งต้นทาง (source)_ เช่น _Azure Storage_ ที่เก็บเอกสาร หรือฐานข้อมูล

2. ทำ _document cracking_ เพื่อ _แยกเนื้อหาจากไฟล์_ เช่น การดึงข้อความและรูปภาพจากไฟล์ PDF

3. _ประมวลผลตามลำดับขั้น_ เพื่อดึงข้อมูลสำคัญและสร้าง _field_ ต่าง ๆ สำหรับ search index โดย field เหล่านี้แบ่งเป็น:
   - _ข้อมูลพื้นฐานของเอกสาร_ เช่น ชื่อไฟล์, วันที่แก้ไขล่าสุด
   - _ข้อมูลที่ได้จาก AI skills_ เช่น:
     - ใช้ **Azure AI Vision** เพื่อสร้าง _tags_ และ _captions_ จากภาพ
     - ใช้ **Azure AI Language** เพื่อสร้าง field สำหรับ _sentiment_ หรือ _named entities_
     - ใช้ **Azure AI Document Intelligence** เพื่อดึง _field values_ จากแบบฟอร์ม

4. _บันทึกผลลัพธ์ที่ดึงได้_ เป็น _search index_ ที่พร้อมใช้งาน

![Diagram of an indexer using AI skills to extract fields from source documents and create an index.](https://learn.microsoft.com/en-us/training/wwl-data-ai/ai-information-extraction/media/indexer.png)

เมื่อสร้าง index เสร็จแล้ว ผู้ใช้สามารถ _ค้นหาข้อมูลใน field ที่ดึงมาได้_ โดยใช้คำค้นหรือเงื่อนไขกรอง (_filtering criteria_) ได้อย่างง่ายดาย

## Persisting extracted data to a knowledge store

นอกจากการสร้าง _searchable index_ แล้ว _Azure AI Search_ ยังสามารถ _จัดเก็บข้อมูลที่ดึงได้_ ลงใน _knowledge store_ บน Azure Storage ได้ด้วย

_indexer_ สามารถบันทึกข้อมูลใน knowledge store ในรูปแบบต่าง ๆ เช่น:
- _ตารางของ field values_: เหมาะสำหรับการวิเคราะห์หรือเชื่อมต่อกับ Power BI และระบบอื่น
- _ภาพที่ดึงมาจากเอกสาร_: เช่น รูปที่แยกออกมาจาก PDF หรือเอกสารแนบ
- _ไฟล์ JSON ที่แทนโครงสร้างข้อมูล_: เช่น แผนผังที่ซับซ้อนของ field และ value ที่จัดเรียงเป็นลำดับชั้น
    
    ![Diagram of an indexer storing tables, image,s and documents in a knowldge store.](https://learn.microsoft.com/en-us/training/wwl-data-ai/ai-information-extraction/media/knowledge-store.png)