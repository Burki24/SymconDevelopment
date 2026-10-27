# Knowledge Base

Hier liegt wiederverwendbares Praxiswissen für Burki24-Symcon-Projekte: typische Fehlerbilder, Diagnosewege, Besonderheiten von IP-Symcon 9 / PHP 8.5 und bewährte, überprüfte Lösungswege.

Knowledge-Artikel sind keine verbindlichen Standards und keine Ersatz-ADRs. Ändert eine Erkenntnis eine verbindliche Regel, wird zusätzlich das zuständige Standarddokument angepasst und gegebenenfalls ein ADR erstellt.

## Katalog

| Artikel | Status | Thema |
| --- | --- | --- |
| [`idempotent-configuration.md`](idempotent-configuration.md) | Bestätigt | wiederholbare Objekt- und Modulkonfiguration |
| [`configuration-form-patterns.md`](configuration-form-patterns.md) | Bestätigt | robuste statische und dynamische Formulare |
| [`variable-presentations.md`](variable-presentations.md) | Bestätigt | native Darstellungen, Legacy-Profile und Actions |
| [`safe-module-migrations.md`](safe-module-migrations.md) | Bestätigt | versionierte und wiederanlauffähige Migrationen |
| [`testing-with-symconstubs.md`](testing-with-symconstubs.md) | Bestätigt | Aussagekraft und Grenzen der Stub-basierten Tests |
| [`runtime-diagnostics.md`](runtime-diagnostics.md) | Entwurf | begrenzte Diagnosezustände ohne neuen Helper-Vertrag |
| [`strict-module-helper-compatibility.md`](strict-module-helper-compatibility.md) | Dokumentationsgeprüft | Basisklassen-Verträge und projektspezifische Strict-Kompatibilität |
| [`stub-loader-root-directories.md`](stub-loader-root-directories.md) | Quelltextgeprüft | zusätzliche Wurzelordner beim Laden einer Bibliothek durch Symcon-Stubs |
| [`debug-rollout-2026-10.md`](debug-rollout-2026-10.md) | Lokal geprüft | OHA-Debug-Aufbau in 64 weiteren Modulen, Nachweise und Abnahmegrenzen |

## Anforderungen an einen Artikel

- konkreter Kontext und betroffene Versionen
- beobachtbare Symptome oder Ausgangslage
- nachvollziehbarer Diagnoseweg
- bestätigte Ursache
- Lösung und Verifikation
- Grenzen, Risiken und verwandte Quellen

Nutze [`TEMPLATE.md`](TEMPLATE.md) als Ausgangspunkt. Entferne überholte Artikel nicht stillschweigend; kennzeichne sie und verweise auf den Nachfolger.
