
ความสามารถของ _Azure AI Vision_ ด้าน _image analysis_ สามารถใช้งานได้ทั้งแบบมีและไม่มีการปรับแต่ง (_customization_)

ตัวอย่างความสามารถที่สามารถใช้งานได้เลยโดยไม่ต้องปรับแต่ง ได้แก่:

- _การอธิบายภาพด้วยคำบรรยาย_ (_describing an image with captions_)  
- _การตรวจจับวัตถุทั่วไปในภาพ_ (_detecting common objects in an image_)  
- _การใส่แท็กให้กับลักษณะภาพ_ (_tagging visual features_)  
- _การแยกข้อความจากภาพ_ (_optical character recognition_)

### Describing an image with captions

_Azure AI Vision_ มีความสามารถในการวิเคราะห์ภาพ ตรวจประเมินวัตถุที่อยู่ในภาพ และสร้างคำอธิบายที่มนุษย์สามารถเข้าใจได้ (_human-readable description_)

ตัวอย่างเช่น ลองพิจารณาภาพต่อไปนี้:

![Diagram of a person on a skateboard.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-computer-vision-azure/media/skateboard.png)

Azure AI Vision returns the following caption for this image:

_A person jumping on a skateboard_

### Detecting common objects in an image

_Azure AI Vision_ สามารถระบุวัตถุทั่วไปในภาพได้หลายพันรายการ ตัวอย่างเช่น เมื่อนำไปใช้กับภาพนักสเกตบอร์ดที่กล่าวถึงก่อนหน้านี้ ระบบให้ผลลัพธ์ดังนี้:

- _skateboard_ (90.40%)  
- _person_ (95.5%)

ผลลัพธ์เหล่านี้มาพร้อมกับ _confidence score_ ซึ่งบอกว่าระบบมั่นใจแค่ไหนว่าวัตถุที่ตรวจเจอนั้นตรงกับสิ่งที่อยู่ในภาพจริง ๆ

นอกจากชื่อวัตถุและค่าความมั่นใจแล้ว _Azure AI Vision_ ยังส่งค่าพิกัดของ _bounding box_ กลับมาด้วย  
พิกัดเหล่านี้ประกอบด้วย _top_, _left_, _width_, และ _height_  ซึ่งช่วยให้คุณรู้ได้ว่าวัตถุแต่ละชิ้นอยู่ตรงไหนในภาพ ดังตัวอย่างนี้:

![Diagram of a skateboarder with bounding boxes around detected objects.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-computer-vision-azure/media/bounding-boxes.png)

### Tagging visual features

Azure AI Vision สามารถแนะนำ _tags_ สำหรับภาพได้โดยอิงจากเนื้อหาภายในภาพ ซึ่ง _tags_ จะถูกผูกกับภาพในรูปแบบของ _metadata_ โดย _tags_ เหล่านี้ช่วยสรุปลักษณะของภาพนั้น ๆ คุณสามารถใช้ _tags_ เพื่อจัดทำดัชนี (_index_) ให้กับภาพ พร้อมกับชุดของคำสำคัญ (_key terms_) สำหรับใช้ในระบบค้นหา

ตัวอย่างเช่น สำหรับภาพนักสเก็ตบอร์ด (_skateboarder_) ที่ระบบวิเคราะห์แล้วอาจได้ _tags_ ดังต่อไปนี้ (พร้อมคะแนนความมั่นใจหรือ _confidence scores_)

- _sport (99.60%)_
- _person (99.56%)_
- _footwear (98.05%)_
- _skating (96.27%)_
- _boardsport (95.58%)_
- _skateboarding equipment (94.43%)_
- _clothing (94.02%)_
- _wall (93.81%)_
- _skateboarding (93.78%)_
- _skateboarder (93.25%)_
- _individual sports (92.80%)_
- _street stunts (90.81%)_
- _balance (90.81%)_
- _jumping (89.87%)_
- _sports equipment (88.61%)_
- _extreme sport (88.35%)_
- _kickflip (88.18%)_
- _stunt (87.27%)_
- _skateboard (86.87%)_
- _stunt performer (85.83%)_
- _knee (85.30%)_
- _sports (85.24%)_
- _longboard (84.61%)_
- _longboarding (84.45%)_
- _riding (73.37%)_
- _skate (67.27%)_
- _air (64.83%)_
- _young (63.29%)_
- _outdoor (61.39%)_

### Optical character recognition

บริการ Azure AI Vision สามารถใช้ความสามารถของ _optical character recognition (OCR)_ เพื่อตรวจจับข้อความที่อยู่ในภาพได้ ตัวอย่างเช่น ลองพิจารณาภาพของฉลากโภชนาการ (_nutrition label_) บนผลิตภัณฑ์ในร้านขายของชำ ระบบสามารถวิเคราะห์และดึงข้อความจากภาพนั้นออกมาได้อย่างแม่นยำ

![Diagram of a nutrition label.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-computer-vision-azure/media/nutrition-label.png)

บริการ Azure AI Vision สามารถวิเคราะห์ภาพนี้และดึงข้อความต่อไปนี้ออกมาได้:

```text
Nutrition Facts Amount Per Serving
Serving size:1 bar (40g)
Serving Per Package: 4
Total Fat 13g
Saturated Fat 1.5g
Amount Per Serving
Trans Fat 0g
calories 190
Cholesterol 0mg
ories from Fat 110
Sodium 20mg
ntDaily Values are based on
Vitamin A 50
calorie diet
```

## Training custom models

ถ้ารูปแบบโมเดลที่มีอยู่ในระบบของ Azure AI Vision ยังไม่ตอบโจทย์ความต้องการของคุณ คุณสามารถใช้บริการนี้เพื่อ _ฝึกโมเดลแบบกำหนดเอง_ (_custom model_) สำหรับ _image classification_ หรือ _object detection_ ได้  

Azure AI Vision จะสร้างโมเดลแบบกำหนดเองจาก _pre-trained foundation model_ ซึ่งหมายความว่าคุณสามารถฝึกโมเดลที่ซับซ้อนได้ โดยใช้จำนวนภาพสำหรับการฝึก (_training images_) เพียงเล็กน้อย
### Image classification

โมเดล _image classification_ ใช้สำหรับทำนายว่าแต่ละภาพอยู่ในประเภทหรือ _class_ ใด ตัวอย่างเช่น คุณสามารถฝึกโมเดลเพื่อแยกประเภทของผลไม้ในภาพได้ เช่น ตรวจสอบว่าภาพนั้นคือแอปเปิล กล้วย หรือส้ม

| Apple                                                                                                                             | Banana                                                                                                                             | Orange                                                                                                                              |
| --------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| ![Diagram of an apple.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-computer-vision-azure/media/apple.png) | ![Diagram of a banana.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-computer-vision-azure/media/banana.png) | ![Diagram of an orange.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-computer-vision-azure/media/orange.png) |

### Object detection

โมเดล _object detection_ จะตรวจจับและจัดประเภท (_classify_) วัตถุในภาพ พร้อมทั้งส่งคืนพิกัดของ _bounding box_ เพื่อระบุตำแหน่งของแต่ละวัตถุในภาพ นอกจากความสามารถด้าน _object detection_ ที่มีอยู่แล้วใน Azure AI Vision คุณยังสามารถฝึก _custom object detection model_ ด้วยภาพของคุณเองได้อีกด้วย

ตัวอย่างเช่น คุณสามารถใช้ภาพถ่ายของผลไม้ในการฝึกโมเดล เพื่อให้สามารถตรวจจับผลไม้หลายชนิดในภาพเดียวได้

![Diagram of multiple detected fruits in an image.](https://learn.microsoft.com/en-us/training/wwl-data-ai/get-started-computer-vision-azure/media/object-detection.png)

