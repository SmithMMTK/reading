
จนถึงตอนนี้ เราได้เรียนรู้เฉพาะ _linear regression_ ซึ่งเป็นโมเดลที่ใช้ _เส้นตรง_ แทนความสัมพันธ์ระหว่าง _feature_ และ _label_ แต่ในความเป็นจริง _regression_ สามารถนำไปใช้กับความสัมพันธ์ที่มีรูปร่างอื่น ๆ ได้เช่นกัน

## Polynomial regression คืออะไร?

_Polynomial regression_ เป็นการสร้างโมเดลที่ใช้ _เส้นโค้งประเภทหนึ่ง_ เพื่ออธิบายความสัมพันธ์ระหว่างข้อมูล โดย _polynomial_ เป็นตระกูลของสมการที่สามารถสร้างเส้นโค้งได้หลายแบบ ตั้งแต่แบบเรียบง่ายไปจนถึงซับซ้อน ยิ่งมี _พารามิเตอร์ในสมการมาก_ เส้นโค้งก็สามารถมีรูปร่างที่ _ซับซ้อนขึ้น_ ได้

ตัวอย่างเช่น _polynomial ที่มี 2 พารามิเตอร์_ ก็จะกลายเป็นเพียง _เส้นตรงธรรมดา_

y = intercept + B1·x

![Diagram showing a two-parameter polynomial regression graph.](https://learn.microsoft.com/en-us/training/modules/understand-regression-machine-learning/media/6-polynomial-graph.png)

ถ้าเป็น _polynomial ที่มี 3 พารามิเตอร์_ เส้นโค้งจะมี _จุดหักงอ_ หรือ _โค้ง_ อยู่หนึ่งครั้ง

y = intercept + B1*x + B2 * x2

![Diagram showing a three-parameter polynomial regression graph.](https://learn.microsoft.com/en-us/training/modules/understand-regression-machine-learning/media/6-three-parameter-polynomial.png)

ถ้าเป็น _polynomial ที่มี 4 พารามิเตอร์_ ก็สามารถมี _จุดโค้ง_ หรือ _หักงอ_ ได้ถึง _สองครั้ง_

y = intercept + B1*x + B2 * x2 + B3 * x3

![Diagram showing a four-parameter polynomial regression graph.](https://learn.microsoft.com/en-us/training/modules/understand-regression-machine-learning/media/6-four-parameter-polynomial.png)

### Polynomial versus other curves

นอกจาก _polynomial_ แล้ว ยังมี _เส้นโค้ง_ อีกหลายประเภทที่สามารถใช้ร่วมกับ _regression_ ได้ เช่น _logarithmic curve_ และ _logistic curve_ (ซึ่งมีลักษณะเป็นรูปตัว S)

เส้นโค้งเหล่านี้สามารถใช้สร้างโมเดลเพื่อจับความสัมพันธ์ในรูปแบบต่าง ๆ ได้เช่นกัน

![Diagram showing polynomial, log and logistic curves.](https://learn.microsoft.com/en-us/training/modules/understand-regression-machine-learning/media/6-polynomial-vs-curves.png)

ข้อดีสำคัญของ _polynomial regression_ คือสามารถใช้ _จับความสัมพันธ์ที่หลากหลายรูปแบบ_ ได้

เช่น เราสามารถใช้ _polynomial regression_ กับความสัมพันธ์ที่เป็น _ลบ_ ในช่วงค่าหนึ่งของ _feature_ แต่กลายเป็น _บวก_ ในช่วงอื่นได้ หรือในกรณีที่ _label_ (_ค่า y_) _ไม่มีขีดจำกัดบนทางทฤษฎี_ ก็สามารถใช้ polynomial regression ได้อย่างยืดหยุ่นเช่นกัน

![Diagram showing polynomial, log and logistic curves with plot points on the polynomial curve.](https://learn.microsoft.com/en-us/training/modules/understand-regression-machine-learning/media/6-example-curves.png)

ข้อเสียสำคัญของเส้นโค้ง _polynomial_ คือ _มักจะขยายผล (extrapolate) ได้ไม่ดี_

กล่าวอีกแบบคือ ถ้าเราพยายามทำนายค่าที่ _อยู่นอกช่วงของข้อมูลฝึก_ โมเดลอาจให้ผลลัพธ์ที่ _เกินจริง_ หรือ _สุดโต่งเกินเหตุ_

อีกข้อเสียหนึ่งคือ _polynomial regression_ มักจะ _overfit_ ได้ง่าย นั่นคือ _โมเดลอาจปรับรูปร่างของเส้นโค้งไปตาม “เสียงรบกวน” ในข้อมูล_ มากเกินไป ซึ่งต่างจากโมเดลที่เรียบง่ายกว่า เช่น _simple linear regression_ ที่จะคงรูปและทนต่อ noise ได้ดีกว่า

![Diagram showing an incorrect polynomial curve with plots.](https://learn.microsoft.com/en-us/training/modules/understand-regression-machine-learning/media/6-curve.png)

## Can curves be used with multiple features?

เราได้เห็นแล้วว่า _multiple regression_ สามารถ _สร้างความสัมพันธ์เชิงเส้นหลายชุด_ ได้พร้อมกัน แต่ความสัมพันธ์เหล่านี้ _ไม่จำเป็นต้องจำกัดอยู่แค่แบบเส้นตรง_ เสมอไป

เราสามารถใช้ _เส้นโค้งรูปแบบต่าง ๆ_ ได้เช่นกันถ้าเหมาะสมกับข้อมูล

แต่อย่างไรก็ตาม ควรระวัง _ไม่ใช้เส้นโค้งอย่าง polynomial กับ features หลายตัว_ หากไม่จำเป็น เพราะจะทำให้ความสัมพันธ์ระหว่างข้อมูล _ซับซ้อนเกินไป_ ซึ่งจะทำให้ _เข้าใจโมเดลได้ยาก_ และยากต่อการประเมินว่าโมเดลจะทำนายผล _ผิดจากความเป็นจริงในโลกจริง_ หรือไม่