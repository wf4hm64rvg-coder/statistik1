# Vortrag 4: Sprechtext

Ausformulierter Sprechtext zu `Vortrag4_Praesentation.pptx`, Folie für Folie. Derselbe Text steht in den
Notizen der Präsentation (Referentenansicht). Reihenfolge der Personen wie in der Gruppenliste (kann getauscht werden).
Die Zeitangaben rechnen mit ruhigem Vortragstempo inklusive Pausen und Zeigen auf die Folien
(etwa 110 Wörter pro Minute). Reservefolien sind nicht eingerechnet.

- **Leorat Krasniqi (Sprecher/in 1):** Folien 1–5, rund 510 Wörter (etwa 4.6 Minuten)
- **Teoman-Doganay Lam (Sprecher/in 2):** Folien 6–10, rund 469 Wörter (etwa 4.3 Minuten)
- **Filip Lazic (Sprecher/in 3):** Folien 11–15, rund 508 Wörter (etwa 4.6 Minuten)

---

## Leorat Krasniqi (Sprecher/in 1)

### Folie 1: Titel

Guten Tag zusammen. Wir sind Leorat Krasniqi, Teoman-Doganay Lam und Filip Lazic, und unser Vortrag heisst «Das Berkeley-Paradoxon». Rechts sehen Sie schon die zwei Zahlen, um die sich heute alles dreht: 1973 wurden an der UC Berkeley 44.5 Prozent der Männer zugelassen, aber nur 30.4 Prozent der Frauen. Wir zeigen Ihnen in drei Teilen, was hinter diesen Zahlen steckt: zuerst Funktionen in Python, dann die Darstellung der scheinbaren Ungerechtigkeit und zum Schluss den genauen Vergleich mit dem Konzept der stochastischen Unabhängigkeit.

### Folie 2: Ausgangslage

Zur Ausgangslage: Im Herbst 1973 bewarben sich 4 526 Personen für ein Graduate-Studium in den sechs grössten Fachbereichen der Universität, die wir A bis F nennen. Weil insgesamt deutlich weniger Frauen zugelassen wurden, befürchtete die Universität eine Klage wegen Diskriminierung. Tabelle 4 unserer Aufgabe zeigt für jeden Fachbereich die Zulassungsquote von Frauen und Männern und wie sich die Bewerbungen auf die Fachbereiche verteilen. Unsere Aufgabe hat drei Teile: (a) Funktionen in Python erklären, (b) die Ungerechtigkeit so darstellen, dass man sie auf einen Blick sieht, und (c) die Verteilungen vergleichen und dabei die stochastische Unabhängigkeit prüfen. Die zentrale Frage lautet also: Wurden Frauen bei der Zulassung tatsächlich benachteiligt?

### Folie 3: Kapitel (a)

Wir beginnen mit Teil (a). Bevor wir die Daten analysieren, zeigen wir das Werkzeug, mit dem wir unseren ganzen Code organisiert haben: Funktionen.

### Folie 4: Funktionen: Grundlagen

Eine Funktion kann man sich wie eine Maschine vorstellen: Zutaten rein, Ergebnis raus. Man baut sie einmal und kann sie beliebig oft benutzen. Darum sagt McKinney: Was man mehr als einmal braucht, gehört in eine Funktion. Mit def bauen wir die Maschine, mit return kommt das Ergebnis heraus. Fehlt return, kommt None heraus, also nichts. Die Zutaten heissen Argumente. Positionsargumente muss man immer angeben. Keyword-Argumente haben eine Voreinstellung: Bei unserer Funktion vierfeldertafel steht fachbereich auf None. Ohne Angabe rechnet sie mit allen Bewerbungen, mit fachbereich gleich A nur mit Fachbereich A. Was in der Funktion passiert, bleibt dort, wie in einer geschlossenen Küche: Die Variable bewerbungen gibt es nur während des Aufrufs. Das ist der lokale Namensraum, darum vermeiden wir globale Variablen. Und unten: kennzahlen gibt scheinbar zwei Werte zurück. In Wahrheit ist es ein Paket, ein Tupel, das wir in quote und anteil auspacken. Für die Frauen in Fachbereich A ergibt das 82.4 und 5.9 Prozent.

### Folie 5: Funktionen als Objekte, Lambda, yield

Vier weitere Konzepte. Erstens: Funktionen sind Objekte. Wir legen sie wie Stationen eines Fliessbands in eine Liste. Jeder Wert aus Tabelle 4 läuft durch: Leerzeichen weg, Prozentzeichen weg, in eine Zahl umwandeln. So wird aus dem Text «82.4%» die Zahl 0.824. Zweitens: Ein Lambda ist eine Mini-Funktion in einer Zeile, bei uns für die Prozentanzeige. Mit partial bauen wir eine vorprogrammierte Taste: derselbe Test, nur fest mit einem Signifikanzniveau von 1 Prozent. Das nennt man Currying. Drittens: Ein Generator funktioniert wie ein Pez-Spender. Mit yield gibt er ein Ergebnis nach dem anderen heraus, Fachbereich für Fachbereich, immer erst, wenn man es braucht. Viertens: try und except sind ein Sicherheitsnetz. Tippt man zum Beispiel 82,4 mit Komma, gibt es eine klare Fehlermeldung statt einer falschen Zahl. Andere Fehler fangen wir bewusst nicht ab, sie sollen sichtbar bleiben. Damit übergebe ich an Teoman.

## Teoman-Doganay Lam (Sprecher/in 2)

### Folie 6: Kapitel (b)

Danke. Ich übernehme Teil (b). Ein Schwerpunkt der Aufgabe liegt auf den Vorüberlegungen zur programmtechnischen Umsetzung. Deshalb zeige ich zuerst, wie wir die Umsetzung geplant haben, und danach, wie die Ungerechtigkeit auf einen Blick aussieht.

### Folie 7: Vorüberlegungen zur Umsetzung

Vor dem Programmieren haben wir vier Fragen geklärt. Erstens die Daten: Tabelle 4 enthält nur Prozente. Für Wahrscheinlichkeiten wie P(W) und für den Chi-Quadrat-Test brauchen wir aber Anzahlen. Diese übernehmen wir aus dem Originaldatensatz von Bickel und Kollegen aus dem Jahr 1975. Unser Code prüft, dass diese Anzahlen alle Werte aus Tabelle 4 reproduzieren, und findet null Abweichungen. Zweitens die Kontrolle: Mit dem Satz der totalen Wahrscheinlichkeit rechnen wir aus den Fachbereichen die Zeile «Total» nach. Drittens die Struktur: ein langes DataFrame mit einer Zeile pro Fachbereich, Geschlecht und Entscheid. Daraus bauen wir jede Kreuztabelle mit pivot_table. Viertens: Alles, was wir mehrmals brauchen, wird eine Funktion, für die Gesamtbetrachtung und für jeden der sechs Fachbereiche. Unten die Libraries: pandas für Tabellen, numpy zum Rechnen, matplotlib für die Grafiken und scipy.stats für den Chi-Quadrat-Test. pandas ist der Standard für Tabellendaten, McKinney ist übrigens selbst der Autor. Mit matplotlib haben wir volle Kontrolle über Farben und Beschriftungen und können die Grafiken für Ausarbeitung und Folien exportieren. Und scipy liefert einen geprüften Chi-Quadrat-Test, statt dass wir die Formel selbst programmieren und Fehler riskieren. Alle vier Libraries sind in Anaconda enthalten, es braucht also keine zusätzliche Installation.

### Folie 8: Die scheinbare Ungerechtigkeit

Damit ein Betrachter die Ungerechtigkeit schnell erkennt, reicht ein einziger Vergleich: die Gesamtquote. Wir verwenden ein Balkendiagramm mit Nullachse, weil man Längen am genauesten vergleichen kann, und beschriften die Werte direkt. Wir zeigen bewusst nur zwei Balken, jede weitere Information würde von der Kernaussage ablenken. Die Farben bleiben in allen Diagrammen gleich, Rot für Frauen und Blau für Männer, so muss man nie die Legende suchen. Männer wurden zu 44.5 Prozent zugelassen, Frauen nur zu 30.4 Prozent. Das ist eine Differenz von 14.2 Prozentpunkten, die Quote der Männer ist rund 1.47-mal so hoch. Anders gesagt: Mit der Quote der Männer wären 817 statt 557 Frauen zugelassen worden. Also Diskriminierung? Genau das prüfen wir in Teil (c).

### Folie 9: Kapitel (c)

Damit kommen wir zu Teil (c). Die Gesamtquote fasst alle sechs Fachbereiche zusammen. Jetzt schauen wir genauer hin, Fachbereich für Fachbereich.

### Folie 10: Je Fachbereich: kein Nachteil für Frauen

Und hier kippt das Bild. In vier von sechs Fachbereichen haben Frauen die höhere Zulassungsquote, nämlich in A, B, D und F. In Fachbereich A sogar um 20.3 Prozentpunkte. Nur in C und E liegen die Männer leicht vorne, mit 2.8 und 3.8 Prozentpunkten. Diese Unterschiede sind klein, der Unterschied in A dagegen ist gross, und zwar zugunsten der Frauen. Übrigens zeichnet dieses Diagramm dieselbe Funktion wie das Diagramm zur Verteilung der Bewerbungen auf der nächsten Folie, nur mit anderen Spalten. In den Fachbereichen, die über die Zulassung entscheiden, sehen wir also keinen Nachteil für Frauen. Wie passt das zur Gesamtquote? Das erklärt Filip.

## Filip Lazic (Sprecher/in 3)

### Folie 11: Frauen wählten selektivere Fachbereiche

Danke. Die Antwort liegt darin, wo sich Frauen und Männer beworben haben. 51.5 Prozent der Männer bewarben sich in A oder B, also in Fachbereichen, in denen rund 64 Prozent zugelassen werden. Von den Frauen waren es nur 7.2 Prozent. Allein in Fachbereich A bewarben sich 825 Männer, aber nur 108 Frauen. 92.8 Prozent der Frauen bewarben sich in C bis F, wo die Quoten nur zwischen 6 und 35 Prozent liegen. Im Diagramm sehen Sie das: Bei A und B dominieren die blauen Balken der Männer, bei C bis F die roten Balken der Frauen.

### Folie 12: Mehr Bewerberinnen, tiefere Zulassungsquote

Hier fassen wir das pro Fachbereich zusammen: auf der x-Achse der Frauenanteil unter den Bewerbungen, auf der y-Achse die Zulassungsquote des Fachbereichs. Die Punktfläche entspricht der Anzahl Bewerbungen. Das Muster ist deutlich: Je höher der Frauenanteil, desto tiefer die Zulassungsquote. Die Korrelation beträgt r gleich minus 0.79. Frauen haben sich also häufiger in Fachbereichen beworben, die stark umkämpft sind.

### Folie 13: Die Erklärung: totale Wahrscheinlichkeit

Warum führt das zur tieferen Gesamtquote? Wegen des Satzes der totalen Wahrscheinlichkeit. Die Gesamtquote eines Geschlechts ist ein gewichteter Mittelwert der Quoten in den Fachbereichen, und die Gewichte sind die Anteile der Bewerbungen. Für die Frauen heisst das: 5.9 Prozent mal 82.4 Prozent plus 1.4 Prozent mal 68 Prozent und so weiter, das ergibt 30.4 Prozent. Frauen haben ihre grossen Gewichte bei den tiefen Quoten, Männer bei den hohen. Was passiert, wenn wir für beide Geschlechter dieselben Gewichte einsetzen, nämlich die Verteilung aller Bewerbungen? Dann liegt die Quote der Frauen bei 43.0 Prozent und die der Männer bei 38.7 Prozent. Der Unterschied kehrt sich um. Im Code ist das derselbe Aufruf der Funktion gesamtquote, nur mit anderen Gewichten.

### Folie 14: Stochastische Unabhängigkeit

Jetzt zur stochastischen Unabhängigkeit. Zwei Ereignisse sind unabhängig, wenn P von Z geschnitten W gleich P von Z mal P von W ist, oder gleichwertig: wenn P von Z gegeben W gleich P von Z ist. Z heisst «zugelassen», W heisst «Bewerbung einer Frau». Insgesamt beobachten wir 0.1231, bei Unabhängigkeit müssten es 0.1572 sein. Der Chi-Quadrat-Test bestätigt das mit einem Wert von 92.2 und einem p-Wert unter 0.001. Insgesamt sind Zulassung und Geschlecht also abhängig. Innerhalb der Fachbereiche B bis F liegen die Werte aber sehr nahe beieinander, alle p-Werte sind grösser als 0.3. Dort können wir die Unabhängigkeit nicht verwerfen. Nur in Fachbereich A gibt es eine Abhängigkeit, und zwar zugunsten der Frauen. Man spricht von bedingter Unabhängigkeit gegeben den Fachbereich. Der Fachbereich ist die Drittvariable, auch Confounder genannt.

### Folie 15: Fazit

Zum Fazit. Die Drittvariable Fachbereich kehrt den Zusammenhang um, das ist das Simpson-Paradoxon. Aggregiert sind Zulassung und Geschlecht abhängig, 30.4 gegen 44.5 Prozent. Je Fachbereich gibt es keinen Nachteil für Frauen. Die Ursache ist, dass sich Frauen häufiger in stark umkämpften Fachbereichen beworben haben. Wir müssen aber auch die Grenzen nennen: Es sind Beobachtungsdaten eines einzigen Jahres, und warum Frauen diese Fachbereiche gewählt haben, können die Daten nicht beantworten. Programmtechnisch hat sich gezeigt: Mit denselben Funktionen konnten wir die Gesamtanalyse, alle sechs Fachbereiche und die Standardisierung rechnen. Unsere wichtigste Lehre: Aggregierte Quoten darf man erst dann als Ursache deuten, wenn man relevante Drittvariablen berücksichtigt hat.

## alle

### Folie 16: Quellen · Fragen?

Vielen Dank für Ihre Aufmerksamkeit. Rechts sehen Sie unsere Quellen. Wir freuen uns auf Ihre Fragen.

---

## Reservefolien (nur bei Rückfragen)

### Folie 18: Reserve: Gesamtquote als gewichteter Mittelwert (Filip Lazic (Sprecher/in 3), bei Rückfrage zu Folie 13)

Diese Tabelle rechnet die Gesamtquote vor. In jeder Zeile multiplizieren wir den Anteil der Bewerbungen mit der Zulassungsquote. Das ergibt den Beitrag des Fachbereichs. Bei den Frauen liegen die grossen Gewichte bei C bis F, zusammen 92.8 Prozent, und dort sind die Quoten tief. Darum ergibt die Summe nur 30.4 Prozent. Bei den Männern liegen 51.5 Prozent der Gewichte bei A und B mit hohen Quoten, die Summe ergibt 44.6 Prozent. Dass es nicht genau 44.5 sind, ist nur ein Rundungseffekt von Tabelle 4.

### Folie 19: Reserve: So funktioniert der Chi-Quadrat-Test (Filip Lazic (Sprecher/in 3), bei Rückfrage zu Folie 14)

So funktioniert der Chi-Quadrat-Test. Die Nullhypothese lautet: Zulassung und Geschlecht sind unabhängig. Dann erwarten wir in jeder Zelle n mal P von Z mal P von W. Für zugelassene Frauen wären das 711.5, beobachtet sind aber nur 557. Die Teststatistik summiert über alle vier Zellen die quadrierte Abweichung geteilt durch den erwarteten Wert. Das ergibt 92.2. Bei einem Freiheitsgrad liegt der kritische Wert für 5 Prozent bei 3.84. Wir verwerfen die Nullhypothese also klar. Im Code genügt ein einziger Aufruf: chi2_contingency.

### Folie 20: Reserve: Der Fachbereich als Drittvariable (Filip Lazic (Sprecher/in 3), bei Rückfrage zu Folie 14 oder bei der Frage nach Kausalität)

Hier sieht man die Struktur des Problems. Das Geschlecht hängt stark mit der Wahl des Fachbereichs zusammen, Chi-Quadrat 1 068.4. Und der Fachbereich hängt stark mit der Zulassung zusammen, Chi-Quadrat 778.9. Der direkte Effekt des Geschlechts auf die Zulassung ist innerhalb der Fachbereiche kaum vorhanden. Der Fachbereich ist also der Confounder, der den Zusammenhang insgesamt erzeugt. Korrelation ist nicht Kausalität.

### Folie 21: Reserve: Ablauf des Programms (Teoman-Doganay Lam (Sprecher/in 2), bei Rückfrage zu Folie 7, falls nach dem Aufbau des Codes gefragt wird)

Hier sieht man den Ablauf unseres Programms in fünf Schritten. Erstens erfassen wir Tabelle 4 als Text und bereinigen sie mit einer Liste von Funktionen. Zweitens prüfen wir sie mit dem Satz der totalen Wahrscheinlichkeit. Drittens laden wir die Originalanzahlen in ein langes DataFrame und prüfen sie gegen Tabelle 4. Viertens analysieren wir mit denselben Funktionen gesamt und je Fachbereich. Fünftens zeichnen wir die Diagramme mit einer festen Farbe pro Geschlecht. Dahinter stehen drei Prinzipien: Jeder wiederholte Schritt ist eine Funktion, wir verwenden kein global, und Fehler werden durch try/except und zwei Gegenproben sofort sichtbar.
