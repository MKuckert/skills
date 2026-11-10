# Statistik: Beobachtungszeit, Auswertung, Integrität

Nur für quantifizierende Designs (A/B-Tests, Modell-/Methodenvergleiche mit numerischem Primärergebnis) laden. Die Kernidee: die Experiment-Aussage ist ein **vor der Beobachtung bestätigender Daten eingefrorener, versionierter Vertrag** — jemand, der sie liest, kann die Auswertung vorhersagen, bevor er die Ergebnisse sieht.

## 1. Hypothese: Präzision und Widerlegbarkeit

- **Wenn / Dann / Weil:** *Wenn* [konkrete Änderung], *dann* wird [Zielmetrik] sich um [erwartete Größe und Richtung] ändern, *weil* [Mechanismus / stützende Evidenz].
  - „Wenn" erzwingt **eine manipulierte Variable** (der kausale Kontrast), „dann" eine **quantifizierte, gerichtete Vorhersage** (nicht „es wird besser"), „weil" einen **prüfbaren Mechanismus** (trennt Diagnose von Vermutung).
- **Widerlegbar:** Es muss ein beobachtbares Ergebnis existieren, das die Hypothese widerlegt. „Der Agent ist besser in Mathematik" widerlegt nichts; „Methode A schlägt Baseline B um ≥ Δ auf der deklarierten Problemdistribution bei gleichem Gesamtbudget" ist widerlegbar.
- **Erst das Estimand schreiben:** Nenne die Größe, die geschätzt wird (z. B. Δ(b) = E[Q_A − Q_B] über die deklarierte Fall-Distribution). Das Schreiben zwingt verdeckte Entscheidungen ins Blickfeld: Welche Distribution liefert die Fälle? Zählt das Budget Inferenz und Ausführung? Wie werden fehlgeschlagene Läufe dargestellt?
- **Ein Primärvergleich:** Wähle einen Primärkontrast (eine Behandlung vs. eine Kontrolle). Weitere Kontraste sind sekundär/explorativ und als solche gekennzeichnet, mit deklarierter Multiplizitätsregel.
- **Deklarieren, was NICHT behauptet wird** (z. B. „absolute Fähigkeit", „Generalisierung über diese Aufgabenfamilie hinaus").

## 2. Bestimmung der Beobachtungszeit (Dauer / Stichprobenbudget)

Die Beobachtungszeit wird **abgeleitet, nicht gewählt**. Kette: Effektgröße → benötigte Stichprobe → Traffic-Rate → Kalenderdauer, dann auf volle Zyklen gerundet.

### 2.1 Power-Analyse: die vier gekoppelten Eingaben

Für einen Standard-Zwei-Gruppen-Test fixiere drei davon und löse nach der vierten auf:

| Eingabe | Bedeutung | Typischer Standardwert |
|---|---|---|
| **Effektgröße / MDE** | Kleinste wahre Differenz, die das Design erkennen soll — „die kleinste Wirkung, die die Entscheidung ändert", nicht „der Lift, den wir hoffen zu sehen" | Geschäftsurteil |
| **α (Signifikanzniveau)** | Tolerierte Falsch-Positiv-Rate unter der Nullhypothese | 0,05 zweiseitig |
| **Power (1−β)** | Wahrscheinlichkeit, den angegebenen Effekt zu erkennen, wenn er real ist | 0,80 |
| **Stichprobengröße** | Anzahl *unabhängiger* Experimenteinheiten pro Arm | wird gelöst |

Wichtige Warnungen:

- **Power ist nicht die Wahrscheinlichkeit, dass die Hypothese wahr ist.** Ein Test mit 80 % Power erkennt einen realen Effekt in MDE-Größe bei wiederholten Läufen ~80 % der Zeit.
- **Stichprobe = unabhängige Einheiten, nicht Zeilen.** Randomisierst du Nutzer, zähle Nutzer — keine Sessions, Klicks oder Käufe. Cluster-randomisierte Designs (Firmen, Klassenzimmer) brauchen clusterbewusste Größenbestimmung; die effektive Stichprobe liegt näher an der Anzahl der Cluster.
- **Effektgrößen-Parameterisierung zum Test passen.** Ein relativer Lift, der in einen Anteils-Rechner gesteckt wird, liefert eine präzise, aber sinnlose Zahl.
- **Richtige Baseline wählen.** Eine siteweite Rate ist eine schwache Baseline für ein Experiment, das nur neuen Mobilnutzern gezeigt wird. Historie mit derselben Metrikdefinition, derselben Eligibilitätsregel und derselben Analyseeinheit ziehen; Wochenmuster prüfen.
- **Szenario-Sensitivität rechnen.** Mindestens drei MDE-Fälle berechnen (optimistisch / erwartet / konservativ). Braucht der konservative Fall 12 Wochen und du hast 4, ist das wertvolle Information: Metrik ändern, Population ändern oder den Test nicht fahren.

Beispielrechnung (zwei Anteile): Kontrolle 20 %, kleinste lohnenswerte Wirkung 22 % (absolute MDE 2 pp, relativ 10 %), α = 0,05 zweiseitig, Power 0,80, gleiche Aufteilung → ≈ 6.500 Nutzer pro Arm (~13.000 gesamt). Bei 4.000 eligible Nutzern/Woche *insgesamt* (auf beide Arme verteilt) sind das ≥3,25 Wochen Rekrutierung *vor* Hinzurechnung der Ergebnis-Reifedauer (z. B. 7-Tage-Aktivierung) und Ausschlüssen.

### 2.2 Von der Stichprobe zur Kalenderdauer

Dauer = (benötigte Stichprobe pro Arm ÷ eligible Traffic pro Arm pro Tag), dann anpassen für:

- **Volle Geschäftszyklen.** Nach *oben* auf ganze Wochen runden. Wochentagseffekte sind real: ein 4-Tage-Test, der zufällig ein Montag–Donnerstag-Fenster spannt, ist verzerrt. Daumenregel: **mindestens eine volle Woche, zwei sicherer**, und nie mitten im Zyklus stoppen.
- **Verzögerte Ergebnisse.** Eine 7-Tage-Aktivierungsmetrik braucht 7 Tage Reife, nachdem der letzte Nutzer rekrutiert ist.
- **Ausschlüsse und Latenz.** Targeting-Filter, Bot-Filterung, fehlende Identifikatoren, Datenlatenz.
- **Traffic-Aufteilung.** Nur der Trafficanteil zählt, der tatsächlich diesem Experiment zugewiesen ist.

Sowohl das **Zuweisungsziel** (Stichprobengröße) als auch das **früheste verantwortbare Auswertungsdatum** dokumentieren.

### 2.3 Fixer Horizont vs. sequenzielle Überwachung (das Peek-Problem)

- Eine Fix-Horizont-Berechnung setzt voraus, dass du **einmalig am geplanten Endpunkt** auswertest. Wiederholtes Prüfen eines konventionellen p-Werts und Stoppen, sobald er 0,05 unterschreitet, bläht Falsch-Positive dramatisch auf: ein Test ohne wahren Effekt, der zwei Wochen täglich gelesen und am ersten signifikanten Tag gestoppt wird, zeigt ~25 % der Zeit Signifikanz statt 5 %.
- **Falsche Antwort:** „fahren, bis das Dashboard Signifikanz zeigt." Richtige Antwort: bis zur vorab berechneten Stichprobe/Dauer fahren, oder ein **gültiges sequenzielles Design** (immer-gültige p-Werte / Alpha-Spending) verwenden, das für die *tatsächliche* Entscheidungsprozedur gepowert ist — und vorab spezifizieren.
- **Frühes Stoppen bei positiven Ergebnissen ist verzerrt.** Wenn du nach drei Niederlagen weitergefahren hättest, begünstigt Stoppen nach drei Siegen positive Evidenz. Entweder ein gültiges sequenzielles Design vorab deklarieren oder den fixen Plan vollständig abwarten.

### 2.4 Phasen: Exploration → Pilot → Protokoll-Freeze → Bestätigung

1. **Exploration** — Beispiele inspizieren, Tooling reparieren, plausible Baselines auswählen. Keine bestätigenden Behauptungen.
2. **Pilot (Entwicklungsdaten)** — Laufzeit, Varianz, Sättigung und Fehlerquoten schätzen; prüfen, dass die Metrik Methoden *unterscheiden* kann (sättigt jede Baseline sofort, ist die Metrik nutzlos — jetzt ändern). Setzt auch realistische Budgets/Kosten.
3. **Protokoll-Freeze** — Metrik, Splits, Budgets, Seeds, Auswertungsskript und Stoppregel fixieren; Hashes/Commits/Digests sowie wer genehmigt hat, dokumentieren.
4. **Bestätigung** — den eingefrorenen Vergleich fahren, ausschließlich mit der deklarierten Methode auswerten.

Die Pilot-Ergebnisse speisen die Power-Zahlen (Varianzschätzung, realistischer Traffic) — deshalb wird die Beobachtungszeit *nach* dem Pilot, aber *vor* der Bestätigung finalisiert.

**Änderungen sind erlaubt, aber versioniert.** Zeigt ein Pilot einen defekten Checker oder ein unmögliches Budget, ändere das Protokoll, erkläre warum, klassifiziere die alten Läufe als explorativ und friere eine neue Version vor der betreffenden Auswertung ein. Das eingefrorene Manifest nie an Ort und Stelle bearbeiten.

### 2.5 Andere Designs (wenn es keine Behandlungs-gegen-Kontroll-Aufteilung gibt)

- **Ein-Stichprobe / Vorher-Nachher.** Vergleich einer Bedingung mit einem bekannten oder historischen Benchmark („schlägt das neue Modell 80 % auf dieser Suite?") wird mit der Einstichprobenformel dimensioniert: n = ((z_{α/2} + z_β)·σ / δ)² für einen Mittelwert, bzw. das Ein-Anteil-Äquivalent für eine Rate. Ein historischer Benchmark ist schwächer als eine konkurrierende Kontrolle (Drift, Saisonalität) — das explizit sagen und wo möglich einen konkurrierenden Holdout fahren.
- **Gematchte / gepaarte Designs.** Paaren (z. B. gleiche Aufgabe + Seed unter beiden Armen) reduziert die Varianz; dimensionieren auf der *Differenz*-Verteilung mit dem gepaarten Test, nicht der marginalen.
- **Qualitative / explorative Studien.** Power-Analyse greift nicht. Dimensionieren nach *Sättigung* (weiter rekrutieren, bis keine neuen Themen/Fälle mehr auftauchen) und die Sättigungs-Stoppregel plus die Auswertungsmethode (Kodierschema, Inter-Rater-Check) vorab deklarieren. Im Template „benötigte Stichprobe" durch die Sättigungsregel ersetzen und die Studie als nicht-bestätigend kennzeichnen, es sei denn, sie ist mit einem bestätigenden Design gekoppelt.

## 3. Auswertung entwerfen

### 3.1 Metrik-Hierarchie (alle vor dem Launch deklarieren)

| Klasse | Rolle | Beispiel |
|---|---|---|
| **Primärergebnis** | Die eine Entscheidungs-Metrik, am nächsten am Wirkmechanismus der Behandlung | offizielle Lösungsrate; 7-Tage-Aktivierung |
| **Kleinste praktisch relevante Wirkung (SESOI/MDE)** | Die Schwelle, die zählt, in absoluten Werten | ≥2 pp Verbesserung |
| **Sekundärergebnisse** | Wichtig, aber nicht entscheidend | Tokens, Kosten, Latenz, Retention |
| **Guardrails** | dürfen sich nicht über eine Grenze hinaus verschlechtern | Fehlerquote, Support-Kontakte, crashfreie Nutzer |
| **Diagnose-Ergebnisse** | erklären *warum*, nie Grundlage der Entscheidung | Exposure-Rate, Funnel-Schritte |
| **Behauptungen, die nicht aufgestellt werden** | explizite Nicht-Behauptungen | „absolute Fähigkeit", Generalisierung über die Testfamilie hinaus |

**Eine** Primärmethode wählen. Ein rauschiges, entferntes Business-Ergebnis ist ein Guardrail, keine Entscheidungs-Metrik — und jede zusätzliche „Primärmetrik" vervielfacht still die Chance, ein günstiges Ergebnis zu finden (Multipler Test).

### 3.2 Entscheidungsregel (alle drei Äste schreiben)

- **Sieg:** Primärmetrik verbessert sich um ≥ MDE mit dem deklarierten statistischen Test bei α, *und* kein Guardrail überschreitet seine Grenze → [konkrete Aktion: ausliefern / übernehmen].
- **Niederlage:** Effekt unter MDE oder negativ → [Aktion: zurückrollen / verwerfen].
- **Unentschieden:** unterpowered, mehrdeutig oder Guardrail-Konflikt → [Aktion: was wir lernen, ob mit größerem Design neu fahren].

Entscheidende Unterscheidung: **ein gescheiterter Überlegenheitstest zeigt keine Äquivalenz.** Wenn die Geschäftsfrage „sind diese nah genug beieinander?" lautet, ein Äquivalenz-/Nicht-Unterlegenheits-Design mit expliziter Marge verwenden. Den Effektschätzwert mit Konfidenz-/Glaubwürdigkeitsintervall berichten und angeben, ob das Intervall Effekte ausschließt, die die Entscheidung ändern würden. Keine ex-post-Power mit dem beobachteten Effekt; „nicht signifikant" nicht als „kein Effekt" lesen.

### 3.3 Vorab zu spezifizierende Auswertungsregeln

- **Analyseeinheit / Paarung** (z. B. gepaart nach Aufgabe + Seed; Resampling nach Aufgabe, nicht nach Zeile).
- **Einbeziehung von Fehlern** — fehlgeschlagene Läufe bleiben im Nenner; die Wiederholungsregel *vor* dem Betrachten der Ergebnisse deklarieren („keine ex-post-Ausschlüsse").
- **Multiplizitätsregel** für alle explorativen Kontraste (nur deskriptiv, oder deklarierte Adjustierung).
- **Sensitivitätsanalysen** — vor Berichterstattung der Ergebnisse deklarieren (z. B. „Läufe mit Infrastrukturfehlern ausschließen" als gekennzeichnete sekundäre Sicht).
- **Nenner- und Stoppregeln** — wenn die Ausführung endet, was bleibt im Nenner.
- **Ausführungsvertrag** — Versionen/Commits/Digests von Code, Umgebung, Modell, Evaluator und dem Auswertungsskript selbst; ein eindeutiges Lauf-ID-Schema.

### 3.4 Integritäts-Hygiene (die Anti-Pattern-Liste)

- **Kein Peeking** ohne sequenzielles Design; kein „stoppen, wenn es überzeugend aussieht".
- **Kein ex-post-Filtern** von Zuweisungen/Segmenten, um einen Sieg zu finden.
- **Kein Umlabeln** explorativer Läufe zu bestätigender Evidenz nach einer Änderung.
- **Alles dokumentieren**: Konfigurations-Hash, Plan, Aufgaben-IDs, Preis-/Kosten-Snapshot, Warnungen (zitieren und erklären statt entfernen).
- **Zugriffe einfrieren, nicht nur Dateien**: welche Komponenten welche Daten sehen dürfen (Entwicklung vs. Evaluator), abgerufene Artefakt-IDs loggen — ein versiegelter lokaler Split verhindert eigenes Tuning-Leak, macht öffentliche Daten aber nicht für das Modell unsichtbar.

Quellen zu diesen Regeln: `quellen.md`.
