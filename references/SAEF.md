# Referenz: Symcon AI Engineering Framework

- Status: Geprüft
- Zuletzt geprüft: 2026-09-26
- Repository: [`doctee/symcon-ai-framework`](https://github.com/doctee/symcon-ai-framework)
- Geprüfter Commit: `9ee24e21e756d581e3e334313bea77f512b211cb`
- Lizenz: PolyForm Noncommercial License 1.0.0, soweit im Quellrepository angegeben

## Referenzzweck

SAEF dient als konzeptionelle Inspirationsquelle für eine strukturierte, KI-unterstützte Symcon-Entwicklung. Geprüft wurden insbesondere:

- zentrale Agentenregeln und eine definierte Leserichtung;
- Engineering- und KI-Prinzipien;
- Standards, ADRs und wiederverwendbare Knowledge-Artikel;
- Vorlagen und Referenzimplementierungen;
- idempotente Konfiguration und explizite Zuständigkeiten;
- begrenzte Runtime-Diagnostik mit Konfigurations-Hash, Metadaten, Statistiken und Fehlerhistorie.

Diese Konzepte werden nicht unverändert übernommen. Maßgeblich sind die eigene Burki24-Architektur, bestehende Module und die Entscheidungen in [`ADR 0002`](../adr/0002-lean-saef-adaptation.md).

## Angepasst übernommen

| SAEF-Konzept | Burki24-Umsetzung |
| --- | --- |
| Agenten-Einstieg | zentrale `AGENTS.md` plus kurze projektspezifische Datei |
| Engineering-Prinzipien | eigene Dokumente unter `principles/` |
| Standards | eigene, auf Symcon 9 und PHP 8.5 zugeschnittene Regeln unter `standards/` |
| ADRs | fortlaufende Entscheidungen unter `adr/` |
| Knowledge Base | belegtes Praxiswissen unter `knowledge/` |
| Vorlagen | schlanke Projekt-, Kontext- und Dokumentationsvorlagen unter `templates/` |
| Helper-first | vorhandener `Symcon_ModuleHelper` statt SAEF-Helper |
| CI und Tests | `Symcon_ModuleCI` v1.0.0, StylePHP, php-cs-fixer, `validate_structure` und Projekttests |
| Runtime-Diagnostik | zunächst Knowledge-Artikel; Helper erst nach eigenen realen Anwendungsfällen |

## Nicht übernehmen

- SAEF-eigene Helper, Bundles und Composer-Gesamtarchitektur
- Deployment-Pakete, Filesets und Runtime-Mirrors
- SSH-/PowerShell-Deployment und Live-System-Gates
- SAEF-spezifische MQTT- und Veröffentlichungsinfrastruktur
- Prompt-Bibliothek und Workstream-Orchestrierung ohne Burki24-Anwendungsfall
- Case Studies als eigene Frameworkschicht

Es wird kein SAEF-Code in dieses Repository kopiert. Falls später eine direkte Codeübernahme erwogen wird, sind Lizenz, Herkunft, Aktualität und eigener Integrationsvertrag vorher gesondert zu prüfen.

## Relevante Quelldokumente

- [`README.md`](https://github.com/doctee/symcon-ai-framework/blob/9ee24e21e756d581e3e334313bea77f512b211cb/README.md)
- [`principles/ENGINEERING_PRINCIPLES.md`](https://github.com/doctee/symcon-ai-framework/blob/9ee24e21e756d581e3e334313bea77f512b211cb/principles/ENGINEERING_PRINCIPLES.md)
- [`principles/AI_PRINCIPLES.md`](https://github.com/doctee/symcon-ai-framework/blob/9ee24e21e756d581e3e334313bea77f512b211cb/principles/AI_PRINCIPLES.md)
- [`standards/SYMCON_STANDARDS.md`](https://github.com/doctee/symcon-ai-framework/blob/9ee24e21e756d581e3e334313bea77f512b211cb/standards/SYMCON_STANDARDS.md)
- [`knowledge/EK-006-runtime-diagnostics.md`](https://github.com/doctee/symcon-ai-framework/blob/9ee24e21e756d581e3e334313bea77f512b211cb/knowledge/EK-006-runtime-diagnostics.md)
