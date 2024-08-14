---
title: "Lichtschranken an Mobile Cassy"
date: 2024-08-04
layout: post
---

## Hard- und Software
In diesem Beitrag kommt folgendes zum Einsatz
* Mobile Cassy WLAN von LD Didactic und Sensor Mikrofon M
* Digital Discovery und Waveforms von Digilent
* ein unter Aufbau gezeigtes Breadboard
* [Arduino-Programm][gh-lichtschranke] zum simulieren einer angeschlossenen Lichtschranke M

## Vorbemerkung
Die nachfolgenden Überlegungen wurden vom Autor von [uranmaschine.de][ur-lichtschranke] angeregt.
Ziel soll es sein, eine Art Trigger-Board zu entwerfen, die das Mobile Cassy in den "Lichtschranken-Modus" versetzt und die Beschaltung einer externen Lichtschranke dann über Pins 2 und 6 zu realisieren.

In der verlinkten Darstellung sollte die Bezeichnung "Timer E" bzw. "Timer F" mit etwas Vorsicht genossen werden. Experimente mit dem hier benutzten Mikrofon M legen nahe, dass es sich eher um einfache Analogeingänge handelt und die bei Anschluss der Lichtschranke M lediglich binär abgefragt werden (über Schwellwert -> high, sonst low). Tatsächliche Hardware-Timer wie etwa noch im Cassy-E verbaut wurden, sind hier nicht mehr zu erwarten. Die Zeitmessung wird wohl der ARM-Prozessor im Mobile Cassy übernehmen.

## Aufbau
Hier ist der Aufbau, der Digital Discovery Logikanalysator ist an Pins 1 und 5 geklemmt:

<img src="/assets/imgs/aufbau-mobile.png" width="600px">

Ein kurzer Blick zeigt, dass es sich offensichtlich um einen I<sup>2</sup>C Bus handeln muss, mit Pin 1 als Datenpin (SDA) und Pin 5 als Takt (SCK):

<img src="/assets/imgs/Logikanalysator.png" width="600px">

## Initialisierung
Es ist klar zu sehen, dass das Mobile Cassy auf dem I<sup>2</sup>C Bus grundsätzlich Adresse 50h abfragt. Dabei läuft der erste Austausch so:
>

worauf das Mikrofon M antwortet
>



## Weitergehende Bemerkungen
* Beim Experimentieren mit dem I<sup>2</sup>C Bus hat das Mobile Cassy Werte auch ohne Beschaltung der Pins 2 und 6 Werte an. Auch Versuche mit anderen Sensoren legen nahe, dass Messwerte auch rein über den I<sup>2</sup>C Bus übertragen werden können. Das Cassy Mobile versucht unter anderem auch Adresse 14h auf dem Bus zu erreichen - ggf. gibt es reservierte Adressen für diese Messdaten und die allgmeine Adresse 50h für die "Verwaltung".
* Die übrige Kommunikation, insbesondere Konfiguration von Messbereichen ist noch unklar.

[gh-lichtschranke]: https://github.com/REcassy/Lichtschranke-M
[ur-lichtschranke]: http://www.uranmaschine.de/524431.Lichtschranke_M/index.php
