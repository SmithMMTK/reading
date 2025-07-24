
_Regression_ เป็นเทคนิควิเคราะห์ข้อมูลที่ _เรียบง่าย_ ใช้งานบ่อย และมีประโยชน์สูง มักถูกเรียกในภาษาพูดว่า “_การวาดเส้น_” (_fitting a line_) ในรูปแบบที่ง่ายที่สุด _regression_ จะพยายามวาดเส้นตรงระหว่างตัวแปรหนึ่งตัว (_feature_) กับอีกตัวหนึ่ง (_label_)

ในรูปแบบที่ซับซ้อนมากขึ้น _regression_ สามารถค้นหาความสัมพันธ์ที่ไม่เป็นเส้นตรง (_non-linear relationship_) ระหว่าง _label_ หนึ่งตัว กับ _features_ หลายตัวได้

## Simple linear regression

_Simple linear regression_ เป็นการสร้างโมเดลความสัมพันธ์แบบเส้นตรง (_linear relationship_) ระหว่าง _feature_ เพียงตัวเดียว กับ _label_ ซึ่งมักเป็นค่าต่อเนื่อง (_continuous label_) โดยมีจุดมุ่งหมายให้ _feature_ สามารถใช้ทำนาย _label_ ได้

เมื่อมองด้วยภาพ ก็จะดูเหมือนมี _เส้นตรงหนึ่งเส้น_ ที่พาดผ่านข้อมูลเพื่อตัวแทนความสัมพันธ์นั้น

![Diagram of a simple linear regression graph on the relationship between age and body temperature.](https://learn.microsoft.com/en-us/training/modules/understand-regression-machine-learning/media/2-simple-linear-regression.png)

_Simple linear regression_ มี _พารามิเตอร์_ อยู่ 2 ตัวคือ:

- _intercept_ (_c_) คือค่าของ _label_ เมื่อตั้งค่า _feature_ ให้เท่ากับศูนย์
- _slope_ (_m_) คืออัตราที่ _label_ จะเพิ่มขึ้นเมื่อ _feature_ เพิ่มขึ้นทีละ 1 หน่วย

ถ้าชอบคิดในเชิงคณิตศาสตร์ ก็สามารถเขียนเป็นสมการง่าย ๆ ได้ว่า:

_y = m·x + c_

โดยที่ _y_ คือ _label_ และ _x_ คือ _feature_

เช่นในสถานการณ์ของเรา ถ้าเราต้องการทำนายว่าแต่ละตัวจะมีไข้หรือไม่ (อุณหภูมิร่างกายสูงขึ้น) จากอายุของสุนัข เราอาจใช้โมเดล:

_temperature = m·age + c_

โดยเราต้องหา _ค่าของ m และ c_ จากกระบวนการ _fitting_ เช่น ถ้าได้ว่า m = 0.5 และ c = 37 ก็แปลว่าอุณหภูมิของสุนัขจะเริ่มที่ 37 องศา และเพิ่มขึ้น 0.5 องศาต่ออายุที่เพิ่มขึ้น 1 ปี

![Diagram showing a simple linear regression graph, of the relationship between age and body temperature with a sharper line.](https://learn.microsoft.com/en-us/training/modules/understand-regression-machine-learning/media/2-linear-graph.png)

ซึ่งหมายความว่า _ทุก ๆ 1 ปี_ ที่อายุเพิ่มขึ้น จะสัมพันธ์กับ _อุณหภูมิร่างกายที่เพิ่มขึ้น 0.5°C_ โดยมีจุดเริ่มต้นที่ _37°C_ เมื่ออายุเท่ากับ 0

## Fitting linear regression

โดยปกติเราจะใช้ _ไลบรารี_ ที่มีอยู่แล้วในการ _fit โมเดล regression_ ให้เราอัตโนมัติ จุดประสงค์หลักของ _regression_ คือการหาเส้นที่ทำให้เกิด _error_ น้อยที่สุด ซึ่ง _error_ ในที่นี้หมายถึง _ความต่างระหว่างค่าจริงของข้อมูล_ กับ _ค่าที่โมเดลทำนายได้_

เช่น ในภาพตัวอย่าง เส้นสีดำจะแสดงถึง _ค่า error_ ระหว่างจุดข้อมูลจริง (จุดกลม) กับค่าที่ถูกทำนายโดยโมเดล (เส้นสีแดง)

![Diagram showing fitting a linear regression graph with plot points and a black line to indicate error.](https://learn.microsoft.com/en-us/training/modules/understand-regression-machine-learning/media/2-fitting-linear-regression.png)

ถ้าดูจากสองจุดนี้บนแกน _y_ จะเห็นว่า _ค่าที่โมเดลทำนาย_ คือ 39.5 แต่ _ค่าจริง_ ของข้อมูลคือ 41

![Diagram showing fitting a linear regression graph with plot points and a dotted black line to measure error.](https://learn.microsoft.com/en-us/training/modules/understand-regression-machine-learning/media/2-fitting-linear-regression.2.png)

ดังนั้นโมเดลนี้ _ผิดไป 1.5_ สำหรับจุดข้อมูลนี้

โดยทั่วไป เราจะ _fit โมเดล_ ด้วยการ _ลดค่าผลรวมของค่าความคลาดเคลื่อนยกกำลังสอง_ (_residual sum of squares_) ให้ต่ำที่สุด ซึ่งขั้นตอนของการคำนวณ _cost function_ มักทำตามลำดับดังนี้:

1. คำนวณ _ความต่างระหว่างค่าจริงกับค่าที่ทำนายได้_ ของแต่ละจุด (เหมือนที่ทำไปก่อนหน้า)
2. ยกกำลังสองของค่าความต่างเหล่านั้น
3. รวม (หรือเฉลี่ย) ค่าที่ยกกำลังสองแล้วทั้งหมด

ขั้นตอนการยกกำลังสองนี้ทำให้ _แต่ละจุดมีผลต่อเส้นไม่เท่ากัน_ โดยเฉพาะพวก _outliers_ ซึ่งคือจุดที่ _เบี่ยงเบนจากรูปแบบหลักของข้อมูล_ จะมี _error_ ที่ใหญ่มากเกินไป และสามารถส่งผลกระทบต่อ _ตำแหน่งของเส้น regression_ ได้อย่างมีนัยสำคัญ

## Strengths of regression

เทคนิค _regression_ มี _จุดแข็ง_ หลายอย่างที่โมเดลที่ซับซ้อนกว่ายังไม่มีหรือทำได้ยาก

### Predictable and easy to interpret

โมเดล _regression_ เข้าใจง่ายเพราะใช้ _สมการคณิตศาสตร์แบบพื้นฐาน_ ที่สามารถ _วาดกราฟ_ ออกมาได้ โมเดลที่ซับซ้อนกว่านั้นมักถูกเรียกว่า _black box_ เพราะเราไม่สามารถรู้ได้แน่ชัดว่าโมเดลคิดอย่างไรหรือตอบสนองต่อข้อมูลอย่างไร

### Easy to extrapolate

โมเดล _regression_ สามารถใช้ _ทำนายค่าที่อยู่นอกขอบเขตของข้อมูล_ ได้ค่อนข้างสะดวก เช่น จากตัวอย่างก่อนหน้า เราสามารถประมาณได้ง่าย ๆ ว่าสุนัขอายุ 9 ปีจะมีอุณหภูมิประมาณ _40.5°C_

แต่อย่าลืมว่า _การขยายผลต้องใช้ความระมัดระวัง_ เช่น โมเดลเดียวกันนี้จะทำนายว่าสุนัขอายุ 90 ปีจะมีอุณหภูมิสูงเกือบเดือด ซึ่งไม่สมเหตุสมผลเลย

### Optimal fitting is usually guaranteed

โมเดล machine learning ส่วนใหญ่ใช้วิธี _gradient descent_ เพื่อ _fit โมเดล_ ซึ่งต้องมีการปรับแต่งหลายจุดและไม่สามารถรับประกันว่าจะเจอคำตอบที่ดีที่สุดเสมอไป

แต่ในทางกลับกัน _linear regression_ ที่ใช้ _sum of squares_ เป็น _cost function_ ไม่จำเป็นต้องพึ่งกระบวนการ _gradient descent_ แบบวนซ้ำเลย เราสามารถใช้วิธีทางคณิตศาสตร์โดยตรงเพื่อคำนวณตำแหน่งของเส้นที่ดีที่สุดได้

แม้คณิตศาสตร์เบื้องหลังจะอยู่นอกขอบเขตของโมดูลนี้ แต่สิ่งที่ควรรู้คือ _ถ้าขนาดข้อมูลไม่ใหญ่มาก_ _linear regression_ จะสามารถหาคำตอบที่ดีที่สุดได้ _โดยไม่ต้องปรับค่าอะไรเป็นพิเศษ_ และ _รับประกันได้ว่าได้คำตอบที่เหมาะสมที่สุด_

