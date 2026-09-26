# Tests

## Ablage und Ziel

Alle Tests liegen unter `tests`; `.tests` wird nicht verwendet. Tests sichern beobachtbares Modulverhalten, Fehlerfälle und Kompatibilitätsverträge ab. Sie sollen bei einem Defekt aus fachlich nachvollziehbarem Grund fehlschlagen.

## Vorgehen

1. Lies vorhandene Tests, Test-Bootstraps und Symcon-Stubs, bevor du neue Testinfrastruktur anlegst.
2. Ergänze für Fehlerkorrekturen möglichst zuerst einen fokussierten Regressionsfall.
3. Prüfe bei Features den kleinsten öffentlichen oder stabilen Einstiegspunkt.
4. Nutze vorhandene Fixtures, Stubs und Hilfen; dupliziere keine Test-Helper.
5. Führe zunächst den betroffenen Test und anschließend die passende Gesamtsuite aus.

## Abdeckungsschwerpunkte

- Konfiguration und wiederholte `ApplyChanges`-Ausführung
- gültige und ungültige Eingabedaten
- Zustandswechsel, Statusmeldungen und öffentliche Actions
- Kompatibilität bestehender Properties, Identifiers und gespeicherter Werte
- Fehlerbehandlung an I/O- und Symcon-Grenzen
- Migrationen und Wiederanlaufverhalten, falls betroffen

Die konkrete Testtiefe richtet sich nach dem Risiko. Reine Struktur- oder Dokumentationsänderungen benötigen keine künstlichen Verhaltenstests, wohl aber die einschlägigen Struktur- und Formatprüfungen.

## Nachweis

Ein Abschlussbericht nennt die wirklich ausgeführten Prüfungen mit Ergebnis. Nicht verfügbare Laufzeitabhängigkeiten oder ausgelassene Tests werden ausdrücklich benannt. Style- und Strukturchecks ersetzen keine Tests des geänderten Verhaltens.
