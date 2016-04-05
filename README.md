# Silent-Box
Arduino Project


my coding
------------------------------
int sensorPin = A0; 

int ledPin = 11;
int sensorValue = 0;
int balance = 0;
int countZero = 0;
int holding = 10;
int delayTime = 500;

void setup () 
{
  pinMode (ledPin, OUTPUT);
  Serial.begin (9600);
}
 
void loop (){
  ReadVolume();

  3fg
  ShowLED();
  
  Serial.println (balance, DEC);
  delay(delayTime);
}

void ShowLED(){
  int ld = balance / 4;
  ld = 255 - ld * 5;
  ld = ld < 0 ? 0 : ld;
  analogWrite(ledPin, ld);
}

void ReadVolume(){ 
  sensorValue = analogRead (sensorPin);
  if(sensorValue == 0){
    countZero++;
    if(countZero >= (holding * 1000 / delayTime)){
      balance = 0;
    }
  }else{
    countZero = 0;
    if(balance == 0){
      balance = sensorValue;
    }else{
      balance = (balance * 2 + sensorValue) / 3;
    }
  }
}
