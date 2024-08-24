---
title: "Hardwareuntersuchungen am Relais M"
date: 2024-08-16
layout: post
---

## Hard- und Software
In diesem Beitrag kommt folgendes zum Einsatz
* Relais M von LD Didactic

## Vorbemerkung
Am Beispiel des Relais M soll gezeigt werden, wie durch sorgfältige Analyse des Hardware-Aufbaus eines Sensors bereits Rückschlüsse auf seine Funktion gezogen werden könne.

## Überblick
Auf der Platine ist folgendes verbaut:
* ein Relais mit 5V Spulenspannung
* ein EEPROM 34LC02 (2kBit)
* ein USBLC6-4 ESD-Schutz für den Mini-DIN-Anschluss
* (vermutlich) ein Transistor im SOT 23 Package mit Beschriftung "MP3 Z4" (Datenblatt war nicht auffindbar)
* einer LED
* zusätzlicher Beschaltung, wie Kondensatoren, Widerständen und Brücken (0-Ohm-Widerstände)

Bemerkenswerter aber: verbaut ist kein Microcontroller oder SoC. Das bedeutet, dass die I<sup>2</sup>C Kommunikation nicht aktiv gesteuert wird. Wie in einem früheren Post vermutet, handelt es sich um einfache Registerabfragen - in diesem Fall Speicherregister des verbauten EEPROM, der darauf mit dem unter dieser Adresse gespeicherten Daten reagiert.

Anschaulich könnte man sagen: Das Relais hat einen Tag (vergleichbar mit einem RFID-Tag an hochwertigen Produkten im Supermarkt oder an Kleidungsstücken), der separat vom restlichen Sensor die Identifikation übernimmt.

Hier ein Bild des EEPROMs auf der Platine:

<img src="/assets/imgs/EEPROM-Relais.PNG" width="300px">

## Ansteuerung des Relais
Spannend ist also die Frage: Wie wird das Relais zum Auslösen gebracht?

Verfolgt man die Leiterbahnen der Spule, so führt diese zuerst über den (vermeintlichen) Transistor und dessen Basis über einen Kondensator zum SCK (Clock)-Anschluss des I<sup>2</sup>-Busses.
Da der Bus im Ruhezustand durch pull-up Widerstände high (+5V) ist, steuert der (nach Messung) PNP-Transistor nicht aus. Er schaltet erst, wenn seine Basis negativ gegenüber der Versorgungsspannung ist.

Dies wird aber gerade durch herunterziehen des Clock-Signals erreicht. Dies führt zum Abfallen der Basisspannung und damit zum Aussteuern des Transistors.

Leybold betreibt hier gewissermaßen I<sup>2</sup>C-Hacking. Die hoch-frequenten (250 kHz Bustakt) Signale der "normalen" Kommunikation werden nicht ausreichen, um ein Schalten zu erreichen und das Ansteuern des Relais wird von den I<sup>2</sup>C-Geräten als ungültig gewertet, da die entsprechende Start-Bedingung nicht erfüllt ist (schließlich wird nur SCK aber nicht SDA für das Relais verwendet, sodass SDA dauerhaft high bleibt).
Sehr clever!

Überprüft werden soll das im nächsten Beitrag an den zwei logischen Konsequenzen:
* Schaltbefehle müssten mit dem Zustand von SCK korrellieren
* Beim Anschalten müsste die Kommunikation der Sensorerkennung zum kurzzeitigen Auslösen führen (ggf. nicht lang genug für das Relais, aber die LED müsste aufleuchten)
