A slight modification from Dr. Rei Lee's [Conebot](https://github.com/rei039474/ConeBot)

# Parts:
* Computation: esp32-cam
* Motor Programmer: ROBOTIS U2D2 part
* Motors: DYNAMIXEL XL330-M077-T motor
* Wheels: omni wheels
* Breadboards: mini breadboard sets
* Power: power bank Anker 321
* Cable: usbc-to-c cable
* caster balls


# Dependency:
1. [Arduino IDE](https://www.arduino.cc/en/software)
2. Dr. Rei Lee's [package](https://github.com/rei039474/Dynamixel_XL330_Servo_Library) to control dynamixel motors (XL330 series)
Download by click code--> download ZIP
unzip ait and move the directoriy to `~/Documents/Arduino/libraries/`

4. [Dynamixel Wizard](https://emanual.robotis.com/docs/en/software/dynamixel/dynamixel_wizard2/)

# Steps:
1. Download and install [Dynamixel Wizard](https://emanual.robotis.com/docs/en/software/dynamixel/dynamixel_wizard2/)

2. Connect computer to motors. Laptop USB--> U2D2 microUSB-->right side of motor 1--> left side of motor 1--> right side of motor 2--> left side of the motor --> battery. Check the pinout of the U2D2 and dynamixels to make sure you are connecting them properly (VDD, GND, and Data, should connect to one another) 

3. In the Dynamixel Wizard, scan the USB port for Baudrate 57600 to find the motors. After the motor is found, make sure torque is off, then change settings for both:
- Baudrate to 115200 bps
- ID 1 and 2 respectively
- Control mode to PWM (not velocity or position).
- Turn torque on and toggle the diagram to get it moving! You only have to do this once.

4. Install the ESP32 Board (from espressif) in the Arduino IDE:

tools--> board --> Boards Manager...--> type esp32 and select esp32 by Expressif--> install

This may take a moment

5. Using the board and a microUSB, connect to ESP32 cam, flash and run a bit of sample code (try [CameraWebServer](https://randomnerdtutorials.com/esp32-cam-video-streaming-face-recognition-arduino-ide/)).

select the board by going to:
tools-->boards> ESP32 Arduino --> select AI Thinker ESP32-CAM
then select the port:
tools--> port--> there should be something like /dev/usb***** on mac or COM*** on Windows.
then go to File-->Examples-->ESP32-->Camera-->CameraWebServer
put in your wifi credentials
```
const char* ssid = "REPLACE_WITH_YOUR_SSID";
const char* password = "REPLACE_WITH_YOUR_PASSWORD";
```
Uncomment this line `#define CAMERA_MODEL_AI_THINKER ` 
and comment out `//#define CAMERA_MODEL_ESP_EYE `

hit the green arrow button on the left to upload the code to the microcontroller

if you go to tools--> serial monitor it will print out an IP address you can go to in a browser from a computer on the same network.

6. Download this repo and open the folder Conebot_Control in the Arduno IDE

File-->Open-->Conebot-main-->Conebot_Control-->Conebot_Control.ino

You will also need the ESP32Servo library
Sketch-->Include Library-->Library Manager-->Type ESP32Servo and install it.

And the Dynamixel XL330 Arduino Library
Sketch-->Include Library--> Add .ZIP Library and select Dynamixel XL330 Arduino Library.ZIP that we downloaded earlier

7. In `wifi_info.h', set it to "WiFi Option 2: Set up your own Wi-Fi network access point with SSID and password" by commenting out the first option.

8. Upload the code onto the board, connect to its network (SSID and password are in "wifi_info.h"), and visit the IP address that it spits out in the Serial monitor. It should show you live video feed, as well as a button display! Try turning the LED on and off.
  
9. Set up the breadboard: hook up servo, ESP32 cam, battery, and motors. (Schematic included)

10. Again, connect to the ESP32's network, and go to the same IP address. You should be able to see the video stream and control all of the motors!

11. Prototype and build a superstructure

12. Done!
