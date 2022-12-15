# SPCN-011
**สร้าง vm and ct on Proxmox cluster**
- ทำการ Create Master VM (ubuntu 22.04)
  - คลิกที่ Create VM ด้านขวาบน
![ezgif-3-3190f34ba1](https://user-images.githubusercontent.com/115150753/207913674-51bf5ba5-6c17-41f4-86c0-325c5d2f6963.gif)

  - ตั้งชื่อ ทำการเลือก Node ตั้งชื่อ และเลือก Resource Pool 
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

**สร้างตัว Clone ที่มาจาก Template**
- คลิกขวาที่ตัว Template และคลิกไปที่ Clone

![Clone1](https://user-images.githubusercontent.com/115150753/207862859-b46640d6-bde0-4d45-904d-2c060cef8bfc.png)

  - ทำการตั้งชื่อ เลือก Node และเลือก Mode เป็น Linked Clone
 - เมื่อติดตั้งเสร็จเรียบร้อยแล้วให้ทำการ Set Up ค่าต่างๆ ด้วยคำสั่งต่อไปนี้
 - Set เวลา โดยใช้คำสั่ง
     - sudo time datectl set-timezone Asia/Bangkok
 - Set ค่าเวลาให้ตรง
      - ntpdate th.pool.ntp.org
      - crontab -e
      - @hourly /usr/sbin/ntpdate th.pool.ntp.org
 - คำสั่งที่ใช้ในการ Set ชื่อ Hostname
      - sudo hostnamectl set-hostname **ชื่อที่ต้องการจะตั้ง**
 - คำสั่งที่ใช้ในการเปลี่ยน Machine-ID
      - rm /var/lib/dbus/machine-id
      - echo -n > /etc/machine-id
      - cat /etc/machine-id
      - ln -s /etc/machine-id /var/lib/dbus/machine-id

**การสร้าง CT**

  - คลิกที่ Create CT ด้านขวาบน
![ezgif-3-ct](https://user-images.githubusercontent.com/115150753/207914608-90f9be76-4cce-45d5-b148-e7b5d6fcf4f2.gif)

 - ทำการตั้งชื่อ เลือก Resource Pool และตั้ง Password
 - ทำการ Load Key SSH ที่ไป Download มาได้จาก Github
 - Template ให้เลือกเป็น Ubuntu-22.04-standard_22.04-1_amd64.tar.zst
 - Network IPv4 ให้เลือกเป็น DHCP IPv6 ให้เลือกเป็น SLAAC 
 - เมื่อติดตั้งเสร็จเรียบร้อยแล้วให้ทำการ Set Up ค่าต่างๆ ด้วยคำสั่งต่อไปนี้
  - Set เวลา โดยใช้คำสั่ง
     - sudo time datectl set-timezone Asia/Bangkok
 - คำสั่งที่ใช้ในการติดตั้ง htop
     - apt install htop

![htop](https://user-images.githubusercontent.com/115150753/207872711-c39b6fdf-7e3b-4356-8780-16ba84218554.png)
