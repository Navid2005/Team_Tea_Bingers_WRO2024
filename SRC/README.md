/// NOTE THIS PLEASE ---
/// The Cheetah Algorithm used in the video for the national interview submission on 20th september on GitHub is this one, it is only partially similar to the original cheetah algorithm, this is because of the following reasons
/// 1.) The DHT11 sensors our team used had broken, and we showing error messages, rendering them unable to be used, hence the library and its related uses are removed in this algorithm
/// 2.) Unfortunately our team ran out of jumper cables during the course of development, hence another servo motor could not be added and thus in the video the robot is only able to turn right and avoid hitting the left wall
/// 3.) A serial monitor is not used in this case as it kept displaying error messages only.
/// 4.) Due to these, the code and connections had to be changed. Please do take note of this, as our robot is exhibiting HALF of the original intended code. This code is 30 lines less than the originally intended one. 


///The cheetah algorithm will work during the open course challenge, it uses several libraries, and allows us to go fast during the straight sections without worry
///The schematics for connections are shown in the SCHEMATICS directory.
///The connections are as follows:
///HC-SR04 Ultrasonic distance sensor: VCC to Arduino Mega 5v, Trigger pin to Arduino Mega PWM (pulse width modulation) pin 8 and pin 7, Echo pin to Arduino Mega digital pin 26 and pin 28, Gnd to Arduino Mega Ground.
///L298N Motor driver: EnA and EnB to Arduino Mega PWM (pulse width modulation) pin 12 and 13 respectively, In1, In2, In3, In4 to Arduino Mega digital pins 22,23,24 and 25 respectively.
///Servo motor: VCC to 5v of the Arduino Mega, Gnd to Arduino Mega Ground, Signal pin is on Arduino Mega PWM (pulse width modulation) 4 


///--------CHEETAH ALGORITHM (VIDEO VERSION)--------///
-

#include "NewPing.h" ///The NewPing library has built in functions to collect distance and time from HC-SR04 sensors such as sonar.ping_cm and sonar.ping.
#include "Servo.h" ///The Servo library has built in functions to allow PWM (pulse width modulation) control, this allows us to control our servo motors with the servo.write(integer angle) function
#define TRIGLEFT 8 /// assigning the trigger pin numberfor the ultrasonic distance sensor on the left hand side of our robot  
#define ECHOLEFT 26 /// assigning the echo pin number for the ultrasonic distance sensor on the left hand side of our robot  
#define TRIGRIGHT 3 /// same but for right hand side distance sensor 
#define ECHORIGHT 28
float speed_sound = 334; ///This is a constant to calculate an accurate distance using the speed of sound, which in typical cases is 334m/s in room temperature air, humidity and temperature can not be factored in making the overall distance reading slightly less accurate.
float dist_left, dist_left_final; ///The 2 variables are used to calculate the left hand side distance from the robot to the wall and convert it to centimeters respectively. 
float dist_right, dist_right_final; ///The same as before but for the right hand side of our robot 
float TIME_LEFT, TIME_RIGHT; ///These variables store the time it takes for the ultrasound echo to return to our HC-SR04 sensors, for the left and right sides respectively.
float MIN_DIST = 100; ///A variable that is used to store a threshold value for intializing a turn 
int MAX_DIST = 5; /// A variable that is used to store a threshold value for how close our robot can get to either one of the walls beside it 
int DIST_LEFT_FINAL, DIST_RIGHT_FINAL; /// A variable used to round up the decimal distance values for the left and right side 
int avg = 10; /// A variable that stores the amount of averages we want to take, in this case, we take 10 averages using the sonar.ping_median(avg) function.
int ENA = 12; ///Assigning pins to L298N motor driver 
int IN1 = 22;
int IN2 = 23;
int IN3 = 24;
int IN4 = 25;
int ENB = 13;
Servo servoRIGHT;      ///Creating an object that is classed as a Servo motor, in this case we utilize one due to no jumper cables available to attach the other.  
NewPing sonar1(TRIGLEFT, ECHOLEFT, 400); ///Creating 2 objects classed as sonar 1 and sonar 2, as we already describe orientation (left side or right side) using distance values, no need for extra specification here.
NewPing sonar2(TRIGRIGHT, ECHORIGHT, 400); ///The 400 is the stated maximum range of HC-SR04, which is 400cm in this case 

void setup() 
{ 
 servoRIGHT.attach(4); ///Assigning the signal pins for our servo motors for PWM control 
 pinMode(ENA, OUTPUT); ///Assigning the mode of each pin for L298N Motor driver.
 pinMode(IN1, OUTPUT);
 pinMode(IN2, OUTPUT);
 pinMode(IN3, OUTPUT);
 pinMode(IN4, OUTPUT);
 pinMode(ENB, OUTPUT);
}

void loop() 
{
 TIME_LEFT = sonar1.ping_median(avg); ///The time taken for an echo of ultrasound to return, this time is then averaged 10 times to give a final reading that is stored in the variable
 TIME_RIGHT = sonar2.ping_median(avg); 
 dist_left = (TIME_LEFT/2)*speed_sound; ///The pre-determined speed of sound and the averaged time taken for echo returns, allow us to get a fairly accurate distance reading up to +-1cm 
 dist_left_final = (dist_left/10000); /// a conversion factor to turn the distance into centimeters
 DIST_LEFT_FINAL = dist_left_final; /// another conversion to turn the decimal values to integer ones
 dist_right = (TIME_RIGHT/2)*speed_sound; ///same thing but for the right hand side sensor 
 dist_right_final = (dist_right/10000);
 DIST_RIGHT_FINAL = dist_right_final; 
 servoRIGHT.write(90); ///servo motor takes its origin position 
 delay(10); ///A delay to allow the robot to be set down and positioned 
 digitalWrite(IN1, LOW); ///Motor driver activates both motors to turn clockwise pushing the robot forward 
 digitalWrite(IN2, HIGH);
 analogWrite(ENA, 200); ///A high speed is given to the motors in the beginning for the open course challenge 
 digitalWrite(IN3, LOW);
 digitalWrite(IN4, HIGH);
 analogWrite(ENB, 200);
 delay(10);
 while (DIST_LEFT_FINAL <= MAX_DIST) ///The while loop is entered if the distance on the left sensor shows equal to or below 5cm 
  {
   servoRIGHT.write(15); ///The action of the right servo steers the front axle to turn away from the left wall
   digitalWrite(IN1, LOW); /// The clockwise direction of the motors in the rear of the robot still remain and their speed is slowed to half their original value to allow a corrective action to be taken 
   digitalWrite(IN2, HIGH);
   analogWrite(ENA, 150);
   digitalWrite(IN3, LOW);
   digitalWrite(IN4, HIGH);
   analogWrite(ENB, 150);
   delay(1000); ///A delay to allow steering action to occur for 1 whole second 
     break; ///The while loop is broken as the steering action has been completed 
  }
  while (DIST_RIGHT_FINAL > MIN_DIST) ///The while loop is entered if the distance on the right distance sensor is above 39.5cm
 {
   servoRIGHT.write(15);
   digitalWrite(IN1, LOW); ///Clockwise direction of the motors continue but they are now drastically slower to allow for accurate turning. 
   digitalWrite(IN2, HIGH);
   analogWrite(ENA, 150);
   digitalWrite(IN3, LOW);
   digitalWrite(IN4, HIGH);
   analogWrite(ENB, 150);
   delay(1000); ///A delay to allow steering action to occur for 1 whole second 
     break; 
 }
 delay(10); ///A final delay to allow all sensors to stabilize and the loop can start again. 
}


HERE IS HOW THE CODE WAS INTENDED TO PERFORM
-

///The cheetah algorithm will work during the open course challenge, it uses several libraries, and allows us to go fast during the straight sections without worry
///The schematics for connections are shown in the SCHEMATICS directory.
///The connections are as follows:
///DHT11 sensor: VCC to Arduino Mega 3.3v, Gnd to Arduino Mega Ground, Data pin to Arduino Mega digital pin 29.
///HC-SR04 Ultrasonic distance sensor: VCC to Arduino Mega 5v, Trigger pin to Arduino Mega PWM (pulse width modulation) pin 8 and pin 7, Echo pin to Arduino Mega digital pin 26 and pin 28, Gnd to Arduino Mega Ground.
///L298N Motor driver: EnA and EnB to Arduino Mega PWM (pulse width modulation) pin 12 and 13 respectively, In1, In2, In3, In4 to Arduino Mega digital pins 22,23,24 and 25 respectively.
///Servo motors: VCC to 5v of the Arduino Mega, Gnd to Arduino Mega Ground, Signal pin is on Arduino Mega PWM (pulse width modulation) pins 3 and 4 


///--------CHEETAH ALGORITHM--------///

#include "NewPing.h" ///The NewPing library has built in functions to collect distance and time from HC-SR04 sensors such as sonar.ping_cm and sonar.ping.
#include "Servo.h" ///The Servo library has built in functions to allow PWM (pulse width modulation) control, this allows us to control our servo motors with the servo.write(integer angle) function
#include "SimpleDHT.h" ///This library allows us to get temperature and humidity data directly from the DHT11 sensor without having to convert analog signals into digital values between 0 and 255
#define pinDHT11 29 /// assigning the data pin number for DHT11 sensor
#define TRIGLEFT 8 /// assigning the trigger pin numberfor the ultrasonic distance sensor on the left hand side of our robot  
#define ECHOLEFT 26 /// assigning the echo pin number for the ultrasonic distance sensor on the left hand side of our robot  
#define TRIGRIGHT 7 /// same but for right hand side distance sensor 
#define ECHORIGHT 28
float TEMP, HUM; ///These are variables to store our temperature and humidity values 
float speed_sound; ///This is a variable to calculate an accurate speed of sound 
float dist_left, dist_left_final; ///The 2 variables are used to calculate the left hand side distance from the robot to the wall and convert it to centimeters respectively. 
float dist_right, dist_right_final; ///The same as before but for the right hand side of our robot 
float TIME_LEFT, TIME_RIGHT; ///These variables store the time it takes for the ultrasound echo to return to our HC-SR04 sensors, for the left and right sides respectively.
float MIN_DIST = 39.5; ///A variable that is used to store a threshold value for intializing a turn 
int MAX_DIST = 5; /// A variable that is used to store a threshold value for how close our robot can get to either one of the walls beside it 
int DIST_LEFT_FINAL, DIST_RIGHT_FINAL; /// A variable used to round up the decimal distance values for the left and right side 
int avg = 10; /// A variable that stores the amount of averages we want to take, in this case, we take 10 averages using the sonar.ping_median(avg) function.
int ENA = 12; ///Assigning pins to L298N motor driver 
int IN1 = 22;
int IN2 = 23;
int IN3 = 24;
int IN4 = 25;
int ENB = 13;
Servo servoRIGHT , servoLEFT; ///Creating objects that are classed as Servo motors, we utilize 2 hence they are aptly named as one lies on the right and the other on the left of our robot 
NewPing sonar1(TRIGLEFT, ECHOLEFT, 400); ///Creating 2 objects classed as sonar 1 and sonar 2, as we already describe orientation (left side or right side) using distance values, no need for extra specification here.
NewPing sonar2(TRIGRIGHT, ECHORIGHT, 400); /// The 400 refers to 400cm which is the maximum range of distance that the HC-SR04 can record 
SimpleDHT11 dht11(pinDHT11); ///Creating a DHT11 object, to obtain temperature and humidity data easily.
void setup() 
{
 Serial.begin(9600); ///starting a serial monitor for error messages 
 servoRIGHT.attach(4); ///Assigning the signal pins for our servo motors for PWM control
 servoLEFT.attach(3); 
 pinMode(ENA, OUTPUT); ///Assigning the mode of each pin for L298N Motor driver.
 pinMode(IN1, OUTPUT);
 pinMode(IN2, OUTPUT);
 pinMode(IN3, OUTPUT);
 pinMode(IN4, OUTPUT);
 pinMode(ENB, OUTPUT);
}
void loop() 
{
 byte T = 0;  /// temporary variables that will change and return to zero as the loop goes on, they store raw analog values from 0 to 255 and are used for both taking repeated temperature and humidity data
 byte H = 0; 
 int error = SimpleDHTErrSuccess; ///An error variable to catch and store errors if DHT11 sensor can not read properly 
 if (error = dht11.read(&T, &H, NULL) != SimpleDHTErrSuccess) ///The if condition reads both temperature and humidity values in degrees celcius and relative percentage respectively.
  {
    Serial.print("Error = ");  ///This if statement section basically checks the DHT11 sensor for any error values and returns the error and error duration.
    Serial.print(SimpleDHTErrCode(error));
    Serial.print(","); 
    Serial.println(SimpleDHTErrDuration(error)); 
    delay(50);
    return;
  }
 TEMP = T; ///The variables store the numerical temperature and humidity values 
 HUM = H; 
 TIME_LEFT = sonar1.ping_median(avg); ///The time taken for an echo of ultrasound to return, this time is then averaged 10 times to give a final reading that is stored in the variable
 TIME_RIGHT = sonar2.ping_median(avg);
 delay(10); ///A small delay to allow the ultrasonic sensors to stabilize their readings 
 speed_sound = 331.5 + 0.6*TEMP + 0.012*HUM; ///The speed of sound varies with temperature and humidity, by factoring in those we get a very accurate speed of sound using the equation shown. 
 dist_left = (TIME_LEFT/2)*speed_sound; ///The accurate speed of sound and the averaged time taken for echo returns, allow us to get an accurate distance reading up to +-0.2cm 
 dist_left_final = (dist_left/10000); /// a conversion factor to turn the distance into centimeters
 DIST_LEFT_FINAL = dist_left_final; /// another conversion to turn the decimal values to integer ones
 dist_right = (TIME_RIGHT/2)*speed_sound; ///same thing but for the right hand side sensor 
 dist_right_final = (dist_right/10000);
 DIST_RIGHT_FINAL = dist_right_final; 
 servoRIGHT.write(90); ///servo motors take their origin position 
 servoLEFT.write(90);
 delay(10000); ///A delay of 10 seconds to allow the robot to be set down and positioned onto the game mat
 digitalWrite(IN1, LOW); ///Motor driver activates both motors to turn clockwise pushing the robot forward 
 digitalWrite(IN2, HIGH);
 analogWrite(ENA, 200); ///A high speed is given to the motors in the beginning 
 digitalWrite(IN3, LOW);
 digitalWrite(IN4, HIGH);
 analogWrite(ENB, 200);
 delay(10);

  while(DIST_RIGHT_FINAL <= MAX_DIST) ///This while loop prevents our robot from bumping into the wall by keeping it away if gets closer than 5 centimeters to the wall 
  {
   servoLEFT.write(15); ///The actions of the servo motor cause the front axle to turn away from the wall on right that the robot is about to hit 
   servoRIGHT.write(165);
   digitalWrite(IN1, LOW); ///The clockwise direction of motors on the rear still remain, but their speed is slowed to below half their original value to allow a corrective action to be taken 
   digitalWrite(IN2, HIGH);
   analogWrite(ENA, 100);
   digitalWrite(IN3, LOW);
   digitalWrite(IN4, HIGH);
   analogWrite(ENB, 100);
   delay(1000); ///A delay to allow the robot to reassess its position 
     break;
  }

  while(DIST_LEFT_FINAL <= MAX_DIST) ///The exact same wall avoidance mechanism using while loop but this is for the left wall 
  {
   servoRIGHT.write(15);
   servoLEFT.write(165);
   digitalWrite(IN1, LOW);
   digitalWrite(IN2, HIGH);
   analogWrite(ENA, 100);
   digitalWrite(IN3, LOW);
   digitalWrite(IN4, HIGH);
   analogWrite(ENB, 100);
   delay(1000);
     break;
  }

 while(DIST_RIGHT_FINAL > MIN_DIST) /// Here the while loop brings about the turning mechanism of the robot, if the distance recorded is greater then 39.5cm, then the vehicle will turn in the direction the distance was recorded in.
 {
   servoRIGHT.write(15);
   servoLEFT.write(165); 
   digitalWrite(IN1, LOW); ///Clockwise direction of the motors continue but they are now drastically slower to allow for accurate turning. 
   digitalWrite(IN2, HIGH);
   analogWrite(ENA, 80);
   digitalWrite(IN3, LOW);
   digitalWrite(IN4, HIGH);
   analogWrite(ENB, 80);
   delay(2000); ///A longer delay to allow the robot to fully clear the turn before straightening its front axle 
     break;
 }

 while(DIST_LEFT_FINAL > MIN_DIST) ///The same turning initialization but it is started if the left hand side sensor records a greater distance than 39.5cm 
 {
   servoLEFT.write(15);
   servoRIGHT.write(165);
   digitalWrite(IN1, LOW);
   digitalWrite(IN2, HIGH);
   analogWrite(ENA, 80);
   digitalWrite(IN3, LOW);
   digitalWrite(IN4, HIGH);
   analogWrite(ENB, 80);
   delay(2000);
     break;
 }
 delay(10); ///A final delay to allow all sensors to stabilize and the loop can start again. 
 
}
