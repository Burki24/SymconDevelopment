# Zugriff auf Symcon-Systeme

## Rollen und Umfang

Vor einem Systemzugriff klären, welche Instanz Entwicklung, Test oder Produktion ist und welche Lese- und Schreibaktionen der aktuelle Auftrag erlaubt. Projektspezifische Rollen und wiederkehrende Freigaben stehen in der lokalen `AGENTS.md` oder im `PROJECT_CONTEXT.md`, ohne private Endpunkte oder Zugangsdaten aufzunehmen.

- Dokumentationsabfragen können im Aufgabenrahmen ohne Zugriff auf Installationsdaten erfolgen.
- Auf einer Entwicklungs- oder Testinstanz sind Tests nur im beauftragten oder ausdrücklich dauerhaft freigegebenen Umfang zulässig.
- Auf Produktivinstanzen benötigen Änderungen, Installationen, Reloads und Tests mit Seiteneffekten einen ausdrücklichen Auftrag für das betroffene System und den konkreten Umfang. Eine Freigabe für die Entwicklung gilt nicht automatisch für die Produktion.
- Auch lesende Zugriffe auf Installationsdaten bleiben auf den für die Aufgabe nötigen Umfang begrenzt. Ein Connector oder Servername allein ist keine Freigabe für weitere Aktionen.
- Unklare Serverrollen vor abhängigen Aktionen klären. Keine Testinstanz allein aus einem Namen vermuten und keine produktive Instanz als Ersatz für eine fehlende Testumgebung verwenden.

## Durchführung

Verhalten mit Laufzeit-, Visualisierungs- oder Geräteabhängigkeit wird bevorzugt auf einer freigegebenen Entwicklungsinstanz geprüft. Vor Tests mit Seiteneffekten betroffene Objekte, externe Aktionen und Wiederherstellung berücksichtigen. Berechtigte Produktivänderungen werden vor Ausführung kurz mit Zweck und Umfang benannt.

Geheimnisse und reale Installationsdaten bleiben gemäß [`PRIVATE_DATA.md`](PRIVATE_DATA.md) außerhalb von Repository, Beispielen und Fixtures. Gelesene Daten werden nicht ungeprüft in Dokumentation oder Prüfberichte übernommen.

<a id="browserpruefung-von-mcp-kachelvorschauen"></a>

## Browserprüfung von MCP-Kachelvorschauen

Für Browserprüfungen der über `symcon_tile_preview` erzeugten Seiten gilt dieser Ablauf:

1. Einen leeren Tab mit `about:blank` erstellen.
2. Den vorhandenen Tab mit `goto(vorschauURL)` zur vom MCP gelieferten HTTP(S)-Adresse navigieren.
3. Den Ladeabschluss anhand einer Screenshot-Beobachtung prüfen; bei einem sichtbaren Ladezustand zunächst dessen Abschluss abwarten.
4. Erst anschließend `getAXState` und DOM-/Locator-Abfragen ausführen sowie Interaktionen und Browserfehler prüfen.

Die Vorschau-URL nicht unmittelbar an `createBrowserTab` übergeben. Im Vergleich mit derselben unveränderten URL erzeugte dieser direkte Öffnungspfad einen `MutationObserver.observe`-Fehler, während die getrennte Navigation mit späterer Accessibility-Abfrage fehlerfrei blieb. Der genaue interne Auslöser ist ohne Stacktrace nicht nachgewiesen; der Befund rechtfertigt keine vorsorglichen Änderungen an Modul- oder Helper-Code.

Bei entsprechenden Meldungen den Öffnungspfad kontrollieren und bei Bedarf dieselbe Kachel zusätzlich über den vom MCP gelieferten direkten HTML-Link prüfen. Fehler weder ausblenden noch allein aufgrund des Vorschauprotokolls einem Modul zuordnen. Native MCP-Kachelvorschauen zeigen nur den Anfangszustand und empfangen keine Live-Pushs. Deshalb Darstellung, lokale Bedienung und echte Live-Updates getrennt nachweisen; ein Vorschaulauf bestätigt keinen nativen Push-Transport.

<a id="mcp-wiederverbindungspruefungen"></a>

## MCP-Wiederverbindungsprüfungen

1. Den geladenen Modul-/Helper-Stand prüfen. Die echte native Kachelvisualisierung und die aktuelle eingebettete HTTP(S)-Ausgabe getrennt von statischen Vorschauen prüfen. Vor Aktionen Ladeabschluss und den aktuellen iframe kontrollieren.
2. Browseraktionen mit begrenzten Wartezeiten ausführen. Bei Klick-Timeouts Sichtbarkeit, iframe-Lage und Actionability-Protokoll prüfen. Liegt ein Button außerhalb des sichtbaren Bereichs, zuerst die Ansicht sichtbar machen. Für einen reinen Zustand-/Transporttest darf alternativ derselbe vorhandene Button per DOM-`click()` ausgelöst werden; diese Alternative dokumentieren und nicht als Nachweis eines erfolgreichen Zeigerklicks ausgeben.
3. Auswahl und Kartenanimation abschließen lassen. Zoom, geografischen Kartenmittelpunkt, Geräteauswahl und gegebenenfalls Popupstatus vor dem Ausfall erfassen. Pane-Offsets sind bei Größenänderungen kein Ersatz für den geografischen Mittelpunkt.
4. Nur die Testansichten über einen temporären lokalen Relay unterbrechen: bestehende Verbindungen schließen und neue vorübergehend abweisen. Dauerhafte Server-/Instanzkonfiguration und andere Clients unverändert lassen. Die Ausfallsperre durch abgewiesene Verbindungen und fehlgeschlagene Datenabrufe bzw. den sichtbaren Ausfallhinweis nachweisen.
5. Erwartete Verbindungsfehler auch in der Testinstrumentierung behandeln. Insbesondere `route.fetch`, `route.fulfill` und `route.continue` können während des absichtlichen Ausfalls fehlschlagen; Fehler abfangen und den betroffenen Request kontrolliert abbrechen. Fehler aus asynchronen Route-Handlern und Socket-Ereignissen dürfen nicht als unbehandelte Promise-Rejections die MCP-Laufzeit beenden. Unerwartete Fehler weiterhin erfassen und bewerten.
6. Einen zusammenhängenden, zeitlich begrenzten Testlauf mit gemeinsamem Steuerzustand und `try/finally` verwenden. Nach einem MCP-Kernel-Reset alle Browser-/Frame-Referenzen neu aufbauen; einen abgebrochenen Lauf nicht als bestanden werten. Zeitbudget an Ladezeit, Transport-Timeout und tatsächlichem Retry-/Backoff-Abstand ausrichten. Bloß längeres Warten ohne Diagnose ersetzt keine Fehlerbehandlung.
7. Nach Freigabe neue erfolgreiche Datenabrufe und das Verschwinden des Ausfallhinweises prüfen. Einen durch den nativen Host ersetzten iframe neu ermitteln. Zoom, Mittelpunkt und Auswahl mit dem Ausgangsstand vergleichen; Popup, Canvas-Anzahl und JavaScript-Fehler zusätzlich kontrollieren. Erhaltene Anzeige ohne nachgewiesenen Wiederanlauf genügt nicht.
8. Browser und Relay im Abschluss-/Fehlerpfad schließen und alle Testverbindungen entfernen. Im Nachweis Testart, beobachteten Ausfall, erfolgreichen Wiederanlauf, Zustandsvergleich und Grenzen festhalten. Tokens, Geräte-IDs, Standortkoordinaten und vollständige Request-URLs nicht in versionierte Berichte übernehmen.

Ein beobachteter `ECONNRESET` einer Browser-Route oder ein Actionability-Timeout ist zunächst ein Befund der Teststeuerung. Ohne weiteren Nachweis darf daraus kein Fehler des Symcon-MCP, des Moduls oder eines Helpers abgeleitet werden.

## Nachweis

Der Abschlussbericht nennt die Rolle des verwendeten Systems, ausgeführte Aktionen, Ergebnisse und ungeprüfte Laufzeitgrenzen. Stub-Tests, Tests auf einer Entwicklungsinstanz und Produktivnachweise werden getrennt ausgewiesen. Nicht ausgeführte Systemprüfungen dürfen nicht als bestanden gelten.
