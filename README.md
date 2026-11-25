# bunk releases

ไฟล์ดาวน์โหลดของ **bunk** โปรแกรมรัน คุม และดูสถานะคำสั่งที่ต้องรันค้างไว้บนเครื่อง dev บน Windows (เช่น `npm run dev`, `python`, `redis-server`, ssh tunnel) แนวคิดเดียวกับ Docker Compose แต่รันคำสั่งตรงๆ ไม่ใช้ container

## ดาวน์โหลดและติดตั้ง

โหลด [`bunk.exe`](https://github.com/Ratchx/bunk-releases/releases/latest/download/bunk.exe) ไฟล์เดียว (ประมาณ 330 MB มี WebView2 มาด้วย หรือเลือกเวอร์ชันที่หน้า [Releases](https://github.com/Ratchx/bunk-releases/releases)) แล้วดับเบิลคลิก จะมีให้เลือก

- **ติดตั้ง** (แนะนำ) ลงที่ `%LOCALAPPDATA%\Programs\bunk` ไม่ต้องใช้สิทธิ์ admin เปิดได้จาก Start menu และพิมพ์ `bunk` ใน terminal ไหนก็ได้ (terminal ที่เปิดไว้ก่อนติดตั้งต้องเปิดใหม่) ติ๊กสร้างทางลัดบน Desktop ได้
- **ใช้แบบพกพา** ไม่ติดตั้ง วาง `bunk.com` ไว้ข้าง `bunk.exe` ในโฟลเดอร์นั้นแล้วเปิดเลย ไม่แตะ Start menu หรือ PATH

ถอนการติดตั้งได้ที่ Settings › Apps › Installed apps › bunk › Uninstall service ทุกตัวจะหยุด และเลือกได้ว่าจะลบรายการโปรเจกต์กับ log ด้วยไหม (ไฟล์ `bunk.toml` ในโปรเจกต์ไม่ถูกแตะ)

- ไฟล์ยังไม่ได้เซ็น code signing ครั้งแรกที่เปิด Windows อาจขึ้น "Windows protected your PC" ให้กด More info → Run anyway
- ติดตั้ง/ถอนแบบไม่ถามด้วย `bunk.exe --install --quiet` และ `bunk.exe --uninstall --quiet` (ใช้ในสคริปต์หรือบน Server ได้)
- ไม่ต้องติดตั้ง WebView2 เอง: เครื่องที่มีอยู่แล้ว (Windows 11, Server 2025, Windows 10 ส่วนใหญ่) bunk ใช้ของ Windows ส่วนเครื่องที่ไม่มี (เช่น Server 2019/2022) bunk แตก WebView2 ที่มาในไฟล์ไว้ในโฟลเดอร์ `webview2` ข้างโปรแกรม (ประมาณ 1 GB ใช้ได้แม้ไม่มีอินเทอร์เน็ต)
- Windows Server Core (ไม่มี GUI) เปิดหน้าต่างไม่ได้ ให้โหลด `bunk.com` จากหน้า release มาใช้จาก terminal อย่างเดียว

หลังติดตั้งในโฟลเดอร์จะมี 2 ไฟล์

| ไฟล์ | คืออะไร |
|---|---|
| `bunk.exe` | โปรแกรมหน้าต่าง และเป็นตัวติดตั้ง/ถอนด้วย (ตัวที่โหลดมามี `bunk.com` กับ WebView2 ฝังมาข้างใน ตัวที่ติดตั้งแล้วเหลือประมาณ 8 MB) |
| `bunk.com` | CLI และ daemon พิมพ์ `bunk` ใน cmd/PowerShell ได้ |

เวอร์ชันก่อน 0.10.0 แจกเป็น zip ใครแตก zip ใช้อยู่แล้วใช้ต่อและอัปเดตในแอปได้ตามเดิม หรือรัน `bunk.exe --install` ในโฟลเดอร์นั้นเพื่อย้ายมาแบบติดตั้ง รายการโปรเจกต์ตามมาเอง แล้วลบโฟลเดอร์เดิม (และเอาออกจาก PATH ถ้าเคยใส่ไว้)

## อัปเดต

ตั้งแต่ 0.5.0 bunk ตรวจหาเวอร์ชันใหม่จาก repo นี้เอง มีเวอร์ชันใหม่จะขึ้นแถบแจ้งในหน้าต่าง กด "อัปเดตเลย" แล้ว bunk จะติดตั้งและเปิดใหม่ให้ service ที่ทำงานอยู่เริ่มใหม่ให้เอง ใช้ได้ทั้งแบบติดตั้งและแบบพกพา

อัปเดตในแอปโหลดแค่ `bunk-app.exe` (ประมาณ 8 MB ไม่มี WebView2) กับ `bunk.com` ส่วน WebView2 ชุดที่มากับ bunk ไม่อัปเดตเอง จะได้ตัวใหม่เมื่อเปิด `bunk.exe` เวอร์ชันใหม่ติดตั้งทับ

ทุก release มี `bunk-update.json` (เวอร์ชัน รายละเอียด และ sha256 ของไฟล์) กับ `bunk-update.json.sig` (ลายเซ็น ed25519) bunk ติดตั้งเฉพาะไฟล์ที่ลายเซ็นตรงกับ public key ที่ฝังอยู่ในโปรแกรม:

```
7eb7ada0524d1fa455f449224e74f939855a96a9f8c343c572838541b629e5ab
```
