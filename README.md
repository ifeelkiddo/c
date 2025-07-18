const int LDR = 4;
const int LED = 5;
const int BUZZER = 21;
const int PIR = 2;

bool motionDetected = false;  // Flag to remember motion detection

void setup() {
  Serial.begin(115200);
  pinMode(LDR, INPUT);
  pinMode(PIR, INPUT);
  pinMode(LED, OUTPUT);
  pinMode(BUZZER, OUTPUT);
}

void loop() {
  int LDRval = analogRead(LDR);
  int pirState = digitalRead(PIR);

  Serial.print("LDR: ");
  Serial.print(LDRval);
  Serial.print(" | PIR: ");
  Serial.println(pirState);

  // Only sets or resets the flag
  if (LDRval <= 400) {  // It is dark
    if (pirState == HIGH) {
      motionDetected = true;  // Motion detected at night
    }
  } else {
    // It is day now, reset the flag and turn everything OFF
    motionDetected = false;
    digitalWrite(LED, LOW);
    noTone(BUZZER);
  }

  // Acts based on the flag
  if (motionDetected) {
    digitalWrite(LED, HIGH);
    tone(BUZZER, 1000);
  }

  delay(100);
}