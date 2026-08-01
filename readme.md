# 🛰️ Flugstabilierungs- und Rettungssystem für RC Segelflugzeuge
### (Autonomous Stabilization, Return-to-Home & Thermic Assist for Gliders)

Dieses Open-Source-Projekt realisiert ein autonomes Sicherheits- und 
Assistenzsystem für RC-Segelflugzeuge, Motorsegler und Flächenmodelle. 
Es basiert auf der Anpassung der iNAV-Flugsteuerung (z. B. auf 
SpeedyBee F405 Wing oder Corewing Hardware-Boards).

Das System richtet sich gezielt an klassische Modellsegelflieger, die 
bisher keine Berührungspunkte mit Multirotor- oder Drohnentechnologien hatten.

---

## 📸 Mechanischer Aufbau & Ansichten

![CorewingFlugcontroller mit GPS Empfänger und usb / Beeper](Bilder/Controller.jpg)

Der Flugcontroller mit GPS Empfänger huckepack, Mini-Empfänger und USB-Modul/ Beeper,
Kabel zum Akku, das Kabel zum Regler fehlt noch.

---

## 🚨 Die realen Risiken beim Segelfliegen

Klassische Segelflugmodelle repräsentieren oft einen sehr hohen finanziellen 
und zeitlichen Wert. Im Flugbetrieb kommt es regelmäßig zu Stresssituationen:

* **Dauerhafter Sichtkontakt-Zwang:** Der Pilot ist ständig gezwungen, das 
  Modell zu beobachten. Ein kurzer Blick auf den Sender 
  oder das Entspannen der Nackenmuskulatur ist oftmals kritisch.
* **Raumlageverlust bei schlechter Sicht:** Dunst, starkes Gegenlicht, weite 
  Entfernungen oder das unbeabsichtigte Einfliegen in Wolkenfetzen führen 
  in Sekunden zum totalen Verlust der Fluglage-Erkennung.
* **Risiko des Wegfliegens:** Ohne Sichtkontakt fliegt das Modell unkontrolliert 
  weiter, was den totalen Verlust des wertvollen Modells bedeutet.
* **Gefährdung durch Absturz:** Verliert das Modell die Eigenstabilität oder 
  gerät in eine unklare Fluglage, kann es unkontrolliert abstürzen. Ein unkontrolliert 
  abstürzendes Modell stellt eine erhebliche physische Gefährdung für Personen, 
  Sachen und den Luftraum am Boden dar.

---

## 💡 Der Lösungsansatz: Die Flugsteuerung als Sicherheits-System

Durch den Einbau einer kompakten Wing-Flugsteuerung zwischen Empfänger und 
Servos wird das System zum unsichtbaren Co-Piloten und zur Lebensversicherung:

1. **Rettungsfunktion bei unklarer Fluglage:** Per Schalterdruck bringt die 
   Software den Segler im Bruchteil einer Sekunde vollautomatisch in eine 
   stabile, waagerechte Fluglage. Der Absturz wird verhindert, die Gefahr am 
   Boden abgewendet und der Pilot kann durchatmen.
2. **Coming Home Funktion (RTH / Rückkehr):** Bei akutem Sichtverlust oder 
   Funkausfall wendet der Segler selbstständig, fliegt zum Startplatz zurück 
   und kreist dort sicher auf einer festgelegten Höhe, bis der Pilot wieder 
   Sichtkontakt hat und manuell übernimmt. Ein Wegfliegen ist unmöglich.
3. **Thermikunterstützung (Kreis-Assistent):** Der FC hält über seine Sensorik 
   (Barometer/GPS) auf Wunsch eine exakte Schräglage und konstante Fahrt. Das 
   zentrierte Kreisen in Aufwinden wird dadurch massiv erleichtert.
4. **Allgemeine Wind-Stabilisierung:** Automatisches Ausgleichen von böigem 
   Wind und Turbulenzen sorgen für ein ruhiges Flugbild.
5. **Manueller Modus:** Manuelle Steuerung ohne Unterstützung
6. **Startunterstützung beim Wurf:** Der FC erkennt den Wurf und steuert das
   Modell auf eine stabile Flughöhe bis der Pilot übernimmt.
7. **Akustische Warnmeldungen:** Der FC erkennt technische Defeckte und
   nicht sichere Startparameter wie Unterspannung, fehlende GPS Synchronisation
   und meldet das über akustisches Beepen.
   
---

## 💻 Minimaler Aufwand durch vordefinierte Setups

Die manuelle Einarbeitung, Konfiguration und das anschließende Testfliegen von
iNAV auf Flächenmodellen ist zeitaufwendig und für viele Piloten abschreckend. 
Dieses Projekt nimmt Ihnen diese Arbeit weitestgehend ab.

Der geringe Aufwand in der Praxis entsteht durch fertige Einstellungs-Setups:

* **Vordefinierte Profile:** Sie laden ein praxiserprobtes Gesamt-Setup 
  (CLI-Dump) direkt auf Ihre Flugsteuerung. Die gesamte grundlegende 
  Mischer- und Stabilisierungslogik ist darin bereits fertig programmiert.
* **Geringe Restanpassung:** Sie müssen das Setup lediglich an drei Punkten 
  auf Ihr individuelles Modell anpassen:
  1. Das genutzte Senderprotokoll einstellen
     (CRSF, SBUS, IBUS, FPORT, SRXL2, DSM2, DSMX, GHST, MAVLINK, JETIEXBUS, SPEKTRUM1024, SPEKTRUM2048)
     (Team BlackSheep, ExpressLRS, FrSky, FlySky, Spektrum, Futaba, Graupner, ImmersionRC, Jeti, RadioMaster)
     
  3. Die Ruderlagen (Mitte) kontrollieren, damit die Klappen gerade stehen.
     
  5. Die maximalen Ruderausschläge und Richtung an Ihre Mechanik angleichen.

Die vollständige Anleitung zur grundlegenden Hardware-Verkabelung, dem Einbau 
des Empfängers und der iNAV-Erstinstallation finden Sie in dieser Anleitung:

➔ **[Hardware-Aufbau & iNAV-Installation (INSTALL_INAV.md)](/Installation/INSTALL_INAV.md)**

---

## 📖 Projekt-Dokumentation & Modell-Setups

Dieses Projekt ist modular aufgebaut, um den Einstieg so einfach wie möglich 
zu gestalten. Hier die verfügbaren Anleitungen:

**[Basis-Anleitung (Installation/INSTALL_INAV.md)](Installation/INSTALL_INAV.md)**  
   > Schritt-für-Schritt: iNAV auf den SpeedyBee flashen, Empfänger verkabeln 
   > und die Elektronik im Modell grundlegend aufbauen.

**[Multiplex Heron Komplettpaket (Multiplex_Heron/MULTIPLEX_HERON.md)](Multiplex_Heron/MULTIPLEX_HERON.md)**  
   > Fertiges Setup für den 2,4m Schaum-E-Segler. Enthält den iNAV-CLI-Dump 
   > und die passende EdgeTX `model16.yml`-Modelldatei direkt im Ordner.

**[ASW 27 Komplettpaket (ASW27_3M6/ASW27_3M6.md)](ASW27_3M6/ASW27_3M6.md)**  
   > Fertiges Setup für die 3,6m Segler-Klasse. Enthält den iNAV-CLI-Dump 
   > und die passende EdgeTX-Modelldatei direkt im Ordner.
   > In Bearbeitung

**[Multiplex Funcub Paket] ()**  
   > Fertiges Setup für die Funcub. Enthält den iNAV-CLI-Dump 
   > Stabilisiertes Schleppflugzeug für Kleinsegler mit Sicherheitsfunktionen.
   > In Bearbeitung

**[Flugtaktiken (Flugtaktik.md)](Flugtaktik.md)** 
   >Flugtaktiken in verschiedenen Situationen.
   >

**[Optionales iNAV Telemetrie-Widget (iNAV_Widget_TX16S/WIDGET.md)](https://github.com/iNavFlight/OpenTX-Telemetry-Widget)**  
   > Das offizielle Open-Source-Widget für das Farbdisplay Ihrer RadioMaster TX16S. 
   > Liefert den künstlichen Horizont, Höhen-Graphen und Sprachansagen live per Funk.
   > In Bearbeitung   

---

## 🔄 Segler, Fernbedienung, optionale Telemetrieanzeige mit Nackenstütze

![Gesamtsystem / Beeper](Bilder/Gesamtsystem.jpg)

Dieses Projekt entfaltet sein volles Potenzial in Kombination mit unserem 
zweiten Repository: Über die [Bluetooth Bridge](../Bluetooth_Bridge) werden die 
autonomen iNAV-Fluglagendaten und der Thermik-Status live per Funk an das 
hauseigene Teleview-Display an der Fernsteuerung oder an die offizielle 
[Telemetry Viewer App](https://google.com) übertragen.

---

## 📜 Lizenz

**MIT License** - Frei für alle Freunde von EdgeTX und des Segelflugs!
