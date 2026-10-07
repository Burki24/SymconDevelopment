# Strict-Module und Helper-Kompatibilität

- Status: Dokumentationsgeprüft; konkrete Helper-Kompatibilität projektspezifisch offen
- Gültig für: IP-Symcon 9 / PHP 8.5, insbesondere Module mit `IPSModuleStrict`
- Zuletzt geprüft: 2026-10-07, offizielle Symcon-Moduldokumentation

## Ausgangslage

Die Basisklasse eines Moduls und eingebundene Helper-Traits bilden einen gemeinsamen PHP-Vertrag. Eine für `IPSModule` geschriebene Implementierung darf nicht allein aufgrund ähnlicher Methodennamen als kompatibel mit `IPSModuleStrict` gelten.

## Diagnose

1. Tatsächliche Basisklasse des Moduls und unterstützte Plattform feststellen.
2. Öffentliche Modulmethoden und von Traits überschriebene Methoden mit der offiziellen Basisklassen-Signatur vergleichen, einschließlich Sichtbarkeit, Parametern und Rückgabetypen.
3. Die tatsächlich eingebundene Version von `Symcon_ModuleHelper` und vorhandene Projekttests prüfen. Ein synthetisches Testobjekt ersetzt keinen Nachweis gegen die echte Basisklasse.
4. Annahmen über Rückgabewerte und Datenfluss prüfen: Laut offizieller Dokumentation benötigen öffentliche Methoden unter `IPSModuleStrict` Type Hints; `RegisterVariable*` liefert dort einen Boolean statt einer Variablen-ID. Weitere Unterschiede betreffen unter anderem Variablenschreibzugriffe und Datenfluss.

## Lösung

Für neue Module wird `IPSModuleStrict` gemäß offizieller Empfehlung verwendet. Bestehende Module werden nicht allein wegen dieser Empfehlung migriert. Ein Wechsel der Basisklasse muss als eigene Kompatibilitätsänderung geplant werden; betroffene Helper, Actions, Variablen und Datenflussverträge gehören zum Umfang.

Passende zentrale Helper werden weiterhin über den vorgesehenen Burki24-Consumer-Prozess eingebunden. Fehlende Kompatibilität wird im zuständigen Helper-Repository als getrennte Änderung behandelt; keine lokalen Kopien oder stillen Ersatzimplementierungen anlegen. Aus diesem Artikel folgt keine pauschale Aussage, dass alle vorhandenen Helper bereits strict-tauglich oder inkompatibel seien.

## Verifikation und Grenzen

PHP-Syntaxprüfung allein belegt keine vollständige Basisklassen-Kompatibilität. Modul und Traits zusammen gegen die verwendete Basisklasse laden, relevante Tests ausführen und Laufzeitbesonderheiten auf einer freigegebenen Entwicklungsinstanz prüfen. Der Bericht unterscheidet dokumentierte Plattformregeln und tatsächlich nachgewiesene Kompatibilität des konkreten Moduls.

In dieser Dokumentationsänderung wurde keine vollständige Helper- oder Modulprüfung durchgeführt.

## Quellen

- [Offizielle Symcon-Moduldokumentation, Abschnitt module.php](https://www.symcon.de/de/llms/developer/sdk-tools/sdk-php/module.md)
- [`standards/PHP_STYLE.md`](../standards/PHP_STYLE.md)
- [`standards/HELPER_USAGE.md`](../standards/HELPER_USAGE.md)
- [`standards/SYMCON_ACCESS.md`](../standards/SYMCON_ACCESS.md)
