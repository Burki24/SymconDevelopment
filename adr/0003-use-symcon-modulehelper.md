# ADR 0003: Symcon_ModuleHelper als kanonische Helper-Quelle verwenden

- Status: Angenommen
- Datum: 2026-09-26
- Entscheider: Burki24
- Ersetzt: –
- Ersetzt durch: –

## Kontext

Mehrere Burki24-Module benötigen dieselben Funktionen für Konfigurationsformulare, Variablendarstellungen, Verbindungen, HTTP-Antworten und weitere technische Querschnittsaufgaben. Lokale Kopien führen zu unterschiedlichen Fehlerkorrekturen, Verträgen und Versionen.

`Symcon_ModuleHelper` besitzt eine versionierte kanonische Quelle, ein Manifest mit Integritätswerten, Tests und einen kontrollierten Consumer-Sync nach `libs/helper`.

## Entscheidung

`Symcon_ModuleHelper` ist die kanonische Quelle für projektübergreifend wiederverwendbare PHP-Helper.

- Consumer verwenden die freigegebenen Dateien unter `libs/helper`.
- Synchronisierte Helper werden im Consumer nicht lokal verändert oder dupliziert.
- Vor einer neuen lokalen Hilfsfunktion wird der vorhandene Helper-Vertrag geprüft.
- Eine neue zentrale Fähigkeit benötigt einen generischen Vertrag und tatsächliche Nutzung in mindestens zwei verschiedenen Libraries. Mehrere Module derselben Library oder nur vorgesehene weitere Nutzer genügen nicht; bis dahin verbleibt der Baustein samt Tests und Ressourcen in seiner Library (Präzisierung der Nutzerfestlegung vom 2026-10-23).
- Geräte-, Provider- und Modulfachlogik verbleibt im zuständigen Projekt.
- Änderungen an öffentlichen Helper-Verträgen werden gemeinsam mit Dokumentation, Tests, Version und Consumer-Auswirkungen bewertet.

Die besondere `src/`-, Manifest- und Sync-Struktur des Helper-Repositories ist keine allgemeine Modulvorlage.

## Alternativen

- **Helper in jedem Modul pflegen:** reduziert Abhängigkeiten, vervielfacht aber Wartung und führt zu auseinanderlaufenden Implementierungen.
- **SAEF-Helper übernehmen:** schafft eine zweite zentrale Quelle mit anderem Vertrag und zusätzlicher Lizenz- und Integrationskopplung.
- **Gemeinsames Composer-Paket:** wäre technisch möglich, passt aber nicht ohne Weiteres zum bestehenden Symcon-Installations- und Consumer-Modell.

## Folgen

Helper-Verträge werden einmal zentral entwickelt und geprüft. Consumer-Updates benötigen eine nachvollziehbare Versions- und Synchronisierungsentscheidung. Ein Consumer kann nicht beliebig einen synchronisierten Helper verändern; projektspezifische Logik muss klar davon getrennt bleiben.

## Nachweise

- [`references/Symcon_ModuleHelper.md`](../references/Symcon_ModuleHelper.md)
- [`standards/HELPER_USAGE.md`](../standards/HELPER_USAGE.md)
- geprüfter Manifest-, Bundle- und Consumer-Sync des Helper-Repositories
