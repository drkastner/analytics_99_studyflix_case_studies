# Einreichungsrichtlinien für Case Studies

## Überblick
Vielen Dank für dein Interesse an unserer Case Study. Dieses Dokument beschreibt den Einreichungsprozess und die Anforderungen.

## Erste Schritte

### 1. Repository forken
- Navigiere zum Repository auf GitHub
- erstelle einen "Fork" in deinem eigenen GitHub-Account
- Clone dein geforktes Repository auf deinen lokalen Rechner

### 2. Versionskontrolle einrichten
- Stelle sicher, dass Git auf deinem Rechner installiert ist
- Wähle einen neuen Ordner auf deinem PC aus, in dem du arbeiten möchtest
- Initialisiere die Git-Versionskontrolle, falls nicht bereits beim Klonen geschehen

## Repository-Struktur

Das Repository ist wie folgt organisiert:

```
analytics_99_studyflix_case_studies/
├── case_study_1/
│   ├── data/              # Eingabedaten für die Case Study
│   ├── output/            # Deine Analyseergebnisse kommen hier hin
│   └── case_study_1_assignment.md
├── case_study_2/
│   ├── data/
│   ├── output/
│   └── case_study_2_assignment.md
└── submission_guidelines.md
```

### Case Study Ordner
- Jede Case Study hat einen eigenen Ordner (z.B. `case_study_1`, `case_study_2`)
- Du wirst darüber informiert, welche Case Study du bearbeiten sollst

### Data Ordner
- Der `/data` Ordner innerhalb jeder Case Study enthält alle notwendigen Eingabedateien
- Verändere die Originaldaten nicht
- Falls du bearbeitete Versionen erstellen musst, speichere diese in `/output`

### Output Ordner
- Der `/output` Ordner ist der Ort, an dem du deine Analyseergebnisse einreichst
- Alle deine Ergebnisse sollten hier abgelegt werden

## Einreichungsanforderungen

### Dateiformat
Du musst deine Analyse in **einem der folgenden Formate** einreichen:

1. **Markdown-Datei** (`.md`)
   - Empfohlen für textlastige Analysen mit Code-Snippets
   - Binde Visualisierungen als eingebettete Bilder ein
   - Beispiel: `case_study_1_loesung.md`

2. **Jupyter Notebook** (`.ipynb`)
   - Empfohlen für Python-basierte Analysen
   - Ermöglicht interaktiven Code, Visualisierungen und Erklärungen
   - Beispiel: `case_study_1_loesung.ipynb`

3. **R Markdown oder Quarto** (`.Rmd`) oder gerendertes HTML ODER (`.qmd`)
   - Empfohlen für R-basierte Analysen
   - Füge sowohl die `.Rmd`-Quelldatei als auch die gerenderte Ausgabe hinzu, wenn möglich
   - Beispiel: `case_study_1_loesung.Rmd` / `case_study_1_loesung.qmd` 

### Was soll in deiner Einreichung enthalten sein

Deine Einreichungsdatei sollte Folgendes enthalten:

1. **Problemverständnis**
   - Kurze Zusammenfassung der Aufgabenziele
   - Dein Ansatz und deine Methodik

2. **Code und Analyse**
   - Gut dokumentierter Code mit Kommentaren
   - Klare Erklärung deines Gedankengangs
   - Begründung für die Wahl der Tools/Bibliotheken

3. **Visualisierungen**
   - Diagramme, Grafiken und Plots wie in der Aufgabenstellung gefordert
   - Stelle sicher, dass Visualisierungen klar beschriftet und interpretierbar sind

4. **Ergebnisse und Erkenntnisse**
   - Beantworte alle in der Aufgabenstellung gestellten Fragen
   - Liefere Interpretationen und Erkenntnisse aus deiner Analyse
   - Hebe Auffälligkeiten oder interessante Befunde hervor

5. **Schlussfolgerungen**
   - Zusammenfassung der wichtigsten Ergebnisse
   - Empfehlungen oder nächste Schritte (falls zutreffend)

### Dateinamen-Konvention
- Verwende aussagekräftige Namen, die die Case Study Nummer enthalten
- Beispiele:
  - `case_study_1_loesung.md`
  - `case_study_1_analyse.ipynb`
  - `case_study_2_ergebnisse.Rmd`

### Output-Dateien
Lege alle Output-Dateien im `/output` Ordner der jeweiligen Case Study ab:
- Deine Haupt-Analysedatei (Markdown/Notebook)
- Alle erstellten Visualisierungen (`.png`, `.jpg`, `.svg`)
- Alle von dir erstellten bearbeiteten Datendateien
- Begleitdokumente, falls erforderlich

## Einreichungsprozess

### 1. Vervollständige deine Arbeit
- Arbeite an der zugewiesenen Case Study in deinem geforkten Repository
- Committe deine Änderungen regelmäßig mit aussagekräftigen Commit-Messages:
  ```bash
  git add case_study_1/output/case_study_1_loesung.md
  git commit -m "Initiale Analyse für Case Study 1 hinzugefügt"
  ```

### 2. Push zu deinem Fork
```bash
git push origin main
```

### 3. Erstelle einen Pull Request
- Navigiere zu deinem geforkten Repository auf GitHub
- Klicke auf "Pull Request", um deine Arbeit an das Original-Repository zu übermitteln
- Füge in der PR-Beschreibung Folgendes hinzu:
  - Welche Case Study du bearbeitet hast
  - Kurzer Überblick über deinen Ansatz
  - Eventuelle Annahmen oder Hinweise für die Reviewer

**Alternative:** Falls anders angewiesen, teile einfach den Link zu deinem geforkten Repository.

## Best Practices

### Code-Qualität
- Schreibe sauberen, lesbaren Code mit korrekter Formatierung
- Füge Kommentare hinzu, um komplexe Logik zu erklären
- Verwende aussagekräftige Variablen- und Funktionsnamen

### Dokumentation
- Erkläre deine Überlegungen und Methodik
- Dokumentiere alle Annahmen, die du getroffen hast
- Notiere eventuelle Einschränkungen oder Herausforderungen

### Reproduzierbarkeit
- Stelle sicher, dass deine Analyse von anderen ausgeführt werden kann
- Gib alle Package-/Bibliotheksanforderungen an
- Verwende relative Pfade (keine absoluten Pfade zu deinem lokalen Rechner)

### Versionskontrolle
- Mache regelmäßige Commits während deiner Arbeit
- Verwende aussagekräftige Commit-Messages
- Halte deinen Fork bei Bedarf mit dem Original-Repository synchron

## Technische Anforderungen

### Unterstützte Programmiersprachen/Tools
- Python (mit Jupyter Notebook)
- R (mit R Markdown)
- SQL (für Datenabfragen, falls zutreffend)
- Jede andere in der Aufgabenbeschreibung genehmigte Sprache

### Gängige Bibliotheken/Packages
Du darfst Standard-Datenanalyse-Bibliotheken verwenden wie:
- Python: pandas, numpy, matplotlib, seaborn, plotly, scikit-learn
- R: tidyverse, ggplot2, dplyr, tidyr

### Umgebungseinrichtung
- Füge eine `requirements.txt` (Python) oder Session-Info (R) hinzu, falls du spezifische Packages verwendest
- Dies hilft, die Reproduzierbarkeit deiner Analyse sicherzustellen

## Bewertungskriterien

Deine Einreichung wird anhand folgender Kriterien bewertet:

1. **Korrektheit**: Genauigkeit der Analyse und Antworten
2. **Code-Qualität**: Sauberer, gut organisierter und dokumentierter Code
3. **Methodik**: Angemessene analytische Ansätze und Techniken
4. **Kommunikation**: Klare Erklärungen und Interpretationen
5. **Erkenntnisse**: Tiefe der Analyse und Qualität der Insights
6. **Präsentation**: Professionelle Formatierung und Visualisierungsqualität

## Fragen oder Probleme?

Falls du auf Probleme stößt mit:
- Datendateien, die beschädigt oder nicht zugänglich erscheinen
- Unklaren Aufgabenstellungen
- Technischen Problemen mit dem Repository

Bitte wende dich an deine Kontaktperson

## Abgabefrist

Die Abgabefrist wird dir separat mitgeteilt. Bitte stelle sicher, dass du deine Arbeit vor dem angegebenen Datum und der Uhrzeit einreichst.

---

**Viel Erfolg bei deiner Case Study! Wir freuen uns darauf, deine Analyse zu prüfen.**
