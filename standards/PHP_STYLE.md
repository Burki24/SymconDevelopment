# PHP-Stil

## Plattform

- Ziel ist PHP 8.5 unter IP-Symcon 9.
- Projektkonfigurationen für StylePHP und php-cs-fixer sind die ausführbare Quelle für Formatierungsdetails.
- Bestehender Code wird nicht allein wegen einer fachlich unabhängigen Änderung vollständig umformatiert.

## Grundsätze

- Schreibe klaren, kleinen und nachvollziehbaren Code.
- Verwende Typinformationen dort, wo sie mit IP-Symcon, bestehenden öffentlichen Verträgen und persistierten Werten kompatibel sind.
- Behalte etablierte Namen für Properties, Variablenprofile, Identifiers, Actions und öffentliche Methoden bei.
- Behandle externe Daten und Konfigurationswerte defensiv und validiere sie an der Systemgrenze.
- Vermeide versteckte Seiteneffekte und globale Zustände, soweit die Symcon-Laufzeit sie nicht vorgibt.
- Bevorzuge frühe, verständliche Fehlerbehandlung gegenüber stillen Fehlschlägen.
- Kommentare erklären Gründe, Randbedingungen und ungewöhnliche Symcon-Besonderheiten; sie wiederholen nicht den Code.

## Helper und Wiederverwendung

Vor einer neuen Hilfsmethode wird nach einer passenden Funktion in `Symcon_ModuleHelper`, `libs/helper` und vergleichbaren Modulen gesucht. Regeln zur Zuständigkeit stehen in [`HELPER_USAGE.md`](HELPER_USAGE.md).

## Formatierung

Formatierungsänderungen werden mit der im Repository festgelegten php-cs-fixer-Konfiguration erzeugt beziehungsweise geprüft. StylePHP und php-cs-fixer müssen gemeinsam erfolgreich sein; manuelle Stilvorlieben dürfen die Projektkonfiguration nicht umgehen.

Automatische Korrekturen werden vor dem Commit auf fachfremde Änderungen geprüft.
