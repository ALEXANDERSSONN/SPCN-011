# SPCN-011
**สร้าง vm and ct on Proxmox cluster**
- ทำการ Create Master VM (ubuntu 22.04)
  - คลิกขวาที่ Create VM ด้านขวาบน
  - ทำการเลือก Node ตั้งชื่อ และเลือก Resource Pool 
  - OS เลือก ISO image เป็น ubuntu-22.04.1-live-server-amd64.iso เลือก type เป็น linux
  - System ใช้ค่า Default และทำการติ๊ก Qemu Agent
  - Disk,CPU,Memory,Network ใช้ค่า Default
  ![confirm ](https://user-images.githubusercontent.com/115150753/207854831-db9a1a5b-2864-4bb5-b410-541f5b8f6e14.png)
   
  6.เมื่อถึงขั้นตอน SSH ให้ทำการ Import SSH จาก Github ของผู้ใช้งานมาด้วย
  ![gitHUB SSH](https://user-images.githubusercontent.com/115150753/207856391-3ba07e9c-1f61-4adb-b8d0-530547290fcb.png)
