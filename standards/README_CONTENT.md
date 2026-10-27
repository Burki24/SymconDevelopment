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

## Pflicht-Badges in Library-READMEs

Jede Library-README enthält unmittelbar nach dem Titel, vor der Beschreibung
oder einem optionalen Titelbild, mindestens diese fünf verlinkten Badges:

1. **Symcon / PHPModul** mit Link zur Symcon-Website.
2. **Symcon Version** mit der tatsächlich unterstützten Mindestversion aus
   `library.json`, beispielsweise `9.0+`, und Link zur Kompatibilitätsangabe.
3. **License** mit der tatsächlichen Projektlizenz und Link zur `LICENSE`.
4. **Check Style** als dynamischer GitHub-Actions-Status des Style-Workflows.
5. **Tests** als dynamischer GitHub-Actions-Status des Test-Workflows.

Die Badges müssen auf das Repository, die realen Workflow-Dateien und den
maßgeblichen Branch der jeweiligen Library angepasst sein. Badge und Ziel-Link
zeigen auf denselben Branch. Während einer Beta auf `dev` wird `dev` verwendet;
bei einem späteren Wechsel des maßgeblichen Release-Zweigs werden beide
Verweise zusammen aktualisiert. Workflow-Dateinamen nicht aus einer fremden
Library ungeprüft übernehmen.

Lizenz und Versionsgrenzen nicht aus einem Beispielbild oder einer anderen
Library kopieren. Insbesondere keine CC-Lizenz anzeigen, wenn tatsächlich
PolyForm Noncommercial verwendet wird. CI-Status niemals statisch mit
„passing“ oder „grün“ vorgeben; er kommt aus dem Workflow-Badge.

Eine zusätzliche Library-Versionsanzeige ist optional. Sie muss mit der
automatischen Versionierung übereinstimmen; keine manuell gepflegte, leicht
veraltende Versionsnummer als Ersatz für `library.json` einführen.

Diese Vorgabe gilt verbindlich für neue und künftig bearbeitete
Library-READMEs aller angebundenen Libraries. Änderungen an anderen Libraries
erfolgen in deren jeweiligen Projekten. Die Vorlage
[`REPO_README.md`](../templates/REPO_README.md) enthält das anzupassende Muster.

## Abgrenzung

Keine Abschnitte zu Fehlerdiagnose, Debugging, Entwicklung, Tests, CI oder internen Architekturentscheidungen in Bibliotheks- und Modul-READMEs. Solche Inhalte gehören in `PROJECT_CONTEXT.md`, geeignete Dokumente unter `docs/`, projektspezifische ADRs oder wiederverwendbare Knowledge-Artikel. Notwendige Benutzerhinweise zu Statusmeldungen, ungültiger Konfiguration und unterstützten Grenzen bleiben bei der jeweiligen Einrichtung oder Bedienung erhalten.

Die verpflichtenden kompakten Status-Badges im README-Kopf sind davon
ausgenommen; ausführliche CI-/Testanleitungen gehören weiterhin in `docs/`.

Die README-Dateien dieser zentralen Entwicklungsbasis sind Kataloge und Orientierung für Entwickler; diese Einschränkung betrifft die Benutzer-READMEs der Modulbibliotheken.

## Pflege

Geänderte Konfiguration, Variablen, Bedienung und öffentliche Funktionen werden in derselben fachlichen Änderung dokumentiert. Historische Changelog-Einträge ersetzen keine aktuelle Benutzeranleitung. Nicht benötigte Vorlagenabschnitte entfernen; vorhandene Projektgliederung erhalten, sofern keine Umstellung beauftragt ist.

Vorlagen: [`MODULE_README.md`](../templates/MODULE_README.md) und [`REPO_README.md`](../templates/REPO_README.md).
