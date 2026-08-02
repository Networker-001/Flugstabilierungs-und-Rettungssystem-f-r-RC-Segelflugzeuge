# Steckbrief INAV Multiplex Heron
====================================================================

1. DIE AERODYNAMISCHEN GRUNDLAGEN (Heron-Spezifisch)
--------------------------------------------------------------------
Die Heron ist aus Elapor (Schaum) gebaut und fliegt aufgrund des dickeren 
Profils und des höheren Widerstands spürbar langsamer als ein reinrassiger 
GFK-Segler.
- REISEGESCHWINDIGKEIT: Die Heron fühlt sich bei ca. 15 m/s am wohlsten. Zu 
  hohe Geschwindigkeiten im Autopiloten führen nur zu unnötigem Akkuverbrauch 
  und weichen, schwammigen Rudern.
- TURN ASSIST: Da die Heron ein ausgeprägtes negatives Wendemoment besitzt, 
  benötigt sie einen sauber arbeitenden Turn Assist, damit das Heck in 
  autonomen Kurven nicht durchhängt. Die Werte sind entsprechend hoch ge-
  wählt, da ein Strömungsabriss bei der Heron sehr gutmütig erfolgt.

2. MECHANISCHE GRUNDEINSTELLUNG (Ruderwege)
--------------------------------------------------------------------
- Querruder: Nach oben +15mm, nach unten -8mm (Wichtige Differenzierung!).
- Höhenruder: Nach oben und unten ca. 10-12mm.
- Seitenruder: Maximaler Ausschlag (ca. 20mm nach links und rechts).

3. STECKBRIEF MULTIPLEX HERON — INAV PARAMETER
====================================================================

| Parameter-Gruppe | iNAV-Variable und Wert | Funktion und Praxis-Bedeutung |
| :---             | :---                   | :---                          |
| **Geschwindigkeit**| `fw_reference_airspeed = 1500`| Basis-Fluggeschwindigkeit von 15 m/s (54 km/h). |
|                  | `nav_fw_cruise_speed = 1500`  | RTH-Reisegeschwindigkeit von 15 m/s (54 km/h). |
|                  | `nav_min_ground_speed = 0`    | Deaktiviert. Kein erzwungenes Gas bei Gegenwind. |
|                  | `nav_fw_pitch2thr = 10`       | Sanfte automatische Drosselzugabe beim Steigen. |
| **Kurvenflug**    | `turn_assist_yaw_gain = 1.000`| Maximales Mitsteuern des Seitenruders in Kurven. |
|                  | `fw_turn_assist_pitch_gain = 0.400`| Hält die Nase im autonomen Kreisflug stabil oben. |
|                  | `yaw_rate = 20`               | Ruhige, vorwählbare Gier-Drehrate (200 Grad/s). |
|                  | `nav_fw_loiter_radius = 5000` | Standard-Kreisradius für den Loiter beträgt 50m. |
| **Höhen & RTH**  | `nav_rth_altitude = 6000`     | Basis-Mindesthöhe für den Rückflug beträgt 60m. |
|                  | `nav_rth_alt_mode = AT_LEAST` | Nutzt aktuelle Höhe, wenn sie über 60 Metern liegt. |
|                  | `nav_rth_home_altitude = 6000`| Zielhöhe bei der Ankunft über dem Platz ist 60m. |
|                  | `nav_min_rth_distance = 500`  | RTH-Sperre im Nahbereich. Wird erst ab 5m aktiv. |
|                  | `nav_rth_climb_first = ON_FW_SPIRAL`| Steigt bei RTH unter 60m erst kreisend im Spiralflug.|
|                  | `nav_rth_allow_landing = NEVER`| Schützt das Modell vor einer autonomen Landung. |
|                  | `nav_rth_use_linear_descent = ON`| Gestreckter, flacher Höhenabbau auf dem Heimweg. |
| **Thermikflug**   | `nav_fw_soaring_motor_stop = ON`| Schaltet den Motor im autonomen Loiter komplett aus.|
|                  | `nav_rth_alt_control_override = ON`| Erlaubt Höhen-Übersteuerung per Tiefen/Höhenruder.|
| **Autostart**    | `nav_fw_launch_velocity = 200`| Motorfreigabe erfolgt erst ab 2 m/s Wurftempo. |
|                  | `nav_fw_launch_accel = 1500`  | Wurferkennung reagiert ab einem Impuls von 1,5G. |
|                  | `nav_fw_launch_thr_delay = 200`| Triebwerk startet verzögert 0,2 Sek. nach Abwurf. |
|                  | `nav_fw_launch_throttle = 1700`| Automatisches Startgas beträgt 70 Prozent Leistung.|
|                  | `nav_fw_launch_climb_altitude = 5000`| Automatische Launch-Abschaltung bei 50 Metern Höhe.|
|                  | `nav_fw_launch_climb_angle = 18`| Hält einen festen, sicheren Steigwinkel von 18°. |
| **Sicherheit**   | `failsafe_procedure = RTH`    | Rettung bei Funkabriss. Modell fliegt nach Hause. |
|                  | `vbat_cell_detect_voltage = 430`| Automatische LiPo-Zellenerkennung beim Anstecken. |
|                  | `vbat_min_cell_voltage = 350` | Akustischer Warnpiepser (Beeper) ab 3,5V pro Zelle.|
|                  | `vbat_crit_cell_voltage = 330`| Kritischer Daueralarm (Beeper) ab 3,3V pro Zelle.  |
| **Hardware**     | `gyro_main_lpf_hz = 25`       | Sanfter 25Hz-Filter dämpft Vibrations-Servo-Zappeln.|
|                  | `align_mag = CW270FLIP`       | Ausrichtungsvorgabe für den Kompass auf dem Board.|

---

4. ERKLÄRUNG DER GESCHWINDIGKEITSPARAMETER

- fw_reference_airspeed = 1500 (in cm/s): Erflogener Bezugswert für die Heron. 
  Bei schnellem Motorflug werden die Ausschläge gedämpft, im langsamen 
  Thermikflug leicht angehoben.
- nav_fw_cruise_speed = 1500 (in cm/s): Entspricht ca. 54 km/h. Das ist das 
  aerodynamische Wohlfühltempo der Heron, bei dem sie extrem effizient gleitet 
  und Strecke macht.
- nav_min_ground_speed = 0 (in cm/s): Vollständig deaktiviert. Der Segler darf 
  bei starkem Gegenwind in der Thermik ruhig auf der Stelle "einparken" oder 
  stehen bleiben, ohne dass iNAV fälschlicherweise den Motor zuschaltet.
- nav_fw_pitch2thr = 10: Bestimmt die sanfte automatische Drosselzugabe, wenn 
  der Autopilot die Nase im Steigflug anhebt.
