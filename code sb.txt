#include<ESP8266WiFi.h>

String i;

WiFiServer server(80);                        //creates a WiFiServer with the given identifier and port number

void setup() {                                // put your setup code here, to run once:
i="";
Serial.begin(9600);
pinMode(16,OUTPUT);
pinMode(15,OUTPUT);
pinMode(4,OUTPUT);
pinMode(0,OUTPUT);
//pinMode(2,OUTPUT);
//pinMode(14,OUTPUT);
//pinMode(12,OUTPUT);
//pinMode(13,OUTPUT);
//pinMode(15,OUTPUT);

  WiFi.disconnect();                          //to disconnect the nodemcu from the previous WiFi connection
delay(2000);
Serial.println("Connecting to Wifi");
WiFi.begin("Srilaxminet","narayana234");             //to specify the username and password of the network to be connected
while((!(WiFi.status()==WL_CONNECTED)))
{
  delay(300);
  Serial.print("...");
}
Serial.println("I am connected");
Serial.println("My local IP is : ");
Serial.print((WiFi.localIP()));               //returns IP address of the local network
server.begin();                               //to initiate the WiFiserver created previously
}

void loop()
{
WiFiClient client=server.available();         //to create a WiFi client
if(!(client))           
{
  return;
}
while(!client.available())
{
  delay(1);
}
i=(client.readStringUntil('\r'));
i.remove(0,5);
i.remove(i.length()-9,9);
if(i=="forward")
{
  digitalWrite(16,HIGH);
  digitalWrite(5,LOW);
  digitalWrite(4,HIGH);
  digitalWrite(0,LOW);
  //Serial.println("forward");
  Serial.println("\n forward");
}
if(i=="reverse")
{
  digitalWrite(5,HIGH);
  digitalWrite(16,LOW);
  digitalWrite(0,HIGH);
  digitalWrite(4,LOW);
  //Serial.println("forward");
  Serial.println("\n reverse");
}
if(i=="stop")
{
  digitalWrite(16,LOW);
  digitalWrite(5,LOW);
  digitalWrite(4,LOW);
  digitalWrite(0,LOW);
  //Serial.println("forward");
  Serial.println("\n stop");
}
if(i=="left")
{
  digitalWrite(16,LOW);
  digitalWrite(5,LOW);
  Serial.println("left");
}
if(i=="right")
{
  digitalWrite(16,HIGH);
  digitalWrite(5,LOW);
  digitalWrite(4,LOW);
  digitalWrite(0,LOW);
  delay(2000);
  //Serial.println("forward");
  Serial.println("right");
}
if(i=="left")
{
  digitalWrite(16,LOW);
  digitalWrite(5,LOW);
  digitalWrite(4,HIGH);
  digitalWrite(0,LOW);
  delay(2000);
  //Serial.println("forward");
  Serial.println("left");
}
}
