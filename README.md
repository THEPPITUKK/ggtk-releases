# GGTK — ไฟล์ติดตั้งสำหรับทีม

โปรแกรม SSH / SFTP / Serial ของทีม (แนว MobaXterm) — repo นี้มี **เฉพาะไฟล์ติดตั้ง** ไม่มีซอร์สโค้ด

## โหลด

ไปที่ **[Releases](../../releases/latest)** → หัวข้อ Assets แล้วเลือกไฟล์ให้ตรงเครื่อง

| เครื่อง | ไฟล์ |
|---|---|
| Mac ชิป Apple (M1 ขึ้นไป) macOS 13+ | `GGTK_<เวอร์ชัน>_aarch64_team.dmg` |
| Windows 10 / 11 (64-bit) | `GGTK_<เวอร์ชัน>_x64-setup.exe` |

## ติดตั้ง

**Mac** — เปิด .dmg → ลาก GGTK ไปที่ Applications → เปิด GGTK → ถ้าเตือน: System Settings → Privacy & Security → **Open Anyway**
ถ้าขึ้น "damaged": รัน `xattr -dr com.apple.quarantine /Applications/GGTK.app` ใน Terminal

**Windows** — ดับเบิลคลิก .exe → ถ้าขึ้น "Windows protected your PC" กด **More info → Run anyway** → Next จนจบ (ไม่ต้องใช้ admin)

ครั้งแรกที่เปิดต้องกด **Agree** ข้อตกลงการใช้งาน — ใช้ภายในทีมเท่านั้น ห้ามแจกต่อ

## แจ้งบั๊ก / ถาม

Discord: https://discord.gg/WG48jFrRgR
