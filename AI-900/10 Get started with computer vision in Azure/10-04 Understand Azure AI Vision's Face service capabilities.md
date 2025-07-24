
ในฐานะที่เป็นหนึ่งในผลิตภัณฑ์ของ Azure AI Vision บริการ _Azure AI Face_ รองรับกรณีใช้งานเฉพาะทาง เช่น การยืนยันตัวตนของผู้ใช้ (_verifying user identity_), การตรวจจับการมีชีวิตอยู่ของบุคคล (_liveness detection_), การควบคุมการเข้าถึงแบบไม่ต้องสัมผัส (_touchless access control_) และการปิดบังใบหน้าในภาพ (_face redaction_)  

มีแนวคิดสำคัญหลายอย่างที่เกี่ยวข้องกับการใช้งาน _Face_ เช่น _face detection_ และ _face recognition_ ซึ่งเป็นพื้นฐานในการทำงานกับบริการนี้

## Facial detection

การทำ _face detection_ คือการระบุบริเวณในภาพที่มีใบหน้าของมนุษย์ โดยทั่วไประบบจะส่งคืนพิกัดของ _bounding box_ ซึ่งเป็นกรอบสี่เหลี่ยมที่ล้อมรอบใบหน้านั้นไว้ เช่นตัวอย่างต่อไปนี้

![Photograph of two faces highlighted in rectangles.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-computer-vision-azure/media/face-detection-1.png)

เมื่อใช้บริการ _Face_ คุณสามารถใช้ลักษณะเฉพาะของใบหน้า (_facial features_) ในการฝึกโมเดล _machine learning_ เพื่อให้ระบบสามารถส่งคืนข้อมูลอื่น ๆ ได้ เช่น _จมูก_, _ตา_, _คิ้ว_, _ริมฝีปาก_ และส่วนอื่น ๆ ของใบหน้า

## Facial Landmarks 

![Screenshot of facial landmarks image showing data around face characteristics.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-computer-vision-azure/media/landmarks-2.png)

## Facial recognition

อีกหนึ่งการประยุกต์ใช้ของการวิเคราะห์ใบหน้าคือการฝึกโมเดล _machine learning_ เพื่อระบุบุคคลที่รู้จักจากลักษณะใบหน้า ซึ่งเรียกว่า _facial recognition_ การฝึกแบบนี้จะใช้ภาพของบุคคลเดิมหลายภาพในการสอนโมเดล เพื่อให้ระบบสามารถตรวจจับบุคคลนั้น ๆ ในภาพใหม่ที่ไม่เคยเห็นมาก่อน

![Photograph of a person identified as "Wendell".](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-computer-vision-azure/media/facial-recognition-1.png)

เมื่อใช้อย่างมีความรับผิดชอบ _facial recognition_ เป็นเทคโนโลยีที่สำคัญและมีประโยชน์ ซึ่งสามารถช่วยเพิ่ม _efficiency_, _security_ และประสบการณ์ของลูกค้า (_customer experiences_) ได้อย่างมาก

## Azure AI Face service capabilities

บริการ Azure AI Face สามารถส่งคืนพิกัดของกรอบสี่เหลี่ยม (_rectangle coordinates_) สำหรับใบหน้ามนุษย์ที่พบในภาพ พร้อมทั้งข้อมูล _attributes_ ที่เกี่ยวข้อง ดังนี้:

- _Accessories_: แสดงว่าบุคคลในภาพมีอุปกรณ์สวมใส่หรือไม่ เช่น _headwear_, _glasses_, _mask_ พร้อมค่าความมั่นใจ (_confidence score_) ระหว่าง 0 ถึง 1 สำหรับแต่ละรายการ
- _Blur_: ระดับความเบลอของใบหน้า ซึ่งอาจบ่งบอกว่าใบหน้านั้นเป็นจุดสนใจหลักของภาพหรือไม่
- _Exposure_: บอกว่าใบหน้าในภาพสว่างเกินไป (_overexposed_) หรือมืดเกินไป (_underexposed_) โดยวิเคราะห์เฉพาะใบหน้า ไม่ใช่ทั้งภาพ
- _Glasses_: ระบุว่าบุคคลใส่แว่นหรือไม่
- _Head pose_: ทิศทางของใบหน้าในพื้นที่ 3 มิติ
- _Mask_: แสดงว่าใบหน้ามีการใส่หน้ากากหรือไม่
- _Noise_: ความพร่ามัวจาก _visual noise_ เช่น เมื่อถ่ายในที่มืดด้วยค่า ISO สูง ภาพอาจดูเป็นเม็ด ๆ ไม่ชัด
- _Occlusion_: ตรวจสอบว่ามีสิ่งของบางอย่างบดบังใบหน้าหรือไม่
- _Quality For Recognition_: ระดับคุณภาพของภาพที่ใช้สำหรับ _facial recognition_ โดยระบุเป็น _high_, _medium_ หรือ _low_

## Responsible AI use

ใคร ๆ ก็สามารถใช้บริการ _Face_ ได้เพื่อ:

- ตรวจจับตำแหน่งของใบหน้าในภาพ
- ตรวจสอบว่าบุคคลใส่ _glasses_ หรือไม่
- ตรวจสอบว่ามี _occlusion_, _blur_, _noise_ หรือ _over/under exposure_ ในแต่ละใบหน้าหรือไม่
- ส่งคืนพิกัด _head pose_ ของแต่ละใบหน้าในภาพ

อย่างไรก็ตาม _Limited Access policy_ กำหนดให้ลูกค้าต้อง [กรอกแบบฟอร์มการขอใช้](https://aka.ms/facerecognition) เพื่อเข้าถึงความสามารถเพิ่มเติมของ Azure AI Face ได้แก่:

### Azure AI Face service

- _Face verification_: ความสามารถในการเปรียบเทียบใบหน้าเพื่อดูความเหมือนกัน
- _Face identification_: ความสามารถในการระบุชื่อบุคคลจากใบหน้าในภาพ
- _Liveness detection_: ความสามารถในการตรวจจับและป้องกันการใช้งานที่ละเมิดนโยบาย เช่น ตรวจสอบว่าวิดีโอที่ป้อนเข้ามานั้นเป็นวิดีโอจริงหรือปลอม
