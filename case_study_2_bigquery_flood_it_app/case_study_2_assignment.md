# Case Study 2 - GA4 BigQuery Analyse: Flood-It! Gaming App

## Überblick

In dieser Case Study analysierst du den öffentlichen Google Analytics 4 (GA4) Datensatz der Flood-It! Gaming App. Du wirst BigQuery verwenden, um Spielerverhalten, Engagement-Metriken, Monetarisierung und weitere wichtige KPIs zu untersuchen.

## Datenzugang

### Zugriff auf den Datensatz einrichten

1.  **Google Cloud Projekt erstellen** (falls noch nicht vorhanden)

    -   Gehe zu [Google Cloud Console](https://console.cloud.google.com/)
    -   Erstelle ein neues Projekt oder wähle ein bestehendes aus
    -   Aktiviere die BigQuery API für dein Projekt

2.  **BigQuery Sandbox nutzen** (kostenlos, kein Kreditkarte nötig)

    -   BigQuery bietet eine [Sandbox](https://cloud.google.com/bigquery/docs/sandbox) mit 1 TB kostenlosen Abfragen pro Monat
    -   Perfekt für diese Analyse ausreichend

3.  **Zugriff auf den Flood-It! Datensatz**

    -   Der öffentliche Datensatz ist verfügbar unter: `firebase-public-project.analytics_153293282`
    -   Dokumentation: [GA4 BigQuery App-Gaming Demo Dataset](https://developers.google.com/analytics/bigquery/app-gaming-demo-dataset?hl=de)
    -   Projekt-ID: `firebase-public-project`
    -   Dataset-ID: `analytics_153293282`
    -   Tabellen: `events_YYYYMMDD` (tägliche Event-Tabellen)

4.  **BigQuery Query Editor öffnen**

    -   Navigiere zu [BigQuery Console](https://console.cloud.google.com/bigquery)
    -   Suche im Explorer nach dem öffentlichen Datensatz `firebase-public-project`
    -   Erweitere das Dataset `analytics_153293282`, um die Event-Tabellen zu sehen
    -   Teste den Zugriff mit einer einfachen Query:

    ``` sql
    SELECT *
    FROM `firebase-public-project.analytics_153293282.events_*`
    WHERE _TABLE_SUFFIX BETWEEN '20180815' AND '20180915'
    LIMIT 10
    ```

### Alternative Zugriffsmöglichkeiten

-   **BigQuery Python Client**: Für Python-basierte Analysen

    ``` python
    from google.cloud import bigquery
    client = bigquery.Client()
    ```

-   **R mit bigrquery**: Für R-basierte Analysen

    ``` r
    library(bigrquery)
    ```

-   **BigQuery UI**: Direkt im Browser über die Google Cloud Console

## Aufgabenstellung

Analysiere den Flood-It! Gaming App Datensatz und beantworte die folgenden Fragen. Dokumentiere deine SQL-Queries, Methodik und Ergebnisse in einem Markdown-File oder Notebook im `/output` Ordner.

Wichtig: Du musst nicht alle Fragen beantworten, aber je mehr du bearbeitest, desto besser. Fokussiere dich auf die Bereiche, die für dich am interessantesten sind.

------------------------------------------------------------------------

## Business Context

Flood-It! ist ein beliebtes Mobile Game, bei dem Spieler farbige Blöcke auf einem Raster durch Farbwechsel verbinden müssen, um das gesamte Spielfeld in möglichst wenigen Zügen zu füllen. Die App generiert Einnahmen durch In-App-Werbung und optionale In-App-Käufe für zusätzliche Funktionen oder Level.

Hier kannst du es ausprobieren: [Flood-It! ausprobieren](https://unixpapa.com/floodit/)

Du bist ein Datenanalyst, der beauftragt wurde, das Nutzerverhalten, Engagement und Monetarisierung der App zu untersuchen, um Empfehlungen für Verbesserungen zu geben. Bitte nutze den folgenden Datensatz mit dem Ziel Hypothesen zu generieren, die der Growth Hacking Manager testen könnte. Ziel des Growth Hacking Managers ist es, möglichst viel Revenue mit den Nutzern der App zu erzielen. Am Ende der Aufgabe solltest Du 3 zentrale Hypthesen nennen können und diese mit Daten untermauern. (Wichtig: Es geht nicht darum, möglichst viele Fragen zu beantworten, sondern darum, eine datengetriebene Analyse durchzuführen und Hypothesen zu generieren.)

Du kannst dabei verschiedene Analysemethoden und Visualisierungen verwenden. Hier sind einige Fragen, die vielleicht helfen könnten, deine Analyse zu strukturieren:

Wie schreiten Nutzer durch die verschiedenen Level? Wie lange interagieren Nutzer mit der App? Was führt zu einer hohen Retention? Wie monetarisieren sich die Nutzer? Welche Nutzer sind besonders wertvoll?

------------------------------------------------------------------------

## Technische Anforderungen

### SQL/BigQuery

-   Alle Analysen sollten primär mit SQL-Queries in BigQuery durchgeführt werden
-   Dokumentiere alle verwendeten Queries in deinem Notebook/Markdown

### Visualisierungen

-   Erstelle aussagekräftige Visualisierungen für deine Ergebnisse
-   Tools: Python (matplotlib/seaborn/plotly), R (ggplot2), Looker Studio, oder direkt in BigQuery

### Dateistruktur

Deine Einreichung im `/output` Ordner sollte enthalten: - `case_study_2_analyse.md` oder `.ipynb` oder `.Rmd` mit: - Alle SQL-Queries - Ergebnisse und Interpretationen - Visualisierungen - `queries/` (optional): Separate SQL-Files für komplexe Queries - `visualizations/`: PNG/JPG der erstellten Charts

### Tools

Du kannst folgende Tools verwenden: - **BigQuery Console**: Für SQL-Queries - **Python**: `google-cloud-bigquery`, `pandas`, `matplotlib`, `seaborn` - **R**: `bigrquery`, `tidyverse`, `ggplot2` - **Looker Studio**: Für interaktive Dashboards (optional)

------------------------------------------------------------------------

## Bewertungskriterien

Deine Analyse wird bewertet nach:

1.  **SQL-Kompetenz**: Korrekte und effiziente BigQuery Queries
2.  **Analytisches Denken**: Sinnvolle Interpretation der Daten und Ableitung von Hypothesen
3.  **Visualisierung**: Klare, aussagekräftige Charts
4.  **Insights**: Qualität der gezogenen Schlussfolgerungen und Hypothesen
5.  **Dokumentation**: Gut strukturierte und nachvollziehbare Analyse
6.  **Tiefe der Analyse**: Fokus und Qualität statt Quantität

------------------------------------------------------------------------

## Hilfreiche Ressourcen

-   [GA4 BigQuery Export Schema](https://support.google.com/analytics/answer/7029846)
-   [BigQuery Standard SQL Syntax](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax)
-   [GA4 App-Gaming Demo Dataset Dokumentation](https://developers.google.com/analytics/bigquery/app-gaming-demo-dataset?hl=de)
-   [BigQuery Best Practices](https://cloud.google.com/bigquery/docs/best-practices)

------------------------------------------------------------------------

## Tipps

-   Beginne mit explorativen Queries, um die Datenstruktur zu verstehen
-   Nutze `LIMIT` bei ersten Tests, um Kosten zu sparen
-   Partitioniere große Queries nach Datum (`WHERE _TABLE_SUFFIX`)
-   Dokumentiere deine Annahmen und Berechnungsmethoden
-   Bei Fragen zur Datenstruktur: Nutze `INFORMATION_SCHEMA` oder `SELECT * LIMIT 10`

------------------------------------------------------------------------

**Viel Erfolg bei der Analyse!**