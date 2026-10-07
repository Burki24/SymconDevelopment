# Inhalte der README-Dateien

## Ziel und Geltungsbereich

Bibliotheks- und Modul-READMEs dienen Benutzern: Sie erklären Zweck, Voraussetzungen, Installation, Konfiguration, sichtbare Variablen, Bedienung und öffentliche Funktionen. Die Bibliotheks-README gibt den Überblick und verlinkt die Modul-READMEs; jedes veröffentlichte Modul hat eine eigene README.

## Inhalte

- Kurze Beschreibung des fachlichen Zwecks und unterstützter Geräte oder Dienste.
- Voraussetzungen und Installation auf Bibliotheksebene; modulspezifische Voraussetzungen und Einrichtung dort ergänzen, wo sie benötigt werden.
- Konfiguration mit Bedeutung, Standardwerten und Abhängigkeiten der Felder.
- Sichtbare Variablen mit Ident, Typ, Bedeutung, Einheit und Bedienbarkeit.
- Öffentliche Funktionen mit Parametern, Rückgabewert und Verwendung, soweit vorhanden.
- Erforderliche Hinweise für Benutzer bei Einschränkungen, inkompatiblen Änderungen oder Migrationen.
- Projektbezogene Lizenzangaben und gegebenenfalls vorhandene Spendenhinweise. Keine fremden Zahlungslinks oder Lizenzentscheidungen aus Referenzvorlagen übernehmen.
- Auf Bibliotheksebene ein Verweis auf die `CHANGELOG.md` nach [`CHANGELOG.md`](CHANGELOG.md).

## Abgrenzung

Keine Abschnitte zu Fehlerdiagnose, Debugging, Entwicklung, Tests, CI oder internen Architekturentscheidungen in Bibliotheks- und Modul-READMEs. Solche Inhalte gehören in `PROJECT_CONTEXT.md`, geeignete Dokumente unter `docs/`, projektspezifische ADRs oder wiederverwendbare Knowledge-Artikel. Notwendige Benutzerhinweise zu Statusmeldungen, ungültiger Konfiguration und unterstützten Grenzen bleiben bei der jeweiligen Einrichtung oder Bedienung erhalten.

Die README-Dateien dieser zentralen Entwicklungsbasis sind Kataloge und Orientierung für Entwickler; diese Einschränkung betrifft die Benutzer-READMEs der Modulbibliotheken.

## Pflege

Geänderte Konfiguration, Variablen, Bedienung und öffentliche Funktionen werden in derselben fachlichen Änderung dokumentiert. Historische Changelog-Einträge ersetzen keine aktuelle Benutzeranleitung. Nicht benötigte Vorlagenabschnitte entfernen; vorhandene Projektgliederung erhalten, sofern keine Umstellung beauftragt ist.

Vorlagen: [`MODULE_README.md`](../templates/MODULE_README.md) und [`REPO_README.md`](../templates/REPO_README.md).
