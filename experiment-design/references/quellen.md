# Quellen

Hintergrund und Belege für die Regeln in `statistik.md`, `vorlage.md` und `checkliste.md`. Nicht für die Arbeit am Experiment nötig — nur bei Rückfragen zur Herkunft einer Regel laden.

## Statistik, Beobachtungszeit, Auswertung

- **GrowthBook — „How to calculate a power analysis for A/B tests"** (2026): die vier gekoppelten Eingaben, MDE als Entscheidungsschwelle, unabhängige Einheiten, Sensitivitätsszenarien, Peeking/sequenzielle Designs. https://www.growthbook.io/insights/power-analysis
- **K. Zavarov — A/B Test Design Template**: das Wenn/Dann/Weil-Hypothesenformat; MDE-Dauertabelle (10 % Baseline, 10k monatliche Besucher: 5 % relative MDE ≈ 692 Tage vs. 20 % relative MDE ≈ 46 Tage — Effektgröße dominiert die Dauer; absolute Werte hängen von der Traffic-Annahme der Quelle ab, eine Nachrechnung mit 10k Besuchern/Monat gesamt ergibt etwa die Hälfte). https://zavarov.com/en/template-abt/
- **CXL — „Tempted to Peek? Why Sequential Testing May Help"**; **Statsig — sequenzielle Tests**; **wasitcausal.com — Sequential Readouts**: tägliches Peeking bläht eine 5 %-Falsch-Positiv-Rate auf ~25 %.
- **ABWex / Omniconvert / Trevo — Dauer-Guides**: auf ganze Wochen aufrunden; Wochentagseffekte; „fahren bis signifikant" ist die falsche Stoppregel.
- **ScaffoldScope — Pre-Registration-Template** (LLM-Agent-Scaffold-Experimente): kausaler Kontrast, Ergebnisse inkl. „Behauptungen, die nicht aufgestellt werden", SESOI-Entscheidungsregel, Ausführungsvertrag (Hashes/Digests), „keine ex-post-Ausschlüsse". https://scaffoldscope.readthedocs.io/en/stable/protocol-template.html
- **System Design V, Kap. 21 — „Preregistering an experiment"** (FDE): Estimand-first-Ausarbeitung, Trennung von Exploration/Pilot/Bestätigung, Zugriffe einfrieren nicht nur Dateien, versionierte Änderungen. https://systemdesign.fde.guru/v/chapters/21/
- **OASIcs DX 2024 — „Design Principles for Falsifiable, Replicable and Reproducible Empirical ML Research"**: Hypothese als widerlegbare logische Aussage; statistisches Testen von H₀ gegen Hₐ.
- **hdd-methodology.md (GitHub)**: Commit von Hypothese + Erfolgsschwelle als Pre-Registration („man kann die Pfosten nicht verschieben").
- **Evidence-Based Software Engineering (Durham)**: kontrollierte Laborversuche beginnen mit einer testbaren Hypothese.
- **ACM CHI — „Some Whys and Hows of Experiments in HCI"**: Heuristiken für Hypothesen, Maße und fordernde (kein Sieg-Niederlage-)Vergleiche.
