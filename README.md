# Guidance-for-the-Blind


#include <SoftwareSerial.h>

SoftwareSerial mySerial(2, 3);

long oldtime = 0;
long counter = 0;
long counter2 = 0;

void setup()
{
  // start serial port at 9600 bps:
  Serial.begin(9600);

  pinMode(12, OUTPUT);
  pinMode(13, OUTPUT);
  
  mySerial.begin(9600);
  mySerial.println("I am back");
}

unsigned char x,y,z,j =0;
int val = 0;

void loop()
{
// read the 4-byte value sent from VB containing coordinates and joint ID. 
  
  if(Serial.available())
  {
    int incoming = Serial.read();
    if (incoming == 255)
          while(1)
      {
        if(Serial.available())
        {
          x = Serial.read();
          break;
        }
      }
      while(1)
      {
        if(Serial.available())
        {
          y = Serial.read();
          break;
        }
      }
      while(1)
      {
        if(Serial.available())
        {
          z = Serial.read();
          break;
        }
      }
      while(1)
      {
        if(Serial.available())
        {
          j = Serial.read();
          break;
        }
      }
    } 
  
  long elapsedtime = millis() - oldtime;
  if(elapsedtime > 3000)
  {
    oldtime = millis();
    if(((x > 20) && (x < 70)) && ((z > 30) && (z < 70)) && (counter < 1)){ //rotate 270
      mySerial.println("Rotate 90 degrees left and sit down");
      counter += 1;
    }
    if(((x > 100) && (x < 170)) && ((z < 46) && (z > 30)) && (counter2 < 1)){ //turn left
      mySerial.println("Turn Left and walk straight");
      counter2 += 1;
    }
    if(((x > 100) && (x < 170)) && (z > 46)) { //walk straight
      mySerial.println("Walk straight");
      counter = 0;
      counter2 = 0;
    }
  }
}
