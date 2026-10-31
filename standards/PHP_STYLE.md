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

## Datenqualität und Protokollwerte

- Unterscheide fehlende, ungültige und veraltete Daten von gültigen Nullwerten und `false`. Fehlende Felder dürfen nicht durch Typumwandlung zu scheinbar gültigen Messwerten werden.
- Lege je Datenart fest, ob der letzte gültige Wert erhalten bleibt, wann er veraltet ist und wie Verfügbarkeit und Zeitpunkt erkennbar werden. Historische Werte dürfen nicht als aktuelle Messung erscheinen. Alarm- und Anwesenheitszustände benötigen eine fachlich begründete Regel für ausbleibende Daten; weder sofortiger Alarm noch pauschales Beibehalten ist universell richtig.
- Belege Einheit, Skalierung und zulässigen Wertebereich durch Herstellerdokumentation, nachvollziehbare Protokollquellen oder unabhängige Referenzvektoren. Eine Variablendarstellung ist keine Quelle für den Gerätevertrag. Noch ungeklärte Annahmen werden im Code und im Projektkontext mit ihren Folgen gekennzeichnet.
- Laufzeitdaten werden aus den zuständigen Properties, Attributen, Buffern oder ausdrücklich vorgesehenen öffentlichen Schnittstellen gelesen. Objektname und Zusammenfassung sind Anzeigeinformationen und keine technischen Ersatzdaten.

## Benutzerhoheit und Objektzugriffe

Bei bestehenden Objekten bleiben vom Benutzer geänderte Namen und Symbole erhalten. Standardbezeichnungen werden bei der Anlage vergeben; spätere Änderungen benötigen eine ausdrücklich vorgesehene Benutzeraktion oder eine dokumentierte Migrationsentscheidung. Stabile Idents bleiben davon unabhängig.

Zugriffe außerhalb der eigenen Instanz sind grundsätzlich lesend. Schreibende Integrationen sind nur über einen ausdrücklich vorgesehenen, dokumentierten und vom Benutzer beauftragten Funktionsvertrag zulässig. Zielobjekte, veränderbare Felder, Bestätigung und Seiteneffekte werden begrenzt; sonstige Einstellungen bleiben erhalten. Geräteaktionen verwenden den öffentlichen Action-Vertrag, keine direkten Wertschreibzugriffe auf fremde Instanzen. Löschungen benötigen eine klare Vorabinformation und bei destruktiven Bedienaktionen eine Bestätigung gemäß [`CONFIGURATION_FORM.md`](CONFIGURATION_FORM.md). Live-Zugriffe des Agenten regelt zusätzlich [`SYMCON_ACCESS.md`](SYMCON_ACCESS.md).

## Fehlerverträge öffentlicher Methoden

- Lege vor der Umsetzung fest, wie Aufrufer Erfolg, Ablehnung, Teilfehler und unbekannten Ausgang erkennen: über kompatible Rückgabewerte beziehungsweise strukturierte Antworten und, soweit erforderlich, Status oder lokalisierte Meldungen. Bestehende öffentliche Verträge bleiben maßgeblich.
- Validiere Parameter und zulässige Kombinationen vor externen Anfragen oder Schreibzugriffen. Nach einem gescheiterten Verbindungsaufbau entfallen davon abhängige Folgeanfragen.
- Debug-Ausgaben ergänzen den Fehlervertrag, ersetzen aber keine für den Aufrufer erforderliche Rückmeldung. Sichere Diagnose folgt [`DEBUG_OUTPUT.md`](DEBUG_OUTPUT.md); private Inhalte und ungeprüfte Exception-Texte werden nicht weitergereicht.
- Ein Fehler einer optionalen Zusatzfunktion darf einen weiterhin funktionsfähigen Hauptdienst nicht pauschal auf Fehler setzen. Beeinträchtigungen bleiben über einen passenden Teilzustand oder eine gezielte Rückmeldung erkennbar, soweit sie für die Nutzung relevant sind.
- Begrenze umfangreiche Antworten durch dokumentierte Seiten oder fachlich geeignete Umfangsgrenzen. Konkrete Laufzeitlimits werden nur mit Nachweis für die unterstützte Plattform vorausgesetzt.

Versionsabhängige Aussagen über Ausgabe- und Fehlerweitergabe, Rückgabelimits oder Darstellungsparameter werden erst nach einem auf Symcon 9.0 bezogenen Nachweis übernommen. Geeignet sind ausdrücklich versionsbezogene offizielle Dokumentation oder ein reproduzierbarer Laufzeitnachweis mit Version, Edition, Aufruf und Ergebnis. Beobachtungen aus 9.1/Rust allein belegen kein Verhalten unter 9.0. Bis dahin wird daraus keine neue Implementierungsvorgabe abgeleitet und kein bestehender Vertrag geändert.

## Helper und Wiederverwendung

Vor einer neuen Hilfsmethode wird nach einer passenden Funktion in `Symcon_ModuleHelper`, `libs/helper` und vergleichbaren Modulen gesucht. Regeln zur Zuständigkeit stehen in [`HELPER_USAGE.md`](HELPER_USAGE.md).

## Basisklasse und Strict-Kompatibilität

Für neue Module wird `IPSModuleStrict` gemäß der [offiziellen Symcon-Empfehlung](https://www.symcon.de/de/llms/developer/sdk-tools/sdk-php/module.md) verwendet. Öffentliche Methoden erhalten vollständige Type Hints. Überschriebene Methoden und eingebundene Traits müssen zur tatsächlich verwendeten Basisklasse passen, einschließlich Sichtbarkeit, Parameter- und Rückgabetypen.

Bestehende Module werden nicht beiläufig von `IPSModule` auf `IPSModuleStrict` umgestellt. Rückgabewerte der Variablenregistrierung, Schreibzugriffe und Datenfluss können sich unterscheiden; ein Wechsel benötigt eine eigene Kompatibilitätsprüfung. Diagnose und Nachweis: [`knowledge/strict-module-helper-compatibility.md`](../knowledge/strict-module-helper-compatibility.md).

## Formatierung

Formatierungsänderungen werden mit der im Repository festgelegten php-cs-fixer-Konfiguration erzeugt beziehungsweise geprüft. StylePHP und php-cs-fixer müssen gemeinsam erfolgreich sein; manuelle Stilvorlieben dürfen die Projektkonfiguration nicht umgehen.

Automatische Korrekturen werden vor dem Commit auf fachfremde Änderungen geprüft.
