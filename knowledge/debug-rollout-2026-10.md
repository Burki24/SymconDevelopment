# Debug-Aufbau nach OpenHomeAlarm: Umsetzung Oktober 2026

Stand: 18.10.2026. Lokale Umsetzung und Prüfung; die Abnahme in einer laufenden Symcon-Installation steht aus.

## Umfang und Ergebnis

Der vom Benutzer akzeptierte OpenHomeAlarm-Aufbau wurde auf 64 weitere Module in zwölf primären Bibliotheken übertragen. OpenHomeAlarm bleibt unverändert. Doppelte Review-, Release- und Worktree-Checkouts wurden nicht zusätzlich bearbeitet. IPS_LMNB enthält keine entsprechenden Modulquellen und ist nicht mit OpenLMNB zu verwechseln.

Die Ausgaben enthalten deutsche Meldungen, Modul und Ereigniskategorie, Funktion und Zeile sowie Instanz, Vorgang, Aufruf und fachlichen Bezug. Start und Ende verbinden den Ablauf mit seinem tatsächlichen Ergebnis. Aktionen, Wertübertragungen, Wertempfang, Fehler und interne beziehungsweise externe Kommunikation erhalten passende Diagnosepunkte. Private Inhalte werden ausgelassen, maskiert oder ausschließlich als Umfang beschrieben.

Der gemeinsame Ablauf liegt im neuen DebugFlowHelper des kanonischen Repositorys Symcon_ModuleHelper. Projektspezifische Adapter binden vorhandene Logger und Basisklassen ein. Die Consumer-Kopien samt DebugHelper und Hashmanifest wurden über den bestehenden Bundle-Weg erzeugt und auf Bytegleichheit geprüft. Die lokale Herkunft ist ehrlich als `working-tree` gekennzeichnet: Für die spätere reguläre Veröffentlichung ist zuerst der zentrale Helper bereitzustellen und anschließend der normale Consumer-Sync auszuführen.

## Nachweise je Bibliothek

| Bibliothek | Module | Lokale Prüfung |
| --- | ---: | --- |
| ShutterButtonControl | 1 | Vollständiger Testlauf erfolgreich; lange Betätigung und STOP, unveränderte Befehle und Ausfall des Debug-Kanals geprüft. |
| Zirkulationspumpensteuerung | 2 | Vollständiger Testlauf erfolgreich; Ein-/Ausschalten, wiederholtes Einschalten und Ausschalten bei defektem Debug-Kanal geprüft. |
| IPS_Wolf_WSR1 | 2 | Neue Debug-, Datenfluss-, Helper-, Empfangspuffer-, Visualisierungs- und Metadatentests erfolgreich. Gesamtlauf durch vorhandenen Strukturfehler blockiert, siehe unten. |
| IPS_Informations | 1 | Neuer lokaler Testlauf erfolgreich; unveränderte Rückgaben, Statusunterdrückung und Schutz privater Inhalte geprüft. |
| BlindControl | 2 | Neuer lokaler Testlauf erfolgreich; Ablehnung bei inaktiver Instanz, fehlende Aktorbefehle, Aufrufpaare und geschützte Hinweise geprüft. |
| iCal-Calendar | 1 | Vollständiger lokaler Testlauf erfolgreich; Kalenderübergabe per Referenz, Fehlerweitergabe sowie Schutz von Kalenderinhalt und ungültigen privaten Suchmustern geprüft. |
| OpenCalendar | 4 | Vollständiger Testlauf einschließlich lokaler CalDAV-HTTP-Integration erfolgreich. |
| OpenLMNB | 4 | Debug- und übrige Einzelprüfungen erfolgreich; Gesamtlauf durch vorhandenen Strukturmarker blockiert, siehe unten. |
| SymconECharts | 30 | Vollständiger Testlauf und Projekt-Qualitätslauf erfolgreich, einschließlich PHP-, JavaScript- und Vertragsprüfungen. |
| IPSViewAssistant | 1 | Vollständiger Testlauf erfolgreich, einschließlich neuer Diagnoseprüfungen. |
| JSLive | 10 | Vollständiger Testlauf erfolgreich; zusätzlicher Abschlusslauf für überlange Diagnosekontexte erfolgreich. |
| Zigbee2MQTT | 6 | Debug-Test: 4 Tests, 312 Assertions erfolgreich. Ergänzender Gesamtlauf mit dokumentiertem lokalem Loaderfilter: 329 Tests, 4788 Assertions ohne Fehler; 14 bestehende Deprecations. Regulärer Gesamtlauf siehe unten. |

Die vollständigen Läufe von elf Bibliotheken wurden zusätzlich zentral ausgeführt; bei Wolf und OpenLMNB reproduzierten sie die bekannten Fehler. Die Debug-Tests der sechs zuerst umgestellten Bibliotheken wurden unabhängig durchgesehen und ausgeführt. Dabei gefundene fehlende Ablehnungsursachen in BlindControl und private Warnlog-Inhalte in iCal wurden innerhalb des Diagnoseumfangs korrigiert und erneut geprüft. Die abschließenden JSLive- und Zigbee2MQTT-Diagnosetests wurden ebenfalls zentral ausgeführt.

Symcon_ModuleHelper: PHP-Testlauf, Manifestprüfung für 27 Helper, Bundle-Tests und simulierte Auto-Merge-Tests erfolgreich. Letztere führen keine tatsächlichen GitHub-Merges aus. Alle zwölf Consumer haben unveränderte Bibliotheksmetadaten und bestehen `git diff --check`; Helper und Abhängigkeiten stimmen mit der zentralen Quelle überein. PHP-Syntax der geänderten Laufzeit- und Diagnose-Dateien wurde geprüft.

## Bereits vorhandene Prüfprobleme

1. **IPS_Wolf_WSR1:** `tests/validate_structure.py` findet den alten Repositorynamen in `.git/config`. Der Fehler bestand bereits vor den Änderungen. Git-Konfiguration und Strukturprüfer wurden dafür nicht verändert.
2. **OpenLMNB:** Der Strukturprüfer erwartet die genaue Signatur `VisualizationThemeCSS(): string`; der vorhandene Code verwendet bereits `VisualizationThemeCSS(array $overrides = []): string`. Der Widerspruch besteht auch im bisherigen HEAD.
3. **Zigbee2MQTT:** Der offizielle Stub-Loader interpretiert den vorhandenen Wurzelordner `state` als Modul und erwartet `state/module.json`. Regulär entstehen dadurch 262 Ladefehler bei 329 Tests. Der zusätzliche erfolgreiche Lauf schließt nur diesen Nichtmodulordner im temporären Test-Bootstrap aus. Benutzerzustand und offizielle Stubs bleiben unverändert. Der reproduzierbare Bootstrap ist in `Zigbee2MQTT/docs/DEBUG_OUTPUT.md` dokumentiert und nach der Prüfung entfernt worden.

IPS_Informations, BlindControl und iCal besitzen außerdem bereits Formatierungsaltlasten in ihren bisherigen Quellen. Sowohl bisheriger HEAD als auch Arbeitsstand scheitern mit derselben Referenzkonfiguration. Es erfolgte keine breite Umformatierung dieser Quellen; die neuen Tests wurden geprüft und formatiert. Ein vollständig grüner Style-Lauf dieser Altbestände wird damit nicht behauptet.

## Aussagegrenzen und nächste Abnahme

Lokale Tests beweisen keine vollständige reale Geräteabnahme. Besonders die positiven Fahr-, Lamellen-, Zeitplan- und Notfallpfade von BlindControl sind durch die neuen fokussierten Tests nicht vollständig abgedeckt. Externe Konten und reale Aktoren wurden nicht angesteuert. Die projektspezifischen Details und Testbefehle stehen jeweils unter `docs/DEBUG_OUTPUT.md` der Bibliotheken.

Die praktische Abnahme erfolgt schrittweise je Bibliothek anhand eines normalen Ablaufs, eines abgelehnten beziehungsweise fehlerhaften Vorgangs und einer Kommunikationssequenz. Dabei sind verständliche deutsche Meldungen, zusammenhängende Vorgangskennungen, Start/Ende, tatsächliche Ergebnisse und das Fehlen privater Inhalte zu prüfen.

Es wurden keine Commits, Pushes, Versionsanhebungen, Veröffentlichungen oder Änderungen am laufenden Symcon-System vorgenommen. Bestehende fremde Änderungen bleiben erhalten.

## Verwandte Regeln

- [Debug-Standard](../standards/DEBUG_OUTPUT.md)
- [ADR 0008](../adr/0008-human-readable-debug-output.md)
- [Stub-Loader und Wurzelordner](stub-loader-root-directories.md)
