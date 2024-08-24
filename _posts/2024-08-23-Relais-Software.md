---
title: "Softwareuntersuchungen an einem Relais M"
date: 2024-08-23
layout: post
---

## Hard- und Software
In diesem Beitrag kommt folgendes zum Einsatz
* Mobile Cassy WLAN von LD Didactic und Relais M
* Digital Discovery und Waveforms von Digilent
* ein unter Aufbau gezeigtes Breadboard

## Vorbemerkungen
In diesem Beitrag soll die Kommunikation zwischen dem Relais M und einem Cassy Mobile untersucht werden. Außerdem wird die Vermutung aus dem [letzten Beitrag][post-relhard] überprüft, dass das Relais per cleverem Hack an die Clock-Leitung des I<sup>2</sup>C Busses angebunden ist.
Diese Funktion wird dann nachgestellt.
Auf dieser Basis gibt es einen funktionstreuen Nachbau des Relais M der [in diesem Beitrag][post-relclone] eräutert wird.

## Aufbau
Der Aufbau ist ähnlich zu dem aus dem Beitrag zum [Mikrofon M][post-mikro]. Hier ist bloß ein Relais hinter einem PNP-Transistor ergänzt (Basis an SCK), um die Vermutung zur Beschaltung des Relais zu prüfen.

<img src="/assets/imgs/relais-breadboard.png" width="600px">

## Initialisierung
Nach der gleichen Methode wie bei dem [Mikrofon M][post-mikro] wird der Datenverkehr untersicht. Das Cassy Mobile fragt erneut an Adresse `50` das Register `00` ab, worauf das Relais antwortet:

`40 00 08 00 9E`

erneut stehen die letzten drei Byte für die Katalognummer des M Relais (524 446). Das erste Byte ist allerdings `40` statt `00` wie bei dem Mikrofon (ggf. ein Hinweis darauf, dass es ein Output ist bzw. den Eingang nicht belegt, damit dieser vom ADC getrennt wird?).

Weitere Kommunikation gibt es nicht.

## Schaltvorgang

Nachstehend ein Bild aus dem Logikanalysator. Die Intialisierung ist darunter noch einmal vergrößert zu sehen.

<img src="/assets/imgs/relais-overview.png" width="600px">

<img src="/assets/imgs/relais-init.png" width="600px">

Klar erkennbar sind die ausgelösten Schaltvorgänge am Pegel von SCK. Das auf dem Breadboard angeschlossene Relais schaltet zeitgleich mit.

[post-relhard]: https://recassy.github.io/2024/08/16/Relais-Hardware.html
[post-relclone]: https://recassy.github.io/2024/08/24/Relais-Clone.html
[post-mikro]: https://recassy.github.io/2024/08/04/MCassy-Lichtschranke.html.html
