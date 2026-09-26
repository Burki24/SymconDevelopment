# ADR 0004: Symcon_ModuleCI als gemeinsame CI-Basis verwenden

- Status: Angenommen
- Datum: 2026-09-26
- Entscheider: Burki24
- Ersetzt: –
- Ersetzt durch: –

## Kontext

Burki24-Symcon-Repositories benötigen wiederkehrende Prüfungen für Stil, Formatierung, Struktur und Tests. Vollständig eigenständige Workflows driften bei Versionen, Matrizen und Fehlerkorrekturen auseinander.

`Symcon_ModuleCI` bündelt die dafür vorgesehene gemeinsame Infrastruktur. Spezialisierte Quell- oder Werkzeug-Repositories können abweichende Anforderungen besitzen.

## Entscheidung

Normale Burki24-Symcon-Modul-Repositories verwenden `Symcon_ModuleCI` v1.0.0 als gemeinsame CI-Basis. Die konkrete, freigegebene Einbindung folgt einer bereits funktionierenden Burki24-Referenz und deckt die im Projekt vorhandenen Varianten von StylePHP, php-cs-fixer, `validate_structure` und Tests ab.

- Projektbezogene Test- und Versionsmatrizen bleiben im jeweiligen Vertrag sichtbar.
- CI-Abhängigkeiten werden nicht beiläufig mit fachlichen Änderungen aktualisiert.
- Eine Prüfung wird nicht entfernt oder abgeschwächt, um einen Pull Request grün zu machen.
- Spezialisierte Repositories dokumentieren ihre begründete Abweichung in der lokalen `AGENTS.md`.

## Alternativen

- **Vollständige Workflows je Repository:** bietet maximale lokale Freiheit, erhöht aber Wartung, Duplikation und Drift.
- **SAEF-Composer- und Testarchitektur:** ist umfangreicher, würde die vorhandene Burki24-Infrastruktur ersetzen und löst keinen belegten zusätzlichen Bedarf.
- **Nur lokale Prüfungen:** sind nützlich, liefern aber keinen reproduzierbaren Pull-Request-Gate auf der vorgesehenen Plattform.

## Folgen

Gemeinsame Verbesserungen können zentral erfolgen, während fachliche Tests im Zielprojekt verbleiben. Änderungen an `Symcon_ModuleCI` haben potenziell mehrere Consumer und benötigen entsprechend breite Prüfung. Spezialisierte Ausnahmen bleiben möglich, müssen aber ausdrücklich dokumentiert werden.

## Nachweise

- [`standards/CI.md`](../standards/CI.md)
- erfolgreiche Verwendung der gemeinsamen Prüfungen in angebundenen Burki24-Modul-Repositories
- PHP-8.5-Verifikation durch GitHub Actions in den jeweiligen Projekten
