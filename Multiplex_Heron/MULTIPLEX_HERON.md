
# Modell-Setup: Multiplex Heron (2,4m E-Segler)

### Ansicht der Anschlüsse und Verkabelung:

<img src="Einbau.jpg" width="1000" alt="Einbau im Heron">

*Physischer Anschluss des FrSky-Empfängers, beeper Moduls und des GPS-Moduls am Flight Controller im eingebauten Zustand.*

## Die Besonderheiten und Flugfunktionen im Überblick

Für den Flugbetrieb wurden im iNAV-System folgende aerodynamische Schutzfunktionen 
und Automatismen konfiguriert:

* **Sicherheits-Priorität (Loiter & RTH):** Die Modi **NAV LOITER** (Kreisflug) 
  und **NAV RTH** (Heimkehr) auf **CH 7** haben absolute Priorität. Sie fangen 
  das Modell bei Raumlage- oder Sichtverlust auf Schalterdruck ab.

* **Erlaubtes Steigen:** Die Konfiguration erzwingt keine starre Flughöhe. 
  Findet der Heron im autonomen Kreisflug einen Aufwind, lässt das System es 
  zu, dass das Modell durch die reine Kraft der Thermik nach oben steigt.

* **Seitenruder-Mitnahme im Kreisflug:** Beim autonomen Kreisen (Loiter) steuert 
  das System das Seitenruder automatisch mit. Das verhindert ein Schieben des 
  Modells und unterstützt ein flaches Kreisen.

* **Schutz vor Strömungsabriss (Nase runternehmen):** Um ein Abkippen über die 
  Tragfläche (Stall) bei nachlassender Fahrt zu verhindern, nimmt die Software 
  automatisch die Nase leicht runter, um die Strömung aufrechtzuerhalten.

* **Manuelle Höhenanpassung im Automatikmodus (Tiefenruder):** Wenn das Modell 
  autonom fliegt (RTH oder Loiter), kann der Pilot über das Tiefenruder aktiv 
  eingreifen. Bei gedrücktem Tiefenruder sinkt das Flugzeug gezielt. Wird der 
  Knüppel losgelassen (Wegnehmen), stabilisiert sich der Heron sofort wieder 
  automatisch auf der aktuellen Höhe und das Sinken stoppt.

* **Manuelle Richtungskorrektur (Seitenruder):** Im autonomen Kreisflug reicht 
  ein einmaliger Ausschlag am Seitenruder aus, um die Kreisrichtung oder die 
  Lage des Kreises im Thermikbart anzupassen. Nach dem Loslassen kreist das 
  Modell autonom auf der korrigierten Flugbahn weiter.

* **Echter Manueller Modus (CH 6):** Im Modus `MANUAL` wird der Gyro komplett 
  deaktiviert. Die Fernsteuerung steuert die Servos direkt an – ohne jede 
  Zwischenregelung des FCs.

* **Automatisches Einmessen (Autotrimm):** Die aktivierte Funktion `FW_AUTOTRIM` 
  ermöglicht es, das Modell im stabilen Geradeausflug perfekt mechanisch 
  einzutrimmen. iNAV lernt die Mittenpositionen fliegend ein.

---
## Der Controller


<img src="Speedybeemini.jpg" width="1000" alt="OutBoxing">

---

## Praxis-Anleitung: Die Schalterbelegung im Flug

Die Steuerung im Alltag erfolgt über zwei Hauptschalter auf den Kanälen 7 und 15 
sowie einen Drehregler auf Kanal 9:

### 1. Der Rettungs- & Sicherheits-Schalter (CH 7)
* **Stellung Oben:** AUS (Manuelle Steuerung)
* **Stellung Mitte:** **NAV LOITER** ➔ Der Heron geht in den autonomen 
  Kreisflug über. Über den Drehregler (**CH 9**) kann der Kreisradius in der 
  Luft stufenlos verengt oder geweitet werden, um das Modell in die Thermik 
  einzuziehen.
* **Stellung Unten:** **NAV RTH** ➔ Der Segler fliegt vollautomatisch zum 
  Startplatz zurück und kreist dort.

### 2. Der 3-Stufen-Klappenschalter (CH 15)
Dieser Schalter steuert die Verwölbung der Tragfläche (Wölbklappen und 
Querruder) für die jeweilige Flugphase:
* **Stellung Oben (Thermik-Phase):** Leichte Negativ-Stellung aller Klappen 
  (Wölbklappen und Querruder fahren minimal nach oben).
* **Stellung Mitte (Normal-Phase):** Neutralstellung (Alle Klappen im Strak).
* **Stellung Unten (Lande-Phase / Butterfly):** Volle Bremsstellung. Die 
  Wölbklappen fahren nach unten, die Querruder nach oben. Die notwendige 
  Tiefenruder-Beimischung wird direkt über den Sender zugemischt.

---
## 3. Kanalbelegung & Schalterfunktionen (Fernsteuerung)

Die folgende Übersicht zeigt die Zuordnung der Kanäle, der physischen Geber 
an Ihrer RadioMaster TX16S und der zugehörigen iNAV-Flugfunktionen:

| Kanal   | Schalter / Geber  | Funktion im Flugbetrieb                            | Min Wert | Mitte |Max Wert |
| :---    | :---              | :---                                               | :---  | :---  |:---  |
| **CH 1**| Knüppel (Thr)     | Throttle (Gas / Motorregler)                       | -100%  | 0% |100 %|
| **CH 2**| Knüppel (Ail)     | Aileron (Querruder)                                | -120%  | 0% |120 %|
| **CH 3**| Knüppel (Ele)     | Elevator (Höhenruder)                              | -100%  | 0% |100 %|
| **CH 4**| Knüppel (Rud)     | Rudder (Seitenruder)                               | -100%  | 0% |100 %|
| **CH 5**| Schalter **SF**   | Aus / Arm (Motor scharf)                           | -100%  | 0% |100 %|
| **CH 6**| Schalter **SB**   | Manual / Stabilisiert (Acro)/ Soaring Unterstützung    | -100%  | 0% |100 %|
| **CH 7**| Schalter **SD**   | Aus / Nav Loiter (Kreis) / Nav RTH (Heimkehr)      | -100%  | 0% |100 %|
| **CH 8**| Schalter **SC**   | Aus / Nav Cruise + Nav Althold (Streckenflug)      | -100%  | 0% |100 %|
| **CH 9**| Drehregler **LS** | Loiter Radius (Live-Regler für Kreisflug)          | -100%  | 0% |100 %|
| **CH 11**| Schalter **SG**| Klappen Modus                                  | 0%  | 40% | 80 %|
| **CH 13**| Schalter **SD**  | Aus / Auto Level Trim (Automatisches Eintrimmen)   | -100%  | 0% | 100 %|
| **CH 15**| Schalter **SG**  | Klappen Ausschlag                                      | 8%  | 0% | 80 %|

---

## 4. Anschluss von Empfänger, GPS und Telemetrie

Die Funk- und Navigationskomponenten werden wie folgt am SpeedyBee F405 Wing 
verkabelt und betrieben:

* **FrSky-Empfänger (Steuersignal):** 
  Der Empfänger wird direkt am ersten Kontakt der Stiftleiste angeschlossen. 
  Das digitale Steuersignal läuft im iNAV-System starr über den **UART 2** 
  (aktiviertes `Serial RX`).
* **GPS-Modul:**
  Das GPS-Modul für die Standortdaten ist an den Anschlüssen von **UART 3** 
  (Spalte *Sensors* ➔ *GPS*) zugewiesen.
* **Telemetrie-Rückkanal (Tele Out):**
  Die Rückübertragung der Flugdaten zum Sender (SmartPort) ist physisch an 
  **Port 4 (seitlicher Stecker)** angeschlossen. Softwareseitig läuft diese 
  Übertragung über den emulierten Port **`SOFTSERIAL1`** (Spalte *Telemetry* 
  ➔ *SmartPort*).

---

## 5. Physische Belegung der Ausgänge (Stiftleisten)

Verkabeln Sie die Komponenten Ihres Multiplex Heron exakt nach diesem Schema an 
den Stiftleisten des SpeedyBee F405 Wing:

* **`Stiftleiste 1`:** Anschluss für den FrSky-Empfänger (Signal, Strom, Masse)
* **`Stiftleiste 2`:** Hauptmotor / Regler (ESC) ➔ (Gaskanal)
* **`Stiftleiste 3`:** Wölbklappe ➔ `smix 1` / `smix 6` / `smix 7`
* **`Stiftleiste 4`:** Höhenruder ➔ `smix 2` (Höhenkanal)
* **`Stiftleiste 5`:** Seitenruder ➔ `smix 0` / `smix 3` (Seitenkanal)
* **`Stiftleiste 6`:** Wölbklappe ➔ `smix 4` / `smix 5`
* **`Stiftleiste 7`:** Querruder Links ➔ (Standard iNAV-Flächenmischer)
* **`Stiftleiste 8`:** Querruder Rechts ➔ (Standard iNAV-Flächenmischer)

## Einbaurichtungen

* **Speedybee Wing Mini**
  Stiftleisten in Flugrichtung nach hinten
  Beschriftung SpeedyBee oben

* **GPS Empfänger**
  Steckbuchse in Flugrichtung hinten
  Schrift nach unten

---

### Ansicht des Senders mit INAV Widget:

<img src="TX16s.jpg" width="500" alt="RadioMaster TX16s">

## Natürlich können auch andere Sender und Protokolle verwendet werden. ##

---

## 6. Einspielen der EdgeTX-Senderkonfiguration (`model16.yml`)

Im Ordner dieses Modells befindet sich die fertige Modelldatei **`model16.yml`** 
für Ihre RadioMaster TX16S. Diese Datei enthält bereits die gesamte Schalter- 
und Mixerbelegung für die Kanäle 1 bis 15.

### Schritt-für-Schritt-Anleitung zum Kopieren:

1. **Verbinden:** Verbinden Sie Ihre RadioMaster TX16S per USB-Kabel mit dem PC 
   und wählen Sie im Sender-Display den Modus **"USB-Massenspeicher"**.
2. **Ordner öffnen:** Öffnen Sie das Laufwerk der SD-Karte auf Ihrem Computer 
   und navigieren Sie direkt in das Verzeichnis: ➔ **`/MODELS/`**
3. **Schauen ob frei:** Kontrollieren Sie in diesem Ordner, ob 
   dort bereits eine Datei mit dem Namen **`model16.yml`** existiert.
4. **Wenn nicht frei, ändern:** Sollte `model16.yml` bereits vorhanden sein, 
   müssen Sie die neue Datei auf Ihrem PC vor dem Kopieren zwingend umbenennen. 
   Wählen Sie die nächste freie, höhere Nummer (z. B. **`model17.yml`**, 
   **`model18.yml`** usw.), um kein bestehendes Modell zu überschreiben.
5. **Kopieren:** Kopieren Sie die (ggf. umbenannte) Datei auf die SD-Karte.
6. **Trennen:** Trennen Sie die USB-Verbindung sicher. Das Modell steht nun 
   in Ihrer Modellauswahl auf dem gewählten Platz bereit.

## 7. Einkaufsliste & Benötigte Hardware

Für den Aufbau dieses Sicherheits- und Assistenzsystems wurden folgende 
Hardware-Komponenten erfolgreich in der Praxis getestet und freigegeben:

| Komponente     | Empfohlenes Modell       | Link (Google-Suche)                                                                   |
| :---           | :---                     | :---                                                                                  |
| **Controller** | SpeedyBee F405 Wing Mini | [SpeedyBee F405 Wing Mini](https://google.com?q=SpeedyBee+F405+Wing+Mini)  |
| **Alternativ** | Corewing Mini            | [Corewing Mini FC](https://google.com?q=corewing+Mini)   |
| **Navigation** | BZGNSS BZ-251 GPS        | [BZGNSS BZ-251 GPS](https://google.com?q=BZGNSS+BZ-251)                 |
| **Empfänger**  | FrSky Archer RS Receiver | [FrSky Archer RS Receiver](https://google.com?q=FrSky+Archer+RS+Receiver)  |
   

## Inhalt dieses Ordners

1. **`heron_inav_cli.txt`:** Der fertige iNAV-CLI-Dump mit allen oben genannten 
   aerodynamischen Filtern, Logikschaltern und Mischern.
2. **`heron_edge_tx.yml`:** Die fertige Modelldatei für Ihre RadioMaster TX16S 
   inklusive vorkonfigurierter Schalterbelegung für alle Flugphasen.
