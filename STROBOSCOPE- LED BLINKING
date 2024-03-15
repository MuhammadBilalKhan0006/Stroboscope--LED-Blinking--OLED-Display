#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#include <Wire.h>

#define ANCHO 128
#define ALTO 64

Adafruit_SSD1306 display(ANCHO, ALTO, &Wire, -1);
const int rpmbutton=5;
const int button = 4;
const int led = 3;
const int displayfreq=6;
int buttonCheck = 0;
int frequency = 1;
int rpm = 60;
int potentiometer=0;
int scaledpotentiometer=0;
void setup() {
  pinMode(rpmbutton, INPUT);
  pinMode(button, INPUT);
  pinMode(led, OUTPUT);
  Serial.begin(9600);
  if (!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {
    Serial.println("no make sense");
    for (;;);
  }
}

void loop() {
  freequency();
   blink();
   slip();
  // initial frequency should be 1 sec, so delay of 1000 ms will work
for(int i=0;i<10;i++){
  digitalWrite(led,HIGH);
  delay(500/frequency);
  digitalWrite(led,LOW);
  delay(500/frequency);
}
 
}
void freequency(){
  blink();
  slip();
  if(rpm==60){
    frequency=1;
  }
  if(rpm!=60){
    frequency=rpm/60;
  }
}

void blink() {
  slip();
  potentiometer=analogRead(A0);
  int speed=map(potentiometer,0,1023,1,100);
    rpm = 60 * speed;
}
void slip(){
  if(digitalRead(button)== HIGH && digitalRead(displayfreq)==LOW){
    int n_rotor=rpm;
   float slip = (((float)3600) - ((float)n_rotor))/ ((float)3600);
   float slip_final=slip*100;
   display.clearDisplay();
   display.setTextSize(1);
    display.setTextColor(WHITE);
    display.setCursor(0, 0);
    display.println("SLIP");
     display.setTextSize(2);  
    display.println(slip_final);
    display.display();
  }
if(digitalRead(button)==LOW && digitalRead(displayfreq)==LOW){
   display.clearDisplay();
    display.setTextSize(1);
    display.setTextColor(WHITE);
    display.setCursor(0, 0);
    display.println("RPM");
    display.setTextSize(2);  
    display.setCursor(0, 10);
    display.println(rpm);
    display.display(); 

}
if(digitalRead(displayfreq)==HIGH && digitalRead(button)==LOW){
    display.clearDisplay();
    display.setTextSize(1);
    display.setTextColor(WHITE);
    display.setCursor(0, 0);
    display.println("Frequency");
    display.setTextSize(2);  
    display.setCursor(0, 10);
    display.println(frequency);
    display.display(); 
}


}
