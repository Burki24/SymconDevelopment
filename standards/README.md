# Standards

Diese Dokumente übersetzen die Engineering-Prinzipien in konkrete gemeinsame Regeln für Burki24-Symcon-Projekte. Die vorhandene Architektur und begründete projektspezifische Abweichungen bleiben zu berücksichtigen.

## Entwicklung

- [`MODULE_STRUCTURE.md`](MODULE_STRUCTURE.md): Repository- und Modulaufbau
- [`PHP_STYLE.md`](PHP_STYLE.md): PHP-Plattform, Code- und Formatierungsregeln
- [`HELPER_USAGE.md`](HELPER_USAGE.md): Zuständigkeit und Nutzung gemeinsamer Helper
- [`CONFIGURATION_FORM.md`](CONFIGURATION_FORM.md): statische und dynamische Konfigurationsformulare
- [`VARIABLE_PRESENTATION.md`](VARIABLE_PRESENTATION.md): native Variablendarstellungen und Actions
- [`SOURCE_VARIABLE_IDENTITY.md`](SOURCE_VARIABLE_IDENTITY.md): Variablen-ID als technische Identität konfigurierter Quellen
- [`MIGRATIONS.md`](MIGRATIONS.md): kompatible, wiederholbare Modulmigrationen
- [`README_CONTENT.md`](README_CONTENT.md): Benutzer-READMEs ohne Fehlerdiagnose und Entwicklungshinweise
- [`CHANGELOG.md`](CHANGELOG.md): sichtbare Änderungen, Format und Versionszuordnung

## Qualität und Zusammenarbeit

- [`TESTING.md`](TESTING.md): Testziele, Ablage und Nachweise
- [`DEBUG_OUTPUT.md`](DEBUG_OUTPUT.md): verständliche deutsche Debug-Ausgaben mit Vorgangsbezug und Schnittstellenergebnissen
- [`CI.md`](CI.md): gemeinsame CI-Basis
- [`GIT_WORKFLOW.md`](GIT_WORKFLOW.md): Branches, Pull Requests und Releases
- [`PRIVATE_DATA.md`](PRIVATE_DATA.md): Geheimnisse und installationsbezogene Daten
- [`SYMCON_ACCESS.md`](SYMCON_ACCESS.md): Rollen und erlaubter Umfang bei Entwicklungs- und Produktivzugriffen

Ein Standard beschreibt gemeinsame Mindestanforderungen. Langfristige Entscheidungen hinter einer Regel werden zusätzlich als ADR dokumentiert; praktische Diagnose- und Lösungsmuster gehören in die Knowledge Base.
