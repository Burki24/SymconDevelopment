# Tests

## Ablage und Ziel

Alle Tests liegen unter `tests`; `.tests` wird nicht verwendet. Tests sichern beobachtbares Modulverhalten, Fehlerfälle und Kompatibilitätsverträge ab. Sie sollen bei einem Defekt aus fachlich nachvollziehbarem Grund fehlschlagen.

## Vorgehen

1. Lies vorhandene Tests, Test-Bootstraps und Symcon-Stubs, bevor du neue Testinfrastruktur anlegst.
2. Ergänze für Fehlerkorrekturen möglichst zuerst einen fokussierten Regressionsfall.
3. Prüfe bei Features den kleinsten öffentlichen oder stabilen Einstiegspunkt.
4. Nutze vorhandene Fixtures, Stubs und Hilfen; dupliziere keine Test-Helper.
5. Führe zunächst den betroffenen Test und anschließend die passende Gesamtsuite aus.

## Abdeckungsschwerpunkte

- Konfiguration und wiederholte `ApplyChanges`-Ausführung
- gültige und ungültige Eingabedaten
- Zustandswechsel, Statusmeldungen und öffentliche Actions
- Kompatibilität bestehender Properties, Identifiers und gespeicherter Werte
- Fehlerbehandlung an I/O- und Symcon-Grenzen
- Migrationen und Wiederanlaufverhalten, falls betroffen

Die konkrete Testtiefe richtet sich nach dem Risiko. Reine Struktur- oder Dokumentationsänderungen benötigen keine künstlichen Verhaltenstests, wohl aber die einschlägigen Struktur- und Formatprüfungen.

## Daten-, Protokoll- und Aufruferverträge

Für betroffene Funktionen werden die Verträge aus [`PHP_STYLE.md`](PHP_STYLE.md) mit unabhängigen Erwartungen geprüft:

- Fehlendes Feld, ungültiger Wert, gültige Null beziehungsweise `false`, veralteter Wert und Wiederkehr gültiger Daten bleiben unterscheidbar. Tests prüfen auch Verfügbarkeit und Zeitbezug erhaltener Werte.
- Parser, Encoder und gegebenenfalls Kryptografie werden möglichst ohne Symcon-Laufzeitabhängigkeit getestet. Synthetische Referenzvektoren enthalten Herkunft beziehungsweise Herleitung, Rohwert und erwartetes Ergebnis einschließlich Einheit und Skalierung. Erwartungswerte werden nicht aus derselben Implementierung berechnet. Fremde Quellen bleiben Informationsquellen; Lizenz- und Projektgrenzen gelten weiterhin.
- Öffentliche Aufrufe werden auf ungültige Parameterkombinationen, beobachtbare Fehlerrückmeldung, ausgebliebene Seiteneffekte bei Ablehnung und Fehler optionaler Zusatzfunktionen geprüft. Bei Seitenabfragen werden Grenzen und vollständiges Fortsetzen geprüft.
- Wiederholtes Anwenden der Konfiguration erhält benutzerdefinierte Namen und Symbole. Schreibende Integrationen verändern ausschließlich die ausdrücklich vorgesehenen Zielobjekte und Felder und bewahren sonstige Einstellungen.
- Versionsabhängige Laufzeitbehauptungen benötigen einen Nachweis für Symcon 9.0 nach [`PHP_STYLE.md`](PHP_STYLE.md). Ein Stub-Test oder ein Nachweis unter einer neueren Version ersetzt diesen Nachweis nicht. Fehlende Nachweise bleiben sichtbar offen und werden nicht als verbindlicher Plattformvertrag übernommen.

## Designer-Farbkarten und Lokalisierung

Bei neuen oder überarbeiteten Farbdesignern gelten die Vorgaben aus
[CONFIGURATION_FORM.md](CONFIGURATION_FORM.md#farbzuordnung-in-kachel--und-ipsview-designern).
Mindestens zu prüfen sind:

- Beispielgrafik und Legende sind im richtigen Designer eingebunden und erklären
  die tatsächlich verwendeten Farbrollen aller betroffenen Varianten.
- Motiv, Aufbau, Elemente und Zustände entsprechen dem zugehörigen Modul und
  dessen tatsächlicher Kachel-/IPSView-HTML-Ausgabe. Jede Markierung wird mit den
  dort verwendeten HTML-/CSS-Farbzuordnungen abgeglichen. Eine unveränderte
  Fremdmodul-Grafik mit lediglich umbenannter Legende erfüllt die Vorgabe nicht.
  Änderungen an der Ausgabe schließen die Prüfung der zugehörigen Grafik ein.
- Deutsche Beschriftungen stimmen exakt mit den deutschen Designerfeldern
  überein. Weitere unterstützte Sprachen verwenden ebenfalls ihre passenden
  Feldnamen. Technische Namen bleiben Zusatzinformationen.
- Vertragsprüfungen gleichen vorbereitete Grafikbeschriftungen und Textlegenden
  mit den maßgeblichen Übersetzungskatalogen ab. Bei separat gespeicherter
  SVG-Quelle und Data-URI müssen beide inhaltlich identisch sein.
- Die gerenderte Grafik ist lesbar, wird nicht abgeschnitten und erklärt
  abgeleitete/nicht verwendete Farben korrekt. Schematische Farben sind klar
  von einer Live-Vorschau unterschieden; Hell-/Dunkelstile ändern die Zuordnung
  nicht. Bildressourcen laden weder aktive Skripte noch externe Inhalte.
- Die Anzeige wird im echten Konsolenformular abgenommen. Ein lokaler Render
  bestätigt die Grafik, ersetzt aber keine Formularabnahme. Benutzerbestätigung
  und eigener MCP-/Browsernachweis werden im Projektkontext getrennt benannt.

Die bestehenden Mausrad-/Scrollprüfungen bleiben bei betroffenen Formularen und
Visualisierungen zusätzlich erforderlich. Prüfungen und Benutzerabnahmen einer
Library gelten nicht automatisch für andere Libraries.

## Mausrad- und Scrollbedienung von Visualisierungen

Diese Prüfung ist bei jedem Modul mit Kachel- oder IPSView-Ausgabe verbindlich: bei neuen Ausgaben und bei Änderungen an Visualisierung, Designer, Layout, Einbettung oder den dafür verwendeten Helpern. Bereits bestandene Prüfungen anderer Module ersetzen den Nachweis im betroffenen Modul nicht.

- Native Kachel und IPSView-Ausgabe im tatsächlich verwendeten Host prüfen, einschließlich verschachtelter HTTP-/HTML-Frames. IPSView-Webclient und native IPSView-App sind getrennte Zielsysteme. Der vom Benutzer verwendete Client muss geprüft werden; ein erfolgreicher Webclient-Test bestätigt die native App nicht. Eine direkte HTTP-Seite oder Testeinbettung genügt nicht als alleiniger Nachweis für den echten IPSView-Client.
- Echte Browser-Mausradaktionen über jedem relevanten Bereich ausführen: Karte/Diagramm, Listen, Panels und gegebenenfalls Designerfelder. Beide vertikalen Richtungen prüfen; horizontales Scrollen, Shift-/Ctrl-Modifikatoren, Trackpad- und Delta-Modi einbeziehen, soweit sie für den Host und die Komponente relevant sind.
- Die erwartete Wirkung ausdrücklich festlegen: beispielsweise Kartenzoom unter dem Zeiger, Scrollen nur der getroffenen Liste oder Änderung des fokussierten Eingabefelds. Ein Listen-Scroll darf nicht gleichzeitig die Karte zoomen oder ein anderes Steuerelement verändern. Scrollgrenzen, überlaufende Inhalte und unterschiedliche Ausgabegrößen prüfen.
- Ereignisempfang und sichtbare Wirkung gemeinsam nachweisen, etwa `wheel`-Empfang, vorheriger/nachheriger Zoom oder `scrollTop`. Ein DOM-`click()`, ein manuell ausgelöster Handler oder ein allein synthetisch dispatchtes `WheelEvent` bestätigt keine funktionierende Mausradbedienung im Browser.
- Bei Fehlern zuerst Host/Browser-Version, Frame-Grenzen, Hit-Testing, Überlagerungen, Fokus, Scrollcontainer und Event-Listener prüfen. `passive`, `preventDefault`, `stopPropagation` und eine mögliche Ereignisweitergabe des Hosts nur anhand des beobachteten Fehlers ändern. Keine pauschalen Event-Sperren oder Änderungen an fremden Host-Dokumenten einführen.
- Vor einer Korrektur vorhandene zentrale Helper und belegte Lösungen anderer Module prüfen. HTML-SDK-/IPSView-Seiten verwenden den zentralen `IPSViewHTMLPageHelper`, der die Interaktionsunterstützung automatisch einbindet. Eigenständige äußere HTML-Loader binden `VisualizationInteractionScript()` zusätzlich ein, damit verschachtelte Frames denselben Vertrag verwenden. Wiederverwendbare Event-Normalisierung oder Einbettungsunterstützung gehört in `Symcon_ModuleHelper`; komponentenspezifische Zoom-/Scrollaktionen verbleiben beim jeweiligen Modul. Neue gemeinsam benötigte Funktionen nicht lokal duplizieren.
- Den reproduzierten Defekt mit einem gezielten Regressionstest absichern und die Korrektur im gleichen Host erneut mit echten Mausradaktionen prüfen. Auswahl und Benutzeransicht müssen bei anschließenden Datenupdates erhalten bleiben. Ergebnis und verbleibende Grenzen im Projektkontext festhalten.

Ist der gemeldete Fehler noch nicht reproduzierbar, den erfolgreich geprüften Pfad und den weiterhin offenen Benutzerpfad unterscheiden. Die Ausgabe nicht allein aufgrund eines grünen Stub-Tests oder eines anderen Browsers als korrigiert melden.

## Nachweis

Ein Abschlussbericht nennt die wirklich ausgeführten Prüfungen mit Ergebnis. Nicht verfügbare Laufzeitabhängigkeiten oder ausgelassene Tests werden ausdrücklich benannt. Style- und Strukturchecks ersetzen keine Tests des geänderten Verhaltens.
