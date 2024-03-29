# Self Balancing Robot

<img src="https://img.shields.io/badge/Github-181717?style=for-the-badge&logo=Github&logoColor=white"> <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=Python&logoColor=white"> <img src="https://img.shields.io/badge/c++-00599C?style=for-the-badge&logo=cplusplus&logoColor=white"> <img src="https://img.shields.io/badge/Arduino-00878F?style=for-the-badge&logo=Arduino&logoColor=white"> <img src="https://img.shields.io/badge/espressif-E7352C?style=for-the-badge&logo=espressif&logoColor=white"> <img src="https://img.shields.io/badge/qt-41CD52?style=for-the-badge&logo=qt&logoColor=white"> <img src="https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white">

---

## Index

- [What is Self Balancing Robot](#what-is-self-balancing-robot)
- [Purpose of Project](#purpose-of-project)
- [Showcase](#showcase)
- [Hardware](#hardware)
- [Body Design](#body-design)
- [How To Use](#how-to-use)
    - [Installation](#installation)
    - [Pin Settings](#pin-settings)
    - [Program Settings](#program-settings)
- [If you want to PID Controll (Only PID Motor Controll) - ESP32 Nano](#if-you-want-to-pid-controll-only-pid-motor-controll---esp32-nano)
    - [Pin Settings](#pin-settings-1)
    - [Program Settings](#program-settings-1)
- [Setback & Wrap Up](#setbacks--wrap-up)
    - [Project Setback](#project-setbacks)
    - [Wrap Up](#wrap-up)
- [To Do](#to-do)
- [Acknowledgements](#acknowledgements)
---

- Preview
![](images/selfBalancingRobot-test.gif)

- Hardware Diagram
![](images/Hardware_Diagram.png)

- State Diagram
![](images/State_diagram.png)

- Database Diagram
![](images/Database_Diagram.png)

## What is Self Balancing Robot
> __Self Balancing Robot__ is a robot that stands on its own like __Segway__.
This Robot requires __PID motor control__ and __Gyro sensor__, and we used __L298N__ and __MPU6050__.

---

## Author

|Name|Role|
|---|---|
|raematchaaa|Control Motor, Hardware & Electric Devices, Sense MPU6050, DB|
|chohongki|GUI (QT), Read RFID, WIFI Socket, UART|

---

## Purpose of Project
1. Deal with ```Acceleration, Gyroscope``` sensor like ```MPU6050``` and input these values on control process.
2. Study PID and apply it to control Robot.
3. Control the MCU wirelessly.
4. Get familiarized with other MCUs than Arduino UNO

---

## Showcase
1. Wireless Data Communication using __Wifi AP__
2. __PID control__
3. __Access MPU6050 registries__ to get Acceleration and Gyroscope values
4. Read __RFID__ tags
5. Remote Control using __GUI__
6. Log Sensor Data into __MySQL__
---

## Hardware
- MCU   :   Espressif ESP32-S3 N16R8, Arduino Uno
- Gyro Sensor   :   GY-521 (MPU 6050)
- Motors (x2)   :   NP01D-288
- Motor Driver  :   L298N
- Wheels    :   $\phi$ 66mm
- Battery   :   1.5V * 4
- RFID      :   MFRC522

---

## Body Design
![Alt text](images/Body_design.png)

---

## How To Use
### Installation
1. ```Arduino > Tools > Board > Boards Manager > esp32 (Espressif)```
2. ```Arduino > Tools > Library Manager > MFRC522```

### Pin Settings
- ESP32-S3
```
TX 17, RX 18

--------------------------
MPU6050

SCL 1
SDA 2
INTERRUPT   14

--------------------------
L298N

IN1 9
IN2 8
IN4 5
IN3 6
ENA 10  // Right Side Motor
ENB 4  // Left Side Motor

```
- UNO
```
RX 0
TX 1

--------------------------
MRFC522

RST_PIN     9     
SS_PIN      10
```

### Program Settings
1. Build ```uno_final/uno_final.ino``` into Arduino Uno
2. Build ```esp32_final/esp32_final.ino``` into ESP32-S3  
    2-1. Connect ESP32-S3 with Serial and Press Reset to find out WIFI IP  
    2-2. Open ```main.py``` and fix IP on line 20  
3. Run ```main.py```

---

## If you want to PID Control (Only PID Motor Control) - ESP32 Nano

### Pin Settings
- ESP32 Nano
![](<images/Balanced Robot.png>)

### Program Settings
1. Build ```Balanced_Robot/Balanced_Robot.ino``` into ESP32 Nano

---

## Setbacks & Wrap Up

### Project Setbacks 
1. Compatibility of hardware configuration with the planned function implementations was not throughly checked in advanced.  
2. Some libraries used during the test period were only available to Arduino Nano ESP32, and not to Esspressif ESP32-S3, causing code integration failures.
3. Unsolved packet loss due to inadequate background knowledge in socket programming.
4. Contrary to the prior expectation, heuristic (trial-and-error) method to determine PID values turned out to be inefficient considering the given amount of time and resources for this project.
5. Inept soldering skills.

### Wrap Up
1. Controlling motors by tuning PID requires depth knowledge in many fields as dynamics of the system and difference in tuning methods.
2. It would be remarkable to be able to design model which can be expressed in mathematical equations such can lead to model-based tuning to control PID instead of guess and check method.
3. Reading and analyzing hardware specifications to choose fit materials for the projects and to discover how to use them are crucial.
4. Every pin should be soldered in place.
5. This project enlightened the team on the subject of data communications and computer networks.

---

## To Do
1. Integrate the code seamlessly.
2. Add MPU6050 monitoring graph on the controller UI.
3. Add keylogger interface for both UI and database.
4. Develop specific real-life application of this robot. 
5. Revamp socket communication.

---

## Acknowledgements
- [Espressif - ESP32](https://github.com/espressif/arduino-esp32)
- [PyQt5 Docs](https://doc.qt.io/qtforpython-5/PySide2/QtWidgets/index.html)
- [I2CDev - MPU6050](https://github.com/jrowberg/i2cdevlib/tree/master/Arduino/MPU6050)
