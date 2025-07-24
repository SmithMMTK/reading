
โมเดล _classification_ ใช้สำหรับการตัดสินใจหรือการจัดประเภทของข้อมูลให้อยู่ในกลุ่มต่าง ๆ ซึ่งแตกต่างจาก _regression_ ที่ให้ผลลัพธ์เป็นตัวเลขแบบ _continuous_ เช่น ส่วนสูงหรือน้ำหนัก โมเดล _classification_ จะให้ผลลัพธ์เป็น _Boolean_ เช่น `true` หรือ `false` หรือเป็นค่าที่อยู่ในกลุ่ม _categorical_ เช่น `apple`, `banana`, หรือ `cherry`

โมเดล _classification_ มีหลายประเภท บางแบบทำงานคล้ายกับ _regression_ แบบดั้งเดิม ขณะที่บางแบบก็ใช้แนวคิดที่แตกต่างโดยสิ้นเชิง หนึ่งในโมเดลที่เหมาะสำหรับการเริ่มต้นเรียนรู้คือ _logistic regression_

## What is logistic regression?

_logistic regression_ เป็นประเภทหนึ่งของโมเดล _classification_ ที่ทำงานคล้ายกับ _linear regression_ ความแตกต่างระหว่าง _logistic_ และ _linear regression_ อยู่ที่รูปทรงของเส้นโค้งที่โมเดลพยายามปรับให้พอดีกับข้อมูล

ในขณะที่ _linear regression_ พยายามหาเส้นตรงเพื่ออธิบายความสัมพันธ์ของข้อมูล _logistic regression_ จะสร้างเส้นโค้งลักษณะรูปตัว S (_s-shaped curve_) ซึ่งเหมาะสำหรับการแบ่งข้อมูลออกเป็นกลุ่ม เช่น ใช่หรือไม่ใช่ (_true/false_) หรือเป็นประเภทใดประเภทหนึ่ง

![diagram showing a logistic regression example graph.](https://learn.microsoft.com/en-us/training/modules/understand-classification-machine-learning/media/2-logistic-regression-graph.png)

_logistic regression_ เหมาะสำหรับการประเมินผลลัพธ์แบบ _Boolean_ มากกว่า _linear regression_ เพราะเส้นโค้งของ _logistic_ จะให้ค่าระหว่าง 0 (_false_) ถึง 1 (_true_) เสมอ เราสามารถตีความค่าที่อยู่ระหว่าง 0 กับ 1 นี้เป็น _probability_ หรือความน่าจะเป็นได้

ตัวอย่างเช่น สมมุติว่าเราต้องการทำนายว่าในวันนี้จะเกิดหิมะถล่มหรือไม่ ถ้าโมเดล _logistic regression_ ให้ผลลัพธ์ออกมาเป็น 0.3 นั่นหมายความว่า โมเดลประเมินว่า **มีโอกาสเกิดหิมะถล่ม 30%**

### Converting outputs to categories

เนื่องจาก _logistic regression_ ให้ผลลัพธ์เป็น _probability_ แทนที่จะเป็นค่า _true/false_ ตรง ๆ เราจึงต้องมีขั้นตอนเพิ่มเติมเพื่อแปลงค่าความน่าจะเป็นนั้นให้เป็นประเภท (_category_) อย่างง่ายที่สุดก็คือการตั้ง _threshold_

เช่น ในกราฟด้านล่าง เราตั้ง _threshold_ ไว้ที่ 0.5 หมายความว่า ถ้าค่า _y_ น้อยกว่า 0.5 เราจะแปลงเป็น _false_ (อยู่ในกล่องล่างซ้าย) และถ้าค่าสูงกว่า 0.5 เราจะแปลงเป็น _true_ (อยู่ในกล่องขวาบน)

![Diagram showing a logistic function graph.](https://learn.microsoft.com/en-us/training/modules/understand-classification-machine-learning/media/2-logistic-function-graph.png)

เมื่อดูจากกราฟ เราจะเห็นว่าเมื่อค่า _feature_ น้อยกว่า 5 ค่าความน่าจะเป็นจะน้อยกว่า 0.5 และจะถูกแปลงเป็น _false_ ส่วนค่า _feature_ ที่มากกว่า 5 จะให้ค่าความน่าจะเป็นมากกว่า 0.5 และถูกแปลงเป็น _true_

สิ่งที่น่าสนใจคือ _logistic regression_ ไม่จำเป็นต้องใช้แค่กับผลลัพธ์แบบ _true/false_ เท่านั้น เราสามารถใช้กับสถานการณ์ที่มีผลลัพธ์มากกว่าสองค่า เช่น `rain`, `snow`, หรือ `sun` ได้เช่นกัน ซึ่งกรณีแบบนี้เรียกว่า _**multinomial logistic regression**_ โดยจะมีการตั้งค่าเพิ่มขึ้นเล็กน้อย แม้ว่าเราจะยังไม่ฝึกใช้ _multinomial logistic regression_ ในบทเรียนต่อไป แต่ก็ควรเก็บไว้พิจารณาเมื่อคุณต้องทำนายข้อมูลที่ไม่ใช่แค่สองทางเลือก

อีกเรื่องที่ควรรู้คือ _logistic regression_ สามารถใช้ _feature_ ได้มากกว่าหนึ่งตัว ซึ่งเราจะพูดถึงในลำดับถัดไป