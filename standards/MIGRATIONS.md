# Modulmigrationen

## Ziel

Migrationen überführen veröffentlichte Installationen kontrolliert in einen neuen Zustand. Sie erhalten Benutzerkonfiguration, stabile Objektidentitäten und relevante Daten, soweit die beschlossene Änderung nichts anderes ausdrücklich verlangt.

Eine neue Property mit kompatiblem Defaultwert ist nicht automatisch eine komplexe Migration. Umbenennungen, Typänderungen, neue Datenformate, geänderte Idents, verschobene Zuständigkeiten und das Entfernen verwalteter Objekte benötigen dagegen eine ausdrückliche Migrationsentscheidung.

## Vorbereitung

Vor der Implementierung werden dokumentiert:

- Ausgangs- und Zielzustand;
- unterstützte Ausgangsversionen;
- betroffene Properties, Attribute, Variablen, Profile, Objekte und externe Daten;
- unverändert zu erhaltende öffentliche Verträge;
- Verhalten bei Teilfehler, Neustart und erneuter Ausführung;
- notwendige Tests und eine sichere Rückfallstrategie.

Unbekannte Altzustände werden nicht durch Vermutungen überschrieben. Falls reale historische Konfigurationen fehlen, wird diese Beweislücke sichtbar benannt.

## Umsetzung

- Registriere aktuelle Properties und Attribute weiterhin deterministisch in `Create()` nach der bestehenden Modulkonvention.
- Führe notwendige Migrationen in einer klaren, versionierten Reihenfolge aus, bevor davon abhängige neue Konfiguration aktiv wird.
- Verwende für dauerhafte Migrationsmarker einen dafür vorgesehenen persistenten Modulzustand, nicht nur flüchtigen Laufzeitstatus.
- Jeder Schritt prüft seinen tatsächlichen Ausgangszustand und bleibt bei Wiederholung sicher.
- Markiere einen Schritt erst nach erfolgreicher Durchführung als abgeschlossen.
- Bewahre stabile Idents, wenn die fachliche Identität einer Variable oder eines Objekts gleich bleibt.
- Lösche Benutzerwerte, Archivhistorie oder manuell angelegte Objekte niemals als unbeabsichtigten Nebeneffekt.
- Protokolliere relevante Fehler mit ausreichendem, aber nicht sensiblem Kontext.

Mehrere historische Schritte dürfen nacheinander auf einen aktuellen Zielstand führen. Ein frisches Modul muss direkt den aktuellen Zustand erhalten und darf keine künstliche Altinstallation durchlaufen.

## Fehler- und Wiederanlaufverhalten

Eine Migration kann durch ungültige Altdaten, fehlende Abhängigkeiten oder einen Laufzeitfehler abbrechen. Danach muss ein erneutes `ApplyChanges()` den Zustand erkennen und sicher fortsetzen oder verständlich abbrechen können.

- Keine Erfolgsmarkierung vor Abschluss aller zugehörigen Seiteneffekte.
- Keine unbeschränkten Wiederholungen externer, nicht idempotenter Aktionen.
- Kein stilles Zurücksetzen auf Defaults bei nicht lesbaren Altdaten.
- Ein nicht automatisch lösbarer Zustand erhält eine klare Status- oder Fehlermeldung und eine dokumentierte manuelle Maßnahme.

## Prüfung

Mindestens erforderlich sind, soweit für die Änderung relevant:

- frische Installation ohne Altzustand;
- jede unterstützte Ausgangsversion oder repräsentative historische Fixtures;
- zweimalige Ausführung derselben Migration;
- bereits vollständig migrierter Zustand;
- Teilzustand nach einem simulierten Fehler und anschließender Wiederanlauf;
- Erhalt von Idents, Werten, Actions und Archivbezug;
- ungültige oder unerwartete Altdaten;
- aktuelle Modul-README und gegebenenfalls ADR.

Migrationstests liegen unter `tests` und verwenden die vorhandenen Symcon-Stubs und Projekt-Fixtures. Ein Test, der nur den gesetzten Versionsmarker prüft, belegt nicht die korrekte Datenüberführung.
