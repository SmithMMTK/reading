
## 📚 ทำไมต้องใช้ n-grams? แล้วได้อะไร?

### 🔍 n-grams คืออะไร?
- การจับกลุ่มคำที่อยู่ติดกันในข้อความ
- ประเภทของ n-grams:
  - **Unigram**: คำเดี่ยว เช่น `"I"`, `"have"`
  - **Bi-gram**: 2 คำติดกัน เช่น `"I have"`, `"have a"`
  - **Tri-gram**: 3 คำติดกัน เช่น `"I have a"`, `"have a dream"`

---

### ✅ ทำไมต้องใช้ n-grams?

| เหตุผล | อธิบาย |
|--------|--------|
| **เข้าใจบริบทของคำ** | คำเดียวอาจมีหลายความหมาย ต้องดูคำรอบข้าง |
| **วิเคราะห์วลีสำคัญ** | เช่น `"easy to use"` บ่งบอกถึงความคิดเห็นเชิงบวก |
| **สร้างโมเดลภาษา** | ใช้เดาคำถัดไปในประโยค เช่น `"I want to ___"` |
| **แยกคำเฉพาะทาง** | เช่น `"machine learning"` คือคำเฉพาะ ไม่ใช่ "machine" กับ "learning" แยกกัน |

---

### 🧠 ตัวอย่างจากประโยค:
> `"I have a dream that one day"`

- **Unigrams**: `["I", "have", "a", "dream", "that", "one", "day"]`
- **Bi-grams**: `["I have", "have a", "a dream", "dream that", "that one", "one day"]`
- **Tri-grams**: `["I have a", "have a dream", "a dream that", "dream that one", "that one day"]`

---

### 🎯 สรุป

- n-grams ช่วยให้ระบบเข้าใจข้อความดีขึ้น
- เหมาะกับงานอย่าง:
  - การวิเคราะห์ความรู้สึก (Sentiment Analysis)
  - การสร้างระบบแนะนำ (Recommendation)
  - การเดาคำถัดไป (Next-word prediction)