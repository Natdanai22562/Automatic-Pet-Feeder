#define BLYNK_PRINT Serial


#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>
#include <Servo.h>
 
Servo petGate;
int gateStart = 45;
int gateEnd = 110  ;
int gateOpenTime = 150;

char auth[] = "o1Ut3Wsc_lWdZp-cRuB89f5Yf0I6xFSk";

// Your WiFi credentials.
// Set password to "" for open networks.
char ssid[] = "xxxxxxxxx";
char pass[] = "xxxxxxxxx";

BLYNK_WRITE(V0)
{
  petGate.write(gateEnd);
  delay(gateOpenTime);
  petGate.write(gateStart);
}

BLYNK_WRITE(V1)
{
  for(int i=0;i<45;i++)
  {
    petGate.write(gateEnd);
    delay(gateOpenTime);
    petGate.write(gateStart);
    delay(gateOpenTime);
  }
}

void setup()
{
  // Debug console
  Serial.begin(9600);
  petGate.attach(D6);
  petGate.write(gateStart);
  Blynk.begin(auth, ssid, pass, "blynk.jpnet.co.th", 8080);
}

void loop()
{
  Blynk.run();
} 
