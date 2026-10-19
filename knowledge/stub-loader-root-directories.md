# Zusätzliche Wurzelordner und der Symcon-Stub-Lader

- Status: Quelltext- und laufzeitgeprüft
- Gültig für: Bibliothekstests mit `symcon/SymconStubs`, geprüfter Commit `f5a55625da66d7ac152a6400ad978bae664cc2be`
- Zuletzt geprüft: 2026-10-18; Fehler in Zigbee2MQTT reproduziert und gezieltes Modulladen vollständig geprüft

## Ausgangslage und Ursache

Tests mit `IPS\ModuleLoader::loadLibrary()` können nach dem Anlegen eines zusätzlichen Wurzelordners scheitern, obwohl der Modulcode unverändert ist.

Die geprüfte Implementierung von `loadModules()` sucht mit `glob($folder . '/*', GLOB_ONLYDIR)` nach Verzeichnissen neben `library.json`. Sie nimmt nur `libs`, `docs`, `imgs`, `tests` und `actions` aus. Alle übrigen Treffer werden an `loadModule()` übergeben, das ohne vorherige Existenzprüfung eine `module.json` liest und dekodiert. Ein Dokumentationsordner wie `adr/` kann damit versehentlich als Modul behandelt werden. Die konkrete Fehlermeldung hängt von PHP-Version und Fehlerbehandlung des Test-Bootstraps ab.

## Diagnose

1. Prüfen, ob der Test die gesamte Bibliothek oder einzelne Module lädt.
2. Die eingebundene Stub-Version und deren Verzeichnisausnahmen lesen.
3. Zusätzliche Wurzelordner mit der Ausnahmeliste vergleichen und den Stacktrace bis zum Laden der `module.json` verfolgen.
4. Änderungen an der Modulimplementierung von Änderungen am Test-Ladepfad unterscheiden.

## Lösungsmöglichkeiten

- Neue Projektdokumentation und ADRs unter `docs/`, beispielsweise `docs/adr/`, ablegen. Die Entscheidungen bleiben versioniert und nach einem Clone verfügbar.
- Einzelne Module gezielt über `loadSingleModule()` laden, wenn dies zum Testvertrag passt. Diese Methode registriert im geprüften Stand nicht die Bibliotheksmetadaten; Tests mit Bibliotheksabfragen brauchen daher weiterhin eine geeignete Registrierung.
- Eine bereits vorhandene Ablage nur im ausdrücklich geplanten Umfang ändern. Nicht pauschal alle Wurzelordner verschieben und nicht den Stub-Lader beiläufig verändern.

## Verifikation und Grenzen

Bei einer konkreten Korrektur den betroffenen Test vor und nach der Änderung ausführen, danach die passende Gesamtsuite. In Zigbee2MQTT wurde am 18.10.2026 der Fehler mit einem vorhandenen lokalen `state`-Ordner reproduziert (262 Ladefehler). Die drei Test-Einstiege wurden auf gezieltes Laden aller sechs Module mit der echten Bibliotheks-ID umgestellt. Ein Regressionstest prüft trotz zusätzlich angelegtem Arbeitsordner sämtliche Modulregistrierungen und deren Zuordnung. Der reguläre Gesamtlauf besteht mit 330 Tests und 4809 Assertions, ohne temporären Filter und ohne Stub- oder Zustandsänderung. Die 14 bestehenden Deprecations bleiben sichtbar. `LibraryTest` validiert weiterhin die Bibliotheksdatei; eine Registrierung ihrer Metadaten im Stub-Kernel wird für diese Tests nicht benötigt.

Die Aussage betrifft diesen Stub-Lader, nicht das Verhalten des echten Symcon-Kernels. Andere Stub-Versionen können abweichen. Die reine Regelwerksstruktur von `SymconDevelopment` ist keine Modulbibliothek und wird durch diese Einschränkung nicht betroffen.

## Quellen

- [SymconStubs: geprüfter KernelStubs.php-Stand](https://github.com/symcon/SymconStubs/blob/f5a55625da66d7ac152a6400ad978bae664cc2be/KernelStubs.php)
- [`standards/MODULE_STRUCTURE.md`](../standards/MODULE_STRUCTURE.md)
- [`testing-with-symconstubs.md`](testing-with-symconstubs.md)
