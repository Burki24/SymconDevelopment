# Git-Workflow

## Zweige

- `dev` ist der dauerhafte Integrationszweig für laufende Entwicklung.
- Aufgaben werden in kurzlebigen, eindeutig benannten Feature- oder Fix-Branches umgesetzt.
- Pull Requests für laufende Entwicklung zielen auf `dev`, sofern die lokale Projektregel nichts ausdrücklich anderes festlegt.
- Nach dem Merge bleibt `dev` bestehen. Optionen zum automatischen Löschen gelten nur für den Quellbranch des Pull Requests, niemals für `dev`.
- Ein stabiler oder Release-Zweig wird ausschließlich nach der dokumentierten Praxis des jeweiligen Repositories verwendet.

## Änderungen vorbereiten

1. Prüfe Status, aktuellen Zweig und nicht zugehörige lokale Änderungen.
2. Aktualisiere die Arbeitsgrundlage nach dem im Projekt erlaubten Verfahren.
3. Halte die Änderung eng am Auftrag und vermische keine unabhängigen Aufräumarbeiten.
4. Führe die betroffenen Tests sowie Style- und Strukturprüfungen aus.
5. Prüfe den vollständigen Diff auf versehentliche Änderungen, Secrets und generierte Dateien.

## Commits und Pull Requests

- Commits sind thematisch geschlossen und verständlich beschrieben.
- Ein Pull Request erklärt Problem, Lösung, Auswirkungen und Prüfungen.
- Architekturentscheidungen und notwendige Dokumentationsänderungen gehören in denselben fachlichen Zusammenhang.
- Fehlgeschlagene oder nicht ausgeführte Prüfungen werden nicht verschwiegen.
- Merge, Push, Tagging, Release und Veröffentlichung erfolgen nur mit entsprechender Berechtigung und ausdrücklichem Auftrag.

## Konflikte und Abweichungen

Konflikte werden anhand der aktuellen Architektur gelöst, nicht durch pauschales Überschreiben. Dauerhafte Abweichungen von diesem Workflow werden in der lokalen `AGENTS.md` dokumentiert; Architekturfolgen erhalten bei Bedarf ein ADR.
