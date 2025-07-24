
_CNNs_ เป็นแกนหลักของโซลูชัน _computer vision_ มาหลายปีแล้ว แม้จะถูกใช้บ่อยในงาน _image classification_ อย่างที่อธิบายไปก่อนหน้า แต่จริง ๆ แล้ว _CNN_ ยังเป็นพื้นฐานของโมเดล _computer vision_ ที่ซับซ้อนยิ่งขึ้น

ตัวอย่างเช่น โมเดล _object detection_ จะผสานการสกัด _features_ ด้วย _CNN_ เข้ากับการตรวจหาบริเวณที่น่าสนใจในภาพ (_regions of interest_) เพื่อระบุตำแหน่งของวัตถุหลายชนิดในภาพเดียวกันได้พร้อมกัน

### Transformers

ความก้าวหน้าส่วนใหญ่ในด้าน _computer vision_ ตลอดหลายทศวรรษที่ผ่านมา ขับเคลื่อนด้วยการพัฒนาโมเดลที่ใช้ _CNN_ เป็นหลัก อย่างไรก็ตาม ในอีกสาขาหนึ่งของ _AI_ อย่าง _natural language processing (NLP)_ มีการใช้สถาปัตยกรรม _neural network_ อีกประเภทหนึ่งที่เรียกว่า _transformer_ ซึ่งช่วยให้สามารถพัฒนาโมเดลที่ซับซ้อนสำหรับการเข้าใจภาษาได้ _transformers_ ทำงานโดยประมวลผลข้อมูลจำนวนมหาศาล และเข้ารหัสคำหรือวลี (_language tokens_) ให้อยู่ในรูปของ _vector-based embeddings_ หรือ _array_ ของค่าตัวเลข ที่แทนมิติทางความหมายต่าง ๆ ของคำนั้น

สามารถนึกภาพ _embedding_ ได้ว่าเป็นชุดของมิติ (_dimensions_) ที่แต่ละมิติเชื่อมโยงกับความหมายหรือบริบทบางอย่าง  
โดยคำที่มักปรากฏในบริบทเดียวกัน จะมีเวกเตอร์ที่อยู่ใกล้กันมากกว่าคำที่ไม่เกี่ยวข้องกัน

ตัวอย่างง่าย ๆ ด้านล่างนี้แสดงให้เห็นคำบางคำ ที่ถูกเข้ารหัสเป็นเวกเตอร์สามมิติ (_3D vectors_) และนำไปแสดงในพื้นที่สามมิติ:

![Diagram of token vectors in a 3D space.](https://learn.microsoft.com/en-us/training/wwl-data-ai/introduction-computer-vision/media/language-encoder.png) 

_tokens_ ที่มีความหมายคล้ายกัน (_semantically similar_) จะถูกเข้ารหัสให้อยู่ในทิศทางของเวกเตอร์ที่ใกล้เคียงกัน  
ซึ่งทำให้เกิดโมเดลภาษาที่มีความเข้าใจเชิงความหมาย (_semantic language model_)

โมเดลแบบนี้ช่วยให้สามารถสร้างโซลูชัน _NLP_ ที่ซับซ้อนได้ เช่น การวิเคราะห์ข้อความ (_text analysis_), การแปลภาษา (_translation_), การสร้างข้อความ (_language generation_) และงานอื่น ๆ อีกมากมาย

> **หมายเหตุ**  
> ที่เราใช้เวกเตอร์เพียงสามมิตินั้นก็เพื่อให้ง่ายต่อการมองภาพ  
> แต่ในความเป็นจริง _encoder_ ใน _transformer networks_ จะสร้างเวกเตอร์ที่มีจำนวนมิติมากกว่านั้นมาก  
> เพื่อกำหนดความสัมพันธ์เชิงความหมาย (_semantic relationships_) ที่ซับซ้อนระหว่าง _tokens_  
> โดยอาศัยการคำนวณทางพีชคณิตเชิงเส้น (_linear algebra_)

> คณิตศาสตร์ที่ใช้ค่อนข้างซับซ้อน เช่นเดียวกับโครงสร้างของ _transformer model_ เอง  
> จุดประสงค์ของเราที่นี่คือการอธิบายแนวคิดโดยรวม เพื่อให้เข้าใจว่า  
> การเข้ารหัส (_encoding_) ช่วยสร้างโมเดลที่สะท้อนความสัมพันธ์ระหว่าง _entities_ ได้อย่างไร

### Multi-modal models

ความสำเร็จของ _transformers_ ในการสร้าง _language models_ ได้นำไปสู่การตั้งคำถามในหมู่นักวิจัย _AI_ ว่า วิธีการแบบเดียวกันนี้จะใช้ได้ผลกับข้อมูลภาพหรือไม่ ผลลัพธ์คือการพัฒนา _multi-modal models_ ซึ่งเป็นโมเดลที่ถูกฝึกด้วยภาพจำนวนมากที่มีคำบรรยาย (_captioned images_) โดยไม่จำเป็นต้องมี _label_ แบบตายตัว ในโมเดลนี้จะมี _image encoder_ ทำหน้าที่สกัด _features_ จากภาพโดยอิงจากค่าพิกเซล และรวมเข้ากับ _text embeddings_ ที่ได้จาก _language encoder_

ผลลัพธ์ที่ได้คือโมเดลที่รวมความสัมพันธ์ระหว่าง _natural language token embeddings_ และ _image features_ ไว้ด้วยกัน ดังที่แสดงในภาพด้านล่าง:

![Diagram of a multi-modal model that encapsulates relationships between natural language vectors and image features.](https://learn.microsoft.com/en-us/training/wwl-data-ai/introduction-computer-vision/media/multi-modal-model.png)

## Bringing it all together

โมเดล _vision_ สมัยใหม่ถูกฝึกด้วยภาพจำนวนมหาศาลจากอินเทอร์เน็ต ซึ่งแต่ละภาพมีคำบรรยาย (_captioned images_) กำกับอยู่ โดยโมเดลเหล่านี้จะประกอบด้วยทั้ง _language encoder_ และ _image encoder_ ผู้ใช้งานมักจะโต้ตอบกับโมเดลประเภทที่เรียกว่า _foundation models_ ซึ่งเป็นโมเดลทั่วไปที่ถูกฝึกมาแล้วล่วงหน้า (_pre-trained_) และสามารถนำไปปรับใช้ (_adapt_) ให้เหมาะกับงานเฉพาะทางต่าง ๆ ได้ ตัวอย่างของการปรับโมเดลพื้นฐาน (_foundation model_) ได้แก่

- _image classification_: ระบุว่าภาพนั้นอยู่ในหมวดหมู่ใด  
- _object detection_: ระบุตำแหน่งของวัตถุแต่ละชิ้นภายในภาพ  
- _captioning_: สร้างคำบรรยายที่เหมาะสมสำหรับภาพ  
- _tagging_: สร้างรายการคำแท็กที่เกี่ยวข้องกับภาพ

![Diagram of a Florence model as a foundation model with multiple adaptive models built on it.](https://learn.microsoft.com/en-us/training/wwl-data-ai/introduction-computer-vision/media/florence-model.png)

_multi-modal models_ ถือเป็นแนวหน้าของเทคโนโลยี _computer vision_ และ _AI_ โดยรวม และคาดว่าจะเป็นแรงขับเคลื่อนสำคัญในการพัฒนาโซลูชันใหม่ ๆ ที่ _AI_ สามารถทำได้ในอนาคต

