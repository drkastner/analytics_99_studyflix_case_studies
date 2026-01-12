# Case Study 2 - GA4 BigQuery Analyse: Flood-It! Gaming App

## Überblick
In dieser Case Study analysierst du den öffentlichen Google Analytics 4 (GA4) Datensatz der Flood-It! Gaming App. Du wirst BigQuery verwenden, um Spielerverhalten, Engagement-Metriken, Monetarisierung und weitere wichtige KPIs zu untersuchen.

## Datenzugang

### Zugriff auf den Datensatz einrichten

1. **Google Cloud Projekt erstellen** (falls noch nicht vorhanden)
   - Gehe zu [Google Cloud Console](https://console.cloud.google.com/)
   - Erstelle ein neues Projekt oder wähle ein bestehendes aus
   - Aktiviere die BigQuery API für dein Projekt

2. **BigQuery Sandbox nutzen** (kostenlos, kein Kreditkarte nötig)
   - BigQuery bietet eine [Sandbox](https://cloud.google.com/bigquery/docs/sandbox) mit 1 TB kostenlosen Abfragen pro Monat
   - Perfekt für diese Analyse ausreichend

3. **Zugriff auf den Flood-It! Datensatz**
   - Der öffentliche Datensatz ist verfügbar unter: `firebase-public-project.analytics_153293282`
   - Dokumentation: [GA4 BigQuery App-Gaming Demo Dataset](https://developers.google.com/analytics/bigquery/app-gaming-demo-dataset?hl=de)
   - Projekt-ID: `firebase-public-project`
   - Dataset-ID: `analytics_153293282`
   - Tabellen: `events_YYYYMMDD` (tägliche Event-Tabellen)

4. **BigQuery Query Editor öffnen**
   - Navigiere zu [BigQuery Console](https://console.cloud.google.com/bigquery)
   - Suche im Explorer nach dem öffentlichen Datensatz `firebase-public-project`
   - Erweitere das Dataset `analytics_153293282`, um die Event-Tabellen zu sehen
   - Teste den Zugriff mit einer einfachen Query:
   ```sql
   SELECT *
   FROM `firebase-public-project.analytics_153293282.events_*`
   WHERE _TABLE_SUFFIX BETWEEN '20180815' AND '20180915'
   LIMIT 10
   ```

### Alternative Zugriffsmöglichkeiten

- **BigQuery Python Client**: Für Python-basierte Analysen
  ```python
  from google.cloud import bigquery
  client = bigquery.Client()
  ```

- **R mit bigrquery**: Für R-basierte Analysen
  ```r
  library(bigrquery)
  ```

- **BigQuery UI**: Direkt im Browser über die Google Cloud Console

## Aufgabenstellung

Analysiere den Flood-It! Gaming App Datensatz und beantworte die folgenden Fragen. Dokumentiere deine SQL-Queries, Methodik und Ergebnisse in einem Markdown-File oder Notebook im `/output` Ordner.

---

## 1. Player Progression Analysis

Untersuche, wie Spieler durch die verschiedenen Level fortschreiten:

### 1.1 Level-Completion Raten
- **Frage**: Wie viel Prozent der Nutzer schließen Level 1 ab? Level 5? Level 10?
- **Hinweis**: Analysiere die `level_complete_*` Events oder ähnliche Level-bezogene Events
- **Zu berechnen**:
  - Anzahl unique User, die jedes Level starten
  - Anzahl unique User, die jedes Level abschließen
  - Completion Rate pro Level

### 1.2 Durchschnittliche Zeit pro Level
- **Frage**: Wie lange brauchen Spieler durchschnittlich, um jedes Level abzuschließen?
- **Hinweis**: Berechne die Zeitdifferenz zwischen Level-Start und Level-Complete Events
- **Zu berechnen**:
  - Durchschnittliche Completion Time für Level 1, 5, 10
  - Median Completion Time
  - Verteilung der Completion Times

### 1.3 Drop-Off Analyse
- **Frage**: An welchen Stellen steigen Nutzer aus?
- **Zu analysieren**:
  - Welche Level haben die höchsten Abbruchraten?
  - Gibt es bestimmte Level, bei denen besonders viele Spieler aufhören?
  - Funnel-Analyse von Level 1 bis Level 10+

---

## 2. Engagement Metrics

Analysiere das Nutzer-Engagement mit der App:

### 2.1 Session Length Distribution
- **Frage**: Wie ist die Verteilung der Session-Längen?
- **Zu analysieren**:
  - Durchschnittliche Session-Dauer
  - Median Session-Dauer
  - Verteilung (Histogram): kurze (<5 min), mittlere (5-15 min), lange Sessions (>15 min)

### 2.2 Daily/Weekly Active Users (DAU/WAU)
- **Frage**: Wie viele Nutzer sind täglich/wöchentlich aktiv?
- **Zu berechnen**:
  - DAU (Daily Active Users) über einen Zeitraum
  - WAU (Weekly Active Users)
  - DAU/WAU Ratio (Engagement-Indikator)

### 2.3 Retention Cohort Analysis
- **Frage**: Wie gut ist die User Retention?
- **Zu analysieren**:
  - Cohort-Analyse: Nutzer nach Registrierungs-/Erste-Session-Datum gruppieren
  - Retention Rate nach 1 Tag, 7 Tagen, 14 Tagen, 30 Tagen
  - Visualisiere die Retention-Curve

---

## 3. Monetization Analysis

Untersuche die Monetarisierungsmetriken der App:

### 3.1 Ad Revenue per User
- **Frage**: Wie viel Ad Revenue generiert die App pro Nutzer?
- **Zu berechnen**:
  - Gesamter Ad Revenue (aus `ad_impression` oder ähnlichen Events)
  - ARPU (Average Revenue Per User)
  - ARPPU (Average Revenue Per Paying User)

### 3.2 In-App Purchase Conversion Rates
- **Frage**: Wie viele Nutzer tätigen In-App Purchases?
- **Zu analysieren**:
  - Anzahl Nutzer mit mindestens einem Purchase
  - Conversion Rate (% der Nutzer, die kaufen)
  - Durchschnittlicher Purchase Value

### 3.3 Beziehung zwischen Spielfortschritt und Monetarisierung
- **Frage**: Gibt es einen Zusammenhang zwischen Level-Fortschritt und Monetarisierung?
- **Zu untersuchen**:
  - Kaufen fortgeschrittene Spieler mehr als Anfänger?
  - Bei welchem Level ist die Purchase-Wahrscheinlichkeit am höchsten?
  - Unterscheidet sich das Ad-Engagement zwischen Käufern und Nicht-Käufern?

---

## 4. Device Performance

Analysiere die Performance auf verschiedenen Geräten:

### 4.1 Completion Rates nach Device
- **Frage**: Welche Geräte haben die besten/schlechtesten Completion Rates?
- **Zu analysieren**:
  - Level Completion Rates gruppiert nach Device Category (mobile, tablet, desktop)
  - Device Model Performance (z.B. iPhone vs. Android-Modelle)
  - Gibt es Devices mit auffällig schlechter Performance?

### 4.2 OS Version Impact
- **Frage**: Beeinflusst die OS-Version das Gameplay?
- **Zu untersuchen**:
  - Completion Rates nach OS (iOS, Android)
  - OS Version (z.B. iOS 15 vs. iOS 16 vs. iOS 17)
  - Crash-Raten oder Performance-Probleme nach OS

---

## 5. User Segmentation

Segmentiere die Nutzer und analysiere Unterschiede:

### 5.1 Casual vs. Hardcore Players
- **Frage**: Wie unterscheiden sich verschiedene Spielertypen?
- **Segmentierung definieren**:
  - Casual: z.B. <3 Sessions pro Woche, kurze Sessions
  - Hardcore: z.B. >5 Sessions pro Woche, lange Sessions, hoher Level-Fortschritt
- **Zu vergleichen**:
  - Engagement-Metriken
  - Monetarisierung
  - Retention

### 5.2 Geografische Unterschiede
- **Frage**: Gibt es regionale Unterschiede im Spielverhalten?
- **Zu analysieren**:
  - Top-Länder nach User-Anzahl
  - Completion Rates nach Land
  - Session-Länge nach Region
  - Monetarisierung nach Land

### 5.3 Time-of-Day Usage Patterns
- **Frage**: Wann spielen Nutzer am häufigsten?
- **Zu untersuchen**:
  - Sessions nach Tageszeit (Morgens, Mittags, Abends, Nachts)
  - Wochentags- vs. Wochenend-Nutzung
  - Peak-Zeiten für Engagement

---

## Technische Anforderungen

### SQL/BigQuery
- Alle Analysen sollten primär mit SQL-Queries in BigQuery durchgeführt werden
- Dokumentiere alle verwendeten Queries in deinem Notebook/Markdown

### Visualisierungen
- Erstelle aussagekräftige Visualisierungen für deine Ergebnisse
- Tools: Python (matplotlib/seaborn/plotly), R (ggplot2), Looker Studio, oder direkt in BigQuery

### Dateistruktur
Deine Einreichung im `/output` Ordner sollte enthalten:
- `case_study_2_analyse.md` oder `.ipynb` oder `.Rmd` mit:
  - Alle SQL-Queries
  - Ergebnisse und Interpretationen
  - Visualisierungen
- `queries/` (optional): Separate SQL-Files für komplexe Queries
- `visualizations/`: PNG/JPG der erstellten Charts

### Tools
Du kannst folgende Tools verwenden:
- **BigQuery Console**: Für SQL-Queries
- **Python**: `google-cloud-bigquery`, `pandas`, `matplotlib`, `seaborn`
- **R**: `bigrquery`, `tidyverse`, `ggplot2`
- **Looker Studio**: Für interaktive Dashboards (optional)

---

## Bewertungskriterien

Deine Analyse wird bewertet nach:

1. **SQL-Kompetenz**: Korrekte und effiziente BigQuery Queries
2. **Analytisches Denken**: Sinnvolle Interpretation der Daten
3. **Visualisierung**: Klare, aussagekräftige Charts
4. **Insights**: Qualität der gezogenen Schlussfolgerungen
5. **Dokumentation**: Gut strukturierte und nachvollziehbare Analyse
6. **Vollständigkeit**: Alle Fragen wurden beantwortet

---

## Hilfreiche Ressourcen

- [GA4 BigQuery Export Schema](https://support.google.com/analytics/answer/7029846)
- [BigQuery Standard SQL Syntax](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax)
- [GA4 App-Gaming Demo Dataset Dokumentation](https://developers.google.com/analytics/bigquery/app-gaming-demo-dataset?hl=de)
- [BigQuery Best Practices](https://cloud.google.com/bigquery/docs/best-practices)

---

## Tipps

- Beginne mit explorativen Queries, um die Datenstruktur zu verstehen
- Nutze `LIMIT` bei ersten Tests, um Kosten zu sparen
- Partitioniere große Queries nach Datum (`WHERE _TABLE_SUFFIX`)
- Dokumentiere deine Annahmen und Berechnungsmethoden
- Bei Fragen zur Datenstruktur: Nutze `INFORMATION_SCHEMA` oder `SELECT * LIMIT 10`

---

**Viel Erfolg bei der Analyse!**
