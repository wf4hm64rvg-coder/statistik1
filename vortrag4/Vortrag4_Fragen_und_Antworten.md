# Vortrag 4: Sprecherplan und mögliche Fragen der Lehrperson

Vorbereitung auf den Vortrag (Aufgabe 4, UC Berkeley 1973). Alle Zahlen stammen aus
`Vortrag4_Berkeley_Analyse.ipynb` und wurden nachgerechnet.

## 1. Sprecherplan

Reihenfolge wie in der Gruppenliste (kann getauscht werden). Jeder Teil dauert etwa 5 Minuten.

| Teil | Folien | Inhalt | Zeit |
|---|---|---|---|
| Leorat Krasniqi | 1–5 | Titel, Ausgangslage, Kapitel (a), Funktionen in Python | 5 Min. |
| Teoman-Doganay Lam | 6–10 | Kapitel (b), Vorüberlegungen, scheinbare Ungerechtigkeit, Kapitel (c), Quoten je Fachbereich | 5 Min. |
| Filip Lazic | 11–15 | Verteilung der Bewerbungen, Streudiagramm, totale Wahrscheinlichkeit, stochastische Unabhängigkeit, Fazit | 5 Min. |
| alle | 16 | Quellen, Fragen | – |

Die Kapiteltrenner (Folien 3, 6, 9) dauern nur ein paar Sekunden. Sie markieren den Übergang
zum nächsten Teil.

Der Vortrag dauert 15 Minuten (3 × 5) und endet mit Folie 16. Mit dem Sprechtext kommt ihr auf
knapp 14 Minuten, also bleibt etwas Puffer.

**Reservefolien 17–21 nur bei Rückfragen:** Sie werden nicht vorgetragen. Fragt die Lehrperson
nach, springt ihr direkt zur passenden Folie.

| Reservefolie | Passt zur Frage nach … | Wer |
|---|---|---|
| 18 Gesamtquote als gewichteter Mittelwert | Folie 13: Wie kommt die Gesamtquote zustande? | Filip Lazic |
| 19 So funktioniert der Chi-Quadrat-Test | Folie 14: Wie funktioniert der Test? | Filip Lazic |
| 20 Der Fachbereich als Drittvariable | Folie 14: Ist das Kausalität / Diskriminierung? | Filip Lazic |
| 21 Ablauf des Programms | Folie 7: Wie ist euer Code aufgebaut? | Teoman-Doganay Lam |

**Tipp:** Jede Person sollte den ganzen Vortrag erklären können. Die Lehrperson kann jede
Frage an jede Person richten.

---

## 2. Fragen zu (a): Funktionen in Python

**Was gibt eine Funktion ohne `return` zurück?**
`None`. Python gibt am Ende jeder Funktion automatisch `None` zurück, wenn kein `return`
erreicht wird.

**Was ist der Unterschied zwischen Positions- und Keyword-Argumenten?**
Positionsargumente werden über ihre Reihenfolge zugeordnet. Keyword-Argumente werden über ihren
Namen übergeben und haben oft einen Standardwert. Keyword-Argumente müssen nach den
Positionsargumenten stehen. Beispiel aus unserem Code: `vierfeldertafel(daten, fachbereich="A")`.
Ohne `fachbereich` gilt der Standardwert `None`, dann wird die Tafel über alle Fachbereiche gebildet.

**Kann eine Funktion wirklich mehrere Werte zurückgeben?**
Nein. Sie gibt ein einziges Tupel zurück, das beim Aufruf entpackt wird:
`quote, anteil = kennzahlen(89, 19, 1835)`. Bei vielen Werten nehmen wir ein Dictionary
(`pruefe_unabhaengigkeit` liefert neun Kennzahlen). Dann sind die Werte über ihren Namen
ansprechbar, z. B. `ergebnis["p-Wert"]`.

**Warum verwendet ihr keine globalen Variablen?**
Eine Funktion, die globale Variablen verändert, hat versteckte Nebenwirkungen. Ihr Ergebnis
hängt dann von der Reihenfolge ab, in der die Notebook-Zellen ausgeführt wurden. McKinney rät
deshalb von `global` ab. Bei uns bekommen alle Funktionen ihre Daten als Argument und geben das
Ergebnis mit `return` zurück. Konstanten wie `FARBEN` lesen wir nur, wir verändern sie nie.

**Was heisst „Funktionen sind Objekte“? Wo nutzt ihr das?**
Funktionen kann man in Listen speichern, Variablen zuweisen und anderen Funktionen übergeben.
Wir legen die Bereinigungsschritte als Liste `[str.strip, entferne_prozentzeichen, in_anteil]` ab.
`bereinige()` wendet sie nacheinander auf jeden Tabellenwert an. Ausserdem übergeben wir
`balken_beschriften()` die Formatierung als Funktion.

**Was ist ein Lambda? Wann ist es sinnvoll?**
Ein Lambda ist eine anonyme Funktion aus einem einzigen Ausdruck, z. B.
`prozent = lambda x: f"{x:.1%}"`. Es lohnt sich, wenn man einer anderen Funktion eine kleine
Funktion übergibt, etwa `ax.yaxis.set_major_formatter(lambda y, _: f"{y:.0%}")`. Für
längere Logik nimmt man besser `def`, weil das lesbarer ist und einen Namen hat.

**Was ist Currying bzw. `partial`?**
Man erzeugt eine neue Funktion, indem man einige Argumente einer bestehenden Funktion festlegt:
`pruefe_streng = partial(pruefe_unabhaengigkeit, alpha=0.01)`. Damit haben wir geprüft, ob die
Ergebnisse auch bei einem Signifikanzniveau von 1 % gleich bleiben. Das ist der Fall.

**Warum ein Generator? Eine Liste hätte doch auch gereicht.**
Bei sechs Fachbereichen bringt der Generator kaum Speichervorteile. Er zeigt das Konzept aus 3.2:
Die Funktion arbeitet erst, wenn ein Wert angefordert wird (Lazy Evaluation). Bei sehr vielen
Gruppen oder grossen Daten spart das Speicher, weil nie alle Ergebnisse gleichzeitig im
Speicher liegen müssen.

**Warum fangt ihr nur `ValueError` ab und nicht alle Fehler?**
Ein Tippfehler in der Tabelle, z. B. `"82,4%"` mit Komma, führt bei `float()` zu einem
`ValueError`. Wir melden ihn mit einer verständlichen Meldung. Andere Fehler wie ein `TypeError`
deuten auf einen echten Programmierfehler hin und sollen nicht versteckt werden. Das empfiehlt
auch McKinney.

---

## 3. Fragen zur Umsetzung und zu den Libraries

**Tabelle 4 enthält nur Prozente. Woher stammen die Anzahlen?**
Aus dem Originaldatensatz von Bickel et al. (1975), der in R als `UCBAdmissions` verfügbar ist:
1 835 Bewerbungen von Frauen und 2 691 von Männern. Ein Rückrechnen aus den gerundeten Prozenten
wäre ungenau. In Fachbereich B kämen z. B. 26 statt 25 Frauen heraus. Der Code prüft, dass die
Anzahlen alle 24 Prozentwerte von Tabelle 4 reproduzieren. Ergebnis: 0 Abweichungen.

**Wozu braucht ihr überhaupt Anzahlen?**
Für (b) und die Quoten je Fachbereich reichen Prozente. Für P(W), P(Z ∩ W) und den
Chi-Quadrat-Test braucht man absolute Häufigkeiten. Tabelle 4 sagt nämlich nicht, wie viele
Frauen und Männer sich insgesamt beworben haben.

**Warum ergibt eure Nachrechnung für Männer 44.6 % statt 44.5 %?**
Das ist ein Rundungseffekt. Tabelle 4 ist auf eine Nachkommastelle gerundet, und beim Summieren
von sechs gerundeten Produkten entsteht eine Abweichung von 0.1 Prozentpunkten. Mit den exakten
Anzahlen ergibt sich 44.52 %.

**Warum pandas, numpy, matplotlib und scipy?**
- **pandas:** Standard für Tabellendaten, `pivot_table` erzeugt jede Kreuztabelle in einer Zeile.
  McKinney ist selbst der Autor von pandas.
- **numpy:** Rechnet auf ganzen Spalten ohne Schleifen und ist die Grundlage von pandas.
- **matplotlib:** Volle Kontrolle über Farben, Beschriftung und den Export als PNG für
  Ausarbeitung und Folien.
- **scipy.stats:** Liefert mit `chi2_contingency` einen geprüften Chi-Quadrat-Test mit
  Teststatistik, p-Wert und erwarteten Häufigkeiten. So müssen wir die Formel nicht selbst
  programmieren und riskieren keine Fehler.

Alle vier sind in Anaconda enthalten, also braucht es keine zusätzliche Installation.

**Warum ein „langes“ DataFrame?**
Eine Zeile je Fachbereich × Geschlecht × Entscheid mit der Spalte `Anzahl`. Aus diesem einen
Format lässt sich jede benötigte Tabelle mit `pivot_table` bauen, gesamthaft oder für einen
einzelnen Fachbereich. Man muss nicht mehrere Tabellen von Hand pflegen.

**Warum Balkendiagramme und kein Kreisdiagramm?**
Längen auf einer gemeinsamen Nullachse kann das Auge am genauesten vergleichen. Ein
Kreisdiagramm zeigt Anteile an einem Ganzen, eignet sich aber nicht für den Vergleich zweier
Quoten. Die Farbe ist pro Geschlecht in allen Abbildungen gleich (Frauen orange, Männer blau),
damit man nicht jedes Mal die Legende lesen muss.

---

## 4. Fragen zu (b) und (c): Statistik

**Was bedeutet stochastische Unabhängigkeit?**
A und B sind unabhängig, wenn P(A ∩ B) = P(A) · P(B) gilt, gleichwertig P(A | B) = P(A) (für
P(B) > 0). Das Wissen, dass B eingetreten ist, ändert dann die Wahrscheinlichkeit von A nicht.
Bei uns: Insgesamt ist P(Z ∩ W) = 0.1231, bei Unabhängigkeit müsste es P(Z) · P(W) =
0.3878 · 0.4054 = 0.1572 sein. Insgesamt sind Zulassung und Geschlecht also abhängig.

**Sind „unabhängig“ und „disjunkt“ dasselbe?**
Nein, beinahe das Gegenteil. Disjunkte Ereignisse mit positiver Wahrscheinlichkeit sind immer
abhängig. Wenn A eintritt, kann B nicht mehr eintreten, also gilt P(B | A) = 0 ≠ P(B).

**Was ist das Simpson-Paradoxon?**
Ein Zusammenhang, der in jeder Teilgruppe gilt, verschwindet beim Zusammenfassen der Gruppen
oder kehrt sich sogar um. Ursache ist eine Drittvariable (Confounder), hier der Fachbereich.
Frauen haben in 4 von 6 Fachbereichen die höhere Quote, insgesamt aber die tiefere.

**Wie kann die Gesamtquote der Frauen tiefer sein, wenn sie in den meisten Fachbereichen höher ist?**
Die Gesamtquote ist ein gewichteter Mittelwert der Fachbereichsquoten (Satz der totalen
Wahrscheinlichkeit). 92.8 % der Frauen bewarben sich in C bis F mit Quoten von 6 % bis 35 %.
Von den Männern bewarben sich 51.5 % in A und B mit Quoten um 64 %. Die Frauen haben also ihre
grossen Gewichte bei den tiefen Quoten. Bei gleicher Fachbereichswahl (Standardisierung) läge
die Quote der Frauen bei 43.0 % und die der Männer bei 38.7 %.

**Was sagt der p-Wert aus?**
Er ist die Wahrscheinlichkeit, unter der Nullhypothese (Unabhängigkeit) eine mindestens so
grosse Abweichung zu beobachten wie in den Daten. Insgesamt ist p ≈ 8 · 10⁻²². Eine so grosse
Abweichung ist bei Unabhängigkeit praktisch unmöglich, also wird H₀ verworfen. Ein p-Wert ist
**nicht** die Wahrscheinlichkeit, dass H₀ wahr ist.

**Wie funktioniert der Chi-Quadrat-Test?**
Man berechnet für jede Zelle die bei Unabhängigkeit erwartete Häufigkeit E = n · P(Z) · P(W).
Bei zugelassenen Frauen wären das 711.5, beobachtet sind 557. Danach summiert man
(B − E)² / E über alle Zellen. Bei der Vierfeldertafel gibt es 1 Freiheitsgrad, der kritische
Wert für α = 5 % ist 3.84. Unser Wert: χ² = 92.2. Details stehen auf Reservefolie 19.

**Warum `correction=False`?**
Ohne Yates-Korrektur entspricht das Ergebnis genau der Formel aus der Vorlesung, man kann es
von Hand nachrechnen. Bei so grossen Anzahlen spielt die Korrektur kaum eine Rolle:
χ² = 91.6 statt 92.2, die Schlussfolgerung bleibt gleich.

**Ihr macht sechs Tests, eines davon ist signifikant. Ist das nicht Zufall?**
Gute Frage, das ist das Problem des multiplen Testens. Mit der Bonferroni-Korrektur prüft man
jeden Test auf α / 6 ≈ 0.83 %. Fachbereich A bleibt mit p < 0.001 klar signifikant, die
übrigen bleiben nicht signifikant (alle p > 0.3). Das Ergebnis ändert sich also nicht.

**Gibt es einen Test, der alle Fachbereiche gemeinsam berücksichtigt?**
Ja, der Cochran-Mantel-Haenszel-Test. Er prüft die bedingte Unabhängigkeit über alle
Fachbereiche hinweg. Mit unseren Daten ergibt er χ² ≈ 1.5 (p ≈ 0.22). Das gemeinsame
Chancenverhältnis Frauen zu Männern liegt bei 1.11. Gegeben den Fachbereich lässt sich also
kein Unterschied nachweisen. Dieser Test ist nicht Teil unseres Notebooks, er dient hier nur
als Ausblick.

**Warum ist Fachbereich A eine Ausnahme?**
In A wurden 82.4 % der Frauen zugelassen und 62.1 % der Männer. Das ist signifikant
**zugunsten** der Frauen. Allerdings bewarben sich dort nur 108 Frauen gegenüber 825 Männern.
Warum A so entschieden hat, können die Daten nicht beantworten. Mögliche Gründe wären
Qualifikation oder Förderprogramme, das wäre aber Spekulation.

**War das Zulassungsverfahren nun diskriminierend oder nicht?**
Die Fachbereiche, die über die Zulassung entschieden, benachteiligten Frauen nicht. Der
aggregierte Unterschied entsteht durch die Fachbereichswahl. Die Daten beweisen aber nicht,
dass es gar keine Ungleichbehandlung gab. Offen bleibt, **warum** Frauen sich vor allem in
überlaufenen Fachbereichen mit wenigen Plätzen bewarben. Gründe könnten die Finanzierung der
Fachbereiche oder gesellschaftliche Prägungen bei der Studienwahl sein. Ausserdem sind
Qualifikationen nicht erfasst, und es handelt sich um Beobachtungsdaten eines einzigen Jahres.
Kurz: Korrelation ist nicht Kausalität.

**Was hättet ihr mit mehr Zeit noch gemacht?**
Den Cochran-Mantel-Haenszel-Test oder eine logistische Regression (Zulassung ~ Geschlecht +
Fachbereich) direkt im Notebook umsetzen. Ausserdem Daten weiterer Jahre beiziehen, um zu
prüfen, ob das Muster stabil ist.
