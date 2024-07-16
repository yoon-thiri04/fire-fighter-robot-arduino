## Code Implemenation of Arduino Fire Fighter Robot
```
#include <Servo.h>
const int sensorMin = 0;     // sensor minimum
const int sensorMax = 1024;  // sensor maximum
const int buzzerPin = 12;
const int pumpPin =9;
const int ENA = 5;
const int ENB = 6;
const int IN1 = 2;
const int IN2 = 3;
const int IN3 = 4;
const int IN4 = 7;
Servo elbowServo;
enum FireState {
  NO_FIRE,
  CLOSE_FIRE,
  ALARM_FIRE
};  
FireState currentState = NO_FIRE;
void setup() {
  pinMode(ENA, OUTPUT);
  pinMode(ENB, OUTPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);
  pinMode(pumpPin, OUTPUT);
  pump("Stop");
  elbowServo.attach(10);
  Serial.begin(9600);
  pinMode(buzzerPin, OUTPUT);
}

void loop() {
  FireDetect();
  handleState();
}

void FireDetect() {
    int sensorReading_left = analogRead(A2);
    Serial.print("Sensor Reading Left : ");
    Serial.println(sensorReading_left);
    int sensorReading_right = analogRead(A0);
    Serial.print("Sensor Reading Right : ");
    Serial.println(sensorReading_right);
    int sensorReading_forward = analogRead(A1);
    Serial.print("Sensor Reading Forward : ");
    Serial.println(sensorReading_forward);
    int feet1 = map(sensorReading_left, sensorMin, sensorMax, 0, 10);
    Serial.print("feet1: ");
    Serial.println(feet1);
    int feet2 = map(sensorReading_right, sensorMin, sensorMax, 0, 10);
    Serial.print("feet2: ");
    Serial.println(feet2);
    int feet3 = map(sensorReading_forward, sensorMin, sensorMax, 0, 10);
    Serial.print("feet3: ");
    Serial.println(feet3);
    if (feet1 <= 4 || feet2 <=3 ) {
     currentState = CLOSE_FIRE;
    } 
    else if (feet1 <= 7 || feet2 <= 8) {
      currentState = ALARM_FIRE;
    } else {
    currentState = NO_FIRE;
    }
}
void pump(String p){
  if(p=="Start"){
    digitalWrite(pumpPin,HIGH);
    Serial.println("Pump ON");
    delay(2000);
  }else if(p=="Stop"){
    digitalWrite(pumpPin,LOW);
    Serial.println("Pump Not On");
    delay(1000);
  }
}
void handleState() {
  int sensorReading_left = analogRead(A2);
  int sensorReading_right = analogRead(A0);
  int sensorReading_forward = analogRead(A1);
  int feet1 = map(sensorReading_left, sensorMin, sensorMax, 0, 10);
  int feet2 = map(sensorReading_right, sensorMin, sensorMax, 0, 10);
  int feet3 = map(sensorReading_forward, sensorMin, sensorMax, 0, 10);
  switch (currentState) {
    case NO_FIRE:
      Serial.println("No Fire");
      elbowServo.write(90);
      digitalWrite(buzzerPin, LOW);
      stopMotors();
      pump("Stop");
      break;
    case CLOSE_FIRE:
        Serial.println(" Close Fire ");
        stopMotors();
        delay(1000);
        pump("Start");
        break;
    case ALARM_FIRE:
        Serial.println("Fire Alarm"); 
        digitalWrite(buzzerPin, HIGH);
        delay(1000);
        digitalWrite(buzzerPin, LOW);
        pump("Stop");
    if (feet1 <= 8) {
        Serial.println("Left");
        moveForward();
        Serial.println("Left Function Called");
} else if (feet2 <= 8) {
        Serial.println("Right");
        moveForward();
        Serial.println("Right Function Called");
      } 
      break;
  }
}
void stopMotors() {
   analogWrite(ENA, 0);
   analogWrite(ENB, 0);
   digitalWrite(IN1, LOW);
   digitalWrite(IN2, LOW);
   digitalWrite(IN3, LOW);
   digitalWrite(IN4, LOW);
}
void moveForward() {
  Serial.println("Forward Loop called");
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, HIGH);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, HIGH);
  delay(1000);
}
```
---
