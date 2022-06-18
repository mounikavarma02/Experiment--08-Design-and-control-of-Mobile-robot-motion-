# Experiment--08-Design-and-control-of-Mobile-robot-motion-
 

## AIM: 
To Design a wheel base for mobile robot and control the motion using forward and reverse motion 
 
### COMPONENTS REQUIRED:
1.	 Patch cables 
2.	L293D motor shield 
3.	Arduino Uno 
4.	USB Interfacing cable 
5.	Connecting wires 
6.	Wheels
7.	DC motor 


### THEORY: 
We can control the speed of the DC motor by simply controlling the input voltage to the motor and the most common method of doing that is by using PWM signal.


DC Motor Speed Control Input Voltage
PWM DC Motor Control
PWM, or pulse width modulation is a technique which allows us to adjust the average value of the voltage that’s going to the electronic device by turning on and off the power at a fast rate. The average voltage depends on the duty cycle, or the amount of time the signal is ON versus the amount of time the signal is OFF in a single period of time.
 

PWM Working Principle - Pulse Width Modulation How It Works
 
 

![image](https://user-images.githubusercontent.com/36288975/174224618-c8d83fea-4456-4706-9974-c8c7641a27e5.png)



![image](https://user-images.githubusercontent.com/36288975/174224728-daf998f2-8ca4-44b8-828d-a3229688cf1e.png)


### PROCEDURE:
1.	Connect the circuit as per the circuit diagram 
2.	Connect the board to your computer via the USB cable.
3.	If needed, install the drivers.
4.	Launch the Arduino IDE.
5.	Select the board (If you the board is arduino uno, select accordingly).
6.	Select your serial port, accordingly ( E.g. COM5 )
7.	Open the file of the program  and verify the error , clear if any errors that are existing 
8.	Upload the program and check for the physical working. 
9.	Ensure safety before powering up the device 
10.	Plot the graph for the output voltage vs the resistance 


### PROGRAM 

```c

#include <AFMotor.h>


//defining pins and variables
#define lefts A0
#define rights A1

//defining motors
AF_DCMotor motor1(1, MOTOR12_1KHZ); 
AF_DCMotor motor2(2, MOTOR12_1KHZ);
AF_DCMotor motor3(3, MOTOR34_1KHZ);
AF_DCMotor motor4(4, MOTOR34_1KHZ);



void setup() {
  //Setting the motor speed
  motor1.setSpeed(180);
  motor2.setSpeed(180);
  motor3.setSpeed(180);
  motor4.setSpeed(180);
  //Declaring PIN input types
  pinMode(lefts,INPUT);
  pinMode(rights,INPUT);
  //Begin serial communication
  Serial.begin(9600);
  
}

void loop(){
  //Printing values of the sensors to the serial monitor
  Serial.println(analogRead(lefts));
  Serial.println(analogRead(rights));
  //line detected by both
  if(analogRead(lefts)<=350 && analogRead(rights)<=350){
    //Forward
    motor1.run(FORWARD);
    motor2.run(FORWARD);
    motor3.run(FORWARD);
    motor4.run(FORWARD);
  }
  //line detected by left sensor
  else if(analogRead(lefts)<=350 && !analogRead(rights)<=350){
    //turn left
    motor1.run(FORWARD);
    motor2.run(FORWARD);
    motor3.run(BACKWARD);
    motor4.run(BACKWARD);
    
  }
  //line detected by right sensor
  else if(!analogRead(lefts)<=350 && analogRead(rights)<=350){
    //turn right
    motor1.run(BACKWARD);
    motor2.run(BACKWARD);
    motor3.run(FORWARD);
    motor4.run(FORWARD);
   
  }
  //line detected by none
  else if(!analogRead(lefts)<=350 && !analogRead(rights)<=350){
    //stop
    motor1.run(RELEASE);
    motor2.run(RELEASE);
    motor3.run(RELEASE);
    motor4.run(RELEASE);
   
  }
  
}
```

### OUTPUT:

![WhatsApp Image 2022-06-18 at 8 43 17 AM](https://user-images.githubusercontent.com/78891098/174420816-6bc6a955-19a1-4092-956b-b988dc5155e5.jpeg)

![WhatsApp Image 2022-06-18 at 8 43 17 AM (1)](https://user-images.githubusercontent.com/78891098/174420819-711e5d44-a55f-4b87-a251-81300ccdaa69.jpeg)

![WhatsApp Image 2022-06-18 at 8 43 18 AM](https://user-images.githubusercontent.com/78891098/174420826-c1a8b6ea-bb04-49fa-8532-30a9361266f1.jpeg)

 
 
 
 
 
 
 
 
 
 
 
 
 
 

 
 














### RESULTS : Arduino uno is interfaced with FSR and output values are indicated on a graph.
