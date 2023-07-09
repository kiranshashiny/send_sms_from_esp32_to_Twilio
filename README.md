# send_sms_from_esp32_to_Twilio

This ESP32 ino sketch sends sms from ESP32 to Twilio.

Simple steps :

1. Create an account in Twilio. ( Get your assigned number, Sid and Auth Token ) https://www.twilio.com/try-twilio

2. Connect the ESP32 to the laptop and install the Twilio_esp32_client library

![image](https://github.com/kiranshashiny/send_sms_from_esp32_to_Twilio/assets/14288989/adbfbd0c-1c70-404d-ace9-1ce10373308e)

3. Upload this sketch after making the necessary changes to SSID SID and the AuthToken in the code.


```

#include "twilio.hpp"

// Set these - but DON'T push them to GitHub!
static const char *ssid = "SIDOFYOUR HOME WiFi";
static const char *password = "Password";

// Values from Twilio (find them on the dashboard)
static const char *account_sid = "xxxxxxxxx";
static const char *auth_token = "YYYYYYYYYYYYY";
// Phone number should start with "+<countrycode>"
static const char *from_number = "+12176287470";

// You choose!
// Phone number should start with "+<countrycode>"
static const char *to_number = "Your Local Number Here";
static const char *message = "Hello <user>, sent from Twilio";

Twilio *twilio;

void setup() {
  Serial.begin(115200);
  Serial.print("Connecting to WiFi network ;");
  Serial.print(ssid);
  Serial.println("'...");
  WiFi.begin(ssid, password);
  Serial.println("Connecting ");

  while (WiFi.status() != WL_CONNECTED) {
    Serial.println("...");
    delay(500);
  }
  Serial.println("Connected!");

  twilio = new Twilio(account_sid, auth_token);

  delay(1000);
  String response;
  bool success = twilio->send_message(to_number, from_number, message, response);
  if (success) {
    Serial.println("Sent message successfully!");
  } else {
    Serial.println(response);
  }
}

void loop() {
  
}

```

![image](https://github.com/kiranshashiny/send_sms_from_esp32_to_Twilio/assets/14288989/125d1c74-bb3b-4f4f-bafa-e9c47b5bed20)


![image](https://github.com/kiranshashiny/send_sms_from_esp32_to_Twilio/assets/14288989/63fec97c-87e6-4aaf-8fd2-4904dfa7b312)


![image](https://github.com/kiranshashiny/send_sms_from_esp32_to_Twilio/assets/14288989/af7fe9fd-e22c-4e57-88dc-70f8cd9b7eed)

