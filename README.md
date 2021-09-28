#define BLYNK_PRINT Serial


#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>
#include <Servo.h>
 
Servo petGate;
int gateStart = 45;
int gateEnd = 105;
int gateOpenTime = 150;

char auth[] = "xxxxxxxxxx";

// Your WiFi credentials.
// Set password to "" for open networks.
char ssid[] = "xxxxxxx";
char pass[] = "xxxxxxxx";

BLYNK_WRITE(V0)
{
  petGate.write(gateEnd);
  delay(gateOpenTime);
  petGate.write(gateStart);
}

BLYNK_WRITE(V1)
{
  for(int i=0;i<5;i++)
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
