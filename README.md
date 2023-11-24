**OUTPUT**

CODE:

#define BLYNK_TEMPLATE_ID "TMPL3wpFP3MEc"
#define BLYNK_TEMPLATE_NAME "medicine reminder"
#define BLYNK_AUTH_TOKEN "zBneVJLkNr4pI6J3mKTwEQEGImWETtuP"

#define BLYNK_PRINT Serial
#include <WiFi.h>
#include <BlynkSimpleEsp32.h>

const int soundSensorPin = A0;
const int motionSensorPin = 2;

char auth[] = BLYNK_AUTH_TOKEN;
char ssid[] = "Redmi Note 10S";
char pass[] = "12345678";

BlynkTimer timer;
int soundFlag = 0;
int motionFlag = 0;

void sendSoundSensor() {
  int soundValue = analogRead(soundSensorPin);
  Serial.print("Sound sensor value: ");
  Serial.println(soundValue);

  int soundThreshold = 500;  // Adjust as needed

  if (soundValue > soundThreshold && soundFlag == 0) {
    Serial.println("Sound detected!");
    Blynk.logEvent("sound_alert", "Sound Detected");
    soundFlag = 1;
  } else if (soundValue <= soundThreshold) {
    Serial.println("No sound detected");
    soundFlag = 0;
  }
}

void sendMotionSensor() {
  int motionValue = digitalRead(motionSensorPin);

  if (motionValue == HIGH && motionFlag == 0) {
    Serial.println("Motion detected!");
    Blynk.logEvent("motion_alert", "Motion Detected");
    motionFlag = 1;
  } else if (motionValue == LOW) {
    Serial.println("No motion detected");
    motionFlag = 0;
  }
}

void setup() {
  pinMode(soundSensorPin, INPUT);
  pinMode(motionSensorPin, INPUT);

  Serial.begin(115200);
  Blynk.begin(auth, ssid, pass);

  timer.setInterval(5000L, sendSoundSensor);  // Adjust the interval as needed
  timer.setInterval(5000L, sendMotionSensor); // Adjust the interval as needed
}

void loop() {
  Blynk.run();a
  timer.run();
}

![WhatsApp Image 2023-11-24 at 9 00 49 AM](https://github.com/vijethk3904/OUTPUT/assets/149647654/48d5dc02-6854-4a9e-b1bb-3363c5845084)

![WhatsApp Image 2023-11-23 at 10 21 27 PM](https://github.com/vijethk3904/OUTPUT/assets/149647654/96bdd051-8fda-40f0-9042-243093bd6b0d)

![WhatsApp Image 2023-11-23 at 9 44 21 PM](https://github.com/vijethk3904/OUTPUT/assets/149647654/989a4e36-2a21-47f2-ad3c-203f398a9a33)

![WhatsApp Image 2023-11-23 at 9 40 19 PM](https://github.com/vijethk3904/OUTPUT/assets/149647654/750beca5-5df9-4f99-9764-bbf28e4fa786)








