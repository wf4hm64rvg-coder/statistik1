# Vortrag 4: Stichworte zum Ablesen

Kurzfassung des Sprechtexts. Fett = Kernzahl oder Schlüsselwort.

## Leorat Krasniqi (Folien 1–5 · ca. 4.5 Min.)

### 1 · Titel

- Begrüssung · «Wir sind **Leorat, Teoman und Filip**»
- Thema: **Das Berkeley-Paradoxon**
- Rechts zeigen: 1973 Männer **44.5 %** zugelassen, Frauen nur **30.4 %**
- 3 Teile: (a) Funktionen in Python → (b) scheinbare Ungerechtigkeit → (c) Vergleich + stochastische Unabhängigkeit

### 2 · Ausgangslage

- Herbst 1973: **4 526** Bewerbungen, Graduate-Studium, 6 Fachbereiche **A–F**
- Weniger Frauen zugelassen → Uni befürchtet **Klage wegen Diskriminierung**
- Tabelle 4: Quote je Fachbereich und Geschlecht + Verteilung der Bewerbungen
- Aufgaben (a), (b), (c) rechts kurz nennen
- Leitfrage: **Wurden Frauen wirklich benachteiligt?**

### 3 · Kapitel (a)

- «Wir starten mit Teil (a): unser Werkzeug für den ganzen Code → **Funktionen**»

### 4 · Funktionen: Grundlagen

- Funktion = **Maschine**: Zutaten rein, Ergebnis raus · einmal bauen, oft benutzen
- McKinney: **mehr als einmal gebraucht → Funktion**
- `def` = Maschine bauen · `return` = Ergebnis raus · ohne return → **None**
- Zutaten = **Argumente** · Positionsargument: muss · Keyword-Argument: hat **Voreinstellung**
- `vierfeldertafel`: fachbereich=None → **alle** · fachbereich="A" → **nur A**
- **Geschlossene Küche:** `bewerbungen` gibt es nur im Aufruf = lokaler Namensraum · **global vermeiden**
- `kennzahlen`: zwei Werte = **ein Paket (Tupel)** → auspacken in quote, anteil → **82.4 %** und **5.9 %**

### 5 · Funktionen als Objekte, Lambda, yield

- **Funktionen sind Objekte** = **Fliessband**: Leerzeichen weg → % weg → Zahl · «82.4%» → **0.824**
- **Lambda** = Mini-Funktion in einer Zeile (Prozentanzeige)
- **partial** = vorprogrammierte Taste: gleicher Test, fest **α = 1 %** = Currying
- **Generator / yield** = **Pez-Spender**: ein Ergebnis nach dem anderen, Fachbereich für Fachbereich
- **try/except** = **Sicherheitsnetz**: «82,4» mit Komma → klare Fehlermeldung · andere Fehler sichtbar lassen
- → «Damit übergebe ich an **Teoman**.»

## Teoman-Doganay Lam (Folien 6–10 · ca. 4.5 Min.)

### 6 · Kapitel (b)

- «Danke. Ich übernehme **Teil (b)**.»
- Schwerpunkt der Aufgabe: **Vorüberlegungen** → zuerst Planung, dann Ungerechtigkeit auf einen Blick

### 7 · Vorüberlegungen zur Umsetzung

- **01 Daten:** Tabelle 4 nur Prozente → für P(W) + Chi-Quadrat **Anzahlen nötig**
- Anzahlen aus Originaldaten (Bickel et al. 1975) · Code prüft: **0 Abweichungen**
- **02 Kontrolle:** Satz der totalen Wahrscheinlichkeit rechnet Zeile «Total» nach
- **03 Struktur:** langes DataFrame (Fachbereich × Geschlecht × Entscheid) → jede Kreuztabelle mit `pivot_table`
- **04 Funktionen:** gesamt + für alle 6 Fachbereiche
- Libraries: **pandas** Tabellen (McKinney = Autor) · **numpy** Rechnen · **matplotlib** Grafiken + Export · **scipy.stats** geprüfter Chi-Quadrat-Test
- Alle in **Anaconda** → keine Zusatzinstallation

### 8 · Die scheinbare Ungerechtigkeit

- Ein Vergleich genügt: **Gesamtquote**
- Balken mit Nullachse, Werte direkt beschriftet, bewusst nur 2 Balken
- Farben überall gleich: **Rot = Frauen, Blau = Männer**
- Männer **44.5 %** vs. Frauen **30.4 %** → **14.2 Prozentpunkte**, Faktor **1.47**
- Mit Männerquote: **817 statt 557** Frauen zugelassen
- «Also Diskriminierung? → prüfen wir in Teil (c)»

### 9 · Kapitel (c)

- Gesamtquote = alle 6 Fachbereiche zusammen → jetzt **Fachbereich für Fachbereich**

### 10 · Je Fachbereich: kein Nachteil für Frauen

- «Hier **kippt das Bild**»
- **4 von 6** Fachbereichen: Frauen höhere Quote (A, B, D, F)
- FB A: **+20.3** Prozentpunkte für Frauen
- Nur C (**−2.8**) und E (**−3.8**) Männer leicht vorne → kleine Unterschiede
- Gleiche Diagramm-Funktion wie auf der nächsten Folie, nur andere Spalten
- → «Wie passt das zur Gesamtquote? Das erklärt **Filip**.»

## Filip Lazic (Folien 11–15 · ca. 4.5 Min.)

### 11 · Frauen wählten selektivere Fachbereiche

- «Danke.» Antwort liegt darin, **wo** sich Frauen und Männer bewarben
- Männer: **51.5 %** in A oder B (Quote ≈ **64 %**)
- Frauen: nur **7.2 %** · allein FB A: **825** Männer, **108** Frauen
- **92.8 %** der Frauen in C–F → Quoten nur **6–35 %**
- Diagramm: A und B blau dominiert · C–F rot dominiert

### 12 · Mehr Bewerberinnen, tiefere Zulassungsquote

- x-Achse: Frauenanteil · y-Achse: Zulassungsquote · Punktfläche = Anzahl Bewerbungen
- Je höher der Frauenanteil → desto tiefer die Quote
- Korrelation **r = −0.79**
- Frauen bewarben sich in **stark umkämpften** Fachbereichen

### 13 · Die Erklärung: totale Wahrscheinlichkeit

- Gesamtquote = **gewichteter Mittelwert** der Fachbereichsquoten · Gewichte = Anteile der Bewerbungen
- Frauen: 5.9 % × 82.4 % + 1.4 % × 68 % + … = **30.4 %**
- Frauen: grosse Gewichte bei **tiefen** Quoten · Männer bei **hohen**
- Gleiche Gewichte für beide → Frauen **43.0 %**, Männer **38.7 %**
- → **Der Unterschied kehrt sich um**
- Code: dieselbe Funktion `gesamtquote`, nur andere Gewichte

### 14 · Stochastische Unabhängigkeit

- Definition: P(Z ∩ W) = P(Z) · P(W)  ⇔  P(Z | W) = P(Z)
- Z = zugelassen · W = Bewerbung einer Frau
- Gesamt: **0.1231** statt **0.1572** → **abhängig** · χ² = **92.2**, p < 0.001
- FB B–F: Werte nahe beieinander, alle p > 0.3 → **unabhängig**
- Nur FB A abhängig → **zugunsten der Frauen**
- = **bedingte Unabhängigkeit** gegeben Fachbereich · Fachbereich = **Confounder**

### 15 · Fazit

- **Simpson-Paradoxon:** Drittvariable Fachbereich kehrt den Zusammenhang um
- Aggregiert abhängig (**30.4 vs. 44.5 %**) · je Fachbereich kein Nachteil für Frauen
- Ursache: Frauen in **umkämpften** Fachbereichen
- Grenzen: Daten **eines Jahres** · Gründe für Fachbereichswahl offen
- Python: dieselben Funktionen für Gesamt, 6 Fachbereiche, Standardisierung
- Lehre: aggregierte Quoten erst **mit Drittvariablen** als Ursache deuten

## Alle zusammen (Folie 16)

### 16 · Quellen · Fragen?

- «Vielen Dank für Ihre Aufmerksamkeit» · Quellen rechts · «Wir freuen uns auf Ihre **Fragen**»

## Reservefolien (nur bei Rückfragen)

### 18 · Gesamtquote als gewichteter Mittelwert (Filip · Frage zu Folie 13)

- Anteil × Quote = **Beitrag** des Fachbereichs
- Frauen: **92.8 %** Gewicht in C–F, tiefe Quoten → Summe **30.4 %**
- Männer: **51.5 %** in A/B, hohe Quoten → Summe **44.6 %** (44.5 = Rundung Tabelle 4)

### 19 · So funktioniert der Chi-Quadrat-Test (Filip · Frage zu Folie 14)

- H₀: Zulassung und Geschlecht **unabhängig**
- Erwartet E = n · P(Z) · P(W) → Frauen zugelassen: erwartet **711.5**, beobachtet **557**
- χ² = Σ (B − E)² / E = **92.2** · df = 1, kritisch **3.84** → **H₀ verwerfen**
- Code: `chi2_contingency`

### 20 · Der Fachbereich als Drittvariable (Filip · Frage nach Kausalität)

- Geschlecht ↔ Fachbereich: χ² = **1 068.4**
- Fachbereich ↔ Zulassung: χ² = **778.9**
- Direkter Effekt Geschlecht → Zulassung: **kaum** · Fachbereich = **Confounder**
- **Korrelation ≠ Kausalität**

### 21 · Ablauf des Programms (Teoman · Frage zum Code-Aufbau)

- 5 Schritte: **Erfassen · Prüfen · Anzahlen · Analysieren · Darstellen**
- Prinzipien: alles als Funktion · **kein global** · Fehler sichtbar (try/except + 2 Gegenproben)
