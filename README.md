# SPCN-011
**สร้าง vm and ct on Proxmox cluster**
- ทำการ Create Master VM (ubuntu 22.04)
  - คลิกที่ Create VM ด้านขวาบน
![ezgif-3-3190f34ba1](https://user-images.githubusercontent.com/115150753/207913674-51bf5ba5-6c17-41f4-86c0-325c5d2f6963.gif)

  - ตั้งชื่อ ทำการเลือก Node ตั้งชื่อ และเลือก Resource Pool 
![ezgif-1-resource](https://user-images.githubusercontent.com/115150753/207926498-4347d60e-45c6-4fff-b154-3af5a063f601.gif)


  - OS เลือก ISO image เป็น ubuntu-22.04.1-live-server-amd64.iso เลือก type เป็น linux
  ![ezgif-1-iso](https://user-images.githubusercontent.com/115150753/207926742-6e6469da-189c-4f34-81d6-5c840e5c10ec.gif)


  - System ใช้ค่า Default และทำการติ๊ก Qemu Agent
  ![ezgif-1-qemu](https://user-images.githubusercontent.com/115150753/207927199-6e985043-34c6-4831-897b-402e3adc30b4.gif)

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

![ezgif-3-template](https://user-images.githubusercontent.com/115150753/207916204-0b57f541-44ee-42f4-a52f-14a7efcedc1d.gif)

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

**การสร้าง VM ด้วย OS ตัวอื่นๆ**

 - คลิกที่ Create VM ด้านขวาบน
![ezgif-3-3190f34ba1](https://user-images.githubusercontent.com/115150753/207913674-51bf5ba5-6c17-41f4-86c0-325c5d2f6963.gif)

 - ตั้งชื่อ ทำการเลือก Node ตั้งชื่อ และเลือก Resource Pool 
![ezgif-1-resource](https://user-images.githubusercontent.com/115150753/207926498-4347d60e-45c6-4fff-b154-3af5a063f601.gif)

 - OS เลือก ISO image เป็น linuxmint-21-mate-64bit.iso เลือก type เป็น linux
![ezgif-2-linuxmint](https://user-images.githubusercontent.com/115150753/208017849-95acec22-ac84-44f7-b252-34ccb3eeb4aa.gif)

 - System ใช้ค่า Default และทำการติ๊ก Qemu Agent
  ![ezgif-1-qemu](https://user-images.githubusercontent.com/115150753/207927199-6e985043-34c6-4831-897b-402e3adc30b4.gif)

 - Disk,CPU,Memory,Network ใช้ค่า Default
 ![otheros3](https://user-images.githubusercontent.com/115150753/208068484-b6b7d238-9540-468c-ae68-0294cc82ef44.png)

 - เมื่อ Boot ขึ้นมาแล้ว ให้เลือก Start Linux Mint 21 Mate 64-bit
 ![Mint 1](https://user-images.githubusercontent.com/115150753/208068939-99827872-ce6f-4ce3-8828-73837b16fa61.png)

 - รอจนกว่าจะเข้ามาที่หน้า Desktop ของ Mint
 ![mint desktop](https://user-images.githubusercontent.com/115150753/208069499-8472ba85-bbd2-43b1-9e58-3750815b4798.png)

 - คลิกไปที่ Install Linux Mint ด้านขวาบน เพื่อทำการติดตั้ง
 ![ezgif-1-install mint](https://user-images.githubusercontent.com/115150753/208070843-47a3680b-5f16-46e9-b5d9-d63d2723c1f1.gif)

 - ทำการติดตั้ง และ Set ค่าต่างๆ
 ![mint install 1](https://user-images.githubusercontent.com/115150753/208072624-166a9639-483d-4497-883a-72f618642dc4.png)

 ![mint install 2](https://user-images.githubusercontent.com/115150753/208072728-56f204d4-04da-46c5-991f-97db6e8c95f5.png)

 ![mint install 3](https://user-images.githubusercontent.com/115150753/208072802-3a29ab3d-414a-4b98-92cf-5fb00d8ce686.png)

 ![mint install 4](https://user-images.githubusercontent.com/115150753/208072830-ccc9e35b-2029-42f9-b031-29cb141bb55a.png)

 - รอติดตั้งจนเสร็จ
 ![mint install 5](https://user-images.githubusercontent.com/115150753/208072889-e3d9a265-3f7d-452a-986f-aef53dae65dc.png)

 - เมื่อติดตั้งเสร็จก็จะได้เป็น Linux Mint ตัวเต็ม
 ![mint install 6](https://user-images.githubusercontent.com/115150753/208074561-7e233d67-3466-4200-b5bf-612fa8ce06e3.png)








