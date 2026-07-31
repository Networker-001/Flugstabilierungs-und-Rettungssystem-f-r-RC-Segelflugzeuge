# 🛰️ Basis-Anleitung: Hardware-Aufbau & iNAV-Konfiguration

Diese Anleitung beschreibt den mechanischen Zusammenbau des SpeedyBee F405 Wing 
Flight Controllers, den Empfänger-Anschluss sowie das Einlesen des fertigen 
Einstellungs-Setups über die Software.

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
