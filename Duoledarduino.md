# Duo adrduino
Name: Tejo van der Burg 
<br>
Vak: IOT
<br>
Datum 13-10-2022
<br>
<br>

## Benodigdheden
1. Arduino.
2. Ledstrip arduino.
3. knop arduino.
4. twee laptop met arduino IDe geinstaleerd.
5. Een adafruit IO acount
<br>


## Intro
Voor deze opdracht moest ik samen met een klasgenoot in dit geval Simon. De een moestervoor zorgen dat doormiddel van een knop er iets in de serial monitor van de ander word gezet. Ik leg hierbij het ontvang gedeelte uit.

<br>

## Stap (1) Arduino openen.
Open Arduino ga bij file naar examples Adafruit Io Arduiono en kies dan AdafruitIO_21_feed_read. Daarnaast kies je juiste board en poort.
<br>

## Stap (2) Instelingen
Ga in de config file je wifi en Adafruit IO gegevens neerzetten. Ook moet je de naam en de feed van adafruitIO neerzetten in je main document.


## Error (1) Verkeerde comport
Ik had perongeluk com 4 geslecteerd in plaats van com 8 hierdoor kreeg ik een error zie de foto hieronder. Het punt was dat de com die gebruikt moet worden voor mijn nodemcu is com 8 is. Nadat ik weer terug switchde op com 8 deed hij het.
![Error van foute com](iot_images/comerror.jfif)
<br>

## Error (2) Geen wifi verbinding want hotspot is scheit
Als ik met men hotsspot verbinde kreeg ik alleen maar puntjes te zien zoals in de foto hieronder. Terwijl mijn settings goed waren. Toen ik mijn verbinding verandere naar de hotsport van Simon deed het wel in een keer.
![veel puntjes](iot_images/puntjeswifi.jfif)
