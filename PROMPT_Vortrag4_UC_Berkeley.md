# Prompt: Vortrag 4 – Zulassungen an der UC Berkeley 1973

Den folgenden Text komplett kopieren und an Claude (oder eine andere KI) geben.
Die PDF *„Datenanalyse mit Python, Kapitel 3“* (liegt im Repo) am besten als Anhang mitschicken.

---

```text
Du bist Tutor:in für Statistik und Python an einer Fachhochschule (ZHAW School of Management
and Law, Studiengang Wirtschaftsinformatik, Modul w.BA.XX.2Stat-WIN.XX, HS 2026).
Hilf unserer Gruppe, die folgende Vortragsaufgabe vollständig und abgabefertig zu lösen.
Schreibe alles auf Deutsch (Schweizer Rechtschreibung, also "ss" statt "ß").

## Rahmen
- Aufgabe 4 (Vortrag-4: Python), 20 Punkte: (a) Theoretische Ausarbeitung 12 P., (b) Präsentation 8 P.
- Gruppe: 3 Personen (Leorat Krasniqi, Teoman-Doganay Lam, Filip Lazic), Vortragswoche 6.
- Schriftliche Ausarbeitung: mindestens 3 × 2 = 6 Seiten (ohne Titelblatt und Quellenverzeichnis).
- Präsentation: 3 × 5 = 15 Minuten laut Regeln (auf dem Aufgabenblatt stehen 20 Minuten –
  plane die Folien so, dass beides möglich ist, z. B. mit Reservefolien).
- Abgabe per E-Mail beim Dozenten der Kleinklasse, spätestens 14.12.2026.
- Werkzeuge: Python in Jupyter Notebook (Anaconda), Libraries pandas, numpy, matplotlib, scipy.

## Daten (Tabelle 4, Quelle: UCB Admissions, UC Berkeley 1973)

| Fachbereich | Zulassungsrate Frauen | Zulassungsrate Männer | Anteil Bewerbungen Frauen | Anteil Bewerbungen Männer |
|---|---|---|---|---|
| A | 82.4 % | 62.1 % | 5.9 % | 30.7 % |
| B | 68.0 % | 63.0 % | 1.4 % | 20.8 % |
| C | 34.1 % | 36.9 % | 32.3 % | 12.1 % |
| D | 34.9 % | 33.1 % | 20.4 % | 15.5 % |
| E | 23.9 % | 27.7 % | 21.4 % | 7.1 % |
| F | 7.0 % | 5.9 % | 18.6 % | 13.9 % |
| Total | 30.4 % | 44.5 % | 100 % | 100 % |

Optional zur Kontrolle: Die absoluten Zahlen gibt es im Datensatz "UCBAdmissions" (R) bzw.
in statsmodels/vega_datasets. Wenn du sie nutzt, zeige, dass sie zu den Prozenten der Tabelle passen.

## Aufgaben
(a) Erläutere basierend auf Quelle 2 (Wes McKinney: "Datenanalyse mit Python", Kapitel 3,
    Abschnitt 3.2 "Funktionen") das Thema Funktionen in Python: Definition mit def, return,
    Positions- und Schlüsselwortargumente, Namensräume/Gültigkeitsbereich (lokal/global),
    mehrere Rückgabewerte, Funktionen als Objekte, anonyme (Lambda-)Funktionen, Currying/partial,
    Generatoren, Fehler- und Ausnahmebehandlung. Jedes Konzept mit kurzem Beispiel – idealerweise
    mit den Berkeley-Daten, damit (a) und (b) zusammenhängen.
(b) Stelle die Verhältnisse in Python so dar, dass ein Betrachter schnell auf die (scheinbare)
    Ungerechtigkeit im Zulassungsverfahren schliessen kann:
    - Gesamtzulassungsquote Frauen vs. Männer (30.4 % vs. 44.5 %)
    - Zulassungsquoten pro Fachbereich (gruppiertes Balkendiagramm)
    - Verteilung der Bewerbungen auf die Fachbereiche nach Geschlecht
    - Selektivität der Fachbereiche vs. Frauenanteil der Bewerbungen (Streu-/Blasendiagramm)
    - Gewichtete / standardisierte Quote (z. B. Frauen-Quoten mit der Männer-Verteilung gewichtet)
(c) Vergleiche die Verteilungen bezüglich Zulassung von Männern und Frauen und interpretiere:
    - Simpson-Paradoxon: insgesamt scheinen Frauen benachteiligt, in 4 von 6 Fachbereichen
      haben sie aber eine höhere Quote. Erkläre die Störvariable "Fachbereich" (Confounder).
    - Gesamtquote als gewichteter Mittelwert (Satz der totalen Wahrscheinlichkeit) vorrechnen.
    - Stochastische Unabhängigkeit: Definition P(A ∩ B) = P(A)·P(B) bzw. P(A | B) = P(A),
      bedingte Wahrscheinlichkeit, bedingte Unabhängigkeit gegeben den Fachbereich.
      Prüfe, ob "Zulassung" und "Geschlecht" insgesamt bzw. innerhalb der Fachbereiche
      (annähernd) unabhängig sind; wenn absolute Zahlen vorliegen, zusätzlich Chi-Quadrat-Test
      (scipy.stats.chi2_contingency) gesamt und pro Fachbereich.
    - Fazit: Korrelation ≠ Kausalität; was man über Diskriminierung aussagen kann und was nicht.

Zusätzlich verlangt der Dozent ausdrücklich:
- Python-Code erläutern und ausführlich kommentieren(!).
- Verwendung der Libraries begründen (warum pandas, numpy, matplotlib, scipy?).
- Schwerpunkt auf den Vorüberlegungen zur programmtechnischen Umsetzung
  (Datenstruktur, Aufteilung in Funktionen, Ablauf, warum diese Diagrammtypen).
- Theoretische Hintergründe auch in der Präsentation zeigen.

## Was du liefern sollst
1. Ein vollständiges Jupyter Notebook (Markdown-Zellen + kommentierte Code-Zellen):
   Daten als pandas DataFrame, eigene Funktionen (passend zu Teil a), alle Diagramme
   (sauber beschriftet, Achsen in %, einheitliche Farben Frauen/Männer), Berechnungen zu (c).
   Der Code muss mit "Run All" fehlerfrei laufen.
2. Die schriftliche Ausarbeitung (mind. 6 Seiten Text) mit Gliederung:
   Titelblatt, Inhaltsverzeichnis, 1 Einleitung, 2 Funktionen in Python (a),
   3 Vorüberlegungen zur Umsetzung, 4 Datenaufbereitung & Visualisierung (b),
   5 Vergleich der Verteilungen & stochastische Unabhängigkeit (c), 6 Fazit,
   Quellenverzeichnis (McKinney; Bickel, Hammel & O'Connell 1975, Science 187;
   Python-/pandas-Dokumentation). Abbildungen nummeriert und im Text referenziert.
3. Eine Präsentation (ca. 12 Folien für 15 Minuten, 3 Sprecher à 5 Min.) mit klarer
   Aufteilung, wer welche Folien hält, und Sprechernotizen zu jeder Folie.
4. Eine kurze Liste möglicher Fragen des Dozenten mit Antworten.

Gehe Schritt für Schritt vor: Erst die Vorüberlegungen, dann das Notebook, dann
Ausarbeitung, dann Folien. Rechne alle Zahlen nach und prüfe, dass Text, Diagramme
und Tabelle übereinstimmen. Erkläre alles so, dass wir es in der Präsentation selbst
verstehen und frei erklären können.
```
