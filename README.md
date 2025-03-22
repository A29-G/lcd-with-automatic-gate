# lcd-with-automatic-gate

#define RLED 5
#define GLED 6
#define BUZ  7
#define MOTOR 4

#include <Adafruit_LiquidCrystal.h>
Adafruit_LiquidCrystal lcd(0);

const int trigPin=2;
const int echoPin=3;

long duration;
int distance;

void setup()
{
  Serial.begin(9600);
   lcd.begin(16,2);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(RLED,OUTPUT);
  pinMode(GLED,OUTPUT);
  pinMode(BUZ,OUTPUT);
  pinMode(MOTOR,OUTPUT);
 
}
void loop()
{
  digitalWrite(trigPin,LOW);
  delay(2);
  digitalWrite(trigPin,HIGH);
  delay(10);
  digitalWrite(trigPin,LOW);
  duration=pulseIn(echoPin,HIGH);
  distance=duration*0.034/2;
 
 
  
  Serial.print(distance);
  Serial.println(" CM");
  if (distance<100)
  {
   digitalWrite(RLED,HIGH);
   digitalWrite(GLED,LOW);
   digitalWrite(BUZ,HIGH);
   digitalWrite(MOTOR,HIGH);
   Serial.println("ALERT..!");
  lcd.setCursor(0,0);
  lcd.print("AUTOMATIC GATE");
  lcd.setCursor(0,1);
  lcd.print("CLOSE");
  }
  else
  {
    digitalWrite(RLED,LOW);
    digitalWrite(GLED,HIGH);
    digitalWrite(BUZ,LOW);
    digitalWrite(MOTOR,LOW);
    Serial.println("SAFE!");
    
    lcd.setCursor(0,0);
  lcd.print("AUTOMATIC GATE");
  lcd.setCursor(0,1);
  lcd.print("OPEN");
    

 
  }
}




