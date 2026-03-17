# ⚡ ระบบจัดการตารางเวรแก้กระแสไฟฟ้าขัดข้อง
### การไฟฟ้าส่วนภูมิภาค สาขา ชยน. (กฟส.ชยน.)

---

## 🚀 วิธีรันโปรเจกต์

### ความต้องการของระบบ
- [Node.js](https://nodejs.org/) v18 ขึ้นไป
- npm v9 ขึ้นไป

### ขั้นตอน
```bash
# 1. ติดตั้ง dependencies
npm install

# 2. รันในโหมด development
npm run dev

# 3. เปิดเบราว์เซอร์ที่
http://localhost:5173
```

### Build สำหรับ Production
```bash
npm run build
# ไฟล์จะอยู่ที่ dist/
```

---

## 📁 โครงสร้างโปรเจกต์

```
duty-schedule/
├── index.html                  # Entry point (Vite)
├── vite.config.js              # Vite config
├── package.json
├── .gitignore
└── src/
    ├── main.jsx                # React bootstrap
    ├── App.jsx                 # หน้าหลัก + layout
    ├── index.css               # Global styles
    ├── data/
    │   ├── employees.js        # ข้อมูลพนักงาน / ผู้ตรวจ / ช่างไฟฟ้า
    │   └── schedule.js         # ตารางเวร มีนาคม 2569
    └── components/
        ├── EditModal.jsx       # Modal แก้ไข / สลับเวร
        ├── ReportModal.jsx     # Modal ออกรายงานเวร
        └── ui/
            ├── Overlay.jsx     # Backdrop overlay
            └── NickChip.jsx    # Badge ชื่อพนักงาน (มีสี)
```

---

## 🌐 Deploy บน GitHub Pages

### วิธีที่ 1 — Manual

```bash
# Build
npm run build

# Push โฟลเดอร์ dist/ ขึ้น branch gh-pages
npm install -g gh-pages
gh-pages -d dist
```

### วิธีที่ 2 — GitHub Actions (อัตโนมัติ)

สร้างไฟล์ `.github/workflows/deploy.yml` ด้วยเนื้อหาด้านล่าง:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm install
      - run: npm run build
      - uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

> ⚠️ อย่าลืมแก้ `base` ใน `vite.config.js` ให้ตรงกับชื่อ repo:
> ```js
> base: '/ชื่อ-repo-ของคุณ/'
> ```

---

## ✨ ฟีเจอร์

| ฟีเจอร์ | รายละเอียด |
|---|---|
| 📅 ตารางเวร | แสดง 3 กะพร้อมกัน พร้อมสีแยกตามพนักงาน |
| ✏️ แก้ไขเวร | เปลี่ยนชื่อพนักงาน เพิ่ม/ลบ reset ได้ |
| 🔄 สลับเวร | คลิกสองชื่อเพื่อสลับ ข้ามกะได้ |
| 📋 รายงานเวร | สร้าง + คัดลอกรายงานอัตโนมัติ |
| 👥 รายชื่อพนักงาน | ข้อมูลครบ พร้อมเบอร์โทร |

---

*พัฒนาโดย Claude • กฟส.ชยน. มีนาคม 2569*
