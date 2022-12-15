# SPCN-011
**สร้าง vm and ct on Proxmox cluster**
- ทำการ Create Master VM (ubuntu 22.04)
  1. คลิกขวาที่ Create VM ด้านขวาบน
  2. ทำการเลือก Node ตั้งชื่อ และเลือก Resource Pool 
  3. OS เลือก ISO image เป็น ubuntu-22.04.1-live-server-amd64.iso เลือก type เป็น linux
  4. System ใช้ค่า Default และทำการติ๊ก Qemu Agent
  5. Disk,CPU,Memory,Network ใช้ค่า Default
  ![confirm ](https://user-images.githubusercontent.com/115150753/207854831-db9a1a5b-2864-4bb5-b410-541f5b8f6e14.png)
