# Adafruit IO
Name: Tejo van der Burg 
<br>
Vak: IOT
<br>
Datum 6-10-2022
<br>
<br>
## Benodigdheden
1. Arduino.
2. Ledstrip arduino.
3. een laptop met arduino IDe geinstaleerd.
<br>

## (1) instaleer Adafruit IO
De eerste stap is om in de libary Adafruit IO Arduino te instaleren. Deze staat niet meteen boven aan je moet wel eerst een paar naar beneden scrollen.
<br>
## (2) maak een acount aan op Adafruit IO
Maak een acount aan op [adafruit IO](https://io.adafruit.com/) maak hier een acount aan. Als dat gedaan is klik op het gele cirkel met een zwarte sleutel erin recht bovenin het scherm. Hierin zie je een key en een username kopieer beide.
<br>
## (3) Maar een colorpikker
Ga op adafruit IO naar dashboard en maak een new dashboard aan. Je mag zelf de naam en de eventuele beschrijving kiezen. Klik dan ook de instelingen logo met een pijl naar benenden rechtsboven op je scherm. klik op create new block. Kies de color picker op de 3de rij van boven helemaal niks. Maak dan een nieuwe feed met de naam colo en selecteer die en maak je blok. Kies dan met de kleurkiezer een kleur.
<br>
## (4) code aanpassen.
Open de arduino op je laptop sluit ook je arduino aan. Vergeet ook die de juist port en board intestellen. Als dat gedaan is doe dan in arduino dit: File > Examples > Adafruit IO Arduino > Adafruitio_14_neopixel. Open eerst de config.h file en verander bovenin bij IO_username "your username" en IO_key "your key" In de key en username die je van adafruit site moest kopieren. Daarna maak met je mobiel een hotspot aan zet de ssid en ww ervan neer bij de wifi_ssid en wifi_pass recepectifelijk. Daarna open de dafruit_14_Neopixel.ino en pas PIXEL_PIN 5 aan naar PIXEL_PIN D5. Als dit gedaan verivieer de voce door op het vinkje linksboven te drukken
<br>
## (5) code uploaden
Upload de code door op het pijltje naar rechts te klikken rechtsboven. Activeer daarna de serial montior rechtsboven op de arduino interface en verander de baud naar 115200. Als daar alleen maar puntjes op verschijnen is dat een teken dat hij niet met de wifi is verboden. Stel de wifi is wel gelukt Krijgt de ledstrip de gekozen kleur van de website.
