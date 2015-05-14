char buffer[18];
byte seven_seg_digits[16][7] = { { 1,1,1,1,1,1,0 }, // = Digito 0
{ 0,1,1,0,0,0,0 }, // = Digito 1
{ 1,1,0,1,1,0,1 }, // = Digito 2
{ 1,1,1,1,0,0,1 }, // = Digito 3
{ 0,1,1,0,0,1,1 }, // = Digito 4
{ 1,0,1,1,0,1,1 }, // = Digito 5
{ 1,0,1,1,1,1,1 }, // = Digito 6
{ 1,1,1,0,0,0,0 }, // = Digito 7
{ 1,1,1,1,1,1,1 }, // = Digito 8
{ 1,1,1,0,0,1,1 }, // = Digito 9
{ 1,1,1,0,1,1,1 }, // = Digito A
{ 0,0,1,1,1,1,1 }, // = Digito B
{ 1,0,0,1,1,1,0 }, // = Digito C
{ 0,1,1,1,1,0,1 }, // = Digito D
{ 1,0,0,1,1,1,1 }, // = Digito E
{ 1,0,0,0,1,1,1 } // = Digito F
}; 

int button = 9;
int errou = 10;
int acertou = 11;


int v = 1; //variavel global de velocidade
int n = 0; //variavel global do numero
int led = 0; //variavel global do led

void sevenSegWrite(byte digit) //Funcao que aciona o display
{
byte pin = 2;
//Percorre o array ligando os segmentos correspondentes ao digito
for (byte segCount = 0; segCount < 7; ++segCount)
{
digitalWrite(pin, seven_seg_digits[digit][segCount]);
++pin;

}
} 

void setup() { 
Serial.begin(9600); 
Serial.flush(); 
pinMode(2, OUTPUT); //Pino 2 do Arduino ligado ao segmento A
pinMode(3, OUTPUT); //Pino 3 do Arduino ligado ao segmento B
pinMode(4, OUTPUT); //Pino 4 do Arduino ligado ao segmento C
pinMode(5, OUTPUT); //Pino 5 do Arduino ligado ao segmento D
pinMode(6, OUTPUT); //Pino 6 do Arduino ligado ao segmento E
pinMode(7, OUTPUT); //Pino 7 do Arduino ligado ao segmento F
pinMode(8, OUTPUT); //Pino 8 do Arduino ligado ao segmento G
pinMode(9, INPUT); 
pinMode(10, OUTPUT);
pinMode(11, OUTPUT);
}

void loop() { 

if (Serial.available() > 0) {
int index=0; 
delay(100); 
int numChar = Serial.available(); 
if (numChar>15) { numChar=15; } 
while (numChar--) { buffer[index++] = Serial.read(); } 
splitString(buffer); 
} 
}

void splitString(char* data) { 
Serial.print("Data entered: "); 
Serial.println(data); 
char* parameter; 
parameter = strtok (data, " ,"); 
while (parameter != NULL) { setLED(parameter); parameter = strtok (NULL, " ,"); }

for (int x=0; x<16; x++) { buffer[x]='\0'; } 
Serial.flush(); 
}

void setLED(char* data) { 
if ((data[0] == 'v') || (data[0] == 'V')) { 
v = strtol(data+1, NULL, 10); 
v = constrain(v,0,10); 
Serial.print("Velocidade: ");
Serial.println(v);
v = 1000/v;
}
if ((data[0] == 'n') || (data[0] == 'N')){
n = strtol(data+1, NULL, 10); 
n = constrain(n,0,9); 
}
if ((data[0] == 'p') || (data[0] == 'P')) {
int i = 0;
do {

for (int count = 9; count >= 0; count--)
{
Serial.print("Numero do led");
Serial.println(led);
Serial.println(count);
Serial.println(n);

if(digitalRead(button) == HIGH   && n == count)
{
digitalWrite(acertou,HIGH);
Serial.println("aaaaaaaaaa");
Serial.println(digitalRead(button));
led++;
}
digitalWrite(acertou,LOW);

delay(v);
sevenSegWrite(count);

Serial.print(led);
}
i++;
}while(i < 9);

} 
delay(1000);
sevenSegWrite(led);
}
