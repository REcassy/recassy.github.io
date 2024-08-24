---
title: "Klonen eines Relais M"
date: 2024-08-24
layout: post
---

## Hard- und Software
In diesem Beitrag kommt folgendes zum Einsatz
* Mobile Cassy WLAN von LD Didactic
* eine Lochrasterplatine (Einzelheiten siehe Aufbau & Schaltplan)
* [ATTiny-Programm][gh-relais] zum initialisieren des Cassy Mobile

## Vorbemerkungen
Wie in den beiden Posts zu [Hard-][post-relhard] und [Software][post-relsoft] des Relais M erläutert, reicht ein EEPROM der unter Adresse `00` die Katalognummer des Relais eingespeichert hat.
Für bessere Flexibilität wird hier ein ATTiny25 genutzt, der per Arduino ISP und ATTinyCore von einem Arduino Uno programmiert wird.

## Aufbau
Nachstehend Bilder von der (nicht ganz so ansehnlichen) Lochrasterplatine

<img src="/assets/imgs/breadboard-upside.png" width="600px">

<img src="/assets/imgs/breadboard-underside.png" width="600px">

Hinweis: Hier ist aus debugging-Gründen noch eine Power-LED angeschlossen, aber leine Relais-LED. Der untenstehende Schaltplan sieht es anders vor.

## Schaltplan

<img src="/assets/imgs/relais-schem.jpg" width="1000px">

Die Schaltung besteht aus zwei Teilen: Dem ATTiny25-Schaltkreis und dem Relais-Schaltkreis.

### ATTiny25
Der ATTiny ist zunächst an VCC und GND direkt über die Mini-DIN Buchse angeschlossen. Dabei ist grundsätzlich ein Entkopplungskondensator von 10µF in der Leitung sowie ein 100nF Kondensator unmittelbar zwischen beiden Pins auf der Unterseite der Fassung (es gibt auch Fassungen mit eingebautem 100nF-Kondensator).

SDA und SCL sind über jeweils einen 5,1K pull-up Widerstand an die Mini-DIN Buchse angeschlossen.

### Relais

Das Relais hingt hinter einem BC557 PNP Transistor (Emitter an +5V, Basis über 1K Widerstand und 10µF Kondensator an SCK, Collector an Relais-Spule).

Die Ausgänge sind wie folgt beschaltet: im Ruhezustand sind schwarz-blau geschlossen, im Schaltzustand schwarz-rot.

## Code
Das [ATTiny-Programm][gh-relais] ist denkbar kurz und realisiert nur, dass auf die entsprechende Abfrage mit der Katalognummer geantwortet wird.

[gh-relais]: https://github.com/REcassy/Relais-M
[post-relhard]: https://recassy.github.io/2024/08/16/Relais-Hardware.html
[post-relsoft]: https://recassy.github.io/2024/08/23/Relais-Software.html
