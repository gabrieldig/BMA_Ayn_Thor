# BMA Abschlussprojekt: Emulation mit Ayn Thor

Dieses Repository enthält die LaTeX-Vorlage für die Berufsmaturitätsarbeit (BMA) an der **Berufsmaturitätsschule Zürich (BMZ)**, Ausrichtung **Technik, Architektur, Life Sciences**.

Die Vorlage wurde anhand aller offiziellen Richtliniendokumente aktualisiert:
1. `4 Richtlinien für die Berufsmaturitätsarbeit BMA 2026.pdf`
2. `1 Bewertung BMA schriftliches Produkt 2026.pdf`
3. `Die BMA-Dschungel-Machete 2018.pdf`

---

## Umgesetzte Richtlinien & Vorgaben

- **Schrift & Zeilenabstand (Kap. 2.10):** 12-Punkt-Schrift (`12pt`), 1.5-Zeilenabstand (`\onehalfspacing`), Blocksatz mit Silbentrennung.
- **Seitenränder:** 30\,mm Rand links für Spiralheftung, 25\,mm rechts, oben und unten.
- **Titelblatt (Kap. 2.1):** Alle Pflichtangaben (Schule, Ausrichtung, Titel, Oberthema, Betreuer, Autoren, Klasse, Abgabetermin, Begriff «Berufsmaturitätsarbeit»).
- **Abstract (Kap. 2.2):** Ca. 150 Wörter im Präsens, exakt gegliedert in die 3 Pflichtabsätze (1. Fragestellung/Zweck, 2. Methoden, 3. Ergebnisse).
- **Verzeichnisse:** Automatisches Inhalts-, Abbildungs- und Tabellenverzeichnis (gemäss Bewertungsraster).
- **Zwei wissenschaftliche Methoden (Kap. 1.4 & Dschungel-Machete):**
  1. *Methode 1:* Fachliteratur- und Quellenrecherche (Theorie).
  2. *Methode 2:* Empirische Testreihen und Performancemessungen auf dem Ayn Thor.
- **Umfang:** Ausgelegt auf 4'000 bis 7'000 Wörter (Partnerarbeit, ohne Verzeichnisse und Anhang).
- **Wissenschaftlicher Schlussteil (Kap. 2.5):** Beantwortung der Leitfrage, Verifikation/Falsifikation der Hypothese. *Wichtig:* Keine Selbsterfahrungen im Schlussteil (gehören in die persönliche Prozessdokumentation).
- **KI-Deklaration (Kap. 1.4 - Neu 2026):** Transparenter Nachweis und Reflexion über den Einsatz generativer KI-Systeme im Anhang.
- **Danksagung & Bescheinigung (Kap. 2.7 & 2.9):** Danksagung sowie offizielle Selbstständigkeitserklärung mit Unterschriftenzeilen.

---

## Kompilierung

Das Dokument kann mit jedem gängigen LaTeX-System kompiliert werden (z.\,B. **TeX Live**, **MiKTeX**, **MacTeX**, **VS Code** oder **Overleaf**):

```bash
pdflatex main.tex
pdflatex main.tex
```
*(Zweimal ausführen, damit Inhalts-, Abbildungs- und Tabellenverzeichnis vollständig aktualisiert werden.)*
