
## Multiclass Classification

*Multiclass classification* ใช้สำหรับทำนายว่าข้อมูลหนึ่ง ๆ ควรถูกจัดอยู่ในคลาสใดจากหลายคลาสที่เป็นไปได้  
เป็นเทคนิค *supervised learning* เช่นเดียวกับ regression และ binary classification  
จึงใช้กระบวนการฝึกโมเดลแบบวนซ้ำคือ *train → validate → evaluate*

ในขั้นตอนนี้จะมีการกันข้อมูลบางส่วนจาก training dataset ไว้เพื่อใช้ตรวจสอบความแม่นยำของโมเดลที่ฝึกแล้ว

### Example – Multiclass Classification

*Multiclass classification* ใช้อัลกอริทึมที่คำนวณค่าความน่าจะเป็นของแต่ละคลาส  
เพื่อให้โมเดลสามารถทำนายคลาสที่มีความเป็นไปได้สูงที่สุดสำหรับข้อมูลหนึ่ง ๆ ได้

ตัวอย่างเช่น สมมุติว่าเรามีข้อมูลเกี่ยวกับเพนกวิน โดยวัด *ความยาวของครีบ* (_x_)  
และทราบสายพันธุ์ของเพนกวินแต่ละตัว (_y_) ซึ่งถูกเข้ารหัสไว้ดังนี้:

- 0: Adelie  
- 1: Gentoo  
- 2: Chinstrap

| **Flipper length (x)** | **Species (y)** |
| ---------------------- | --------------- |
| 167                    | 0               |
| 172                    | 0               |
| 225                    | 2               |
| 197                    | 1               |
| 189                    | 1               |
| 232                    | 2               |
| 158                    | 0               |

## Training a Multiclass Classification Model

การฝึกโมเดล *multiclass classification* ต้องใช้อัลกอริทึมที่สามารถเรียนรู้จากข้อมูล  
และสร้างฟังก์ชันที่คำนวณค่าความน่าจะเป็นสำหรับแต่ละคลาสที่เป็นไปได้

อัลกอริทึมที่นิยมใช้มี 2 ประเภทหลัก:

- **One-vs-Rest (OvR)**: แยกปัญหา multiclass ออกเป็นหลาย binary classification โดยให้แต่ละคลาสแข่งกับคลาสอื่นรวมกัน (หนึ่งคลาส vs ที่เหลือ)
- **Multinomial**: สร้างฟังก์ชันที่คำนวณความน่าจะเป็นของทุกคลาสพร้อมกัน โดยตรง

### One-vs-Rest (OvR) Algorithms

*One-vs-Rest* เป็นเทคนิคที่แปลงปัญหา multiclass ให้กลายเป็นหลายปัญหา binary classification  
โดยจะฝึกฟังก์ชันแยกแต่ละคลาสออกจากคลาสอื่น ๆ ทั้งหมด

สำหรับโมเดลจำแนกสายพันธุ์เพนกวิน จะได้ฟังก์ชันดังนี้:

- f⁰(x) = P(y = 0 | x)
- f¹(x) = P(y = 1 | x)
- f²(x) = P(y = 2 | x)

แต่ละฟังก์ชันจะเป็น sigmoid function ที่ให้ค่าความน่าจะเป็นระหว่าง 0.0 ถึง 1.0  
โมเดลจะเลือกคลาสที่ให้ค่าความน่าจะเป็นสูงที่สุดเป็นคำตอบสุดท้าย

### Multinomial Algorithms

*Multinomial* เป็นอัลกอริทึมที่ใช้ในการแก้ปัญหา *multiclass classification*  
โดยสร้างฟังก์ชันเดียวที่ให้ผลลัพธ์เป็นเวกเตอร์ของความน่าจะเป็นสำหรับแต่ละคลาส

ผลลัพธ์คือเวกเตอร์ (หรืออาเรย์ของค่า) ที่แสดงการแจกแจงความน่าจะเป็นของทุกคลาส  
โดยแต่ละคลาสจะมีค่าความน่าจะเป็นของตนเอง และผลรวมของค่าทั้งหมดจะเท่ากับ 1.0

เช่น:  
f(x) = [P(y = 0 | x), P(y = 1 | x), P(y = 2 | x)]

ฟังก์ชันที่นิยมใช้คือ *softmax* ซึ่งอาจให้ผลลัพธ์เช่น:  
[0.2, 0.3, 0.5]

ค่าทั้งสามแทนความน่าจะเป็นของคลาส 0, 1 และ 2 ตามลำดับ  
ในกรณีนี้ โมเดลจะเลือกคลาส 2 เพราะมีความน่าจะเป็นสูงที่สุด

ไม่ว่าจะใช้อัลกอริทึมแบบ *One-vs-Rest* หรือ *multinomial*  
เป้าหมายสุดท้ายคือการใช้ฟังก์ชันที่ได้จากการฝึกโมเดล เพื่อเลือกคลาสที่น่าจะเป็นที่สุดจาก features (_x_) และทำนาย label (_y_) ให้เหมาะสม

## Evaluating a Multiclass Classification Model

เราสามารถประเมินโมเดล *multiclass classification* ได้ 2 วิธีหลัก:

- คำนวณเมตริกแบบ *binary classification* แยกแต่ละคลาส  
  (เช่น precision, recall, F1-score ของแต่ละคลาส)
- คำนวณเมตริกแบบรวม (*aggregate metrics*) ที่พิจารณาทุกคลาสรวมกัน  
  (เช่น macro average, micro average)

สมมุติว่าเราได้ทำการ validate โมเดล multiclass แล้ว และได้ผลลัพธ์ดังนี้:

| Flipper length (x) | Actual species (y) | Predicted species (ŷ) |
| ------------------ | ------------------ | --------------------- |
| 165                | 0                  | 0                     |
| 171                | 0                  | 0                     |
| 205                | 2                  | 1                     |
| 195                | 1                  | 1                     |
| 183                | 1                  | 1                     |
| 221                | 2                  | 2                     |
| 214                | 2                  | 2                     |
The confusion matrix for a *multiclass classifier* คล้ายกับของ *binary classifier*  
แต่จะมีหลายแถวและหลายคอลัมน์มากกว่า  
โดยแสดงจำนวนการทำนาย (ŷ) เทียบกับค่าจริง (y) สำหรับแต่ละคลาส

![Diagram of a multiclass confusion matrix.](https://learn.microsoft.com/en-us/training/wwl-data-ai/fundamentals-machine-learning/media/multiclass-confusion-matrix.png)

จาก confusion matrix นี้ เราสามารถคำนวณเมตริกแยกสำหรับแต่ละคลาสได้ดังนี้:

- **Recall** (หรือ *Sensitivity*): สัดส่วนของข้อมูลที่เป็นคลาสนั้นจริง ๆ แล้วโมเดลทำนายถูก  
  Recall = TP / (TP + FN)
- **Precision**: สัดส่วนของการทำนายว่าเป็นคลาสนั้น แล้วถูกจริง  
  Precision = TP / (TP + FP)
- **F1-score**: ค่ากลางระหว่าง precision และ recall  
  F1 = 2 × (Precision × Recall) / (Precision + Recall)

เราจะคำนวณ TP, FP, FN และ TN ของแต่ละคลาสโดยพิจารณาว่า  
"คลาสที่สนใจ = positive" และ "คลาสอื่น ๆ = negative"

| Class | TP  | TN  | FP  | FN  | Accuracy | Recall | Precision | F1-Score |
| ----- | --- | --- | --- | --- | -------- | ------ | --------- | -------- |
| **0** | 2   | 5   | 0   | 0   | 1.0      | 1.0    | 1.0       | 1.0      |
| **1** | 2   | 4   | 1   | 0   | 0.86     | 1.0    | 0.67      | 0.8      |
| **2** | 2   | 4   | 0   | 1   | 0.86     | 0.67   | 1.0       | 0.8      |
ในการคำนวณเมตริกโดยรวมของโมเดล *multiclass classification*  
ให้นำค่า TP, TN, FP, และ FN จากทุกคลาสมารวมกัน

- **Overall Accuracy** = (TN + TP) ÷ (TN + FN + FP + TP)
  = (13 + 6) ÷ (13 + 6 + 1 + 1) = **0.90**

- **Overall Recall** = TP ÷ (TP + FN)  
  = 6 ÷ (6 + 1) = **0.86**

- **Overall Precision** = TP ÷ (TP + FP)  
  = 6 ÷ (6 + 1) = **0.86**

- **Overall F1-score** = (2 × Precision × Recall) ÷ (Precision + Recall)  
  = (2 × 0.86 × 0.86) ÷ (0.86 + 0.86) = **0.86**

