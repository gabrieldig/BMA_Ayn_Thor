# Persönliches Projektjournal (Arbeitsjournal)

**Verfasser:** Gabriel Di Giuseppe  
**Berufsmaturitätsarbeit (BMA) 2026** – Berufsmaturitätsschule Zürich (BMZ)  
**Ausrichtung:** Technik, Architektur, Life Sciences (Klasse BIN23e)  
**Partnerarbeit mit:** David Martin Felicio Reichlin  
**Thema:** Emulation mit Ayn Thor – Dekonstruktion von Software-Emulatoren und empirische Grenzwertanalyse auf moderner Handheld-Hardware  
**Oberthema:** Was läuft im Hintergrund?  
**Begleitende Lehrperson:** Alexander Körner  
**Abgabetermin:** 27. November 2026  

---

## 1. Vorbemerkung zur individuellen Prozessdokumentation

Gemäss **Kapitel 3 der BMA-Richtlinien 2026** ist die Prozessdokumentation bei Partnerarbeiten **individuell** von jedem Verfasser zu erstellen. 
Dieses Dokument enthält ausschliesslich die von mir (**Gabriel Di Giuseppe**) geleisteten Tätigkeiten, meine persönlichen Arbeitszeiten sowie die von mir bewältigten Problemstellungen und Lösungsansätze.

Gemäss **Kapitel 1.4 der Richtlinien** deklariere ich zudem den Einsatz generativer KI-Systeme für meine Aufgabenbereiche transparent:
- **Zulässige Unterstützung:** Strukturierung, Formulierungshilfen bei Abstract/Hypothesen, LaTeX-Syntax und Paket-Debugging.
- **Eigene wissenschaftliche & technische Leistung:** Rechnerarchitektur-Recherche, vollständige Kernentwicklung des CHIP-8-Interpreters in Rust, Konfiguration von Mesa Turnip, Durchführung der Switch- und Baseline-Messungen, Datenanalyse und Verfassen der Fachtexte.

---

## 2. Individuelles Projektjournal: Gabriel Di Giuseppe

| Nr. | Datum | Tätigkeit / Mein Arbeitspaket | Form | Zeit (h) | Persönliche Erkenntnisse, Probleme & Lösungen | KI-Nutzung & Einsatzzweck |
|:---:|:---|:---|:---:|:---:|:---|:---|
| **1** | 22.08.2026 | **Themenfindung & Projekt-Scoping:** Diskussion mit David über das Oberthema «Was läuft im Hintergrund?». Erarbeitung des Fokus auf hardwarenahe Emulation und Eingrenzung auf den Ayn Thor (Qualcomm Snapdragon 8 Gen 2). | Partnerarbeit | 3.5 | **Erkenntnis:** Thema war anfangs zu weit gefasst (x86 vs. ARM). Ich habe vorgeschlagen, uns auf drei konkrete Konsolen-Generationen (3DS, Wii, Switch) zu beschränken. | **ChatGPT:** Abfrage von Ideen zur Strukturierung eines Hardware-Emulationsthemas. |
| **2** | 29.08.2026 | **Formulierung Leitfrage & Hypothesen:** Definition der Hauptforschungsfrage sowie der drei wissenschaftlichen Hypothesen (H1: JIT-Overhead, H2: NCE & Speicherbandbreite, H3: Mesa Turnip Grafiktreiber). | Partnerarbeit | 4.0 | **Problem:** Hypothese 2 war zunächst zu unpräzise bezüglich Flaschenhals formuliert.<br>**Lösung:** Präzisierung auf die Speicherbandbreite und GPU-Maxwell-Translation bei Switch-NCE. | **Claude:** Sprachliche Schärfung der Hypothesen zur Gewährleistung der Falsifizierbarkeit. |
| **3** | 05.09.2026 | **Projektvereinbarung & Meilensteinplanung:** Ausarbeitung des Meilensteinplans für die Betreuungsperson A. Körner (Abstimmung von Theorie, Rust-Entwicklung, Messungen und Schreibphase). | Partnerarbeit | 2.5 | **Fortschritt:** Vereinbarung wurde von Herrn Körner genehmigt. Arbeitsaufteilung und Zeitbudget festgelegt. | **Keine** (Eigenständige Planung) |
| **4** | 16.09.2026 | **Theorie-Recherche Emulationstechniken:** Literatur- und Quelltextrecherche zu Interpreter vs. dynamischem JIT-Recompiler vs. Native Code Execution (NCE). Konzeption von Kapitel 3.4. | Einzelarbeit | 5.0 | **Erkenntnis:** NCE funktioniert nur bei identischer Host- und Gast-Befehlssatzarchitektur (ARM64 zu ARM64), erfordert aber Kernel-Patching / MMU-Mapping. | **Keine** (Fachliteratur, Emulatoren-Source-Code & Whitepaper) |
| **5** | 23.09.2026 | **Rust Cargo-Workspace & CHIP-8 Kern:** Initialisierung des Repositories, Aufsetzen des Multi-Crate-Workspaces (`chip8_core`, `desktop`). Implementierung des Speichers (4096 Bytes), der Register V0–VF, des I-Registers und des Program Counters. | Einzelarbeit | 6.0 | **Problem:** Typensichere Verwaltung des CHIP-8-Speicherlayouts und Stack-Pointers in Rust ohne unsicheren Code (`unsafe`).<br>**Lösung:** Modellierung über feste Arrays `[u8; 4096]` und `[u16; 16]`. | **Keine** (Eigenständige Programmierung in Rust) |
| **6** | 28.09.2026 | **Implementierung Opcode-Decoder & ALU:** Ausprogrammierung der 35 Maschinenbefehle (Bitmanipulationen, mathematische Additionen mit Carry-Flag in VF, bedingte Sprünge `3XNN`, `4XNN` und Timer-Logik). | Einzelarbeit | 7.0 | **Problem:** Bei der Sprite-Zeichnung (`Dxyn`) stimmte die XOR-Pixel-Kollision nicht, Sprites flackerten in *Pong*.<br>**Lösung:** Schreiben automatisierter Rust-Unit-Tests; Bug im Setzen des Carry-/Collision-Flags behoben. | **Keine** (Eigenständige Programmierung & Debugging) |
| **7** | 10.10.2026 | **Treiber-Architektur & Turnip-Integration:** Erforschung der Funktionsweise alternativer GPU-Treiber unter Android. Testen von Mesa Turnip Driver (v26.x) auf der Adreno-740-GPU im Vergleich zum Qualcomm-Stock-Treiber. | Einzelarbeit | 4.5 | **Erkenntnis:** Mesa Turnip implementiert moderne Vulkan-Erweiterungen wesentlich sauberer als der Qualcomm-Herstellertreiber und verhindert Shader-Abstürze in Eden. | **Keine** (Praktische Treiber-Injektion & GitHub-Release-Analyse) |
| **8** | 14.10.2026 | **Definition der Messmatrix:** Zusammen mit David Erstellung der Testmatrix (`testmatrix_scene5.csv`) und Definition der relevanten Metriken (FPS, Frametimes, Peak FT, Jank-Events, CPU-Cluster-Last, Watt, Akku-Entladung). | Partnerarbeit | 3.0 | **Fortschritt:** Feste Standardbedingungen (300 s Aufzeichnungsdauer, Raumtemperatur 21 °C, Standard-Lüfterprofil) für wissenschaftliche Reproduzierbarkeit festgelegt. | **Antigravity AI:** Formatierung der Markdown- und Tabellenvorlagen für die Messreihen. |
| **9** | 19.10.2026 | **Baseline-Messung CHIP-8:** Kompilierung des fertigen Rust-Interpreters und Durchführung der Nulllinien-Messung `TEST-CHIP8-01` mit *Pong* über Scene 5. | Partnerarbeit | 3.0 | **Ergebnis:** Baseline ermittelt (2.1 % CPU-Auslastung, 1.80 W Leistungsaufnahme, 28.2 °C SoC-Temperatur). Bildet die Referenz für minimalen Dolmetscher-Overhead. | **Keine** (Empirische Messung) |
| **10** | 19.10.2026 | **Switch-Benchmark 1x Native (Eden):** Durchführung des 300s-Stresstests `TEST-NSW-01` (*Mario Kart 8 Deluxe*, 1x Handheld, NCE aktiv, Vulkan-Backend, Mesa Turnip). | Einzelarbeit | 4.5 | **Ergebnis:** Aufzeichnung der Telemetrie: 54.0 Avg FPS, 7.41 W Leistungsaufnahme, Peak-Temperatur 91.5 °C. Lüfter läuft im Dauerbetrieb; 14 Jank-Events protokolliert. | **Keine** (Empirische Messung & Telemetrieaufzeichnung) |
| **11** | 19.10.2026 | **Git-Transfer & LaTeX-Preamble:** Einrichten des Git-Repositories, Strukturierung des LaTeX-Dokuments (`main.tex`), Einbinden der Corporate Identity der BMZ und Konfiguration der Kopf-/Fusszeilen. | Einzelarbeit | 3.0 | **Problem:** Paketkollisionen zwischen `tabularx`, `xcolor` und `tcolorbox`.<br>**Lösung:** Bereinigung der Lade-Reihenfolge in der Preamble. Commit `df7ff70`. | **Antigravity AI:** Behebung von LaTeX-Paketkonflikten und Makro-Syntax. |
| **12** | 20.10.2026 | **Switch-Benchmark 2x Skalierung (Eden):** Durchführung von `TEST-NSW-02` (2x Auflösung) zur gezielten Überprüfung der GPU- und Speicherbandbreiten-Grenze. | Einzelarbeit | 4.5 | **Ergebnis:** FPS sinken auf 51.8, während die GPU-Last auf 95.8 % ansteigt (im Vergleich zu 41.5 % CPU). Klare Bestätigung von Hypothese H2. | **Keine** (Empirische Messung) |
| **13** | 20.10.2026 | **Schreibphase Kapitel 6 & NCE-Auswertung:** Verfassen von Kapitel 6.1 (CHIP-8-Architektur) und Kapitel 7.2/7.3 (NCE-Auswertung, GPU-Last und Energiebedarf) in `main.tex`. | Partnerarbeit | 5.5 | **Fortschritt:** Detaillierte Ausarbeitung des technischen Unterschieds zwischen PowerPC-JIT (Wii) und ARM64-NCE (Switch) im Text verankert. | **DeepL / Claude:** Grammatikalische Gegenlesung und sprachliche Glättung der Textabschnitte. |
| **14** | 21.10.2026 | **Schlussteil, Abstract & Verzeichnisse:** Ausformulierung von Kapitel 9 (Beantwortung der Leitfrage) sowie des dreiteiligen Abstracts (Zweck, Methodik, Resultate) gemäss Vorgaben von Kapitel 2.2 der Richtlinien. | Einzelarbeit | 4.0 | **Fortschritt:** Abstract auf exakt ~150 Wörter optimiert; formale Kriterien der BMZ geprüft. | **Claude:** Feedback zur Einhaltung des 150-Wörter-Rahmens des Abstracts. |
| **15** | 21.10.2026 | **Qualitätssicherung & LaTeX-Finalisierung:** Zweifache Kompilierung des Dokuments, Beseitigung von Overfull-H-Boxen, finale Prüfung der Verzeichnisse (Inhalt, Abbildungen, Tabellen). | Partnerarbeit | 3.0 | **Ergebnis:** PDF (`main.pdf`, 43 Seiten, 5.4 MB) vollständig und fehlerfrei erstellt. | **Antigravity AI:** Feinjustierung der Tabellenbreiten und `smartfigure`-Platzhalter. |

---

## 3. Persönliche Arbeitszeit-Statistik (Gabriel Di Giuseppe)

- **Gesamter persönlicher Arbeitsaufwand:** **56.0 Stunden**
  - *Davon eigenständige Einzelarbeit:* 34.5 Stunden (61.6 %)
  - *Davon gemeinsame Partnerarbeit mit David:* 21.5 Stunden (38.4 %)

### Verteilung nach Tätigkeitsbereichen:
1. **Konzeption, Forschungsfragen & Planung:** 10.0 h (17.9 %)
2. **Praktische Entwicklung (Rust CHIP-8 Interpreter):** 13.0 h (23.2 %)
3. **Mesa Turnip Recherche & Treiberanalyse:** 4.5 h (8.0 %)
4. **Empirische Messungen (Baseline & Switch NCE):** 12.0 h (21.4 %)
5. **Dokumentation, LaTeX-Satz & Finalisierung:** 16.5 h (29.5 %)

---

## 4. Persönliche Erklärung zur KI-Nutzung

Ich bestätige, dass ich generative KI-Systeme ausschliesslich im Rahmen der Bestimmungen von Kapitel 1.4 der BMA-Richtlinien 2026 als Hilfsmittel zur sprachlichen Optimierung, Formatierung und Ideenfindung eingesetzt habe. 

Sämtliche Programmierarbeiten in Rust, das Aufsetzen der Android-Testumgebung, die Durchführung der Messungen auf dem Ayn Thor sowie die fachliche Interpretation der Ergebnisse wurden von mir bzw. im Team mit David Reichlin vollständig eigenständig erarbeitet.
