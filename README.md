# ระบบคลังสินค้า — คู่มือ Deploy

## 📁 ไฟล์ในโฟลเดอร์นี้
```
index.html   ← ตัวแอปหลัก (แก้ไข URL+KEY ก่อน deploy)
vercel.json  ← config สำหรับ Vercel
README.md    ← ไฟล์นี้
```

---

## ขั้นตอนที่ 1 — ตั้งค่า Supabase ใน index.html

เปิดไฟล์ `index.html` หาบรรทัดนี้ (ประมาณบรรทัด 290):

```javascript
var SUPABASE_URL = 'https://YOUR_PROJECT.supabase.co';   // ← วาง Project URL
var SUPABASE_KEY = 'YOUR_ANON_KEY';                       // ← วาง anon/public key
```

แก้เป็นค่าจริงจาก:
**Supabase Dashboard → Settings → API**

ตัวอย่าง:
```javascript
var SUPABASE_URL = 'https://abcdefghijkl.supabase.co';
var SUPABASE_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...';
```

---

## ขั้นตอนที่ 2 — ทดสอบในเครื่องก่อน

เปิด index.html ใน browser โดยตรง (double-click) ถ้าเห็นข้อมูลจาก Supabase แสดงว่าพร้อม

---

## ขั้นตอนที่ 3 — Deploy ขึ้น Vercel (ฟรี)

### วิธีที่ 1: ลากวางง่ายที่สุด
1. ไปที่ https://vercel.com → Sign up ด้วย GitHub/Google
2. กดปุ่ม **"Add New Project"** → **"Browse"**
3. **ลาก folder `inventory_app` ทั้งโฟลเดอร์** วางลงในหน้า Vercel
4. กด **Deploy** → รอ ~30 วินาที
5. ได้ URL เช่น `https://inventory-app-xxx.vercel.app`

### วิธีที่ 2: ผ่าน GitHub (แนะนำสำหรับ update ในอนาคต)
1. สร้าง repo ใหม่ใน GitHub (private ได้)
2. upload ไฟล์ทั้งสองขึ้น repo
3. Vercel → Import Git Repository → เลือก repo
4. Deploy → ได้ URL
5. ต่อไปถ้าแก้ไขไฟล์และ push → Vercel auto-deploy ทันที

---

## ⚠️ ก่อน Production จริง

1. **Supabase RLS** — ไปที่ Supabase → Authentication → เปิดระบบ login
   แล้วแก้ Policy จาก `allow_all_dev` เป็น policy ที่ require authentication

2. **Custom Domain** — Vercel รองรับ custom domain ฟรี
   เช่น `inventory.yourcompany.com`

3. **Environment Variables** (ถ้าต้องการซ่อน key) — 
   ใช้ Vercel Edge Config หรือ build-time injection แทนการใส่ key ตรงในไฟล์

---

## Free Tier Limits

| บริการ | ฟรี | เกิน |
|--------|-----|------|
| Supabase | 500MB DB, 2 projects | $25/เดือน |
| Vercel | Bandwidth ไม่จำกัด, 100GB | $20/เดือน |
