# BMA Testprotokoll-Vorlage: Performance-Messungen auf dem Ayn Thor

**Projekt:** Berufsmaturitätsarbeit (BMA) – *Emulation mit Ayn Thor*  
**Autoren:** David Martin Felicio Reichlin, Gabriel Di Giuseppe  
**Messwerkzeuge:** **Shizuku** (erweiterte ADB-Berechtigungen) + **Scene 5** (Hardware-Monitoring & Frame-Recording)

---

## 1. Setup & Vorbereitung auf dem Ayn Thor

### 1.1 Shizuku & Scene 5 initialisieren
1. **Entwickleroptionen aktivieren:** Android-Einstellungen $\rightarrow$ *Über das Tablet* $\rightarrow$ 7-mal auf *Build-Nummer* tippen.
2. **Wireless Debugging / USB-Debugging:** In den *Entwickleroptionen* aktivieren.
3. **Shizuku starten:** Shizuku-App öffnen $\rightarrow$ Starten via Wireless Debugging (oder via PC-Terminal `adb shell sh /sdcard/Android/data/moe.shizuku.privileged.api/start.sh`).
4. **Scene 5 Berechtigung:** Scene 5 öffnen $\rightarrow$ Betriebsmodus auf **Shizuku-Modus** stellen $\rightarrow$ Berechtigung im Dialog dauerhaft gewähren.

### 1.2 Scene 5 On-Screen-Display (OSD) & Recording konfigurieren
In Scene 5 unter **Monitor / Floating Window** folgende Telemetriewerte aktivieren:
- **FPS & Frametimes:** Echtzeit-FPS, $\varnothing$ FPS, 1% Low FPS, Frametime (ms), Jank / Stutter Count
- **CPU:** Gesamtauslastung (%), Frequenz Cluster Little (Cortex-A510), Frequenz Cluster Mid (Cortex-A715/A710), Frequenz Prime-Core X3 (GHz)
- **GPU:** Adreno 740 Auslastung (%), GPU-Taktfrequenz (MHz)
- **Power & Akku:** Momentane Leistungsaufnahme in Watt / mW ($P$), Entladestrom in mA ($I$), Batteriespannung in mV ($U$)
- **Thermik:** SoC-Temperatur (°C), Akkutemperatur (°C)
- **RAM:** Verwendeter Arbeitsspeicher (GB / MB)

> **Tipp (CSV-Export):** In Scene 5 unter *Record* vor Spielbeginn auf **Start Recording** tippen. Nach 10 Minuten Spielzeit auf **Stop** tippen. Die exportierte CSV-Datei enthält sekundengenaue Messreihen und kann direkt als Rohdaten für Diagramme verwendet werden!

### 1.3 Standardisierte Versuchsbedingungen (Konstanten)
Um wissenschaftlich valide und vergleichbare Daten zu erheben, müssen folgende Bedingungen bei jedem Test exakt eingehalten werden:

| Parameter | Standardwert | Dokumentierter Wert |
| :--- | :--- | :--- |
| **Akkustand zu Beginn** | Mindestens 80\,\% bis 100\,\% | `____ %` |
| **Ladekabel** | **Nicht angeschlossen** (verhindert Ladeerwärmung & verfälschte Watt-Werte) | Nicht angeschlossen |
| **Display-Helligkeit** | Fixiert auf 50\,\% (automatische Helligkeit AUS) | `50 %` |
| **Netzwerk** | Flugmodus aktiviert (keine Hintergrund-Syncs) | Flugmodus AN |
| **Audio** | Lautstärke 50\,\% über interne Lautsprecher | `50 %` |
| **Lüfterprofil (Ayn Fan)**| Fixiert (z.\,B. *Smart / Standard* oder *Sport*) | `________________` |
| **Performance-Modus** | Ayn Performance-Governor (z.\,B. *Standard* oder *High*) | `________________` |
| **Raumtemperatur** | Ca. 20--22\,°C | `____ °C` |
| **Testdauer pro Run** | 10 Minuten aktive Spielsequenz (nach 2 Min. Warmup) | 10 Min. |
| **Messwiederholungen** | 3 Durchläufe pro Testfall (Mittelwert bilden) | 3 Durchläufe |

---

## 2. Detailliertes Messprotokoll (Einzeltest-Bogen)

*(Diesen Bogen für jeden einzelnen Testdurchlauf ausfüllen oder duplizieren)*

### Stammdaten des Testfalls
- **Test-ID:** `TEST-___` (z.\,B. `TEST-PS2-GT4-01`)
- **Datum & Uhrzeit:** `____.__.2026, __:__ Uhr`
- **Tester / Protokollant:** `[ ] David   [ ] Gabriel`
- **Plattform / Zielkonsole:** `[ ] Atari 2600   [ ] Nintendo DS   [ ] PlayStation 2   [ ] Nintendo Switch   [ ] CHIP-8`
- **Spiel / Referenztitel:** `________________________________________`
- **Gespielte Spielszene / Benchmark-Strecke:** `________________________________________`

### Emulator- & Grafik-Konfiguration
- **Emulator & Version:** `________________________________________` (z.\,B. *NetherSX2 v1.9-4248*, *Sudachi v1.0.8*)
- **Grafik-Backend:** `[ ] Vulkan   [ ] OpenGL`
- **GPU-Treiber:** `[ ] Qualcomm System-Adreno   [ ] Mesa Turnip Driver (Version: __________)`
- **Interne Render-Auflösung:** `[ ] 1x Native   [ ] 2x Native   [ ] 3x Native   [ ] Andere: ______`
- **Frame-Skip / Hacks:** `[ ] Aus   [ ] Ein (Wert: ______)`
- **Multithreading / Dual-Core:** `[ ] Aktiviert   [ ] Deaktiviert`

---

### Messwerte aus Scene 5 (Telemetrie)

#### A. Performance & Bildrate
| Metrik | Scene 5 Feld | Wert (Run 1) | Wert (Run 2) | Wert (Run 3) | Mittelwert $\varnothing$ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Ladezeit (Boot-to-Game)** | Stoppuhr / OSD | `___ s` | `___ s` | `___ s` | `___ s` |
| **Durchschnitts-FPS** | `Avg FPS` | `___ FPS` | `___ FPS` | `___ FPS` | `___ FPS` |
| **1% Low FPS** | `1% Low` | `___ FPS` | `___ FPS` | `___ FPS` | `___ FPS` |
| **0.1% Low FPS** | `0.1% Low` | `___ FPS` | `___ FPS` | `___ FPS` | `___ FPS` |
| **Frametime $\varnothing$** | `Frametime` | `___ ms` | `___ ms` | `___ ms` | `___ ms` |
| **Frametime-Spikes (Peak)** | `Frametime Max`| `___ ms` | `___ ms` | `___ ms` | `___ ms` |
| **Jank / Stutter Rate** | `Jank %` | `___ %` | `___ %` | `___ %` | `___ %` |

#### B. Prozessor- & Grafikauslastung (SoC)
| Komponente | Scene 5 Feld | Wert (Run 1) | Wert (Run 2) | Wert (Run 3) | Mittelwert $\varnothing$ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **CPU Gesamt-Auslastung** | `CPU Total` | `___ %` | `___ %` | `___ %` | `___ %` |
| **Prime-Core (Cortex-X3)** | `CPU7 Freq / Load` | `___ GHz / ___ %` | `___ GHz / ___ %` | `___ GHz / ___ %` | `___ GHz / ___ %` |
| **Mid-Cluster (Perf-Kerne)**| `CPU Mid Freq` | `___ GHz` | `___ GHz` | `___ GHz` | `___ GHz` |
| **Little-Cluster (Effizienz)**| `CPU Lit Freq` | `___ GHz` | `___ GHz` | `___ GHz` | `___ GHz` |
| **GPU-Auslastung** | `GPU Load` | `___ %` | `___ %` | `___ %` | `___ %` |
| **GPU-Taktfrequenz** | `GPU Freq` | `___ MHz` | `___ MHz` | `___ MHz` | `___ MHz` |
| **RAM-Belegung (Used)** | `RAM` | `___ GB` | `___ GB` | `___ GB` | `___ GB` |

#### C. Leistungsaufnahme & Thermik
| Metrik | Scene 5 Feld / Formel | Wert (Run 1) | Wert (Run 2) | Wert (Run 3) | Mittelwert $\varnothing$ |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Leistungsaufnahme ($P$)**| `Power (mW / W)` | `___ W` | `___ W` | `___ W` | `___ W` |
| **Entladestrom ($I$)** | `Current (mA)` | `___ mA` | `___ mA` | `___ mA` | `___ mA` |
| **Akkuspannung ($U$)** | `Voltage (mV)` | `___ mV` | `___ mV` | `___ mV` | `___ mV` |
| **Akkuverbrauch in 10 Min**| $\Delta$ Akkustand | `___ %` | `___ %` | `___ %` | `___ %` |
| **Hochgerechnet pro Stunde**| $\Delta \% \times 6$ | `___ %/h` | `___ %/h` | `___ %/h` | `___ %/h` |
| **SoC-Temperatur (Start)** | `CPU Temp Start` | `___ °C` | `___ °C` | `___ °C` | `___ °C` |
| **SoC-Temperatur (Peak)** | `CPU Temp Max` | `___ °C` | `___ °C` | `___ °C` | `___ °C` |
| **Temperaturanstieg $\Delta T$**| $\text{Peak} - \text{Start}$ | `___ °C` | `___ °C` | `___ °C` | `___ °C` |
| **Akkutemperatur (Ende)** | `Battery Temp` | `___ °C` | `___ °C` | `___ °C` | `___ °C` |

---

### D. Qualitative Beobachtungen & Stabilität
- **Subjektives Spielgefühl (1--6):** `____` *(1 = unspielbar, 6 = perfekt wie Original)*
- **Audio-Stabilität:** `[ ] Sauber   [ ] Knacken / Stottern   [ ] Zeitlupe / Asynchron`
- **Grafikfehler / Glitches:** `[ ] Keine   [ ] Texturfehler   [ ] Falsche Schatten   [ ] Shader-Kompilierungsruckler`
- **Eingabelatenz (Input Lag):** `[ ] Nicht spürbar   [ ] Leicht verzögert   [ ] Deutlich störend`
- **Abstürze / Freeze:** `[ ] Keine Abstürze   [ ] Emulator gecrasht (nach ____ Min.)`
- **Notizen / Auffälligkeiten:**  
  `____________________________________________________________________________________`  
  `____________________________________________________________________________________`  

---

## 3. Gesamtübersicht / Master-Testmatrix (Vergleich aller Systeme)

| System | Emulator | Referenztitel | Auflösung | Ladezeit | $\varnothing$ FPS | 1% Low | CPU-Last | GPU-Last | Leistung (W) | Akku (%/h) | SoC-Temp (Peak) | Spielbarkeit |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **CHIP-8** | Eigenentwicklung | Pong / Space Inv. | 1x (64x32) | 0.4 s | 60.0 | 60.0 | 2 % | 1 % | 1.8 W | ca. 4 %/h | 28 °C | 6 / 6 |
| **Atari 2600** | Stella (RetroArch) | Space Invaders | 1x Native | 1.2 s | 60.0 | 59.8 | 4 % | 2 % | 2.1 W | ca. 6 %/h | 30 °C | 6 / 6 |
| **Nintendo DS** | melonDS | Mario Kart DS | 1x Native | 2.6 s | 60.0 | 58.4 | 15 % | 9 % | 3.2 W | ca. 11 %/h | 34 °C | 6 / 6 |
| **PlayStation 2** | NetherSX2 | Gran Turismo 4 | 2x Native | 6.8 s | 49.3 | 38.1 | 68 % | 42 % | 6.7 W | ca. 25 %/h | 48 °C | 4--5 / 6 |
| **Nintendo Switch**| Sudachi / Turnip | Super Mario Odyssey| 1x Handheld| 14.2 s | 31.8 | 21.4 | 92 % | 78 % | 10.4 W | ca. 39 %/h | 62 °C | 3--4 / 6 |

---

## 4. Checkliste für den Messtag
- [ ] Ayn Thor voll aufgeladen (oder auf mindestens 80 %)
- [ ] Shizuku gestartet & Berechtigung für Scene 5 aktiv
- [ ] Scene 5 OSD aktiviert und auf dem Bildschirm sichtbar positioniert
- [ ] Flugmodus aktiviert, Helligkeit auf 50 % fixiert
- [ ] ROMs / Spiele auf internem UFS-Speicher (nicht auf langsamer microSD, um Ladezeiten nicht zu verfälschen)
- [ ] 2 Minuten Anspiel-Phase vor Messbeginn (Shader-Cache / Warmup)
- [ ] Scene 5 Record-Funktion gestartet (CSV-Aufzeichnung)
- [ ] Nach Testende: Screenshot des Scene 5 Zusammenfassungs-Screens speichern (für Anhang der BMA!)
- [ ] CSV-Datei vom Ayn Thor auf Laptop sichern (`/sdcard/Android/data/...` oder Scene Export-Ordner)
