# Referenz: Symcon_ModuleHelper

- Status: Geprüft
- Zuletzt geprüft: 2026-09-26
- Repository: [`Burki24/Symcon_ModuleHelper`](https://github.com/Burki24/Symcon_ModuleHelper)
- Geprüfter Commit: `7a6abe82eb785f1e213bdcb79578a9753d492a03`
- Repository-Version: `3.18.5`
- Zielplattform: IP-Symcon 9.0 / PHP 8.5

## Referenzzweck

`Symcon_ModuleHelper` ist die zentrale, versionierte Quelle der wiederverwendbaren Burki24-Symcon-Helper. Das Repository dient als Referenz für:

- die klare Eigentümerschaft gemeinsamer Helper;
- maschinenlesbare Versionen, Abhängigkeiten, Assets und SHA-256-Prüfsummen;
- zentrale Dokumentation öffentlicher und protected Helper-Verträge;
- Tests einzelner Helper und repositoryübergreifender Synchronisierungsregeln;
- kontrollierte Verteilung nach `libs/helper` in Consumer-Repositories;
- ein dauerhaftes `dev`-/`main`-Modell mit automatisierter Versionierung und Rücksynchronisierung.

## Relevante Bausteine

| Pfad | Referenzaspekt |
| --- | --- |
| `AGENTS.md` | Kurze Anbindung an `SymconDevelopment` und dokumentierte Projektausnahmen |
| `README.md` | Helper-Verträge, Nutzung, Zielplattform und Dokumentationsregel |
| `manifest.json` | Versionen, Abhängigkeiten, Assets und Integritätswerte |
| `src/` | Kanonische Helper-Quellen dieses speziellen Quellrepositories |
| `tests/` | Helper-, Dokumentations-, Bundle- und Sync-Sicherheitsprüfungen |
| `.github/scripts/sync_helper_consumers.py` | Guarded Vendor-Sync in konfigurierte Consumer-Repositories |
| `.github/workflows/` | Tests, Style, Metadaten, Übersetzungen und Consumer-Sync |
| `HELPER_SYNC_SETUP.md` | Voraussetzungen und Sicherheitsgrenzen der Verteilungsautomation |

## Bewusste Ausnahmen von den allgemeinen Standards

- Das Repository ist selbst keine Symcon-Library und besitzt daher keine `library.json`, keine Modulverzeichnisse und keine Modul-READMEs.
- Die kanonischen Quellen liegen unter `src/`. `libs/helper` ist ausschließlich die erzeugte Zielstruktur in Consumer-Repositories.
- Die spezialisierte Manifest-, Metadaten- und Sync-CI ersetzt hier `Symcon_ModuleCI` und `validate_structure`.
- Die zentrale `README.md` dokumentiert alle Helper; direkte PHPDoc-Blöcke sichern zusätzlich öffentliche und protected APIs.

Diese Ausnahmen sind kein Vorbild für normale Modul-Repositories. Dort gelten weiterhin die allgemeine Modulstruktur, `libs/helper`, Modul-READMEs und die vorgesehene ModuleCI-Basis.

## Verifikation

Beim Pilotdurchlauf wurden folgende Nachweise erbracht:

- Manifest und Consumer-Konfiguration sind gültiges JSON.
- 24 Helper stimmen mit Versionen und SHA-256-Werten im Manifest überein.
- Übersetzungskataloge waren vollständig und synchron.
- Metadaten-, Bundle- und Guarded-Auto-Merge-Tests waren erfolgreich.
- Die Syntaxprüfung war für 58 PHP-Dateien erfolgreich.
- Alle Helper- und Dokumentationsvertragstests waren erfolgreich.
- GitHub Actions bestätigte PHP 8.5, StylePHP und die vollständige Testsuite.
- Der Merge nach `main` erzeugte Repository-Version `3.18.5`.
- `main` und `dev` wurden anschließend automatisch auf denselben Commit gebracht.
- Der vollständige Consumer-Sync wurde erfolgreich und ohne unnötige `source_sha`-Änderungen abgeschlossen.

Die lokalen PHP-Prüfungen liefen ergänzend unter PHP 8.2. Die maßgebliche PHP-8.5-Verifikation erfolgte in GitHub Actions.

## Übertragbare Leitlinien

1. Gemeinsame Helper besitzen genau eine kanonische Quelle; Consumer verändern synchronisierte Kopien nicht lokal.
2. Ein Sync überträgt vollständige, deklarierte Bundles einschließlich Abhängigkeiten und Assets.
3. Automatische Pull Requests werden nur bei geprüftem Autor, erwartetem Zielbranch und exakt begrenztem Dateiumfang automatisch zusammengeführt.
4. Unveränderte Payloads erzeugen keine reinen Provenienz- oder `source_sha`-Pull-Requests.
5. Änderungen an öffentlichen Verträgen werden gemeinsam mit Dokumentation, Tests und Versionsinformationen ausgeliefert.

## Nicht übernehmen

- Keine GitHub-App-, Auto-Merge- oder repositoryübergreifende Sync-Infrastruktur in normalen Modul-Repositories einführen.
- Keine Secrets, App-IDs oder Consumer-Listen aus dieser Referenz kopieren.
- Die spezielle `src/`-Struktur und CI-Ausnahme nicht als allgemeine Burki24-Modulstruktur interpretieren.
- Die Referenz nicht als Freigabe für Deployment-, Runtime-Mirror-, SSH-/PowerShell- oder MQTT-Frameworkteile verwenden.

Vor einer Nutzung sind Commit, Manifest-Schema, Workflows und Consumer-Vertrag erneut auf Aktualität zu prüfen.
