# SPCN-011
**สร้าง vm and ct on Proxmox cluster**
- ทำการ Create Master VM (ubuntu 22.04)
  - คลิกขวาที่ Create VM ด้านขวาบน
  - ทำการเลือก Node ตั้งชื่อ และเลือก Resource Pool 
  - OS เลือก ISO image เป็น ubuntu-22.04.1-live-server-amd64.iso เลือก type เป็น linux
  - System ใช้ค่า Default และทำการติ๊ก Qemu Agent
  - Disk,CPU,Memory,Network ใช้ค่า Default
  ![confirm ](https://user-images.githubusercontent.com/115150753/207854831-db9a1a5b-2864-4bb5-b410-541f5b8f6e14.png)
   
  - เมื่อถึงขั้นตอน SSH ให้ทำการ Import SSH จาก Github ของผู้ใช้งานมาด้วย
  ![gitHUB SSH](https://user-images.githubusercontent.com/115150753/207856391-3ba07e9c-1f61-4adb-b8d0-530547290fcb.png)
 
 เมื่อติดตั้งเสร็จเรียบร้อยแล้วให้ทำการ Set Up ค่าต่างๆ ด้วยคำสั่งต่อไปนี้
  - Set เวลา โดยใช้คำสั่ง
     - sudo time datectl set-timezone Asia/Bangkok
  - คำสั่งที่ใช้ในการอัพเดท
     - sudo apt update; sudo apt upgrade -y
  - คำสั่งที่ใช้ติดตั้ง Qemu Agent และการใช้งาน Qemu
     - sudo apt install qemu-guest-agent
     - sudo systemctl start qemu-guest-agent
     - sudo systemctl status qemu-guest-agent
   - คำสั่งที่ใช้ติดตั้ง NANO
      - apt install nano
   - คำสั่งที่ใช้ติดตั้ง dnsutils
      - apt install dnsutils
   - คำสั่งที่ใช้ติดตั้ง crontab
      - apt install crontab
   - set ค่าเวลาให้ตรง
      - ntpdate th.pool.ntp.org
      - crontab -e
      - @hourly /usr/sbin/ntpdate th.pool.ntp.org
   - คำสั่งการ ping
      - ping 1.1.1.1

**การ Clone Master VM ให้ไปเป็น Template**
    - ให้คลิกขวาไปที่ Master VM และคลิกไปที่ convert to template
![Convert template](https://user-images.githubusercontent.com/115150753/207861788-e874b337-986f-4da1-9222-983db74ef103.png)

