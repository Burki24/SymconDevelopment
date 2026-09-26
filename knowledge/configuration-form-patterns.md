# Robuste dynamische Konfigurationsformulare

- Status: Bestätigt
- Gültig für: IP-Symcon 9 / Module mit `form.json` und optionalem `GetConfigurationForm()`
- Zuletzt geprüft: 2026-09-26

## Ausgangslage oder Symptom

Ein statisches Formular funktioniert, aber nach dynamischen Ergänzungen lässt sich die Instanzkonfiguration nicht mehr öffnen, Felder verlieren Werte oder leere Laufzeitdaten führen zu ungültigem JSON.

## Diagnose

1. Validiere die unveränderte `form.json` separat.
2. Rufe `GetConfigurationForm()` für leere, normale und fehlerhafte Laufzeitzustände auf und dekodiere das Ergebnis erneut.
3. Vergleiche persistente Feldnamen mit den registrierten Properties.
4. Prüfe, ob dynamischer Code notwendige Wurzelfelder überschreibt oder Array-/Objektformen verwechselt.
5. Prüfe externe Zugriffe beim Öffnen des Formulars auf Timeout und Fehlerbehandlung.

## Ursache

Dynamische Formulare werden häufig vollständig im PHP-Code zusammengesetzt oder behandeln eine optionale Laufzeitantwort als zwingende Voraussetzung. Dadurch vermischen sich statische Konfiguration, UI-Zustand und fachliche Laufzeitlogik.

## Lösung

- Halte die stabile Grundstruktur in `form.json`.
- Lade und validiere sie mit dem vorhandenen `ConfigurationFormHelper`, wenn dieser im Projekt eingebunden ist.
- Ergänze nur die wirklich dynamischen Abschnitte.
- Stelle für fehlende Daten einen gültigen leeren oder erklärenden UI-Zustand bereit.
- Verwende stabile Schlüssel in Listen und Configuratoren.
- Behandle `visible` und `enabled` nur als UI-Hilfe; validiere Properties erneut in `ApplyChanges()`.
- Delegiere komplexe Actions an Modulmethoden und halte Formularskripte klein.

## Verifikation

Das zurückgegebene Formular lässt sich in allen relevanten Zuständen als JSON-Objekt dekodieren. Persistente Werte bleiben nach Öffnen, Interaktion und erneutem Übernehmen erhalten. Dynamische Listen funktionieren leer und gefüllt, und Fehlerzustände blockieren nicht das gesamte Formular.

## Grenzen und Risiken

Nicht jede dynamische Änderung lässt sich ohne Laufzeitzugriff erzeugen. Solche Zugriffe benötigen kurze, kontrollierte Fehlerpfade und dürfen keine Geheimnisse oder vollständigen externen Antworten in der UI ausgeben.

## Quellen und verwandte Einträge

- [`standards/CONFIGURATION_FORM.md`](../standards/CONFIGURATION_FORM.md)
- [`references/Symcon_ModuleHelper.md`](../references/Symcon_ModuleHelper.md)
- [Lokale Symcon-Dokumentation](../references/symcon/README.md)
