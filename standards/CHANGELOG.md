# Changelog

## Verbindliche Grundlage

Jede Modulbibliothek besitzt eine `CHANGELOG.md` im Repository-Wurzelverzeichnis. Jede für Benutzer sichtbare Änderung wird im selben fachlichen Änderungszusammenhang eingetragen. Der Eintrag beschreibt die Auswirkung für Benutzer, nicht die interne Implementierung.

## Format

Veröffentlichte Versionen stehen mit der neuesten zuerst in diesem Format:

```markdown
# 07.10.2026 - Version 1.2.0

## Neu

- Die Konfiguration bietet eine zusätzliche Auswahl für den Betriebsmodus.

## Fixes

- Gespeicherte Einstellungen bleiben nach einem Neustart erhalten.
```

- Versionsüberschrift: `# <TT.MM.JJJJ> - Version <Version>`. Die Version entspricht exakt der `version` in `library.json`; eine vorhandene Beta-Kennzeichnung darf ergänzt werden.
- Kategorien: `## Neu` und `## Fixes`. Leere Kategorien entfallen.
- Ein Punkt pro Änderung, in verständlichem Deutsch. Überschriften und Listen erhalten die erforderlichen Leerzeichen und Leerzeilen.
- Das Datum bezeichnet die Veröffentlichung. Während der Entwicklung stehen noch nicht veröffentlichte Änderungen oben unter `# Unveröffentlicht`, mit denselben Kategorien.
- Erst bei ausdrücklich beauftragter Release-Vorbereitung wird dieser Abschnitt der bestätigten Version und dem Veröffentlichungsdatum zugeordnet. Version, Build und Datum in `library.json` werden nicht nebenbei geändert.
- Bestehende historische Einträge werden nicht ungefragt umformatiert. Neue Einträge folgen diesem Standard.

## Inhalt und Kompatibilität

Dokumentiert werden neue oder geänderte Funktionen, Variablen, Konfigurationsfelder, Darstellungen und Fehlerkorrekturen. Verhaltensänderungen, entfernte Funktionen und erforderliche Benutzerschritte müssen eindeutig erkennbar sein. Bei Auswirkungen auf bestehende Installationen enthält der passende Eintrag einen Hinweis mit `Achtung:`, etwa zu geänderter Bedienung, Migration oder notwendiger Neukonfiguration.

Reine Formatierung, interne Refactorings ohne sichtbare Wirkung und redaktionelle Dokumentationskorrekturen benötigen keinen Eintrag. Neue oder korrigierte Installationsanweisungen mit praktischer Auswirkung dürfen aufgenommen werden. Keine Zugangsdaten, realen ObjectIDs oder privaten Installationsdetails verwenden.

## Prüfung und Release

Vor Abschluss einer Änderung prüfen:

1. Jede sichtbare Änderung besitzt einen passenden Eintrag; doppelte Beschreibungen werden zusammengeführt.
2. Erforderliche Benutzerschritte und Kompatibilitätsfolgen sind verständlich beschrieben.
3. Bereits veröffentlichte Einträge bleiben erhalten.
4. Beim Release stimmen Version und Datum mit den freigegebenen Metadaten überein; der veröffentlichte Umfang ist vollständig enthalten.

Branch- und Releaseablauf bleiben gemäß [`GIT_WORKFLOW.md`](GIT_WORKFLOW.md). Vorlage: [`templates/CHANGELOG.md`](../templates/CHANGELOG.md).
