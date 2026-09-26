# Sichere und wiederholbare Modulmigrationen

- Status: Bestätigt
- Gültig für: veröffentlichte Burki24-Symcon-Module
- Zuletzt geprüft: 2026-09-26

## Ausgangslage oder Symptom

Eine neue Modulversion funktioniert bei frischen Instanzen, während aktualisierte Installationen alte Properties, Datenformate oder Objektstrukturen behalten. Alternativ läuft eine Migration bei jedem `ApplyChanges()` erneut oder markiert sich trotz Teilfehler als abgeschlossen.

## Diagnose

1. Stelle fest, welche reale Ausgangsversion und welche gespeicherten Daten vorliegen.
2. Vergleiche registrierte Properties, Attribute, Idents, Variablentypen und externe Datenformate.
3. Prüfe Reihenfolge und Dauerhaftigkeit des Migrationsmarkers.
4. Simuliere einen Abbruch zwischen einzelnen Seiteneffekten.
5. Führe denselben Stand erneut aus und beobachte, ob bereits erledigte Schritte sicher erkannt werden.

## Ursache

Die Implementierung beschreibt nur den aktuellen Zielzustand und berücksichtigt nicht, dass veröffentlichte Instanzen persistente Altverträge tragen. Ein einzelner Versionsmarker ersetzt keine Prüfung des tatsächlichen Zustands.

## Lösung

- Definiere für jeden Schritt Ausgangs- und Zielzustand.
- Ordne Schritte monoton und führe nur fehlende Übergänge aus.
- Bewahre stabile Idents und Daten, sofern die fachliche Identität erhalten bleibt.
- Setze den dauerhaften Marker erst nach erfolgreichem Abschluss.
- Entkopple externe, nicht sicher wiederholbare Aktionen von rein lokalen Datenübergängen.
- Gib bei nicht automatisch lösbaren Altdaten eine klare Diagnose und dokumentierte manuelle Maßnahme aus.

## Verifikation

Verwende repräsentative historische Fixtures oder rekonstruierte Altzustände. Prüfe frische Installation, jede unterstützte Ausgangsversion, doppelte Ausführung, bereits migrierten Zustand und Wiederanlauf nach Teilfehler. Der Nachweis umfasst die überführten Daten und Verträge, nicht nur den Versionsmarker.

## Grenzen und Risiken

Ohne reale historische Daten bleibt die Kompatibilität teilweise unbewiesen. Datenlöschung, Typwechsel und Eingriffe in Archivhistorien benötigen einen gesonderten, besonders engen Umfang und gegebenenfalls eine Rückfallmöglichkeit.

## Quellen und verwandte Einträge

- [`standards/MIGRATIONS.md`](../standards/MIGRATIONS.md)
- [`knowledge/idempotent-configuration.md`](idempotent-configuration.md)
- [`standards/TESTING.md`](../standards/TESTING.md)
