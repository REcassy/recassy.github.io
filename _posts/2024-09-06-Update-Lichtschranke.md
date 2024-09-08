---
title: "Update: Fertige Lichtschrankenadapter"
date: 2024-09-06
layout: post
---

## Ziel
In diesem Post zeige ich die ersten voll aufgebauten Lichtschrankenadapter für das Mobile Cassy.

Alle Daten zum Nachbauen sind bei [Github][gh-lichtschranke] verfügbar.

## Errata
Zwischen der hier gezeigten Platine und der im github repository verfügbaren bestehen folgende Unterschiede:
* die Bezeichnung der Steckbuchsen J4/J5 ist zwischen beiden Board-Varianten unterschiedlich
* der Kondensator C2 ist falsch gepolt

## Platinen
<img src="/assets/imgs/PCB-vorne.PNG" width="600px">
<img src="/assets/imgs/PCB-hinten.PNG" width="600px">

Hier sieht man beide Platinen-Varianten wie sie von JLCPCB geliefert wurden.

## Bauteile
Die benötigten Bauteilen sind hier aufgelistet (Reichelt-Bestellnummern dienen nur als Beispiel):

| Bezeichnung  | Bauteil | Formfaktor | Reicheltnummer |
| ------------- | ------------- | ------------- | ------------- |
| U1  |  ATiny25 | DIP-8 | ATTINY 25-20 PU |
| U2 | USBLC6 | SOT-23-6 |  USBLC6-2SC6 |
| C1, C3 | 50V 100nF Keramikkondensator | 1206 |  WAL 1206B104K500 |
| C2 | 50V 10µF Elektrolytkondensator | RM2,5 |  SU-A 10U 50|
| R1, R2 | 0,25W 5K1 Widerstand | 0207 |  1/4W 5,1K |
| J1 | Mini-Din 6 Buchse | N/A | EB-DIOS M06 |
| J2-J5 | 4mm ID, 5mm OD Messingrohr | N/A | N/A |
| J2-J5 | 4mm Laborbuchse | N/A | SEP 2610 F48  |

Für die Steckverbinder kann man entweder das selbst zuzuschneidene Messingrohr (günstig aber aufwändig) oder die fertigen Buchsen nehmen.

## Aufbau
Zuerst werden die drei SMD-Bauteile bestückt. Dabei ist der ESD-Schutz-Chip USBLC6 der schwierigste, weil er nur im SOT23-6-Formfaktor von Reichelt erhältlich ist.

<img src="/assets/imgs/LS-SMD.png" width="600px">

Die beiden Entkopplugskondensatoren C1 (für USBLC6) und C3 (für ATTiny) sind hingegen recht einfach zu verlöten, da sie im 1206 Formfaktor vorgesehen sind.

Der ATTiny wird idealerweise in einen Sockel gesetzt, was das spätere Austauschen und neu programmieren erleichtert. Er kann aber auch direkt verlötet werden und sitzt dann auf C3 auf.

<img src="/assets/imgs/L-Adapter-oben.PNG" width="300px">

Oben sieht man gut den unter dem Sockel eingesetzten Kondensator.

<img src="/assets/imgs/LS-1.png" width="600px">
__Oben sieht man die Vertauschung von J5 und J4__
<img src="/assets/imgs/LS-2.png" width="600px">

Die weiteren Komponenten werden wie üblich eingesetzt und verlötet. Bei der Variante mit den Messingbuchsen hilft es, diese vorher mit einem kleinen Gasbrenner (z.B. Flambiergerät) vorzuwärmen, dann lassen sie sich leichter verlöten. Das Ausrichten der Messingbuchsen fällt tatsächlich schwer, gegebenfalls kann man sich eine kleine Ausrichthilfe per 3D-Druck erstellen.

<img src="/assets/imgs/L-Adapter-vorne.PNG" width="300px">
<img src="/assets/imgs/L-Adapter-2.PNG" width="300px">

Beim zuschneiden der Messingrohre (Innendurchmesser 4mm, Wandstärke 0,5mm) hilft ein einfacher Rohrschneider:

<img src="/assets/imgs/rohrschneider.png" width="300px">

## Programmierung
Programmiert wird der ATtiny mithilfe eines Arduino Uno. Schrittfolge:
* Zur Arduino IDE fügt man ATTinyCore als Board-Manager hinzu
* Aus dem Beispielbereich der Arduino IDE lädt man den ISP-Sketch auf den Uno
* Anschließend verbindet man den Arduino mit dem ATtiny (Details siehe [Github][gh-lichtschranke])
* Der ATtiny wird mit "Bootloader brennen" vorbereitet (setzen der E-Fuses)
* Das Programm wird auf den Arduino ogespielt


<img src="/assets/imgs/LS-Programmierung.png" width="600px">

## Funktionsweise

Die Buchsen +5V und GND (rot und blau) können genutzt werden, um die Lampe einer Lichtschranke zu versorgen. Die zulässige Stromaufnahme ist seitens LD nicht dokumentiert, mit 100mA sollte man aber auf der sicheren Seite sein. LEDs sind in jedem Fall zu bevorzugen.

Die beiden Eingänge (schwarze Buchsen, J2 ist Lichtschranke 1, J3 ist Lichtschranke 2) werden wie folgt bedient:
* das Cassy zieht J2 auf 5V und J3 auf 3,7 V (der Unterschied muss durch die originale Lichtschranke bedingt sein)
* die an den Adapter angeschlossene Lichtschranke muss diese Spannung jetzt gegen Masse, mindestens aber unter 2V ziehen, um eine Verdunklung zu registrieren
* dafür funktionieren naturbedingt Fotodioden und Fototransistoren
* Fotowiderstände könnten bei richtiger Dimensionierung ebenfalls funktionieren

## Test mit Fischertechnik-Lichtschranke
Da es von Fischertechnik kleine Glühlämpchen und Fototransistoren gibt, lohnt sich folgender Test:

<img src="/assets/imgs/ft-lichtschranke.png" width="600px">

Man beachte den Anschluss des Fototransistors (gelb) zwischen J2 und GND!

## Gehäuse
Im Moment sind die Platinen zur "nackten" Benutzung vorgesehen, ein 3D-gedrucktes Gehäuse ist in Planung.

[gh-lichtschranke]: https://github.com/REcassy/Lichtschranke-M
