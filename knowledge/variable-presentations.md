# Native Variablendarstellungen und Legacy-Profile

- Status: Bestätigt
- Gültig für: IP-Symcon 9 / `Symcon_ModuleHelper` 3.x
- Zuletzt geprüft: 2026-09-26

## Ausgangslage oder Symptom

Eine Variable enthält den richtigen Wert, erscheint aber mit falscher Einheit, ungeeigneter Bedienung oder abweichenden Auswahlwerten. Nach einer Modernisierung funktioniert die Visualisierung, aber eine bestehende Action oder ein altes Profilverhalten ist verloren gegangen.

## Diagnose

1. Prüfe Variablentyp, Ident und fachliche Wertebedeutung getrennt von der Darstellung.
2. Ermittle, ob eine native Presentation, ein Legacy-Profil oder eine benutzerdefinierte Vorlage aktiv ist.
3. Vergleiche Wertebereich, Schrittweite, Einheit, Nachkommastellen, Optionen, Icons und Farben.
4. Prüfe bei steuerbaren Variablen Action-Aktivierung und `RequestAction()`.
5. Suche nach lokalen Presentation-Arrays, für die bereits eine Methode im `VariablePresentationHelper` existiert.

## Ursache

Typ, Darstellung und Action werden als ein einziger Vertrag behandelt oder eine optische Modernisierung ersetzt unbeabsichtigt semantische Details des bisherigen Profils. Lokale Presentation-Kopien können zusätzlich vom zentralen Helper abweichen.

## Lösung

- Nutze für neue beziehungsweise bewusst modernisierte Variablen eine passende native Darstellung.
- Verwende den zentralen `VariablePresentationHelper`, wenn sein Vertrag passt.
- Erhalte Ident, Typ und Action-Verhalten bei rein visuellen Änderungen.
- Migriere Legacy-Profile nur nach einem vollständigen Vergleich ihrer Semantik.
- Belasse geräte- oder providerspezifische Ableitung im jeweiligen Modul und übergib dem Helper bereits fachlich bestimmte Parameter.

## Verifikation

Prüfe Darstellung und Bedienung in den vom Projekt unterstützten Visualisierungen. Tests sichern das Presentation-Array, gültige und ungültige Actions sowie wiederholtes `ApplyChanges()` ab. Bestehende Installationen behalten Werte, Idents und erwartetes Action-Verhalten.

## Grenzen und Risiken

Benutzer können Darstellungen oder Vorlagen installationsbezogen angepasst haben. Eine modulverwaltete Umstellung darf solche Anpassungen nicht ohne ausdrückliche Produktentscheidung überschreiben.

## Quellen und verwandte Einträge

- [`standards/VARIABLE_PRESENTATION.md`](../standards/VARIABLE_PRESENTATION.md)
- [`references/Symcon_ModuleHelper.md`](../references/Symcon_ModuleHelper.md)
- [Lokale Symcon-Dokumentation](../references/symcon/README.md)
