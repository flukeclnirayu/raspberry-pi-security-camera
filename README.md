# Raspberry Pi Security Camera
สวัสดีครับ โปรเจคนี้เป็นการประยุกต์ใช้ Raspberry Pi 4 ร่วมกับ NoIR Camera เพื่อใช้เป็นกล้องตรวจจับการเคลื่อนไหวผ่าน MotionEye OS ครับ
## Features
• ถ่ายภาพนิ่ง 1 ภาพเมื่อตรวจพบการเคลื่อนไหว   
• ถ่ายวิดีโอเมิ่อตรวจพบการเคลื่อนไหว  
## Optionals
• ส่งข้อความแจ้งเตือนและภาพนิ่งให้ผู้ใช้ผ่านทาง LINE Notify (ต้องปิดการถ่ายวิดีโอ)
## อุปกรณ์
• Raspberry Pi 4 Model B 2GB RAM  
• Power Supply  
• Raspberry Pi NoIR Camera V2 8MP  
• 8GB Micro SD Card  
## ขั้นตอนการติดตั้ง
### 1. ติดตั้ง Raspberry Pi NoIR Camera บน Raspberry Pi 4
### 2. ติดตั้ง MotionEye OS
2.1 ดาวน์โหลดและติดตั้ง SD Memory Card Formatter จาก https://www.sdcard.org/downloads/formatter/  
2.2 ใส่ SD Card ใน SD Card Reader เพื่อเชื่อมต่อเข้ากับคอมพิวเตอร์  
2.3 ใช้โปรแกรม SD Memory Card Formatter ในการ Format SD Card  
(อย่าลืมเช็ค Drive Letter เช่น D:\ หรือ E:\ ว่าเป็นของ SD Card รึเปล่า)  
2.4 ดาวน์โหลดและติดตั้ง Win32DiskImager จาก https://sourceforge.net/projects/win32diskimager/  
2.5 ดาวน์โหลด motioneyeos-raspberrypi4-20200606.img.xz หรือ MotionEye OS SD Card Image เวอร์ชั่นล่าสุด จาก https://github.com/ccrisan/motioneyeos/releases  
2.6 แตกไฟล์ MotionEye OS SD Card Image ที่ได้ทำการดาวน์โหลดมา  
2.7 เปิดโปรแกรม Win32DiskImager แล้วทำการเลือกไฟล์นามสกุล .img ที่ได้จากการแตกไฟล์  
2.8 กดปุ่ม Write เพื่อทำการติดตั้ง
### 3. ตั้งค่าการเชื่อมต่อแบบไร้สาย
3.1 ดาวน์โหลดและติดตั้ง Notepad++ จาก https://notepad-plus-plus.org/downloads/  
3.2 เปิดโปรแกรม Notepad++ แล้วคัดลอกโค้ดด้านล่างนำไปวางลงในไฟล์
```
country=TH  
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev  
update_config=1  
network={  
  ssid="NETWORK-NAME"  
  psk="NETWORK-PASSWORD"  
}
```  
3.3 เปลี่ยนข้อความ NETWORK-NAME และ NETWORK-PASSWORD เป็นชื่อ WiFi แล้วรหัสผ่านของเราตามลำดับ  
(ไม่ต้องลบ " ออก)  
3.4 กด Save As ไปไว้ในหน้าแรกของ SD Card Drive (จะมีไฟล์ต่าง ๆ เช่น bcm2711-rpi-4-b.dtb, bootcode.bin, cmdline)  
เลือก Save as type: All Types แล้วตั้งชื่อว่า wpa_supplicant.conf
### 4. ถอด SD Card ที่เชื่อมต่อกับคอมพิวเตอร์แล้วนำไปใส่ในช่อง SD Card ของ Raspberry Pi 4
### 5. เสียบสาย Power Supply เข้ากับ Raspberry Pi 4
### 6. ค้นหา IP Address ของ Raspberry Pi 4
6.1 ดาวน์โหลด Wireless Network Watcher จาก https://www.nirsoft.net/utils/wnetwatcher.zip  
6.2 แตกไฟล์ wnetwatcher.zip ที่ได้ทำการดาวน์โหลดมา  
6.3 เปิดโปรแกรม Wireless Network Watcher เพื่อค้นหา IP Address ของ Raspberry Pi 4  
(Network Adapter Company = "Raspberry Pi ...")
### 7. นำ IP Address ที่ได้ไปใส่ในช่องค้นหาของ Browser เพื่อไปที่หน้าหลักของ MotionEye
### 8. กดปุ่ม switch user เพื่อทำการ Login (ปุ่มที่ 2 จากมุมซ้ายบน)
#### ในช่อง Username ให้ใส่ว่า admin ส่วนช่อง Password ให้เว้นว่างเอาไว้
### 9. ตั้งค่าเบื้องต้น
9.1 กดปุ่ม settings (ปุ่มที่ 1 จากมุมซ้ายบน)  
9.2 ในส่วนของ Preferences > Layout Columns เปลี่ยนจาก 3 เป็น 1  
9.3 ในส่วนของ General Settings > Time Zone เปลี่ยนจาก UTC เป็น Asia/Bangkok  
9.4 ในส่วนของ Video Device  
• Automatic Brightness เปลี่ยนจาก OFF เป็น ON  
• Frame Rate เปลี่ยนจาก 2 เป็น 30  
9.5 ในส่วนของ Text Overlay > Text Scale เปลี่ยนจาก 1 เป็น 2  
9.6 ในส่วนของ Still Images  
• Image File Name เปลี่ยนจาก %Y-%m-%d/%H-%M-%S เป็น %Y-%m-%d/%H-%M  
• Capture Mode เปลี่ยนจาก Manual เป็น Motion Triggered (One Picture)  
9.7 ในส่วนของ Movies > Movie Format เปลี่ยนจาก H.264/OMX เป็น MPEG4  
9.8 ในส่วนของ Motion Detection  
• Frame Change Threshold เปลี่ยนจาก 0.7% เป็น 2.5%  
• Auto Noise Detection เปลี่ยนจาก ON เป็น OFF และเปลี่ยน Noise Level จาก 12% เป็น 25%  
9.9 กดปุ่ม Apply เพื่อ Reboot System</br></br>
AND DONE !
## การตั้งค่าการแจ้งเตือนผ่านทาง LINE Notify
### 1. ดาวน์โหลดและติดตั้ง Putty จาก https://www.putty.org/
### 2. เปิดโปรแกรม Putty และใส่ IP Address ของ Raspberry Pi 4 จากนั้นกดปุ่ม Open
#### xxx.xxx.x.xx (ลบ http:// ด้านหน้า และ / ด้านหลังออก) หากมีหน้าต่างเด้งขึ้นมาให้เลือกตอบ Accept
### 3. login as: admin
### 4. สร้าง Directory /data/script ด้วยคำสั่ง
```
mkdir /data/script
```
### 5. เข้าไปที่เว็บไซต์ https://notify-bot.line.me/en/ แล้วทำการ Log in
### 6. กดที่ชื่อผู้ใช้มุมขวาบนแล้วเลือก My Page
### 7. กดปุ่ม Generate Token ใต้หัวข้อ Generate access token
### 8. ตั้งชื่อ Token เช่น MotionEye Notify และกดเลือกแชทที่จะส่งการแจ้งเตือนแบบ 1-on-1 chat
### 9. กดปุ่ม Generate Token
#### จะมีข้อความแจ้งเตือนไปทาง LINE Notify ว่าได้ทำการ Generate Token เรียบร้อยแล้ว
### 10. คัดลอก Token เอาไว้แล้วกดปุ่ม close
### 11. กลับมาที่โปรแกรม Putty เพื่อสร้าง Shell Script สำหรับส่งข้อความด้วยคำสั่ง
```
cd /data/script
```
```
nano linenotify_alert.sh
```
#### คัดลอกโค้ดด้านล่างนำไปวางลงใน Script โดยเปลี่ยนข้อความ [access_token] เป็น Token ที่เราได้ทำการคัดลอกไว้
```
#!/bin/bash
curl -k -X POST -H 'Authorization: Bearer [access_token]' -F "message=$1" https://
notify-api.line.me/api/notify
```
#### กด Ctrl-X เพื่อออก nano จะถามว่าต้องการ save ไฟล์หรือไม่ ให้กด y เพื่อ save และกด Enter เพื่อยืนยันชื่อไฟล์
### 12. สร้าง Shell Script สำหรับส่งภาพนิ่งด้วยคำสั่ง
```
nano linenotify_push.sh
```
#### คัดลอกโค้ดด้านล่างนำไปวางลงใน Script โดยเปลี่ยนข้อความ [access_token] เป็น Token ที่เราได้ทำการคัดลอกไว้
```
#!/bin/bash
curl -k -X POST -H 'Authorization: Bearer [access_token]' -F "message=$1" -F "imageFile=@$2" https://
notify-api.line.me/api/notify
```
#### กด Ctrl-X เพื่อออก nano จะถามว่าต้องการ save ไฟล์หรือไม่ ให้กด y เพื่อ save และกด Enter เพื่อยืนยันชื่อไฟล์
### 13. เปลี่ยนรูปแบบของไฟล์เป็นแบบ Executable ด้วยคำสั่ง
```
chmod 755 linenotify_alert.sh
chmod 755 linenotify_push.sh
```
### 14. เข้าไปดู Directory ที่เก็บภาพและวิดีโอด้วยคำสั่ง
```
cd /data/output/Camera1/
```
```
ls
```
### เลือก Directory ที่ต้องการด้วยคำสั่ง
```
cd %Y-%M-%D
```
### โดยที่ %Y %M และ %D แทนด้วยปี เดือน และวัน ตามลำดับ
```
ls
```
### 15. ทดสอบ Shell Script ด้วยคำสั่ง
```
bash /data/script/linenotify_alert.sh "Hello there."
```
```
bash /data/script/linenotify_push.sh "Hello there." "/data/output/Camera1/%Y-%M-%D/%H-%M-%S.jpg"
```
#### ข้อความ Hello there. และภาพที่เลือกจะแจ้งเตือนมาทาง LINE Notify
### 16. ใช้ IP Address ของ Raspberry Pi ใส่ในช่องค้นหาของ Browser เพื่อไปที่หน้าหลักของ MotionEye
### 17. กดปุ่ม settings (ปุ่มที่ 1 จากมุมซ้ายบน)
### 18. ในส่วนของ File Storage > Run A Command ให้ใส่คำสั่ง
```
cp %f /data/output/Camera1/lastsnap.jpg; bash /data/script/linenotify_push.sh "Here is the still image." "/data/output/Camera1/lastsnap.jpg"
```
### 19. ในส่วนของ Movies เปลี่ยนจาก ON เป็น OFF
### 20. ในส่วนของ Motion Notification > Run A Command ให้ใส่คำสั่ง
```
bash /data/script/linenotify_alert.sh "Motion Detect at %Y-%m-%d %H:%M Waiting to send a still image..."
```
#### เมื่อตรวจพบการเคลื่อนไหว motionEye จะทำการการแจ้งเตือนมาทาง LINE Notify
### 21. กดปุ่ม Apply
### AND DONE !
