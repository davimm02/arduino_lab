#include <SoftwareSerial.h>
#define butGreen 2
#define ledGreen 3
#define butRed 4
#define ledRed 5
#define ledBlue 6
#define butBlue 7
#define ledYellow 8
#define butYellow 9
#define buzzer 10

int stateGreen = 0;
int stateBlue = 0;
int stateYellow = 0;
int stateRed = 0;

int seq[11];

int pressed = -1;
int i = 0;
int x  = 0;

bool alive = false;

void setup(){
  pinMode(butGreen, INPUT_PULLUP);
  pinMode(ledGreen, OUTPUT);
  pinMode(butRed, INPUT_PULLUP);
  pinMode(ledRed, OUTPUT);
  pinMode(butBlue, INPUT_PULLUP);
  pinMode(ledBlue, OUTPUT);
  pinMode(butYellow, INPUT_PULLUP);
  pinMode(ledYellow, OUTPUT);
  pinMode(buzzer, OUTPUT);
  // Serial.begin(9600);
}

void sound(int s){
  tone(buzzer, 1000 + 250*s);
  delay(980);
  noTone(buzzer);
}

bool allDown(){
  // Serial.print("G - ");
  // Serial.print(digitalRead(butGreen));
  // Serial.print(" Y - ");
  // Serial.print(digitalRead(butYellow));
  // Serial.print(" B - ");
  // Serial.print(digitalRead(butBlue));
  // Serial.print(" R - ");
  // Serial.print(digitalRead(butRed));
  // Serial.print("\n");
  return !(digitalRead(butGreen)==LOW || digitalRead(butRed)==LOW || digitalRead(butYellow)==LOW || digitalRead(butBlue)==LOW);
}

void light(int n){
  if(n==0) digitalWrite(ledGreen, HIGH); 
  else if(n==1) digitalWrite(ledRed, HIGH);	
  else if(n==2) digitalWrite(ledBlue, HIGH);
  else if(n==3) digitalWrite(ledYellow, HIGH);
  sound(n);
  digitalWrite(ledGreen, LOW);
  digitalWrite(ledBlue, LOW);
  digitalWrite(ledRed, LOW);
  digitalWrite(ledYellow, LOW);
  
}

int butPress(){
  if (digitalRead(butGreen)==LOW) return 0;
  else if (digitalRead(butRed)==LOW) return 1;
  else if (digitalRead(butBlue)==LOW) return 2;
  else if (digitalRead(butYellow)==LOW) return 3;
}

void loop(){
  if(!alive || x>9){
    randomSeed(analogRead(1));
	  digitalWrite(ledGreen, HIGH);
    digitalWrite(ledBlue, HIGH);
    digitalWrite(ledRed, HIGH);
    digitalWrite(ledYellow, HIGH);
    
    sound(alive ? 5 : -2);

    digitalWrite(ledGreen, LOW);
    digitalWrite(ledBlue, LOW);
    digitalWrite(ledRed, LOW);
    digitalWrite(ledYellow, LOW);
    digitalWrite(RESET, HIGH);
    x=0;
    alive=true;
  }
  
  if(x<11) seq[x] = random(0, 4);
  // Serial.println(seq[x]); //prints the sequence
  x+=1;
  for(i=0; i<x; i++){
    delay(1000);
    light(seq[i]);
  }
  
  for(int j=0; j<x; j++){
    // Serial.write("entrou1\n");
    while(allDown());
    // Serial.write("entrou2\n");
	  pressed = butPress();
    light(pressed);
    while(!allDown());
    if(pressed!=seq[j]){ alive = false; j=x; }
  }
}
