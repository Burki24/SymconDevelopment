# Zentrale Arbeitsregeln für Burki24-Symcon-Projekte

Diese Datei ist die gemeinsame Basis für Repositories, die ausdrücklich auf sie verweisen. Sie ersetzt keine projektspezifische Analyse. Eine lokale `AGENTS.md` darf begründete Projektdetails ergänzen oder Regeln ausdrücklich verschärfen; Abweichungen müssen sichtbar und nachvollziehbar sein.

## 1. Vor jeder Änderung

1. Lies die lokale `AGENTS.md`, dieses zentrale Regelwerk und die für die Aufgabe relevanten Dokumente unter `standards/`.
2. Lies die vorhandene Architektur, insbesondere `README.md`, `library.json`, betroffene `module.json`-Dateien, Modul-READMEs, Helper, Tests und CI-Konfiguration.
3. Suche nach vorhandenen Funktionen und vergleichbaren Modulen, bevor du neue Abstraktionen, Dateien oder Helper einführst.
4. Prüfe den Arbeitsbaum und erhalte fremde oder nicht zur Aufgabe gehörende Änderungen.
5. Grenze Ziel, betroffene Dateien, Kompatibilitätsanforderungen und passende Nachweise ein.

Bestehendes Verhalten und vorhandene Konventionen haben Vorrang vor Vermutungen. Bei Widersprüchen wird nicht stillschweigend eine neue Architektur eingeführt.

## 2. Technische Basis

- Entwickle für IP-Symcon 9 und PHP 8.5.
- Nutze die bestehende Repository- und Modulstruktur; maßgeblich ist [`standards/MODULE_STRUCTURE.md`](standards/MODULE_STRUCTURE.md).
- Gemeinsamer Code liegt unter `libs/helper`, nicht unter `.shared`.
- Tests liegen unter `tests`, nicht unter `.tests`.
- Jedes Modul besitzt eine gepflegte `README.md`.
- Bevorzuge `Symcon_ModuleHelper` und andere bereits eingebundene zentrale Funktionen.
- Erzeuge keine lokalen Kopien zentraler Helper. Fehlt eine allgemein nutzbare Funktion, prüfe zuerst eine Ergänzung im zuständigen Helper-Repository als separate Änderung.
- Konfiguration und Migrationen müssen bei wiederholter Ausführung sicher sein und dürfen keine unnötigen Seiteneffekte erzeugen.

## 3. Umsetzung

- Ändere nur, was für die konkrete Aufgabe erforderlich ist.
- Respektiere öffentliche Modulverträge, Property-Namen, Identifiers, Statuscodes und persistierte Konfiguration.
- Trenne fachliche Änderungen von rein mechanischer Formatierung.
- Übernimm keine Implementierung blind aus Referenzen; prüfe Version, Kontext und Vertrag.
- Dokumentiere neue oder geänderte Benutzerfunktionen in der Modul-`README.md`.
- Dokumentiere langfristige oder repositoryübergreifende Architekturentscheidungen als ADR.
- Überführe wiederverwendbare Diagnose- oder Lösungsinformationen nach `knowledge/`, wenn sie nicht projektspezifisch sind.

## 4. Qualität und Nachweise

Nutze zuerst die vom Zielrepository dokumentierten Befehle und Konfigurationen. Mindestens relevant sind:

- betroffene Tests unter `tests`;
- StylePHP;
- php-cs-fixer im Prüfmodus;
- `validate_structure`;
- weitere projektbezogene Prüfungen aus CI oder `composer.json`.

Die gemeinsame CI-Basis ist `Symcon_ModuleCI` v1.0.0. Details stehen in [`standards/CI.md`](standards/CI.md) und [`standards/TESTING.md`](standards/TESTING.md).

Melde zum Abschluss, welche Prüfungen tatsächlich ausgeführt wurden und welche nicht. Ein grüner Formatierungscheck ersetzt keine Verhaltensprüfung.

## 5. Git und Pull Requests

- Arbeite in einem zur Aufgabe passenden Branch und halte Commits thematisch fokussiert.
- Pull Requests für laufende Entwicklung zielen auf den dauerhaften Zweig `dev`, sofern das Projekt nichts Abweichendes festlegt.
- `dev` bleibt nach dem Merge bestehen und wird nicht als kurzlebiger Feature-Branch behandelt oder automatisch gelöscht.
- Committe, pushe, merge oder veröffentliche nur auf ausdrücklichen Auftrag.

Siehe [`standards/GIT_WORKFLOW.md`](standards/GIT_WORKFLOW.md).

## 6. Ausdrücklich nicht Teil dieser Basis

Führe keine SAEF-spezifischen Deployment-Frameworks, Runtime-Mirrors, Filesets, SSH-/PowerShell-Orchestrierung oder MQTT-Frameworkschichten allein aufgrund dieser Basis ein. Für solche Fähigkeiten ist eine eigene fachliche Entscheidung im betroffenen Projekt erforderlich.
