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

## Nachweis

Der Abschlussbericht nennt die Rolle des verwendeten Systems, ausgeführte Aktionen, Ergebnisse und ungeprüfte Laufzeitgrenzen. Stub-Tests, Tests auf einer Entwicklungsinstanz und Produktivnachweise werden getrennt ausgewiesen. Nicht ausgeführte Systemprüfungen dürfen nicht als bestanden gelten.
