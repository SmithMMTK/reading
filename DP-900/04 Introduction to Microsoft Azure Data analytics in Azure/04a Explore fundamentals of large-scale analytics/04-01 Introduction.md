
โซลูชัน _large-scale data analytics_ คือการผสมผสานระหว่างระบบคลังข้อมูลแบบดั้งเดิม (_data warehousing_) ที่ใช้สนับสนุน _business intelligence (BI)_ กับเทคนิคการวิเคราะห์ _big data_ 

ระบบ _data warehousing_ แบบดั้งเดิม มักเริ่มจากการ _copy_ ข้อมูลจากระบบธุรกรรม (_transactional data stores_) แล้วโหลดเข้าไปยังฐานข้อมูลแบบ _relational_ ที่ออกแบบ _schema_ ไว้ให้เหมาะสำหรับการสืบค้นและสร้างโมเดลแบบ _multidimensional_

ในทางตรงกันข้าม ระบบประมวลผล _Big Data_ จะจัดการข้อมูลปริมาณมากที่มาในหลากหลายรูปแบบ ทั้งแบบ _batch_ และแบบ _real-time stream_ โดยข้อมูลจะถูกจัดเก็บไว้ใน _data lake_ แล้วใช้ _distributed processing engine_ อย่างเช่น _Apache Spark_ ในการประมวลผล

การรวมกันของการจัดเก็บข้อมูลที่ยืดหยุ่นใน _data lake_ และความสามารถในการวิเคราะห์แบบ _SQL_ จาก _data warehouse_ นำไปสู่รูปแบบการออกแบบระบบวิเคราะห์ข้อมูลขนาดใหญ่ที่เรียกว่า _data lakehouse_

