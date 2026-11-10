# Checkliste: Experiment-Qualität

Prüfe die fertige Formulierung Punkt für Punkt. Mangelhafte Punkte dem Nutzer konkret benennen (Abschnitt + was fehlt).

**N/A-Regel:** Jeder Punkt ist Pflicht. Trifft ein Punkt auf dieses Experiment nicht zu, im Dokument mit `[n/a: Grund]` markieren — nie stillschweigend weglassen.

**Kurzmodus** (`Typ: nicht-bestätigend (Kurzmodus)`, bei niedriger Entscheidungshöhe): Pflicht sind nur Hypothese, Primärkriterium mit Schwellwert, Guardrails, alle drei Entscheidungsäste und Rollback-Bedingungen. Alle übrigen Punkte dürfen `[n/a: Kurzmodus]` erhalten. Ergebnisse aus dem Kurzmodus gelten nicht als bestätigende Evidenz.

## Kern-Check (jedes Experiment)

### Versuchsanordnung: Situation, Problem
- [ ] Situation ist beschreibbar, ohne dass der Leser den Kontext kennen muss.
- [ ] Das Problem/Herausforderung ist als konkrete Schwierigkeit formuliert, nicht als Wunsch.
- [ ] Beteiligte Personen/Personengruppen sind benannt (Rollen oder Namen), nicht nur „das Team".
- [ ] Population / Randomisierungseinheit ist definiert (wer ist eligible; die unabhängige Einheit).

### Veränderung von Einflussgrößen: Lösung
- [ ] Die Veränderung ist so konkret, dass ein Dritter sie exakt umsetzen kann (Parameter, Werte, Texte, Abläufe).
- [ ] Es ist eindeutig, was NICHT geändert wird (der Rest der Situation bleibt unverändert).
- [ ] Feinjustierung ist explizit erlaubt oder verboten; bei Erlaubnis: Regeln, Entscheidungsträger, Obergrenze.

### Zugrundeliegende Hypothese
- [ ] Ein falsifizierbarer Satz im Wenn/Dann/Weil-Format: „Wenn X, dann Y messbar an Z, weil W."
- [ ] Erfolg ist quantitativ oder zumindest objektiv beobachtbar — mit Schwellwert, nicht „verbessert".
- [ ] Der Mechanismus („weil") ist benannt und durch Evidenz gestützt oder prüfbar — keine bloße Behauptung.
- [ ] Motivation/Fragestellung ist getrennt vom Hypothesensatz formuliert.
- [ ] Baseline/Kontrolle ist benannt (inkl. Wert aus relevanter Historie — oder, falls keine existiert, Plan zur Baseline-Messung vor Start).
- [ ] Es sind explizite Nicht-Behauptungen formuliert (z. B. Generalisierungsgrenzen).

### Neben- & Gegenthesen
- [ ] Min. eine flankierende Hypothese oder alternative Annahme vorhanden.
- [ ] Min. eine Antithese/Risiko-Perspektive vorhanden (wer sieht das Risiko, welches Szenario?).
- [ ] Es ist klar, was passiert, wenn die Hauptthese widerlegt wird (Weg zu Alternativ-Annahmen).

### Auswertung
- [ ] Laufzeit/Endpunkt ist festgelegt (Datum oder Bedingung).
- [ ] Mindestens ein objektives Bewertungskriterium mit Schwellwert (Zahl, Skala, Fragebogen, Rubrik/Kodierschema).
- [ ] Guardrails sind deklariert (was darf sich nicht über eine Grenze hinaus verschlechtern), damit ein „Sieg" keinen Kollateralschaden verdecken kann.
- [ ] Sekundär- und Diagnose-Ergebnisse sind gelistet; Diagnose-Ergebnisse sind explizit nicht Entscheidungsgrundlage.
- [ ] Alle drei Entscheidungsäste (Sieg/Niederlage/Unentschieden) sind geschrieben, jeweils mit konkreter Aktion.
- [ ] Beobachterunabhängigkeit ist adressiert (z. B. blinde Auswertung, Standard-Fragebogen, automatische Messung).
- [ ] Fehler-/Ausschlussregeln sind vorab deklariert („keine ex-post-Ausschlüsse").
- [ ] Nachvollziehbarkeit: Datenquelle/Protokoll ist definiert, sodass ein anderer die Auswertung wiederholen könnte.
- [ ] Störfaktoren/Variablen sind benannt und für jede ein Umgang (konstant halten, messen, kontrollieren) existiert.

### Hinweise zur Experiment-Durchführung
- [ ] Konsequenzen des Experiments (Erfolg UND Misserfolg) sind genannt.
- [ ] Rollback-Bedingungen sind explizit: wann wird zurückgerollt, wer entscheidet.
- [ ] Doku-Plan existiert: was wird wann dokumentiert (Versuchsprotokoll?), und eine verantwortliche Person ist benannt.
- [ ] Ausführungsvertrag: Version/Stand aller beteiligten Artefakte ist dokumentiert (bei technischen Experimenten Commits/Digests von Code, Umgebung, Modell, Evaluator, Auswertungsskript); eindeutiges Lauf-/Durchgangs-Schema.
- [ ] Der Änderungs-Pfad ist verstanden (neue Version, alte Läufe reklassifiziert), falls der Pilot sättigt oder scheitert.

### Global
- [ ] Kann jemand die Auswertung allein aus dem Dokument vorhersagen, bevor er die Ergebnisse sieht?
- [ ] Keine erfundenen Details: alle Lücken sind als `[offen: …]` markiert, nicht Zutreffendes als `[n/a: Grund]`.
- [ ] Das Experiment ist klein genug, in der Laufzeit abgeschlossen zu werden (sonst: Vorschlag zur Zerlegung).

## Statistik-Check (nur quantifizierende Designs, zusammen mit `statistik.md`)

- [ ] Die Größe in der „dann"-Klausel ist an eine Entscheidung gekoppelt (MDE = kleinste Wirkung, die unser Vorgehen ändert — nicht der hoffnungsvolle Lift).
- [ ] Die Dauer wurde *abgeleitet* (Stichprobe ÷ Traffic, ganze Wochen, Reifedauer) statt geraten; Zuweisungsziel und früheste verantwortbare Auswertung sind dokumentiert.
- [ ] Power-Analyse: alle vier Eingaben (MDE, α, Power, Stichprobe) sind festgelegt; Stichprobe zählt unabhängige Einheiten, nicht Zeilen.
- [ ] Sensitivitätsszenarien (optimistisch/erwartet/konservativ) sind berechnet.
- [ ] Die Stoppregel ist fix — und falls die Überwachung kontinuierlich ist, handelt es sich um ein gepowertes sequenzielles Design (kein Peeking).
- [ ] Es gibt genau eine Primärmethode; zusätzliche „Primärmetriken" sind als sekundär/explorativ gekennzeichnet, mit Multiplizitätsregel.
- [ ] Ein gescheiterter Überlegenheitstest wird nicht als Äquivalenz gelesen (falls Geschäftsfrage „nah genug beieinander?": Äquivalenz-Design mit expliziter Marge).
- [ ] Zugriffe sind eingefroren, nicht nur Dateien (welche Komponenten welche Daten sehen dürfen; abgerufene Artefakt-IDs loggen).
