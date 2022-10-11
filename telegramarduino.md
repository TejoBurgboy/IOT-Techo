# Adafruit IO
Name: Tejo van der Burg 
<br>
Vak: IOT
<br>
Datum 12-10-2022
<br>
<br>

## Benodigdheden
1. Arduino.
2. Ledstrip arduino.
3. een laptop met arduino IDe geinstaleerd.
4. Een mobiel met Telegram erop geinstaleerd.
<br>

## (1) Telegram Botfather
Open deze [link](https://t.me/botfather) op je telefoon. Als dat goed gaat opent telegram en start je een gesprek met de BotFather. Klik op begin en dan doet hij automatish /start voor je op android. Vervolg dit met een /newbot. Geef de bot een naam en een username. Nu krijg je een lang bericht met een link en een code bewaar die beide.
<br>
![Botfather](iot_images/bot.jfif)
<br>

## (2) Telegram Idbot
Open deze [link](https://t.me/myidbot) op je telefoon. Dit doet hetzelfde als bij de bot father en klik op begin. Stuur nu naar deze bot /getid. Nu krijg je een ID te zien bewaar ook deze.
<br>
![Idbot](iot_images/bot2.jfif)
<br>


## (3) Arduino voorbereiding.
Zorg dat je van arduino ESP8266 of ESP32 geinstaleerd heb en ook de bijbehorde borden heb. Instaleerd door ook [de universal telegram bot via deze link](https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot/archive/master.zip). Na het downloaden van de zip ga je naar sketch>include Libary> add.zip Libary.... Than add the libary. Tot slot ga naar sketch>include libary> manage libary. Er zoek dan naar de ArduinoJson en instaleer die.
<br>

## (4) Arduino Code.
Open Arduino en plak deze code erin.
```
#ifdef ESP8266
  #include <WiFi.h>
#else
  #include <ESP8266WiFi.h>
#endif
#include <WiFiClientSecure.h>
#include <UniversalTelegramBot.h>   // Universal Telegram Bot Library written by Brian Lough: https://github.com/witnessmenow/Universal-Arduino-Telegram-Bot
#include <ArduinoJson.h>

// Replace with your network credentials
const char* ssid = "REPLACE_WITH_YOUR_SSID";
const char* password = "REPLACE_WITH_YOUR_PASSWORD";

// Initialize Telegram BOT
#define BOTtoken "XXXXXXXXXX:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"  // your Bot Token (Get from Botfather)

// Use @myidbot to find out the chat ID of an individual or a group
// Also note that you need to click "start" on a bot before it can
// message you
#define CHAT_ID "XXXXXXXXXX"

#ifdef ESP8266
  X509List cert(TELEGRAM_CERTIFICATE_ROOT);
#endif

WiFiClientSecure client;
UniversalTelegramBot bot(BOTtoken, client);

// Checks for new messages every 1 second.
int botRequestDelay = 1000;
unsigned long lastTimeBotRan;

const int ledPin = 2;
bool ledState = LOW;

// Handle what happens when you receive new messages
void handleNewMessages(int numNewMessages) {
  Serial.println("handleNewMessages");
  Serial.println(String(numNewMessages));

  for (int i=0; i<numNewMessages; i++) {
    // Chat id of the requester
    String chat_id = String(bot.messages[i].chat_id);
    if (chat_id != CHAT_ID){
      bot.sendMessage(chat_id, "Unauthorized user", "");
      continue;
    }
    
    // Print the received message
    String text = bot.messages[i].text;
    Serial.println(text);

    String from_name = bot.messages[i].from_name;

    if (text == "/start") {
      String welcome = "Welcome, " + from_name + ".\n";
      welcome += "Use the following commands to control your outputs.\n\n";
      welcome += "/led_on to turn GPIO ON \n";
      welcome += "/led_off to turn GPIO OFF \n";
      welcome += "/state to request current GPIO state \n";
      bot.sendMessage(chat_id, welcome, "");
    }

    if (text == "/led_on") {
      bot.sendMessage(chat_id, "LED state set to ON", "");
      ledState = LOW;
      digitalWrite(ledPin, ledState);
    }
    
    if (text == "/led_off") {
      bot.sendMessage(chat_id, "LED state set to OFF", "");
      ledState = HIGH;
      digitalWrite(ledPin, ledState);
    }
    
    if (text == "/state") {
      if (digitalRead(ledPin)){
        bot.sendMessage(chat_id, "LED is ON", "");
      }
      else{
        bot.sendMessage(chat_id, "LED is OFF", "");
      }
    }
  }
}

void setup() {
  Serial.begin(115200);

  #ifdef ESP8266
    configTime(0, 0, "pool.ntp.org");      // get UTC time via NTP
    client.setTrustAnchors(&cert); // Add root certificate for api.telegram.org
  #endif

  pinMode(ledPin, OUTPUT);
  digitalWrite(ledPin, ledState);
  
  // Connect to Wi-Fi
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);
  #ifdef ESP32
    client.setCACert(TELEGRAM_CERTIFICATE_ROOT); // Add root certificate for api.telegram.org
  #endif
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.println("Connecting to WiFi..");
  }
  // Print ESP32 Local IP Address
  Serial.println(WiFi.localIP());
}

void loop() {
  if (millis() > lastTimeBotRan + botRequestDelay)  {
    int numNewMessages = bot.getUpdates(bot.last_message_received + 1);

    while(numNewMessages) {
      Serial.println("got response");
      handleNewMessages(numNewMessages);
      numNewMessages = bot.getUpdates(bot.last_message_received + 1);
    }
    lastTimeBotRan = millis();
  }
}
```
After that chage a few things. bij const char change the ssid and the password into the ones of your wifi. Vul bij bottoken de token van je bot in. En de ID van van je chat moet je invullen Bij CHAT_ID. Zorg daarna dat je juist board en port gekozen heb. Veriveer ook je code daarna nog. Als je dat lukt upload je code. Als er een lampje op je aruino brandt doet ie het.
<br>
![Lampaan](iot_images/lamp_aan.jfif)
<br>
## (5) Ledpin error
Ik had opbasis van de eerste opdrachten de Ledpin naar D5 verandert hierdoor zag ik geen licht als ik iets zei op telegram. Later toen ik het terug veranderde naar 2 deed het lampje het wel als ik de juiste input had.
<br>
## Bronnen
*[Telegram control](https://randomnerdtutorials.com/telegram-control-esp32-esp8266-nodemcu-outputs/)
