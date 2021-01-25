
#include <Servo.h>   
Servo servo;     
int trigPin = A1;    
int echoPin = A2;   
int servoPin = A0;
int led= 10;
long duration, dist, average;   
long aver[3];   


void setup() {       
    Serial.begin(9600);
    servo.attach(servoPin);  
    pinMode(trigPin, OUTPUT);  
    pinMode(echoPin, INPUT);  
    servo.write(0);         
    delay(100);
    servo.detach(); 
} 

void measure() {  
 digitalWrite(10,HIGH);
digitalWrite(trigPin, LOW);
delayMicroseconds(5);
digitalWrite(trigPin, HIGH);
delayMicroseconds(15);
digitalWrite(trigPin, LOW);
pinMode(echoPin, INPUT);
duration = pulseIn(echoPin, HIGH);
dist = (duration/2) / 29.1;   
}


void loop() { 
  for (int i=0;i<=2;i++) {
    measure();               
   aver[i]=dist;            
    delay(1);             
  }
 dist=(aver[0]+aver[1]+aver[2])/3;    

if ( dist<25 ) {

 servo.attach(servoPin);
  delay(1);
 servo.write(0);  
 delay(3000);       
 servo.write(90);    
 delay(1000);
 servo.detach();      
}
Serial.print(dist);
}
