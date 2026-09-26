# Idempotente Modulkonfiguration

- Status: Bestätigt
- Gültig für: IP-Symcon 9 / PHP 8.5 / Burki24-Modul-Repositories
- Zuletzt geprüft: 2026-09-26

## Ausgangslage oder Symptom

Nach erneutem `ApplyChanges()` entstehen doppelte Objekte, bestehende Benutzerwerte werden zurückgesetzt oder unveränderte Konfiguration löst erneut teure Seiteneffekte aus. Fehler treten häufig erst nach mehreren Konfigurationsänderungen oder einem Neustart auf.

## Diagnose

1. Führe dieselbe Konfiguration mindestens zweimal aus und vergleiche Objektbaum, Idents, Actions und gespeicherte Werte.
2. Prüfe, ob Objekte über stabile Idents beziehungsweise die vorhandenen `Register*`- und `Maintain*`-Muster wiedergefunden werden.
3. Suche nach Erzeugung anhand sichtbarer Namen oder fest codierter ObjectIDs.
4. Trenne gewünschte Konfiguration von Laufzeitwerten, Caches und zuletzt beobachtetem Zustand.
5. Prüfe externe Schreibzugriffe, Timer- und Eventregistrierung auf unnötige Wiederholung.

## Ursache

Konfiguration wird als einmaliger Installationsablauf statt als wiederholbar ausführbare Zustandsangleichung behandelt. Häufig fehlen stabile technische Identitäten oder Code setzt bei jedem Lauf Defaults und Seiteneffekte erneut durch.

## Lösung

- Beschreibe den gewünschten Zielzustand und gleiche den vorhandenen Zustand daran an.
- Verwende stabile Idents und die vorhandenen Modulmethoden zur Registrierung und Pflege.
- Erzeuge fehlende Objekte, aktualisiere nur tatsächlich geänderte Eigenschaften und entferne ausschließlich eindeutig modulverwaltete Objekte.
- Bewahre Benutzerwerte und Archivbezug, sofern keine dokumentierte Migration etwas anderes verlangt.
- Trenne das Registrieren technischer Verträge in `Create()` von konfigurationsabhängiger Aktivierung in `ApplyChanges()` nach der vorhandenen Projektkonvention.
- Begrenze externe Seiteneffekte und speichere nur dann einen Konfigurationsfingerabdruck, wenn damit ein konkreter Diagnose- oder Optimierungsbedarf gelöst wird.

## Verifikation

- frische Installation;
- zweimaliges `ApplyChanges()` ohne Änderung;
- Wechsel zwischen gültigen Konfigurationen und zurück;
- Neustart beziehungsweise erneutes Laden des Moduls;
- unveränderte Idents, Benutzerwerte, Actions und relevante Archivzuordnung;
- keine zusätzlichen Objekte, Events oder Timer nach Wiederholung.

## Grenzen und Risiken

Externe Systeme können trotz gleicher lokaler Konfiguration einen veränderten Zustand besitzen. Eine notwendige erneute Synchronisierung ist deshalb nicht automatisch ein Idempotenzfehler, muss aber von lokaler Objektanlage und Migration getrennt bleiben.

## Quellen und verwandte Einträge

- [`standards/MODULE_STRUCTURE.md`](../standards/MODULE_STRUCTURE.md)
- [`standards/MIGRATIONS.md`](../standards/MIGRATIONS.md)
- [`principles/ENGINEERING.md`](../principles/ENGINEERING.md)
