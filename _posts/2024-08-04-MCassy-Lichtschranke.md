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


## Aufbau
Hier ist der Aufbau, der Digital Discovery ist an Pins 1 und 5 geklemmt:

<img src="/assets/imgs/aufbau-mobile.png" width="600px">

Ein kurzer Blick zeigt, dass es sich offensichtlich um einen I<sup>2</sup>C Bus handeln muss, mit Pin 1 als Datenpin (SDA) und Pin 5 als Takt (SCK):

<img src="/assets/imgs/Logikanalysator.png" width="600px">

[gh-lichtschranke]: https://github.com/REcassy/Lichtschranke-M
