# bunk releases

ไฟล์ดาวน์โหลดของ **bunk** โปรแกรมรัน คุม และดูสถานะคำสั่งที่ต้องรันค้างไว้บนเครื่อง dev บน Windows (เช่น `npm run dev`, `python`, `redis-server`, ssh tunnel) แนวคิดเดียวกับ Docker Compose แต่รันคำสั่งตรงๆ ไม่ใช้ container

## ดาวน์โหลด

ไปที่ [Releases](https://github.com/Ratchx/bunk-releases/releases/latest) แล้วโหลด `bunk-<เวอร์ชัน>-windows-x64.zip` แตกไว้ในโฟลเดอร์ที่เขียนได้ (เช่นใน Documents) ใน zip มี 2 ไฟล์ที่ต้องอยู่ด้วยกัน:

| ไฟล์ | คืออะไร |
|---|---|
| `bunk.exe` | โปรแกรมหน้าต่าง ดับเบิลคลิกแล้วใช้ได้เลย |
| `bunk.com` | CLI และ daemon พิมพ์ `bunk` ใน cmd/PowerShell ได้ |

ต้องมี Microsoft Edge WebView2 Runtime (มากับ Windows 11 อยู่แล้ว)

## อัปเดต

ตั้งแต่ 0.5.0 bunk ตรวจหาเวอร์ชันใหม่จาก repo นี้เอง มีเวอร์ชันใหม่จะขึ้นแถบแจ้งในหน้าต่าง กด "อัปเดตเลย" แล้ว bunk จะติดตั้งและเปิดใหม่ให้ service ที่ทำงานอยู่เริ่มใหม่ให้เอง

ทุก release มี `bunk-update.json` (เวอร์ชัน รายละเอียด และ sha256 ของไฟล์) กับ `bunk-update.json.sig` (ลายเซ็น ed25519) bunk ติดตั้งเฉพาะไฟล์ที่ลายเซ็นตรงกับ public key ที่ฝังอยู่ในโปรแกรม:

```
7eb7ada0524d1fa455f449224e74f939855a96a9f8c343c572838541b629e5ab
```
