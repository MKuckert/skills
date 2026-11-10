# Vorlage: Experiment

Protokollversion: v[N] — eingefroren [UTC-Datum], genehmigt von [Name]

Typ: [bestätigend / explorativ / nicht-bestätigend (Kurzmodus)]

Fülle jedes Kapitel vollständig aus. Fehlende Punkte markiere als `[offen: …]`, nicht zutreffende als `[n/a: Grund]`.

> Hinweis (nicht ins fertige Dokument übernehmen): Quantifizierende Designs (A/B-Test, Modell-/Methodenvergleich mit numerischem Primärergebnis): zusätzlich `references/statistik.md` laden; das quantifizierende Bullet in „Auswertung" und die Statistik-Checkliste dann nach deren Regeln ausfüllen.

## Versuchsanordnung: Situation, Problem

Beschreibe die aktuelle Situation und welche Herausforderung sie darstellt.

Benenne die am Problem beteiligten Personen/Personengruppen:

Population / Randomisierungseinheit — wer oder was ist für die Änderung eligible, und welche Einheit wird unabhängig randomisiert bzw. ausgewertet:

## Veränderung von Einflussgrößen: Lösung

Hauptgegenstand des Experiments. Was konkret wird im Vergleich zur Situation angepasst oder verändert? (Sehr spezifisch und konkret.)

Manipulierte Variable: das eine, was sich ändert. Was bleibt fixiert (z. B. Prozess, Team-Zusammensetzung, Preise, Tools, Software-/Modellversion, Budget, Umgebung):

Feinjustierung während des Experiments erlaubt? (ja/nein; wenn ja: nach welchen Regeln, wer entscheidet, wie oft?)

## Zugrundeliegende Hypothese

Konkret ausformulieren im Wenn/Dann/Weil-Format: *Wenn* [konkrete Änderung], *dann* wird [Zielmetrik] sich um [erwartete Größe und Richtung] ändern, *weil* [Mechanismus / stützende Evidenz].

- Widerlegbarkeit: welches beobachtbare Ergebnis würde die Hypothese widerlegen?
- Baseline: was ist die Kontrolle und ihr Wert aus relevanter Historie (Datenfenster, Metrikdefinition)? Falls keine Historie existiert: wie wird die Baseline vor Start gemessen?
- Behauptungen, die NICHT aufgestellt werden (z. B. „absolute Fähigkeit", Generalisierung über den Testbereich hinaus):

Welche Motivation liegt dem Experiment zugrunde, was soll herausgefunden werden? (Erklärender Text — getrennt vom Hypothesensatz.)

## Neben- & Gegenthesen

Flankierende Hypothesen, die neben diesem Experiment bestehen. Dies können auch Folgehypothesen oder alternative Annahmen sein.

Antithesen, aus denen jemand ein Risiko liest, sollten hier genannt werden. Bei Widerlegung der ursprünglichen Hypothese im Experiment können diese z. B. erneut herangezogen werden.

## Auswertung

Wie lange (bis zu welchem Zeitpunkt) läuft das Experiment?

- Quantifizierende Designs: die Dauer wird *abgeleitet, nicht gewählt* (Effektgröße/MDE → Stichprobe → Traffic-Rate → Kalenderdauer, auf volle Geschäftszyklen gerundet; siehe `statistik.md`).
  - Primärvergleich: [Behandlungs-ID] vs. [Kontroll-ID]
  - α: [0,05 zweiseitig]   Power: [0,80]   Aufteilung: [50/50]
  - Benötigte Stichprobe pro Arm: [N] (Methode: [Test + verwendete Software/Funktion])
  - Sensitivitätsszenarien (optimistisch / erwartet / konservativ): [Dauer jeweils]
  - Erwartete Rekrutierungsrate: [Einheiten/Woche]; Ergebnis-Reifedauer: [Tage]
  - Früheste verantwortbare Auswertung: [Datum]. Stoppregel: fixer Horizont bei [Datum/Stichprobe] — KEIN optionales frühes Stoppen bei positiven Ergebnissen (oder: sequenzielles Design [Name], für diese Regel gepowert).
  - Pilot-Ergebnisse, die diese Zahlen informieren (Varianz, Sättigung, Fehlerquote): [… oder: Pilot folgt]
- Qualitative/explorative Studien: Sättigungs-Stoppregel (weiter rekrutieren, bis keine neuen Themen/Fälle mehr auftauchen) und Auswertungsmethode (Kodierschema, Inter-Rater-Check) vorab deklarieren.

Metrik-Hierarchie (alle vor Start deklarieren):

- Primärergebnis: [die eine Entscheidungs-Metrik + exakte Definition]
- Kleinste praktisch relevante Wirkung (MDE/SESOI): [Schwelle in absoluten Werten]
- Sekundärergebnisse: [Liste]
- Guardrails (max. zulässige Verschlechterung): [Liste + Grenzen]
- Diagnose-Ergebnisse (erklären *warum*, nie Entscheidungsgrundlage): [Liste]

Lege fest, wie herausgefunden wird, ob die Hypothese korrekt ist oder nicht. Lege objektive Bewertungskriterien fest und überlege, wie Beobachterunabhängigkeit sichergestellt ist (z. B. durch einen objektiven Fragebogen, der erhoben wird). Wie wird Nachvollziehbarkeit und Reproduzierbarkeit anstelle von Bauchgefühl sichergestellt?

Entscheidungsregel — alle drei Äste schreiben:

- SIEG: Primärkriterium erfüllt den vorab festgelegten Schwellwert (quantifizierend: [Primärmetrik] verbessert sich um ≥ MDE mit dem deklarierten statistischen Test bei α; qualitativ: Kriterium laut Kodierschema/Rubrik erfüllt), kein Guardrail-Bruch → [konkrete Aktion: ausliefern / übernehmen]
- NIEDERLAGE: Schwellwert verfehlt (quantifizierend: unter MDE oder negativ) → [konkrete Aktion: zurückrollen / verwerfen]
- UNENTSCHIEDEN: [Bedingungen, z. B. unterpowered, mehrdeutig, Guardrail-Konflikt] → [Aktion / Plan, mit größerem Design neu zu fahren]

Auswertungsregeln vorab spezifizieren: Analyseeinheit/Paarung, Einbeziehung von Fehlern („keine ex-post-Ausschlüsse"), Multiplizitätsregel für explorative Kontraste, Sensitivitätsanalysen.

Welche möglichen Variablen sind vorhanden, die Einfluss auf das Experiment haben könnten? Wie wird interne Validität sichergestellt?

## Hinweise zur Experiment-Durchführung

Mache transparent, was das Experiment bedeutet und was im Anschluss passiert. Nenne mögliche Konsequenzen (Erfolg UND Misserfolg). Unter welchen Bedingungen bleiben Veränderungen erhalten oder werden sogar zurückgerollt? (Rollback-Bedingungen explizit: wann, wer entscheidet.)

Ausführungsvertrag — eindeutige Identifikation dessen, was lief: Version/Stand aller beteiligten Artefakte (z. B. Dokumente, Fragebögen, Prozessbeschreibung; bei technischen Experimenten Commits/Digests von Code, Umgebung, Modell, Evaluator und Auswertungsskript) und ein eindeutiges Lauf-/Durchgangs-Schema:

Wie erfolgt die Dokumentation während und im Anschluss an das Experiment? Gibt es z. B. ein Versuchsprotokoll? Wer ist hierfür verantwortlich?

Änderungen am Protokoll sind erlaubt, aber versioniert — nie an Ort und Stelle bearbeiten:

| v | Datum | Änderung | Grund | betroffene Läufe reklassifiziert zu |
|---|-------|----------|-------|-------------------------------------|
