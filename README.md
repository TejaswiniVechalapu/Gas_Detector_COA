#CODE

#include <LiquidCrystal.h>
LiquidCrystal lcd(2, 3, 4, 5, 6, 7);

int sensorPin = A0;
int buzzer = 13;
int G_led = 8;
int R_led = 9;


int read_value;
int set = 100;
void setup(){

  pinMode(sensorPin, INPUT);
  
  pinMode(buzzer,OUTPUT);
  pinMode(R_led,OUTPUT);
  pinMode(G_led,OUTPUT);
  
  lcd.begin(16,2);
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("  WELCOME TO  ");
  lcd.setCursor(0,1);
  lcd.print(" GAS DETECTOR ");
  delay(2000);
  lcd.clear();
}

void loop()
{
  read_value = (analogRead(sensorPin));

  read_value = read_value - 100;
  if(read_value<0){read_value=0;}

  lcd.setCursor(0, 0);
  lcd.print("Smoke Level: ");
  lcd.print(read_value);
  lcd.print("  ");

  if(read_value > set)
  {
    lcd.setCursor(0, 1);
    lcd.print("Alert....!!!   ");
    digitalWrite(buzzer, HIGH);
    digitalWrite(R_led, HIGH);
    digitalWrite(G_led, LOW);
    delay(1000);
  }
  
  if(read_value < set)
  {
    lcd.setCursor(0, 1);
    lcd.print(".....Normal....");
    digitalWrite(buzzer, LOW);
    digitalWrite(R_led, LOW);
    digitalWrite(G_led, HIGH);
  }
delay(100);
}
