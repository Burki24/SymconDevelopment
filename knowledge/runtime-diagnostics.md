# Begrenzte Runtime-Diagnostik

- Status: Entwurf
- Gültig für: wiederholt laufende, zustandsbehaftete oder supportrelevante Symcon-Komponenten
- Zuletzt geprüft: 2026-09-26

## Ausgangslage oder Symptom

Der aktuelle Modulstatus ist sichtbar, aber nach einem sporadischen Fehler fehlen Zeitpunkt, Ursache und letzter erfolgreicher Zustand. Alternativ sammeln Module unbegrenzt JSON, vollständige Antworten oder Zähler in einem unklaren Sammelspeicher.

## Diagnose

Trenne vier Fragen:

1. Welcher knappe Zustand ist für Benutzer und Automationen relevant?
2. Welche Details gehören nur ins Log?
3. Welche wenigen Informationen müssen einen Neustart überstehen, damit ein späterer Fehler noch erklärbar ist?
4. Welche Daten wachsen heute ohne Grenze oder enthalten private Informationen?

## Ursache

Operativer Zustand, flüchtiges Debugging, persistente Diagnose und fachlicher Cache besitzen keine getrennte Zuständigkeit. Dadurch sind entweder zu wenige Informationen verfügbar oder Diagnoseablagen werden zu unbeschränkten Datenspeichern.

## Lösung

Je nach belegtem Bedarf können getrennte Bausteine eingesetzt werden:

- ein stabiler Konfigurations-Hash für die zuletzt verarbeitete gewünschte Konfiguration, ohne volatile Felder;
- kleine Registry-Metadaten wie Schema-Version, vorheriger Hash oder aktuelle Phase;
- typisierte Zähler und Zeitstempel für Ausführungen, Fehler, Wiederholungen und letzten Erfolg;
- eine fest begrenzte Liste der letzten relevanten Fehler mit Zeitpunkt, Kategorie und bereinigtem Kontext.

Diese Daten ergänzen Logs und Fehlerbehandlung; sie ersetzen sie nicht. Geheimnisse, private Netzwerkdaten, vollständige Payloads und unbegrenzte Historien gehören nicht in Diagnosestrukturen.

Für Burki24 existiert dafür zunächst kein neuer zentraler Helper-Vertrag. Ein Projekt führt nur die tatsächlich benötigten Teile lokal und klar gekapselt ein. Erst nach mindestens zwei belegten, kompatiblen Anwendungen wird eine Aufnahme in `Symcon_ModuleHelper` bewertet.

## Verifikation

- Diagnose bleibt nach vielen Ausführungen größenbegrenzt.
- Konfigurations-Hash ändert sich nur bei relevanter Konfiguration.
- Zähler und Zeitstempel besitzen eindeutige Semantik.
- Fehlerkontext enthält keine sensiblen Daten.
- Neustart und wiederholtes `ApplyChanges()` erhalten beziehungsweise initialisieren den vorgesehenen Zustand korrekt.

## Grenzen und Risiken

Zusätzliche Diagnosevariablen erhöhen sichtbare und persistente Komplexität. Kleine, zustandslose Module benötigen diese Struktur in der Regel nicht. Ein Hash ist weder Signatur noch Sicherheitsprüfung.

## Quellen und verwandte Einträge

- [`standards/PRIVATE_DATA.md`](../standards/PRIVATE_DATA.md)
- [`knowledge/idempotent-configuration.md`](idempotent-configuration.md)
- [`adr/0002-lean-saef-adaptation.md`](../adr/0002-lean-saef-adaptation.md)
- [SAEF: Runtime Diagnostics](https://github.com/doctee/symcon-ai-framework/blob/9ee24e21e756d581e3e334313bea77f512b211cb/knowledge/EK-006-runtime-diagnostics.md) als konzeptionelle Inspirationsquelle
