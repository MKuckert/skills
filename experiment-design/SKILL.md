---
name: experiment-design
description: Hilft beim Formulieren von Experimenten nach einer strukturierten Vorlage (Versuchsanordnung, Veränderung von Einflussgrößen, Hypothesen, Auswertung, Durchführung). Verwende, wenn der Nutzer ein Experiment entwerfen, formulieren oder strukturieren will — z. B. Produkt- oder Geschäfts-Experimente wie A/B-Tests, Pilotierungen oder Hypothesenprüfungen, wenn er einen unstrukturierten Textblock/Brain-Dump zu einem Experiment liefert, der erst sortiert und in die Vorlage überführt werden soll, oder wenn er nach Hilfe bei Hypothesen, Gegen-/Nebenthesen und Auswertungskriterien fragt.
---

# Experiment formulieren

Du hilfst dem Nutzer, ein Experiment entlang der Vorlage in `references/vorlage.md` zu formulieren. Lies die Vorlage (Pfad relativ zu diesem Skill-Verzeichnis), bevor du loslegst.

**Abzweigung nach Experimenttyp:** Ist das Experiment ein quantifizierendes Design (A/B-Test, Modell-/Methodenvergleich mit numerischem Primärergebnis), lade zusätzlich `references/statistik.md` und ziehe deren Regeln für Hypothese, Beobachtungsplan und Auswertung heran. Bei qualitativen oder explorativen Studien gilt statt Power-Analyse die Sättigungsregel (in der Vorlage, Abschnitt „Auswertung"). Bei niedriger Entscheidungshöhe („einfach testen") erlaube den Kurzmodus (siehe `references/checkliste.md`), setze im Vorlagenkopf aber explizit `Typ: nicht-bestätigend (Kurzmodus)`.

## Vorgehen

**Optional: Grilling-Skill.** Falls im aktuellen Kontext ein Skill namens `grilling` verfügbar ist, lade ihn und nutze seine Methode für die kritische Durchforstung des Experiments (vor allem bei Schritt 3 und der Qualitätsprüfung in Schritt 4). Falls nicht, ignoriere diesen Punkt — dieser Skill funktioniert ohne ihn vollständig.

1. **Kontext klären.** Liefert der Nutzer am Anfang einen kompletten Textblock (Brain-Dump, Notizen, Fließtext), lies ihn vollständig und sortiere ihn vor der strukturierten Arbeit grob vor: Ordne die Aussagen den Vorlagen-Abschnitten zu, markiere Lücken und Mehrdeutigkeiten, und zeige dem Nutzer eine kompakte Übersicht (was ist wo gelandet, was fehlt, was ist unklar) — erst dann abschnittsweise weiter. Nichts erfinden: Unklares bleibt als `[offen: …]` oder Rückfrage. Liefert der Nutzer nur ein Thema oder eine vage Idee, stelle zuerst gezielte Fragen (max. 3–5 pro Runde), bevor du textlich weiterarbeitest. Bei quantifizierenden Designs kläre zusätzlich, ob dies ein Pilot-Lauf oder der bestätigende Lauf ist und ob bereits ein Pilot gefahren wurde (Pilot-Ergebnisse speisen die Beobachtungszeit — siehe `references/statistik.md`, Abschnitt 2.4). Falls im aktuellen Kontext ein Tool zur strukturierten Nutzerabfrage (z. B. `ask_user`) verfügbar ist, nutze es, wenn mehrere unabhängige Entscheidungen offen sind — bündle die Fragen einer Teilsektion pro Call (nicht das gesamte Dokument in einer Abfrage). Falls nicht, stelle die Fragen als nummerierte Liste im Chat. Unbeantwortete Fragen landen als `[offen: …]` im Dokument, statt erneut nachzufragen.
2. **Abschnittsweise arbeiten.** Gehe die Vorlage in der Reihenfolge durch: Versuchsanordnung → Veränderung von Einflussgrößen → Zugrundeliegende Hypothese → Neben- & Gegenthesen → Auswertung → Durchführung. Für jeden Abschnitt: erst prüfen, ob die nötigen Informationen vorliegen; fehlende Punkte als konkrete Fragen ansprechen (wieder max. 3–5 pro Abschnitt). Die Checkliste aus Schritt 4 ist ein Selbstcheck — stelle daraus keine Frage-Kaskade an den Nutzer; nachgefragt wird nur, was faktisch fehlt.
3. **Konkret nachbohren (ggf. mit `grilling`).** Vage Formulierungen sind der häufigste Fehler. Bestehe auf:
   - *Versuchsanordnung:* Benannte Personen/Personengruppen, nicht „die Teammitglieder".
   - *Veränderung:* Exakt was wird geändert (Parameter, Text, Ablauf, Schwellwerte)? Und: Darf die Lösung während des Experiments feinjustiert werden — ja/nein, und wenn ja, nach welchen Regeln?
   - *Hypothese:* Falsifizierbarer Satz im Wenn/Dann/Weil-Format mit messbarem Erfolgskriterium und genanntem Mechanismus, keine Binsenweisheit.
   - *Auswertung:* Objektive Kriterien (Zahlen, Fragebogen, Logs) mit Schwellwerten und Guardrails, nicht „wir schauen uns das an".
   - *Gegenthesen:* Wenn der Nutzer keine Antithese liefern kann, schlage mindestens einen Kandidaten selbst vor (als Vorschlag gekennzeichnet).
4. **Qualitätsprüfung vor der Fertigstellung.** Lade `references/checkliste.md` und prüfe die komplette Formulierung Punkt für Punkt dagegen (Kern-Check immer; Statistik-Check nur bei quantifizierenden Designs, dann zusammen mit `references/statistik.md`). Nicht zutreffende Punkte erhalten `[n/a: Grund]` — nie stillschweigend weglassen. Nenne dem Nutzer, was fehlt oder schwach ist — auch wenn der Nutzer nicht danach gefragt hat.
5. **Ausgabe.** Liefere das fertige Experiment als Markdown-Dokument exakt in der Struktur der Vorlage (gleiche Überschriften). Die Anleitungstexte und Hinweise der Vorlage werden durch die Inhalte ersetzt, nicht mitkopiert. Befülle die Änderungs-Tabelle bereits mit einer v1-Zeile. Wenn der Nutzer es speichern will, schreib es in eine Datei, z. B. `experiment-<kurzname>.md` im aktuellen Verzeichnis.

## Stil

- Schreibe auf Deutsch, präzise und ohne Füllwörter.
- Keine erfundenen Details: Wenn der Nutzer etwas nicht angibt, markiere die Lücke im Dokument als `[offen: …]` statt sie zu erfinden. Nicht Zutreffendes markiere als `[n/a: Grund]`.
- Halte die Hypothese als einen Satz formulierbar; alles andere (Motivation, Erwartungshorizont) gehört in den erklärenden Text drumherum.
