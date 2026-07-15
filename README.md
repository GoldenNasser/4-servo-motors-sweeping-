# 4 Servo Motors Sweeping - Arduino Uno

## 📝 Description
This repository contains the first task for the Electronics and Electrical Power track (Smart Methods). The project demonstrates how to control 4 micro servo motors simultaneously using an Arduino Uno. 

Based on the task requirements, the Arduino is programmed to make all four servos perform a sweeping motion continuously for **2 seconds**. After the time elapses, all motors automatically stop and hold their position at exactly **90 degrees**.

## 🔗 Live Simulation
You can view and interact with the live simulation directly on Tinkercad:
**[👉 Click here to view the Tinkercad Project](https://www.tinkercad.com/things/011jDcSAdFI-nassers-task/editel?sharecode=MIMjg0s3zGtr1JehAcfAlwRR9Yg78InXJjWT1njmlxY)**

## 🛠️ Components Used
* 1x Arduino Uno R3
* 4x Micro Servo Motors
* 1x Breadboard
* Jumper Wires

## 🔌 Circuit Wiring
As shown in the project documentation:
* **Power:** All servos are powered by the `5V` and `GND` pins from the Arduino via the breadboard.
* **Signal:** The signal wires of the servos are connected to the Arduino's PWM capable pins: `3`, `5`, `6`, and `9`.

## 📁 Repository Contents
This repository includes the following files to fully document the simulation and circuitry:
* `Arduino Uno 1st task - photo.png`: A high-quality screenshot of the circuit wiring and components setup in Tinkercad.
* `Arduino Uno 1st task - simulation.brd`: The exported board file.
* `Arduino Uno 1st task - video.mp4`: A video recording demonstrating the Tinkercad simulation in action, showing the 2-second sweep and the 90-degree hold.

## 🚀 How to Run (Tinkercad)
1. Open the [Tinkercad link](https://www.tinkercad.com/things/011jDcSAdFI-nassers-task/editel?sharecode=MIMjg0s3zGtr1JehAcfAlwRR9Yg78InXJjWT1njmlxY) provided above, or recreate the circuit as shown in the `photo.png` file.
2. Ensure the C++ code is uploaded to the Arduino in the code section.
3. Start the simulation. The motors will sweep for 2 seconds and then lock at 90 degrees.

## THE CODE
#include <Servo.h>

// تعريف المحركات الأربعة
Servo servo1;
Servo servo2;
Servo servo3;
Servo servo4;

// متغير للتأكد من تنفيذ المهمة مرة واحدة فقط
bool taskCompleted = false;

void setup() {
  // ربط المحركات بمنافذ الـ PWM
  servo1.attach(3);
  servo2.attach(5);
  servo3.attach(6);
  servo4.attach(9);
}

void loop() {
  if (!taskCompleted) {
    unsigned long startTime = millis();
    int pos = 0;
    int step = 1; // مقدار حركة السيرفو

    // تشغيل حركة الـ Sweep لمدة ثانيتين (2000 ملي ثانية)
    while (millis() - startTime < 2000) {
      servo1.write(pos);
      servo2.write(pos);
      servo3.write(pos);
      servo4.write(pos);

      pos += step;
      // عكس الاتجاه عند الوصول لأقصى زاوية أو أدنى زاوية
      if (pos >= 180 || pos <= 0) {
        step = -step; 
      }
      delay(15); // نفس التأخير الزمني الموجود في مثال Sweep الكلاسيكي
    }

    // بعد مرور الثانيتين، تثبيت جميع المحركات على زاوية 90 درجة
    servo1.write(90);
    servo2.write(90);
    servo3.write(90);
    servo4.write(90);

    // تغيير حالة المتغير لكي لا تتكرر الحركة
    taskCompleted = true; 
  }
}
