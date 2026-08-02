Steckbriefe für verschiedene Modellkathegorien
====================================================================

Wenn Sie ein anderes Modell als den Heron oder die ASW 27 mit diesem iNAV-
System ausrüsten möchten, müssen Sie die Konfiguration an die spezifische 
Aerodynamik und das Gewicht Ihres Modells anpassen. 

Kategorie 1: Leichte Schaumsegler und Einsteiger-Modelle
--------------------------------------------------------------------
* **Beispiel-Modelle:** Multiplex EasyGlider, Graupner Elektro Junior, 
  Volantex Ranger, FMS Easy Trainer, Multiplex Heron.
* **Flugcharakteristik:** Hoher Eigenwiderstand, dickes Profil, fliegt langsam, 
  reagiert sehr gutmütig auf Strömungsabrisse.

Kategorie 2: Mittlere GFK/CFK-Leistungssegler (bis 4m Spannweite)
--------------------------------------------------------------------
* **Beispiel-Modelle:** ASW 15/19/24/28 (Standardklasse), Alpina 4000, 
  F3B/F3J/F5J Wettbewerbsmaschinen, Schalenbau-Modelle, ASW 27 (GFK).
* **Flugcharakteristik:** Aerodynamisch, geringer Widerstand, läuft im 
  Gleitflug sehr weit, ausgeprägtes negatives Wendemoment durch lange, schlanke 
  Tragflächen.

Kategorie 3: Schwere GFK/CFK-Großsegler (ab 5m Spannweite & Scale)
--------------------------------------------------------------------
* **Beispiel-Modelle:** Alpina 5000, ASH 26, ASW 28 (Großmaßstab), 
  Großsegler der 5-Meter-Klasse mit hoher Eigenmasse.
* **Flugcharakteristik:** Hohe Trägheit um alle Achsen, immense Masse (6-9 kg), 
  hohe Flächenbelastung. Benötigt zwingend weite Kreisbahnen und eine höhere 
  Grundgeschwindigkeit, um Strömungsabrisse in Wenden sicher zu verhindern.

Kategorie 4: Schnelle Hangsegler und Hotliner
--------------------------------------------------------------------
* **Beispiel-Modelle:** Multiplex Blizzard, Simprop Lift Off, F3K/F3RES 
  (Sonderfall sehr leicht aber schnell), reinrassige Hangflitzer.
* **Flugcharakteristik:** Extrem agil, sehr hohe Grundgeschwindigkeit, muss 
  aktiv auf Fahrt gehalten werden, engere Wenderadien.

---


INAV-SCHLÜSSELPARAMETER 
--------------------------------------------------------------------

| Gruppe | iNAV-Variable | Funktion und Praxis-Bedeutung |
| :--- | :--- | :--- |
| **Speed** | `fw_reference_airspeed` | Aerodynamischer Bezugswert (in cm/s). Dämpft Ruder im Schnellflug, hebt sie im Langsamflug an. |
| | `nav_fw_cruise_speed` | Standard-Fluggeschwindigkeit (in cm/s) für RTH-Streckenflug und Geradeausflug. |
| `nav_min_ground_speed` | Zwingt Motor bei starkem Gegenwind zu (in cm/s). Bei Schaumseglern '0' für freies Einparken. Bei GFK-Großseglern auf Sicherheitsfahrt (13-14 m/s), um Strömungsabrisse und Ruderlosigkeit in autonomen Wenden absolut zu verhindern oder den Parameter . |
| | `nav_fw_pitch2thr` | Prozentuale automatische Drosselzugabe, wenn der Autopilot die Nase zum Steigen anhebt. |
| **Kurve** | `turn_assist_yaw_gain` | Regelt das Mitsteuern des Seitenruders. Wichtig gegen das negative Wendemoment langer Flächen. |
| | `fw_turn_assist_p_gain`| Gleicht Sinken im Kreisflug aus. Hält die Nase in autonomen Kurven starr horizontal auf Höhe. |
| | `yaw_rate` | Maximale Gier-Drehrate im autonomen Flug. Niedrige Werte erzwingen weiche Wenden. |
| | `nav_fw_loiter_radius` | Standard-Radius (in cm) für den Loiter. Im Flug per Regler live anpassbar. |
| | `nav_fw_bank_angle` | Begrenzt den maximalen Querneigungswinkel (Schräglage) in autonomen Phasen. |
| **RTH** | `nav_rth_altitude` | Vordefinierte Basis-Mindesthöhe (in cm) für den Rückflug zum Startplatz. |
| | `nav_rth_alt_mode` | Rechenlogik. Bei 'AT_LEAST' wird eine große Höhe (z. B. 465m) starr beibehalten. |
| | `nav_rth_home_altitude`| Zielhöhe (in cm), auf der das Modell bei Ankunft über dem Startplatz einrasten soll. |
| | `nav_min_rth_distance` | Mindestabstand (in cm). Blockiert RTH im Nahbereich gegen hektische Wenden über dem Kopf. |
| | `nav_rth_climb_first` | Bei 'ON_FW_SPIRAL' steigt das Modell erst kreisend auf, anstatt geradeaus in Hindernisse zu fliegen. |
| | `nav_rth_allow_landing`| Steuert Landeautomatik. Steht starr auf 'NEVER' für unendliche Warteschleifen über dem Piloten. |
| | `nav_rth_use_linear_desc`| Aktiviert den gestreckten, sehr flachen und materialschonenden Höhenabbau über die RTH-Strecke. |
| **Thermik**| `nav_fw_soaring_mot_stop`| Schaltet den Motor im Loiter hart aus, sobald das Soaring-Feature im Aufwind greift. |
| | `nav_rth_alt_control_ovr`| Erlaubt dem Piloten das bewusste manuelle Sinkenlassen des Seglers im RTH per Höhenruder. |
| **Launch**| `nav_fw_launch_velocity`| Mindest-Abwurfgeschwindigkeit (in cm/s), die beim Handstart erreicht sein muss vor Motorfreigabe. |
| | `nav_fw_launch_accel` | Benötigter Beschleunigungsimpuls in G-Kräften (1500 = 1,5G) beim Wurf zur Launch-Aktivierung. |
| | `nav_fw_launch_thr_delay`| Verzögerung (in ms). Motor startet erst, wenn die Hand sicher aus dem Propellerkreis raus ist. |
| | `nav_fw_launch_throttle` | Motorleistung im automatischen Steigflug (1700 = 70% Gas, 2000 = 100% Vollgas). |
| | `nav_fw_launch_climb_alt`| Start-Sicherheitshöhe (in cm). Bei Erreichen schaltet sich der Launch-Assistent vollautomatisch ab. |
| | `nav_fw_launch_climb_ang`| Fester, stabilisierter Steigwinkel in Grad, den der Autopilot unmittelbar nach dem Handstart einnimmt. |
| **Sicher**| `failsafe_procedure` | Notfall-Aktion bei totalem Funkabriss. Steht starr auf 'RTH' für autonome Heimkehr zum Piloten. |
| | `vbat_cell_detect_volt`| Spannungsschwelle (in mV) zur automatischen Erkennung der LiPo-Zellenzahl beim Anstecken (starr 430). |
| | `vbat_min_cell_voltage` | Löst die akustische Low-Battery-Warnung über den Beeper aus (350 = 3,50V pro Zelle). |
| | `vbat_crit_cell_voltage` | Löst den kritischen Daueralarm über den Beeper aus (330 = 3,30V pro Zelle). |
| **Board** | `gyro_main_lpf_hz` | Tiefpass-Filter für den Gyro. Niedrige Werte (25 Hz) schonen Servogetriebe vor Mikrovibrationen. |
| | `align_mag` | Softwareseitige Ausrichtung des Magnetkompasses auf dem Board für fehlerfreie RTH-Berechnungen. |

---

VERGLEICHSTABELLE DER INAV-PARAMETER
====================================================================

| Gruppe | iNAV-Variable / Funktion | Kat. 1: Heron (Schaum) | Kat. 2: ASW 27 (GFK) | Kat. 3: Großsegler (5m) | Kat. 4: Hotliner / Hang |
| :---   | :---                     | :---                   | :---                 | :---                    | :---                    |
| **Speed**| `fw_reference_airspeed`  | 1500 (15 m/s)          | 1600 (16 m/s)        | 1900 (19 m/s)           | 2000 (20 m/s)           |
|        | `nav_fw_cruise_speed`    | 1500 (15 m/s)          | 1600 (16 m/s)        | 1900 (19 m/s)           | 2000 (20 m/s)           |
|        | **`nav_min_ground_speed`**| **0 (Deaktiviert)**    | **1300 (13 m/s)**    | **1400 (14 m/s)**       | **0 (Deaktiviert)**     |
|        | `nav_fw_pitch2thr`       | 10                     | 4                    | 4                       | 3                       |
| **Kurve**| **`turn_assist_yaw_gain`**| **1.000 (Maximum)**    | **0.600**            | **0.750 (Langes Heck)** | **0.400**               |
|        | **`fw_turn_assist_p_gain`**| **0.400**              | **0.400**            | **0.400**               | **0.450**               |
|        | `yaw_rate`               | 20                     | 3                    | 2 (Extrem weich)        | 5                       |
|        | `nav_fw_loiter_radius`   | 5000 (50 Meter)        | 4800 (48 Meter)      | 6500 (65 Meter Radius)  | 4200 (42 Meter)         |
|        | `nav_fw_bank_angle`      | 30 Grad                | 30 Grad              | 25 Grad (Flache Wenden) | 38 Grad                 |
| **RTH** | `nav_rth_altitude`       | 6000 (60 Meter)        | 6000 (60 Meter)      | 6000 (60 Meter)         | 6000 (60 Meter)         |
|        | `nav_rth_alt_mode`       | AT_LEAST               | AT_LEAST             | AT_LEAST                | AT_LEAST                |
|        | `nav_rth_home_altitude`  | 6000 (60 Meter)        | 6000 (60 Meter)      | 6000 (60 Meter)         | 6000 (60 Meter)         |
|        | `nav_min_rth_distance`   | 500 (5 Meter)          | 500 (5 Meter)        | 500 (5 Meter)           | 500 (5 Meter)           |
|        | `nav_rth_climb_first`    | ON_FW_SPIRAL           | ON_FW_SPIRAL         | ON_FW_SPIRAL            | ON_FW_SPIRAL            |
|        | `nav_rth_allow_landing`  | NEVER                  | NEVER                | NEVER                   | NEVER                   |
|        | `nav_rth_use_linear_desc`| ON                     | ON                   | ON                      | ON                      |
| **Thermik**| `nav_fw_soaring_mot_stop`| ON                   | ON                   | ON                      | ON                      |
|        | `nav_rth_alt_control_ovr`| ON                     | ON                   | ON                      | ON                      |
| **Launch**| `nav_fw_launch_velocity` | 200 (2 m/s)            | 200 (2 m/s)          | 200 (2 m/s)             | 200 (2 m/s)             |
|        | `nav_fw_launch_accel`     | 1500 (1,5G)            | 1500 (1,5G)          | 1500 (1,5G)             | 1500 (1,5G)             |
|        | `nav_fw_launch_thr_delay` | 200 (0,2 Sek.)         | 200 (0,2 Sek.)       | 200 (0,2 Sek.)          | 200 (0,2 Sek.)          |
|        | `nav_fw_launch_throttle`  | 1700 (70% Gas)         | 2000 (100% Gas)      | 2000 (100% Vollgas)     | 2000 (100% Gas)         |
|        | `nav_fw_launch_climb_alt` | 5000 (50 Meter)        | 5000 (50 Meter)      | 5000 (50 Meter)         | 5000 (50 Meter)         |
|        | `nav_fw_launch_climb_ang` | 18 Grad                | 18 Grad              | 15 Grad (Flacher Steig) | 22 Grad                 |
| **Sicher**| **`failsafe_procedure`**  | **RTH**                | **RTH**              | **RTH**                 | **RTH**                 |
|        | **`vbat_cell_detect_volt`**| **430**                | **430**              | **430**                 | **430**                 |
|        | `vbat_min_cell_voltage`   | 350                    | 350                  | 350                     | 350                     |
|        | `vbat_crit_cell_voltage`  | 330                    | 330                  | 330                     | 330                     |
| **Board** | `gyro_main_lpf_hz`       | 25 Hz                  | 25 Hz                | 25 Hz                   | 30 Hz (Direktes An-     |
|        |                          |                        |                      |                         | sprechen der Ruder)     |
|        | `align_mag`               | CW270FLIP              | CW90FLIP             | CW90FLIP                | *Je nach Einbau*        |




