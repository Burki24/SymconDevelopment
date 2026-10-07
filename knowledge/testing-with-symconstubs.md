# Tests mit Symcon-Stubs sinnvoll abgrenzen

- Status: Bestätigt
- Gültig für: Burki24-Modul-Repositories mit Tests unter `tests`
- Zuletzt geprüft: 2026-09-26

## Ausgangslage oder Symptom

Lokale Tests sind grün, aber die Ausführung unter IP-Symcon verhält sich anders. Umgekehrt wird auf Tests verzichtet, weil eine vollständige Symcon-Laufzeit lokal nicht verfügbar ist.

## Diagnose

1. Lies Bootstrap, Stub-Version und vorhandene Test-Helper des Zielrepositories.
2. Ordne jeden Test einer beobachtbaren Anforderung zu.
3. Markiere Laufzeitgrenzen, die der Stub nur vereinfacht oder gar nicht abbildet.
4. Prüfe, ob Assertions öffentliches Verhalten sichern oder lediglich interne Implementierungsdetails spiegeln.
5. Vergleiche lokale Plattformversion mit der maßgeblichen PHP-8.5-CI.

## Ursache

Stubs werden entweder als vollständige Symcon-Simulation missverstanden oder wegen ihrer Grenzen gar nicht genutzt. Beides verliert wertvolle Nachweise: reine PHP-Logik und viele Modulverträge sind gut testbar, reale Laufzeitintegration jedoch nicht vollständig.

## Lösung

- Nutze die bestehende Stub- und Testinfrastruktur des Repositories.
- Teste Konfiguration, öffentliche Actions, Datenumwandlung, Fehlerfälle, Migrationen und idempotente Wiederholung an stabilen Einstiegspunkten.
- Isoliere externe Dienste an klaren Grenzen und bevorzuge realistische Fixtures gegenüber tautologischen Mocks.
- Ergänze bei Laufzeitbesonderheiten einen klar benannten manuellen oder CI-basierten Nachweis.
- Leite erwartete Werte aus Vertrag und Beispieldaten ab, nicht aus derselben Implementierungslogik wie der Produktcode.

## Verifikation

Führe zuerst den betroffenen Test, danach die passende Gesamtsuite sowie Style- und Strukturprüfungen aus. Der Abschlussbericht nennt getrennt, was Stubs, CI und gegebenenfalls ein realer Symcon-Test tatsächlich belegen.

## Grenzen und Risiken

Stubs beweisen keine vollständige Ereignisreihenfolge, Visualisierungsdarstellung, Gerätekommunikation oder jedes Verhalten nativer Symcon-Funktionen. Eine grüne Testsuite ersetzt deshalb nicht automatisch einen erforderlichen Integrations- oder Praxistest.

## Quellen und verwandte Einträge

- [`standards/TESTING.md`](../standards/TESTING.md)
- [`standards/CI.md`](../standards/CI.md)
- [Offizielle Symcon-Dokumentation für KI-Agenten](../references/symcon/README.md)
