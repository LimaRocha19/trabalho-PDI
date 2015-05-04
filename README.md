# trabalho-PDI


char buffer[18];
int pinA = 2;
int pinB = 3;
int pinC = 4;
int pinD = 5;
int pinE = 6;
int pinF = 7;
int pinG = 8;

void setup() {
  Serial.begin(9600);
  Serial.flush();
  pinMode(pinA,OUTPUT);
  pinMode(pinB,OUTPUT);
  pinMode(pinC,OUTPUT);
  pinMode(pinD,OUTPUT);
  pinMode(pinE,OUTPUT);
  pinMode(pinF,OUTPUT);
  pinMode(pinG,OUTPUT);
  
  /* Estamos usando 255 como padrão de luminosidade devido ao display fraco fornecido pelo laboratório */
}

void loop() {
 if (Serial.available() > 0) {
   int index=0;
   delay(100); 
   int numChar = Serial.available();
   if (numChar>15) {
    numChar=15;
    }
   while (numChar--) {
    buffer[index++] = Serial.read();
   }
   splitString(buffer);
  } 
}

void splitString(char* data) {
  Serial.print("Data entered: ");
  Serial.println(data);
  char* parameter;
  parameter = strtok (data, " ,");
  while (parameter != NULL) {
   setLED(parameter);
   parameter = strtok (NULL, " ,");
}
   
  for (int x=0; x<16; x++) {
   buffer[x]='\0';
   }
  Serial.flush();
}

void setLED(char* data) {
  if ((data[0] == 'v') || (data[0] == 'V')) {
   int Ans = strtol(data+1, NULL, 10);
   Ans = constrain(Ans,0,10);
   Ans = 1000/Ans;
   
  contagem(Ans);
    
  }
}

void contagem(int interval) {
    digitalWrite(pinA,HIGH);
    digitalWrite(pinB,HIGH);
    digitalWrite(pinC,HIGH);
    digitalWrite(pinF,HIGH);
    digitalWrite(pinG,HIGH);
    delay(interval);
    digitalWrite(pinA,LOW);
    digitalWrite(pinB,LOW);
    digitalWrite(pinC,LOW);
    digitalWrite(pinF,LOW);
    digitalWrite(pinG,LOW);
    
    digitalWrite(pinA,HIGH);
    digitalWrite(pinB,HIGH);
    digitalWrite(pinC,HIGH);
    digitalWrite(pinD,HIGH);
    digitalWrite(pinE,HIGH);
    digitalWrite(pinF,HIGH);
    digitalWrite(pinG,HIGH);
    delay(interval);
    digitalWrite(pinA,LOW);
    digitalWrite(pinB,LOW);
    digitalWrite(pinC,LOW);
    digitalWrite(pinD,LOW);
    digitalWrite(pinE,LOW);
    digitalWrite(pinF,LOW);
    digitalWrite(pinG,LOW);
    
    digitalWrite(pinA,HIGH);
    digitalWrite(pinB,HIGH);
    digitalWrite(pinC,HIGH);
    delay(interval);
    digitalWrite(pinA,LOW);
    digitalWrite(pinB,LOW);
    digitalWrite(pinC,LOW);
    
    digitalWrite(pinA,HIGH);
    digitalWrite(pinC,HIGH);
    digitalWrite(pinD,HIGH);
    digitalWrite(pinE,HIGH);
    digitalWrite(pinF,HIGH);
    digitalWrite(pinG,HIGH);
    delay(interval);
    digitalWrite(pinA,LOW);
    digitalWrite(pinC,LOW);
    digitalWrite(pinD,LOW);
    digitalWrite(pinE,LOW);
    digitalWrite(pinF,LOW);
    digitalWrite(pinG,LOW);
    
    digitalWrite(pinA,HIGH);
    digitalWrite(pinC,HIGH);
    digitalWrite(pinD,HIGH);
    digitalWrite(pinF,HIGH);
    digitalWrite(pinG,HIGH);
    delay(interval);
    digitalWrite(pinA,LOW);
    digitalWrite(pinC,LOW);
    digitalWrite(pinD,LOW);
    digitalWrite(pinF,LOW);
    digitalWrite(pinG,LOW);
    
    digitalWrite(pinB,HIGH);
    digitalWrite(pinC,HIGH);
    digitalWrite(pinF,HIGH);
    digitalWrite(pinG,HIGH);
    delay(interval);
    digitalWrite(pinB,LOW);
    digitalWrite(pinC,LOW);
    digitalWrite(pinF,LOW);
    digitalWrite(pinG,LOW);
    
    digitalWrite(pinA,HIGH);
    digitalWrite(pinB,HIGH);
    digitalWrite(pinC,HIGH);
    digitalWrite(pinD,HIGH);
    digitalWrite(pinG,HIGH);
    delay(interval);
    digitalWrite(pinA,LOW);
    digitalWrite(pinB,LOW);
    digitalWrite(pinC,LOW);
    digitalWrite(pinD,LOW);
    digitalWrite(pinG,LOW);
    
    digitalWrite(pinA,HIGH);
    digitalWrite(pinB,HIGH);
    digitalWrite(pinD,HIGH);
    digitalWrite(pinE,HIGH);
    digitalWrite(pinG,HIGH);
    delay(interval);
    digitalWrite(pinA,LOW);
    digitalWrite(pinB,LOW);
    digitalWrite(pinD,LOW);
    digitalWrite(pinE,LOW);
    digitalWrite(pinG,LOW);
    
    digitalWrite(pinB,HIGH);
    digitalWrite(pinC,HIGH);
    delay(interval);
    digitalWrite(pinB,LOW);
    digitalWrite(pinC,LOW);
    
    digitalWrite(pinA,HIGH);
    digitalWrite(pinB,HIGH);
    digitalWrite(pinC,HIGH);
    digitalWrite(pinD,HIGH);
    digitalWrite(pinE,HIGH);
    digitalWrite(pinF,HIGH);
    delay(interval);
    digitalWrite(pinA,LOW);
    digitalWrite(pinB,LOW);
    digitalWrite(pinC,LOW);
    digitalWrite(pinD,LOW);
    digitalWrite(pinE,LOW);
    digitalWrite(pinF,LOW);
}
