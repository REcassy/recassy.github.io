---
title: "Update: Fertige Lichtschrankenadapter"
date: 2024-09-06
layout: post
---

## Ziel
In diesem Post zeige ich die ersten voll aufgebauten Lichtschrankenadapter für das Mobile Cassy.

Alle Daten sind bei [Github][gh-lichtschranke] verfügbar.

## Errata
Zwischen der hier gezeigten Platine und der im github repository verfügbaren bestehen folgende Unterschiede:
* die Bezeichnung der Steckbuchsen J4/J5 ist zwischen beiden Board-Varianten unterschiedlich
* der Kondensator C2 ist falsch gepolt

## Platinen
<img src="/assets/imgs/PCB-vorne.PNG" width="600px">
<img src="/assets/imgs/PCB-hinten.PNG" width="600px">

Hier sieht man beide Platinen-Varianten wie sie von JLCPCB geliefert wurden.

## Aufbau
Zuerst werden die drei SMD-Bauteile bestückt. Dabei ist der ESD-Schutz-Chip USBLC6 der schwierigste, weil er nur im SOT23-6-Formfaktor von Reichelt erhältlich ist.

Die beiden Entkopplugskondensatoren C1 (für USBLC6) und C3 (für ATTiny) sind hingegen recht einfach zu verlöten, da sie im 1206 Formfaktor vorgesehen sind.

Der ATTiny wird idealerweise in einen Sockel gesetzt, was das spätere Austauschen und neu programmieren erleichtert. Er kann aber auch direkt verlötet werden und sitzt dann auf C3 auf.

<img src="/assets/imgs/L-Adapter-oben.PNG" width="600px">
<img src="/assets/imgs/L-Adapter-vorne.PNG" width="600px">
<img src="/assets/imgs/L-Adapter-2.PNG" width="600px">

Die weiteren Komponenten werden wie üblich eingesetzt und verlötet. Bei der Variante mit den Messingbuchsen hilft es, diese vorher mit einem kleinen Gasbrenner (z.B. Flambiergerät) vorzuwärmen, dann lassen sie sich leichter verlöten. Das Ausrichten der Messingbuchsen fällt tatsächlich schwer, gegebenfalls kann man sich eine kleine Ausrichthilfe per 3D-Druck erstellen.

Beim zuschneiden der Messingrohre (Innendurchmesser 4mm, Wandstärke 0,5mm) hilft ein einfacher Rohrschneider:

<img src="/assets/imgs/rohrschneider.png" width="600px">

## Funktionsweise

Die Buchsen +5V und GND (rot und blau) können genutzt werden, um die Lampe einer Lichtschranke zu versorgen

## Test mit Fischertechnik-Lichtschranke

## 

[gh-lichtschranke]: https://github.com/REcassy/Lichtschranke-M
