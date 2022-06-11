#include <SPI.h> 
#include "RF24.h" 

int joyX = A1;
int joyY = A2;


int dataX;
int dataY;

int data[2];

RF24 radio(10,9); 
                                      
const uint64_t pipe = 0xE8E8F0F0E1LL; 


void setup(void){
  Serial.begin(9600);
  radio.begin();                     
  radio.openWritingPipe(pipe);      

void loop(){
  //Send signal data
  dataX = analogRead(joyX);
  dataY = analogRead(joyY);
  
  data[0] = dataX;
  data[1] = dataY;

  Serial.print("Data X:"); Serial.println(dataX);
  Serial.print("Data Y:"); Serial.println(dataY);
  radio.write(data, sizeof(data));
  
}
