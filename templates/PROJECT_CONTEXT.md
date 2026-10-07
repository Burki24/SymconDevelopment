# Projektkontext

Dieses Dokument beschreibt die fachliche und technische Orientierung eines einzelnen Repositories. Es ergänzt die lokale `AGENTS.md`, enthält aber keine duplizierten zentralen Standards.

## Zweck und Benutzer

- Projektzweck: <!-- Welches Problem löst das Repository? -->
- Hauptnutzer: <!-- Wer verwendet oder administriert es? -->
- Nicht im Umfang: <!-- Welche naheliegenden Aufgaben gehören bewusst nicht dazu? -->

## Unterstützte Plattform

- IP-Symcon: 9.x
- PHP: 8.5
- Zusätzliche Laufzeiten oder Dienste: <!-- falls vorhanden -->
- Relevante Kompatibilitätszweige: <!-- falls vorhanden -->

## Einstiegspunkte

| Bereich | Datei oder Verzeichnis | Bedeutung |
| --- | --- | --- |
| Bibliothek | `library.json` | <!-- Name und Bibliotheksvertrag --> |
| Änderungen | `CHANGELOG.md` | <!-- unveröffentlichte Änderungen und Versionshistorie --> |
| Modul | `ModulName/module.php` | <!-- fachliche Hauptverantwortung --> |
| Konfiguration | `ModulName/form.json` | <!-- wichtige Properties --> |
| Helper | `libs/helper/` | <!-- eingebundene zentrale Helper --> |
| Tests | `tests/` | <!-- wichtigste Testgruppen --> |
| CI | `.github/workflows/` | <!-- verwendete ModuleCI-Einstiege --> |

Nicht vorhandene Bereiche werden entfernt; weitere relevante Einstiegspunkte werden ergänzt.

## Architektur und Datenfluss

Beschreibe die wichtigsten Komponenten und ihren Datenfluss in wenigen Absätzen oder einer kleinen Textgrafik. Benenne insbesondere externe Dienste, Parent-/Child-Verbindungen, öffentliche Methoden, Actions und persistente Zustände.

## Öffentliche und persistente Verträge

- Properties: <!-- stabile Namen, Typen oder Verweis auf Modul-README -->
- Variablen und Idents: <!-- besonders kompatibilitätskritische Einträge -->
- Öffentliche Methoden: <!-- falls vorhanden -->
- Datenformate und Caches: <!-- falls vorhanden -->
- Migrationen: <!-- aktuelle Marker oder relevante ADRs -->

## Gemeinsame Abhängigkeiten

- `Symcon_ModuleHelper`: <!-- verwendete Helper und Version -->
- `Symcon_ModuleCI`: v1.0.0 <!-- begründete Abweichung dokumentieren -->
- Weitere Abhängigkeiten: <!-- Name, Version und Zweck -->

## Projektspezifische Entscheidungen

- <!-- Link auf lokale ADRs oder kurze bestehende Architekturentscheidung -->

## Prüfung und Veröffentlichung

- Lokale Prüfungen: <!-- dokumentierte Befehle oder Verweis -->
- Maßgebliche CI: <!-- Workflows und unterstützte Matrix -->
- Branch- und Release-Besonderheiten: <!-- nur Abweichungen von zentralem Standard -->
- Notwendige Praxistests: <!-- Symcon, Gerät, Visualisierung oder externer Dienst -->

## Diagnose und Entwicklung

- Fehlerdiagnose: <!-- relevante Statusmeldungen, bereinigte Logs oder Dokumente unter docs/ -->
- Entwicklungshinweise: <!-- interne Architekturhinweise und technische Einschränkungen -->
- Systemrollen und erlaubte Zugriffe: <!-- Entwicklungs-/Test-/Produktivrolle und auftragsbezogene oder ausdrückliche dauerhafte Freigaben, ohne private Endpunkte -->

Diese internen Hinweise gehören nicht in die Benutzer-READMEs.

## Bekannte Risiken und offene Fragen

- <!-- bestätigte technische Schuld, fehlende Nachweise oder geplante Migration -->

## Pflege

Aktualisiere dieses Dokument, wenn sich Einstiegspunkte, Datenfluss, öffentliche Verträge oder Abhängigkeiten wesentlich ändern. Einzelne Implementierungsdetails und temporäre Aufgaben gehören nicht hierher.
