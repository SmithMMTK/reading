
โซลูชัน Machine Learning ที่ออกแบบอย่างรอบคอบ เป็นรากฐานของแอปพลิเคชัน AI ในปัจจุบัน เช่น การวิเคราะห์เชิงพยากรณ์ (predictive analytics), การแนะนำเฉพาะบุคคล (personalized recommendations) ฯลฯ โดยใช้ข้อมูลที่มีอยู่ในการสร้าง insight ใหม่ ๆ

นักวิทยาศาสตร์ข้อมูล (data scientists) ต้องตัดสินใจในหลายทางเพื่อแก้ปัญหา ML ซึ่งการตัดสินใจเหล่านั้นมีผลต่อ *ต้นทุน*, *ความเร็ว*, *คุณภาพ*, และ *อายุการใช้งาน* ของโซลูชัน

ในโมดูลนี้ คุณจะได้เรียนรู้วิธีออกแบบโซลูชัน ML แบบครบวงจร (end-to-end) บน Microsoft Azure ที่ใช้ได้จริงในระดับองค์กร โดยจะสำรวจผ่านกรอบแนวคิด 6 ขั้นตอน เพื่อวางแผน, ฝึกสอน (train), นำไปใช้งาน (deploy), และติดตามผล (monitor) โซลูชัน ML

![Diagram showing the six steps of the machine learning process.](https://learn.microsoft.com/en-us/training/wwl-data-ai/design-machine-learning-model-training-solution/media/machine-learning-process.png)

1. Define the problem: กำหนดปัญหาให้ชัดเจน – ตัดสินใจว่าโมเดลควร *ทำนายอะไร* และ *เงื่อนไขใดถือว่าโมเดลประสบความสำเร็จ*
2. Get the data: ค้นหาแหล่งข้อมูลที่เหมาะสม และจัดการ *เข้าถึงข้อมูล* ได้อย่างถูกต้อง
3. Prepare the data: สำรวจข้อมูลเบื้องต้น (explore), ทำความสะอาด (clean), และแปลงข้อมูล (transform) ให้ตรงกับ *ข้อกำหนดของโมเดล*
4. Train the model: เลือกอัลกอริทึมที่เหมาะสม พร้อมปรับค่า *hyperparameters* โดยใช้วิธี *ลองผิดลองถูก* (trial and error)
5. Integrate the model: นำโมเดลไป *deploy* บน endpoint เพื่อให้สามารถ *ใช้งานจริงในการทำนาย*
6. Monitor the model: ติดตามประสิทธิภาพของโมเดลอย่างต่อเนื่อง – ดูว่าโมเดลยัง *ทำงานแม่นยำ* หรือไม่