#include <Blynk.h>
#define BLYNK_PRINT SwSerial
#include <Ethernet.h>
#include <deprecated.h>
#include <MFRC522.h>
#include <MFRC522Extended.h>
#include <require_cpp11.h>
#include <BlynkSimpleStream.h>


//Blynk
/*************************************************************
#include <deprecated.h>
#include <MFRC522.h>
#include <MFRC522Extended.h>
#include <require_cpp11.h>

#define BLYNK_PRINT Serial
#include <SoftwareSerial.h>
SoftwareSerial SwSerial(0, 1); // RX, TX

  This is a simple demo of sending and receiving some data.
  Be sure to check out other examples!
 *************************************************************/

// Template ID, Device Name and Auth Token are provided by the Blynk.Cloud
// See the Device Info tab, or Template settings
#define BLYNK_TEMPLATE_ID "TMPLhgH3bq55"
#define BLYNK_DEVICE_NAME "SmartLock"
#define BLYNK_AUTH_TOKEN "BCxk2bm7s3Z8ERjEYaSQ1FxX5JaorDIk"

// Comment this out to disable prints and save space
#define BLYNK_PRINT SwSerial


#include <SoftwareSerial.h>
SoftwareSerial SwSerial(1, 0); // RX, TX

#include <BlynkSimpleStream.h>
char auth[] = BLYNK_AUTH_TOKEN;



// ****************************************************************************************** //


// Comment this out to disable prints and save space
#define BLYNK_PRINT SwSerial

//#include <BlynkSimpleSerialBLE.h>
#include <SPI.h>
#include <MFRC522.h>
#include <Servo.h>

 
#define SS_PIN 10
#define RST_PIN 9
#define buzzer 4
#define LED_G 5
#define LED_R 6
#define S1 A0

#define SERVO_PIN 3
Servo myservo;

#define ACCESS_DELAY 2000
#define DENIED_DELAY 1000
MFRC522 mfrc522(SS_PIN, RST_PIN);   // Create MFRC522 instance.

 
void setup() 
{
  Serial.begin(9600);   // Initiate a serial communication
  SPI.begin();          // Initiate  SPI bus
  mfrc522.PCD_Init();   // Initiate MFRC522
  Blynk.begin(Serial, auth);
  tone(buzzer, OUTPUT);
  noTone(buzzer);
  pinMode(LED_G, OUTPUT);
  pinMode(LED_R, OUTPUT);
  myservo.attach(SERVO_PIN);
  myservo.write( 45 );
  Serial.println("Tap the card");
  Serial.println();
}


void loop() 
{
  Blynk.run();
  // Look for new cards
  if ( ! mfrc522.PICC_IsNewCardPresent()) 
  {
    return;
  }
  // Select one of the cards
  if ( ! mfrc522.PICC_ReadCardSerial()) 
  {
    return;
  }
  //Show UID on serial monitor
  Serial.print("UID tag :");
  String content= "";
  byte letter;
  for (byte i = 0; i < mfrc522.uid.size; i++) 
  {
     Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
     Serial.print(mfrc522.uid.uidByte[i], HEX);
     content.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
     content.concat(String(mfrc522.uid.uidByte[i], HEX));
  }
  Serial.println();
  Serial.print("Message : ");
  content.toUpperCase();
  if (content.substring(1) == "00 1F C6 20" || content.substring(1) == "F0 68 E0 1F" ) //change here the UID of the card
  {
    Serial.println("     Access Granted    ");
    Serial.println();
    int i=0;
    do
    {
      i++;
      digitalWrite(LED_G,HIGH);
      delay(800);
      digitalWrite(LED_G, LOW);
      tone(buzzer, 4000);
      delay(300);
      noTone(buzzer);
      delay(100);
    }
    while(i<1);
    myservo.write(230);
    delay(4000);
    myservo.write(55);

  }
 
 else   {
      Serial.println("    Access Denied   ");
      int i=0;
      do
      {
        i++;
        digitalWrite(LED_R,HIGH);
        delay(300);
        digitalWrite(LED_R, LOW);
        tone(buzzer, 4000);
        delay(200);
        noTone(buzzer);
        delay(100);
      }
      while(i<4);

    delay(DENIED_DELAY);
  }
}

//Blynk
BLYNK_WRITE(V0) //Write to Virtual Pin V0
{
  int pin = param.asInt();
  if (pin == 1)
  {
    myservo.write(230);
  }
  else
  {
    myservo.write(50);
  }
}

//Blynk



BLYNK_WRITE(V1) //Write to Virtual Pin V2
{
  int pin = param.asInt();
  if (pin == 1)
  {
    digitalWrite(LED_G,HIGH);
    tone(buzzer, 4000);
    delay(300);
    noTone(buzzer);
    delay(100);
  }
  else
  {
    digitalWrite(LED_G,LOW);
    tone(buzzer, 4000);
    delay(200);
    noTone(buzzer);
    delay(100);
  }
}

BLYNK_WRITE(V2) //Write to Virtual Pin V2
{
  int pin = param.asInt();
  if (pin == 1)
  {
    digitalWrite(LED_R,HIGH);
    tone(buzzer, 4000);
    delay(300);
    noTone(buzzer);
    delay(100);
  }
  else
  {
    digitalWrite(LED_R,LOW);
    tone(buzzer, 4000);
    delay(200);
    noTone(buzzer);
    delay(100);
  }
}

//Read ID in RFID CARD
BLYNK_READ(V4) //Read from Virtual Pin V4
{
  String content= "";
  byte letter;
  for (byte i = 0; i < mfrc522.uid.size; i++) 
  {
     Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
     Serial.print(mfrc522.uid.uidByte[i], HEX);
     content.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
     content.concat(String(mfrc522.uid.uidByte[i], HEX));
  }
  Serial.println();
  Serial.print("Message : ");
  content.toUpperCase();
  if (content.substring(1) == "00 1F C6 20" || content.substring(1) == "F0 68 E0 1F" ) //change here the UID of the card
  {
    Serial.println("     Access Granted    ");
    Serial.println();
    int i=0;
    do
    {
      i++;
      digitalWrite(LED_G,HIGH);
      delay(800);
      digitalWrite(LED_G, LOW);
      tone(buzzer, 4000);
      delay(300);
      noTone(buzzer);
      delay(100);
    }
    while(i<1);
    myservo.write(230);
    delay(4000);
    myservo.write(45);

  }
 
 else   {
      Serial.println("    Access Denied   ");
      int i=0;
      do
      {
        i++;
        digitalWrite(LED_R,HIGH);
        delay(300);
        digitalWrite(LED_R, LOW);
        tone(buzzer, 4000);
        delay(200);
        noTone(buzzer);
        delay(100);
      }
      while(i<4);
    delay(DENIED_DELAY);
  }
}
