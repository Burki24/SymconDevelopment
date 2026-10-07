# ADR 0002: SAEF schlank und konzeptionell adaptieren

- Status: Angenommen
- Datum: 2026-09-26
- Entscheider: Burki24
- Ersetzt: –
- Ersetzt durch: –

## Kontext

Das Symcon AI Engineering Framework (SAEF) verbindet Engineering-Prinzipien, Agentenregeln, Standards, ADRs, Knowledge-Artikel, Vorlagen, Helper, Tests und umfangreiche Deployment-Infrastruktur. Burki24 besitzt mit `Symcon_ModuleHelper`, `Symcon_ModuleCI`, StylePHP, Symcon-Stubs und den bestehenden Modul-Repositories bereits eine funktionierende technische Basis.

Eine vollständige Übernahme würde parallele Helper- und CI-Verträge sowie Betriebswerkzeuge einführen, für die in den Burki24-Projekten kein belegter Bedarf besteht. Gleichzeitig sind die explizite Leserichtung, dokumentierte Entscheidungen und wiederverwendbares Wissen für langfristig gepflegte Projekte wertvoll.

## Entscheidung

`SymconDevelopment` übernimmt SAEF ausschließlich als konzeptionelle Inspiration und bildet eine kleine, Burki24-spezifische Engineering-Schicht.

Übernommen beziehungsweise angepasst werden:

- eine zentrale `AGENTS.md` und eindeutige Leserichtung;
- Engineering- und KI-Zusammenarbeitsprinzipien;
- eigene Symcon-, PHP-, Test-, CI- und Git-Standards;
- ADRs und eine Knowledge Base;
- schlanke Projekt- und Dokumentationsvorlagen;
- kuratierte Referenzen und eine klare Leserichtung zur offiziell gepflegten Symcon-Dokumentation.

Nicht übernommen werden:

- SAEF-eigene PHP-Helper und Helper-Bundles;
- Deployment-Frameworks, Filesets und Runtime-Mirrors;
- SSH-/PowerShell-Orchestrierung und Live-System-Gates;
- SAEF-spezifische MQTT-Frameworkschichten;
- die Composer-Gesamtarchitektur und Prompt-Bibliothek;
- Case Studies ohne konkreten Burki24-Nutzen.

Diagnosekonzepte wie Konfigurations-Hashes, Statistiken und begrenzte Fehlerhistorien werden zunächst als Wissen dokumentiert. Zentraler Helper-Code entsteht erst nach belegter Nutzung und eigener Vertragsentscheidung.

## Alternativen

- **SAEF vollständig übernehmen:** bietet viele fertige Bausteine, verdoppelt aber Zuständigkeiten und führt nicht benötigte Betriebsinfrastruktur ein.
- **SAEF als direkte Abhängigkeit verwenden:** erzeugt Versions-, Lizenz- und Integrationskopplung zu einer Architektur, die nicht auf die bestehenden Burki24-Repositories zugeschnitten ist.
- **Nur informell weiterarbeiten:** vermeidet Dokumentationsaufwand, lässt Entscheidungen und wiederkehrendes Wissen jedoch erneut in Chats und Einzelprojekten verschwinden.

## Folgen

Die bestehenden technischen Quellen bleiben maßgeblich: gemeinsame PHP-Funktionen in `Symcon_ModuleHelper`, CI in `Symcon_ModuleCI` und Fachlogik in den Modul-Repositories. `SymconDevelopment` bleibt überwiegend dokumentationsbasiert und kann schrittweise aus realer Projekterfahrung wachsen.

Neue SAEF-Funktionen werden nicht automatisch übernommen. Jede spätere Erweiterung benötigt einen eigenen Burki24-Anwendungsfall, eine Lizenzprüfung bei direkter Codeübernahme und eine klare Zuständigkeit.

## Nachweise

- [`references/SAEF.md`](../references/SAEF.md) mit geprüftem Upstream-Commit und Übernahmematrix
- Vergleich der SAEF-Struktur mit der vorhandenen Burki24-Infrastruktur
- bereits produktiv verwendete zentrale Helper- und CI-Repositories
- Pilotanbindung von `Symcon_ModuleHelper`, OpenHomeAlarm und OpenCalendar an die zentrale `AGENTS.md`
- bewusster Ausschluss der nicht benötigten Deployment- und Runtime-Schichten in `AGENTS.md` und `ARCHITECTURE.md`
