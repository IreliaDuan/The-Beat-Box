# The Beat Box
Irelia Duan

#Summary 
The beat box project is using Led lights to display the volume and beatsthrough the analog sound sensor. It uses analog sound sensor to sense the volume, the volume higher LED darker, and the volume lower LED lighter. Also, it detects sound every 0.05 second, so the LED could follow the beats of the music.

I think my project should be slow interaction.The concept of my project basically is LED light interacts with the music and beats. User could choose the music which they like and enjoy the LED display for the volume and the beat.

#Components
- Several LED light bulbs
- analog sound sensor
- 9V battery
- arduino kit
- mini breadboard
- wires

#Circuit
Please See Fritzing Diagram in my PDF
- breadboard connect to 5V GND on Arduino
- LED connect to -11 on Arduino
- analog sound sensor connect to breadboard & A0 on Arduino
- 9V battery connect to Arduino

#Video On youtube: The Beat Box
https://www.youtube.com/watch?v=KDY_VmAbNpA

#Coding
【Original authors:Haohua Zhang】 

【Addition & revision: Irelia Duan】  


int sensorPin = A0;   
int ledPin = 11;  
int sensorValue = 0;  
int balance = 0;  
int countZero = 0;  
int holding = 0;   
int delayTime = 50; 

void setup () 

{

  pinMode (ledPin, OUTPUT);
  
  Serial.begin (9600);
  
}

 
 
void loop (){

  ReadVolume();
  
  ShowLED();
  
  
  
  Serial.println (balance, DEC);
  
  delay(delayTime);
  
}



void ShowLED(){

  int ld = balance / 4;
  
  ld = 255 - ld * 200;
  
  ld = ld < 0 ? 0 : ld;
  
  analogWrite(ledPin, ld);
  
}



void ReadVolume(){ 

  sensorValue = analogRead (sensorPin);
  
  if(sensorValue == 0){
  
    countZero++;
    
    if(countZero >= (holding * 400 / delayTime)){
    
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




  
