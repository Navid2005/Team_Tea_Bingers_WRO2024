INTRODUCTION ʕ⁠·⁠ᴥ⁠·⁠ʔ:
-

WELCOME TO OUR GITHUB PAGE FOR WRO 2024, WE'RE TEAM TEA BINGERS, SO GRAB A CUP OF TEA, SIT BACK AND READ ON ABOUT OUR DISCOVERIES ~ ☕ ദ്ദി(>ᴗ•)! 

🌟 ｡⁠◕⁠‿⁠◕⁠｡ 🌟 

Hailing all the way from Bangladesh, we aim to fuse our creativity, coding skills and mechatronics knowledge to inspire many across the world to try their hands in the field of robotics ~ 🇧🇩

FIRSTLY, A LITTLE ABOUT OUR TEAM:

Our Team consists of 2 members guided by 1 coach.

We are:

1.) AKM Navid Iqbal 🐼,
Coding enthusiast, and a math wizz. He's able to take visions, and turn them into "mathematically" accurate realities. (^⁠_⁠_⁠_⁠^)

"If I'm able to take 1 step, I'll be able to take a thousand more."


2.) Humaira Quyum 🐻‍❄️,
Design enthusiast and skin care fanatic. She worked on the external design, including which components to be used. (⁠ ⁠╹⁠▽⁠╹⁠ ⁠)

"Rest is as important as the work."


Coach: 
Azima Nashra Quyum 🦊
Encouraging, Humble, Kind and uplifting, she has singlehandedly kept us motivated throughout the challenges we faced. (⁠≧⁠▽⁠≦⁠)

"Keep tinkering, because the solution you are looking for may be a few adjustments away." 


This repository serves as not only a journal for the development of our robot, named Coco, but also as a gateway to showcase the challenges we faced to overcome as a team. This way it ensures that our efforts can be replicated and even improved upon for any robotics enthusiasts stumbling across our repository ~ (⁠ ⁠◜⁠‿⁠◝⁠ ⁠)

Here onwards is the gateway to our coding progress journal: from the paper-bound sketches of our initial designs, to the final robot operating, we aspire to showcase our journey in complete details on this page. ~ (⁠◔⁠‿⁠◔⁠)







PROGRESS TAB (LAST UPDATED 20TH SEPT 2024)
-
Check here for daily updates and changes made to our robot and see how it develops in front of your eyes 

Coco was intially conceptualized to be rectangular in shape, with large wheels to allow for the best grip and a large surface area to allow components to be added without any difficulty as shown in first models created, a more detailed description is given in the MODELS directory, and whilst it seemed great, we had to go back on the drawing board as the steering system was not well-suited and did not work as planned, nevertheless, here is the first iteration of COCO, COCO V1.0: 

![Angled view of coco V1 0](https://github.com/user-attachments/assets/dd64bba0-5738-4167-a465-3b3ddb0d7ecb)

Eventually we fixed the issues by using a different steering system, this is the one currently being used:

![Screenshot 2024-09-20 210449](https://github.com/user-attachments/assets/34d156da-4e30-420a-a118-f396ca9e77a4)

Furthermore, with a square base and 


ELECTRICAL COMPONENTS AND ENGINEERING MATERIALS USED (LAST UPDATED 20TH SEPT 2024)
-

Here are the following parts and components used, their purpose and whether they were implemented properly

1.) HC-SR04 Ultrasonic Distance sensors (implemented):
They are used for sensing and measuring the distance to the sides, initializing a turning maneuver and to slow down the motors during turning 

2.) DHT11 Temperature and Humidity sensor(not implemented):
This is used to increase the accuracy of the distance sensors mentioned above as they rely on the speed of sound to measure distances, as the speed of sound is affected by both temperature and humidity, both of them are factored into our calculations. Currently it is not implemented as our team's sensors are experiencing issues and are broken. 

3.) SG90 Servo Motor (Partially implemented):
The servo motor is used to control the steering mechanism by pulling and pushing a copper rod against the axle, currently due to a lack of jumper wires, only the right hand side servo motor has been added.

4.) Yellow Wheels, 25mm thickness (Implemented):
These were the wheels chosen, as they are readily available, and have a rubber tire that allows for better grip during acceleration, the tires on the front axle wheels have been removed and the rubber tires caused too much friction for any meaningful turning maneuver to be created.

5.) 3.7volt Lithium-Ion rechargeable batteries (implemented):
These were chosen for their rechargeable properties, and with a charging module, or a powerbank it provides and adequate source of power to both the Motor driver and Arduino

6.) L298N Motor driver module (Implemented):
This motor driver module allows us to control 2 DC motors, by changing their rotation direction, changing their speed and this allows complete motor control to speed up or slow down during different sections of the track 

7.) Plastic DC gear motors (implemented):
The gear motors provide decent torque and can run on a larger range of voltages, hence they were chosen to power the robot's movement 

8.) Cardboard Box (Implemented):
This is cut and shaped into a chassis for our robot, capable of being marked on, drawn on and cut easily. It is readily available in large quantities and has fair durability when layers of cardboard are sandwiched with glue 

9.) 608 Ball Bearings (Implemented):
These are small and compact allowing a rotational steering mechanism to be implemented, it can also be easily glued and put into place.


10.) Wooden dowels (Implemented):
This is used to form the front axle on our robot as they are sturdy enough to support the downward weight of the components.

11.) Arduino Mega (Implemented):
The microcontroller used, this is because of its large IOT pin assortment which is required for 

VEHICLE SPECIFICATIONS (LAST UPDATED 20TH SEPTEMBER 2024):
-







