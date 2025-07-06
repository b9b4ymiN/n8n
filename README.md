# My Personal n8n Instance on Render

นี่คือโปรเจกต์สำหรับรัน n8n instance ส่วนตัวของผม ซึ่งถูก deploy และทำงานอยู่บน [Render](https://render.com/) โดยใช้บริการใน Free Tier

โปรเจกต์นี้เป็นการ "Fork" มาจากโปรเจกต์ต้นแบบ [render-examples/n8n](https://github.com/render-examples/n8n) และได้มีการปรับแก้ไฟล์ `render.yaml` เพื่อให้ใช้ชื่อ Service ที่กำหนดเองได้

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/b9b4ymiN/n8n)


## 🛠️ สรุปขั้นตอนการติดตั้ง (Initial Setup Summary)

1.  **Fork Repository:** คัดลอกโปรเจกต์จาก `render-examples/n8n` มาไว้ที่บัญชีนี้
2.  **แก้ไข `render.yaml`:**
    - เข้าไปแก้ไขไฟล์ `render.yaml` โดยตรงใน GitHub
    - เปลี่ยนค่า `name` จาก `n8n-service` เป็น `hatai-n8n` เพื่อกำหนด URL ที่ต้องการตั้งแต่ต้น
3.  **Deploy บน Render:**
    - ใช้ฟีเจอร์ **"New Blueprint"** ในการติดตั้ง
    - เชื่อมต่อกับ Repository นี้
4.  **ตั้งค่า Environment Variables:**
    - `GENERIC_TIMEZONE`: `Asia/Bangkok`
5.  **ตั้งค่า Keep-Alive:**
    - ใช้บริการภายนอก (cron-job.org) เพื่อยิง request มาที่ URL ของ n8n เพื่อป้องกันไม่ให้ Service เข้าสู่สถานะ Sleep

---

## 🔄 วิธีการอัปเดตในอนาคต (How to Update)

Render ถูกตั้งค่าให้ **Auto-Deploy** หมายความว่าทุกครั้งที่มีการ `push` การเปลี่ยนแปลงใหม่ๆ มาที่ `main` branch ของ Repository นี้ Render จะทำการดึงโค้ดไปติดตั้งใหม่อัตโนมัติ

หากต้องการอัปเดต n8n ให้เป็นเวอร์ชันล่าสุดตามโปรเจกต์ต้นฉบับ สามารถทำได้โดยใช้คำสั่ง Git บนเครื่องคอมพิวเตอร์ของคุณ:

```bash
# 1. ดึงการเปลี่ยนแปลงล่าสุดจากโปรเจกต์ต้นฉบับ (upstream)
git pull upstream main

# 2. ส่งการเปลี่ยนแปลงที่ได้มาไปยัง Repository ของคุณบน GitHub (origin)
git push origin main
```

หลังจาก `push` เสร็จแล้ว Render จะเริ่มกระบวนการ deploy ใหม่ให้เอง

 