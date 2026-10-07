# ADR 0007: Benutzer-READMEs und Versionshistorie trennen

- Status: Angenommen
- Datum: 2026-10-07
- Entscheider: Burki24
- Ersetzt: –
- Ersetzt durch: –

## Kontext

Die bisherigen Modul-README-Vorlagen mischen Benutzeranleitung, Fehlerdiagnose und Entwicklungshinweise. Ein eigenständiger gemeinsamer Changelog-Standard fehlt. Nach dem Vergleich mit dem Symcon-Regelwerk wurde ausdrücklich beauftragt, Changelogs zu vereinheitlichen und Fehlerdiagnose sowie Entwicklungshinweise aus den Benutzer-READMEs zu entfernen.

## Entscheidung

Bibliotheks- und Modul-READMEs konzentrieren sich auf Voraussetzungen, Installation, Konfiguration, Variablen, Bedienung, öffentliche Funktionen und notwendige Benutzerhinweise. Fehlerdiagnose, Entwicklung, Tests und CI werden in interner Projektdokumentation gehalten. README-Kataloge der zentralen Entwicklungsbasis bleiben Entwicklerorientierung.

Jede Modulbibliothek führt eine `CHANGELOG.md`. Sichtbare Änderungen werden im selben fachlichen Änderungszusammenhang erfasst. Veröffentlichte Abschnitte verwenden Datum und tatsächliche Bibliotheksversion sowie die Kategorien `Neu` und `Fixes`; bis zur beauftragten Release-Vorbereitung stehen neue Einträge unter `Unveröffentlicht`. Versionsmetadaten werden nur auf ausdrücklichen Auftrag erhöht.

Die vorhandenen Helper-, CI-, Test- und Git-Entscheidungen bleiben bestehen. Bestehende Modul-Repositories werden durch diese Regelwerksänderung nicht automatisch geändert.

## Alternativen

- **Gemischte README beibehalten:** alle Informationen stehen zusammen, die Benutzeranleitung enthält jedoch weiterhin interne Arbeitsanweisungen entgegen dem ausdrücklichen Wunsch.
- **Nur Changelog ergänzen:** verbessert die Versionshistorie, löst aber die Trennung der README-Inhalte nicht.
- **Alle neuen Einträge sofort einer geplanten Version zuordnen:** vermeidet einen unveröffentlichten Abschnitt, setzt aber unbestätigte Release-Metadaten voraus und kann der tatsächlichen `library.json` widersprechen.

## Folgen

Standards, Agentenregeln und Vorlagen werden konsistent angepasst. Diagnose- und Prüfhinweise bleiben auffindbar, beispielsweise im `PROJECT_CONTEXT.md` oder unter `docs/`. Beim Release wird der Changelog ausdrücklich mit den bestätigten Metadaten abgeglichen. Vorhandene historische Changelog-Formate werden nicht ungefragt umgeschrieben.

## Nachweise

- ausdrücklicher Benutzerauftrag vom 07.10.2026
- [`standards/README_CONTENT.md`](../standards/README_CONTENT.md)
- [`standards/CHANGELOG.md`](../standards/CHANGELOG.md)
- [`templates/MODULE_README.md`](../templates/MODULE_README.md)
- [`templates/REPO_README.md`](../templates/REPO_README.md)
- [`templates/CHANGELOG.md`](../templates/CHANGELOG.md)
