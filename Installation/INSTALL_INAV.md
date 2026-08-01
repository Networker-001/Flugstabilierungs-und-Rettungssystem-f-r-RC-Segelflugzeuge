# 🛰️ Basis-Anleitung: Hardware-Aufbau & iNAV-Konfiguration

Diese Anleitung beschreibt den mechanischen Zusammenbau des SpeedyBee F405 Wing 
Flight Controllers, den Empfänger-Anschluss sowie das Einlesen des fertigen 
Einstellungs-Setups über die Software.


<img src="SppedybeePorts.jpg" width="600" alt="Anschlüsse">
---

## 🔧 1. Mechanischer Aufbau des Flight Controllers

Der SpeedyBee F405 Wing wird als Platinen-Sandwich geliefert und muss vor dem 
Einbau im Rumpf mechanisch vorbereitet werden:

* **Stiftleisten einlöten:** Die beiliegenden Servo-Stiftleisten (Pins) müssen 
  sauber und absolut gerade auf den vorgesehenen Pads verlötet werden. Dies ist 
  wichtig, damit die Servostecker später mechanisch blockierungsfrei sitzen.
* **Verschrauben des Sandwichs:** Das Board besteht aus der Hauptplatine und 
  dem darauf aufgesteckten USB-/Wireless-Board. Verschrauben Sie die Platinen 
  vibrationssicher mit den beiliegenden Kunststoff-Abstandshaltern.
* **Einbaulage im Modell:** Platzieren Sie den Controller absolut gerade 
  (parallel zur Längs- und Querachse des Seglers) im Rumpf. Fixieren Sie ihn 
  fest über Verschraubungen oder mit dickem, vibrationsdämpfendem Klebeband.

---

## 🔌 2. Universelle Stromversorgung & BEC

Das integrierte BEC des Controllers übernimmt die Stromversorgung aller 
Komponenten direkt über den Flugakku:

* **Hauptakku-Anschluss:** Die Zuleitung vom Flugakku (oder die dicken Kabel 
  des Motorreglers/ESC) wird direkt an die massiven Lötpads **`BAT+`** und 
  **`GND`** des Boards gelötet.
* **Servo-Spannung (Jumper):** Wählen Sie über die physische Steckbrücke 
  (Jumper) auf der Platine die passende Spannung für Ihre Ruderservos. 
  Standardmäßig sind dies 5 Volt (für klassische Servos) oder optional 
  6V/7.4V (falls moderne HV-Servos im Segler verbaut sind).

---

## 📻 3. Anschluss des FrSky-Empfängers

Die Verbindung zwischen dem FrSky-Empfänger und dem SpeedyBee erfolgt über 
zwei getrennte Signalwege (Steuerung und Telemetrie-Ausgang):

1. **Der Steuerkanal-Anschluss (Stiftleiste):**
   Der Empfänger wird direkt an den ersten drei Kontakten der werkseitigen 
   Empfänger-Stiftleiste des Controllers angesteckt. Diese Kontakte liefern 
   die Stromversorgung und das Steuersignal:
   * **`+` (5V)**  ➔ Stromversorgung für den Empfänger
   * **`-` (GND)** ➔ Gemeinsame Masse
   * **`S` (Signal)** ➔ SBUS- / CPPM-Steuersignal des Empfängers
2. **Der Telemetrie-Rückkanal (UART 4):**
   Für die Übertragung der Flugdaten zurück zum Sender wird das SmartPort-Signal 
   (S.Port) des Empfängers fest mit dem seriellen Port 4 des FCs verbunden:
   * **`S.Port-Pin`** des Empfängers ➔ Verbunden mit Pad **`TX4`** (UART 4)

---

## 💻 4. iNAV-Software einrichten & Profil laden

Nachdem die Hardware verbaut ist, wird das fertige Modell-Setup eingelesen. 
Dazu nutzen Sie das PC-Programm "iNAV Configurator".

### 1. Software starten und verbinden:
1. Laden Sie den **iNAV Configurator** für Windows/Mac herunter und starten 
   Sie das Programm.
2. Verbinden Sie den SpeedyBee Flight Controller per USB-Kabel mit Ihrem PC.
3. Wählen Sie oben rechts den passenden COM-Port aus und klicken Sie auf 
   den grünen Button **`Connect`** (Verbinden).
4. **Wichtig bei der Erstverbindung:** Da der Controller neu ist, öffnet sich 
   ein Willkommens-Fenster (Wizard), das nach Modelltyp, Kompass und Sensoren 
   fragt. **Schließen oder überspringen Sie diesen Assistenten einfach!** 
   Wir konfigurieren nichts manuell, da das fertige Profil im nächsten Schritt 
   all diese Einstellungen vollautomatisch einstellt.


### 2. Das fertige Profil einlesen (CLI):
Um die gesamte Mischer- und Stabilisierungslogik fehlerfrei aufzuspielen, 
wird die Einstellungs-Datei (CLI-Dump) aus dem jeweiligen Modellordner geladen:
1. Öffnen Sie im linken Menü den untersten Reiter **`CLI`** (Befehlszeile).
2. Klicken Sie unten auf den Button **`Load from file`** (Aus Datei laden).
3. Wählen Sie die heruntergeladene Textdatei Ihres Modells aus (z. B. aus dem 
   Ordner `Multiplex_Heron`).
4. Die Befehle werden automatisch in das Textfenster geladen. Klicken Sie 
   anschließend auf den Button **`Execute`** (Ausführen) oder tippen Sie 
   unten das Wort **`save`** ein und drücken Sie die Eingabetaste (Enter).
5. Der Flight Controller brennt die Konfiguration in den Flash-Speicher und 
   startet automatisch neu. Das Modell ist nun grundlegend eingerichtet.

### 3. Senderprotokoll & Empfänger-Typ kontrollieren:

Das geladene Profil ist werkseitig bereits steckerfertig für Ihren FrSky-
Empfänger vordefiniert. Kontrollieren Sie im linken Menü unter **`Receiver`**, 
ob der Typ auf **`Serial`** und der Provider starr auf **`SBUS`** stehen. 

Sollten Sie ein anderes Funksystem nutzen, suchen Sie Ihr Protokoll in der 
folgenden Tabelle und stellen Sie den zugehörigen Anschluss/UART manuell ein:

| Ihr Funksystem / Protokoll | Physischer Steuer-Anschluss | Telemetrie-Rückkanal (Tele Out)      | iNAV Ports-Menü |
| :---                       | :---                        | :---                                 | :---            |
| **SBUS** (FrSky / Futaba)  | Großer SBUS-Pin (Leiste 1)  | **Seitlicher Stecker (Port 4)**       | **UART 2** (Steuerung) / **SOFTSERIAL 1** (Tele Out) |
| **CRSF / ELRS** (ELRS / TBS)| Separater 4-Pin-Stecker     | *Automatisch integriert (Kein Kabel)* | **UART 1** (Kombiniert) |
| **IBUS** (FlySky)          | Separater 4-Pin-Stecker     | *Automatisch integriert (Kein Kabel)* | **UART 1** (Kombiniert) |
| **SUMD** (Graupner HoTT)   | Separater 4-Pin-Stecker     | *Automatisch integriert (Kein Kabel)* | **UART 1** (Kombiniert) |
| **SRXL2** (Spektrum)       | Separater 4-Pin-Stecker     | *Automatisch integriert (Kein Kabel)* | **UART 1** (Kombiniert) |
| **FPORT** (FrSky optional) | Separater 4-Pin-Stecker     | *Automatisch integriert (Kein Kabel)* | **UART 1** (Kombiniert) |

*Hinweis zur manuellen Konfiguration:* Schalten Sie im Menü **`Ports`** den 
ermittelten UART in der Spalte *Serial RX* aktiv. Wählen Sie danach im Menü 
**`Receiver`** den Typ *Serial* und Ihr passendes Protokoll aus.

Schalten Sie Ihre Fernsteuerung ein. Die farbigen Balken im Menü `Receiver` 
müssen nun synchron reagieren. Falls Sie Änderungen vornehmen mussten, klicken 
Sie unten rechts starr auf **`Save and Reboot`**.

### 4. Servomitten und Ausschläge einmessen (Outputs):

Nach dem Neustart müssen die mechanischen Mittenpositionen und die maximalen 
Ruderwege der Servos kontrolliert und exakt auf Ihr Modell angepasst werden:

1. Navigieren Sie im iNAV Configurator in das linke Menü auf den Reiter 
   **`Outputs`** (Ausgänge).

2. Schalten Sie den Sicherheits-Schalter **`Enable motor and servo outputs`** 
   oben rechts aktiv, um Strom auf die Servos zu geben.

3. **Servomitten einstellen (Mid):** Bringen Sie die Ruderflächen am Modell 
   mechanisch so weit wie möglich in den Strak (Neutralstellung). Korrigieren 
   Sie kleine Abweichungen im iNAV-Menü, indem Sie den Wert für die 
   Mittenposition (Standard **`1500`** µs) in der Spalte **`Mid`** beim 
   jeweiligen Servo anheben oder absenken. Das Servo reagiert dabei sofort 
   live auf jede Werteänderung.

4. **Endpunkte begrenzen (Min / Max):** Bewegen Sie die Steuerknüppel an der 
   Fernsteuerung auf Vollausschlag. Reduzieren Sie die Standardwerte in den 
   Spalten **`Min`** (Standard `1000`) und **`Max`** (Standard `2000`) so weit, 
   dass die Ruder mechanisch nicht auf Anschlag laufen, die Scharniere nicht 
   überlastet werden und der Ausschlag symmetrisch ist.

5. **Speichern:** Klicken Sie unten rechts zwingend auf den roten Button 
   **`Save`**. Erst durch diesen Klick werden die geänderten Werte dauerhaft 
   auf dem Flight Controller gesichert.
