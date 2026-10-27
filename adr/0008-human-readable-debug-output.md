# ADR 0008: Einheitliche, verständliche Debug-Ausgaben

- Status: Angenommen
- Datum: 2026-10-18
- Entscheider: Burki24, Auftrag im Debug-Chat
- Ersetzt: –
- Ersetzt durch: –

## Kontext

Menschen müssen die programmierten Abläufe und ihre Auswirkungen anhand der Debug-Ausgabe verstehen können. Einzelne Fehlertexte ohne Quelle, Entscheidung oder Ergebnis genügen dafür nicht. Die Umstellung beginnt ausdrücklich mit OpenHomeAlarm als Pilot.

## Entscheidung

Die Module folgen dem [Debug-Standard](../standards/DEBUG_OUTPUT.md): deutsche Meldungen, einheitliche Ereignisse, Funktions- und Zeilenangaben, Start und Ende mit Ergebnis sowie nachvollziehbare Werte, Aktionen und interne beziehungsweise externe Kommunikation. Vorgangs- und Aufrufkennungen verbinden verschachtelte Abläufe.

Die bestehende zentrale Quelle `Symcon_ModuleHelper/DebugHelper` übernimmt Bereinigung und Begrenzung. Fachliche Erklärungen und sichere Auswahl der Daten verbleiben im Modul. Eine neue gemeinsame Ablaufabstraktion wird erst aus weiteren nachgewiesenen Anwendungen abgeleitet. Die Modulverträge und das fachliche Verhalten bleiben erhalten.

Für den am 18.10.2026 beauftragten Rollout auf die übrigen Module wird die
wiederkehrende Vorgangs-, Aufruf- und Ergebnisführung als `DebugFlowHelper`
in der zentralen Quelle bereitgestellt. Taster- und Zirkulationssteuerung
belegen die erste gemeinsame Nutzung. Die fachlichen Entscheidungen und
Schnittstellenmeldungen verbleiben im jeweiligen Modul. OHA bleibt die
abgenommene Referenz und wird dabei nicht erneut umgebaut.

## Alternativen

- Nur Fehlertexte übersetzen: verbessert die Sprache, erklärt aber weder Ablauf noch Wirkung.
- Sämtliche Argumente und Antworten ausgeben: erzeugt Geheimnislecks und schwer lesbare Datenmengen.
- Sofort alle Module mechanisch umstellen: übersieht fachliche Unterschiede und verhindert eine überprüfbare Pilotabnahme.

## Folgen

Der Pilot erhält automatisierte Nachweise und eine eigene manuelle Debug-Abnahme. Weitere Module werden einzeln geprüft und umgestellt. Eine lokale Implementierung oder grüne Stub-Suite ist keine Freigabe für Installation, Veröffentlichung oder nachgewiesene Gerätewirkung.
