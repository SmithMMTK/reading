
![Diagram of Azure Cosmos DB as a store for multiple NoSQL formats.](https://learn.microsoft.com/en-us/training/wwl-data-ai/explore-non-relational-data-stores-azure/media/azure-cosmos-db.png)

_Azure Cosmos DB_ รองรับ _API_ หลากหลายแบบ ทำให้นักพัฒนาสามารถใช้รูปแบบคำสั่ง (_semantics_) ของฐานข้อมูลที่คุ้นเคยในการทำงานกับข้อมูลใน _Cosmos DB_ ได้ โครงสร้างข้อมูลภายในจะถูก _abstract_ ออกไป เพื่อให้นักพัฒนาสามารถ _store_ และ _query_ ข้อมูลผ่าน _API_ ที่ใช้งานเป็นประจำได้อย่างสะดวก เช่น ถ้าเคยใช้ _MongoDB_, _Gremlin_ หรือ _SQL-like query_ ก็สามารถใช้ _API_ แบบนั้นกับ _Cosmos DB_ ได้เลย

 Note: 
	
	_API_ ย่อมาจาก _Application Programming Interface_ ซึ่งเป็นชุดคำสั่งที่ระบบฐานข้อมูล (หรือซอฟต์แวร์อื่น ๆ) เตรียมไว้ให้นักพัฒนาใช้งาน เพื่อเขียนโปรแกรมที่เข้าถึงข้อมูลได้สะดวก โดยแต่ละระบบฐานข้อมูลอาจมี _API_ แตกต่างกันไป

_Cosmos DB_ ใช้การสร้าง _index_ และ _partitioning_ เพื่อให้สามารถ _read_ และ _write_ ข้อมูลได้อย่างรวดเร็ว และสามารถ _scale_ เพื่อรองรับข้อมูลปริมาณมหาศาลได้

คุณยังสามารถเปิดใช้งาน _multi-region writes_ ได้ โดยเพิ่ม _Azure regions_ ที่ต้องการเข้าไปในบัญชี _Cosmos DB_ ทำให้ผู้ใช้งานที่อยู่คนละภูมิภาคสามารถทำงานกับข้อมูลใน _local replica_ ของตนเองได้อย่างรวดเร็วและมีประสิทธิภาพ

## When to use Cosmos DB

_Cosmos DB_ เป็นระบบจัดการฐานข้อมูลที่ _scalable_ สูงมาก โดยจะจัดสรรพื้นที่ใน _container_ ให้กับแต่ละ _partition_ โดยอัตโนมัติ ซึ่งแต่ละ _partition_ สามารถขยายได้ถึง 10 GB และระบบจะสร้างและดูแล _index_ ให้อัตโนมัติ ทำให้แทบไม่มีงานดูแลระบบ (_administrative overhead_) ให้ต้องกังวล

_Cosmos DB_ ถือเป็นบริการพื้นฐาน (_foundational service_) บน _Azure_ ที่ถูกใช้งานโดยผลิตภัณฑ์ของ Microsoft หลายตัวในระบบขนาดใหญ่ที่มีความสำคัญสูง เช่น _Skype_, _Xbox_, _Microsoft 365_, _Azure_ และอื่น ๆ อีกมากมาย

_Cosmos DB_ เหมาะกับหลายสถานการณ์ เช่น

- _IoT และ telematics_: ระบบเหล่านี้มักมีข้อมูลจำนวนมากไหลเข้ามาแบบไม่สม่ำเสมอ _Cosmos DB_ สามารถรับและจัดเก็บข้อมูลได้อย่างรวดเร็ว ข้อมูลนี้สามารถนำไปใช้กับบริการวิเคราะห์ เช่น _Azure Machine Learning_, _Microsoft Fabric_ และ _Power BI_ หรือจะประมวลผลแบบ _real-time_ ด้วย _Azure Functions_ ที่ทำงานทันทีเมื่อมีข้อมูลเข้ามาก็ได้

- _ธุรกิจค้าปลีกและการตลาด_: Microsoft เองใช้ _Cosmos DB_ ในระบบ _e-commerce_ ของ _Windows Store_ และ _Xbox Live_ และยังมีการใช้ในอุตสาหกรรมค้าปลีกเพื่อจัดเก็บข้อมูลแคตตาล็อก และเก็บเหตุการณ์ที่เกิดขึ้นในกระบวนการสั่งซื้อสินค้า (_event sourcing_)

- _เกม_: ส่วนฐานข้อมูลเป็นหัวใจสำคัญของแอปพลิเคชันเกมสมัยใหม่ ที่แม้การประมวลผลกราฟิกจะอยู่ที่เครื่องของผู้เล่น แต่ข้อมูลส่วนบุคคล เช่น สถิติเกม การเชื่อมต่อโซเชียล หรือกระดานคะแนนสูงสุด มักดึงมาจากคลาวด์ _Cosmos DB_ รองรับความเร็วระดับมิลลิวินาทีต่อคำสั่ง และรองรับปริมาณคำขอมหาศาลในช่วงเปิดตัวเกมหรือเพิ่มฟีเจอร์ใหม่

- _เว็บและแอปมือถือ_: _Cosmos DB_ นิยมใช้งานร่วมกับแอปพลิเคชันเว็บและมือถือ เหมาะกับการออกแบบข้อมูลเชิงสังคม การเชื่อมต่อบริการภายนอก และประสบการณ์ผู้ใช้งานที่ปรับให้เหมาะกับแต่ละคน (_personalized experience_) โดยมี _SDK_ ที่รองรับการพัฒนาแอป iOS และ Android ผ่าน _Xamarin_ อีกด้วย
    

For additional information about uses for Cosmos DB, read [Common Azure Cosmos DB use cases](https://learn.microsoft.com/en-us/azure/cosmos-db/use-cases).