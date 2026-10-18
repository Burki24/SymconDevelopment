# Einheitliche Debug-Ausgaben

## Ziel und Geltung

Debug-Ausgaben erklären Menschen, was ein Modul auslöst, welche Werte es verarbeitet und welche Auswirkungen daraus folgen. Die Vorgabe gilt für die schrittweise Umstellung der Symcon-Module. OpenHomeAlarm ist das Pilotmodul; andere Module werden dadurch nicht automatisch geändert.

## Gemeinsamer Aufbau

Die native Symcon-Debug-Kategorie verwendet `<Modul> | <Ereignis> | <Funktion>:<Zeile>`. Die strukturierte Nutzlast enthält mindestens `Instanz`, `Vorgang`, `Aufruf`, `Meldung` und `Bezug`. Die Quellstelle wird automatisch mit `__FUNCTION__` und `__LINE__` beziehungsweise aus einem argumentfreien Aufrufkontext bestimmt; keine manuell gepflegten Zeilennummern.

| Ereignis | Bedeutung |
| --- | --- |
| `START` | Funktion beginnt; relevante freigegebene Eingaben stehen im Bezug. |
| `ENDE` | Funktion endet; der Bezug enthält das tatsächliche Ergebnis oder den Abbruch. |
| `AKTION` | Fachlicher Vorgang, Entscheidung oder Zustandsänderung. |
| `SENDEN` | Übergabe an eine interne oder externe Schnittstelle beziehungsweise Schreiben eines Statuswertes. |
| `EMPFANG` | Empfangene Daten, gelesener Quellwert oder Antwort einer Schnittstelle. |
| `FEHLER` | Fehler mit verständlicher Ursache, betroffenem Vorgang und erkennbarem weiteren Verhalten. |

- Meldungen und erläuternde Feldnamen sind deutsch, unabhängig von der Oberflächensprache. Technische Funktionsnamen, Identifiers, Schnittstellenfelder und Fehlerklassen bleiben zur Wiederauffindbarkeit unverändert.
- Der Bezug nennt die betroffene Quelle oder das Ziel: insbesondere Variablen-ID, Bereich, Aktion, Status-Identifier oder Schnittstelle. Gleichnamige Quellen bleiben anhand ihrer IDs unterscheidbar.
- Zusammengehörige verschachtelte Aufrufe teilen eine Vorgangskennung; die Aufrufnummer unterscheidet einzelne Funktionsaufrufe. Ein neuer äußerer Aufruf beginnt einen neuen Vorgang. Asynchrone Folgeereignisse erhalten ohne belegbar übertragene Kennung einen eigenen Vorgang.
- Werte werden mit ihrer Bedeutung und gegebenenfalls Einheit ausgegeben, zum Beispiel `VerzögerungSekunden`. Nachrichtenwerte, tatsächlich gelesene Werte und geschriebene Werte dürfen nicht verwechselt werden.

## Funktionen und Ergebnisse

Öffentliche Modul-Einstiege einschließlich Lebenszyklus, Bedienung, Timer und Exporte erhalten Start und Ende. Zusätzlich werden entscheidende interne Aktions- und Kommunikationsgrenzen erfasst. Kleine reine Berechnungen und Getter benötigen keine eigenen Start-/Endmeldungen, wenn ihr Ergebnis im aufrufenden Ablauf erkennbar ist. Der konkrete Umfang wird pro Modul dokumentiert.

Jeder erfasste Start besitzt auch bei früher Rückgabe und behandelbaren PHP-Ausnahmen ein Ende, vorzugsweise über `finally`. Ein Ausnahmeabbruch wird als solcher gemeldet und verändert die ursprüngliche Ausnahmebehandlung nicht. Prozessabbrüche außerhalb der kontrollierten PHP-Ausführung können kein garantiertes Ende liefern.

Ein `true` oder `false` wird entsprechend dem jeweiligen Funktionsvertrag erklärt. Funktionen ohne Rückgabewert behaupten keinen fachlichen Erfolg; ihre Einzelentscheidungen stehen im Ablauf. Umfangreiche Text-/JSON-Ergebnisse und Exporte werden mit Art und Umfang beschrieben, ohne ihren Inhalt zu protokollieren.

## Aktionen und Kommunikation

- Bedienaktion: Auslöser und gewünschte Operation, Ablehnungsgrund oder tatsächliche Zustandsänderung.
- Empfang: Quelle, empfangener beziehungsweise tatsächlich gelesener Wert und anschließende Entscheidung.
- Statusausgabe: Ziel-Identifier und geschriebener Wert. Unterdrückte oder unveränderte Schreibvorgänge werden nicht allein für Debug erneut ausgeführt.
- Konfigurierte Aktion: Schnittstelle, Aktion und bekanntes Ziel, Übergabe und Antwort. Beliebige Skriptparameter können Geheimnisse enthalten und bleiben geschützt.
- Externe Schnittstelle: Partner, Operation, relevante sichere Parameter, Transportergebnis und fachliche Antwort. Übergabe, Annahme und bestätigte Wirkung sind unterschiedliche Ergebnisse.
- Fehler: deutsche Ursache, Funktion und Quellstelle sowie gegebenenfalls Fehlerklasse, Fehlerzeile oder HTTP-Status. Ablehnung, Überspringen und Scheitern dürfen nicht als Erfolg erscheinen.

## Datenschutz und Ausführungsverhalten

Es gelten [PRIVATE_DATA.md](PRIVATE_DATA.md) und [HELPER_USAGE.md](HELPER_USAGE.md). Formatierung, Maskierung und Längenbegrenzung verwenden den zentralen `DebugHelper`; keine lokalen Kopien seiner Bereinigungslogik.

Codes, PINs, Zugangsdaten, Zugriffstoken, Empfangskennungen, Sicherungsinhalte und unkontrollierte Anfrage-/Antwortkörper werden gar nicht erst an die Debug-Ausgabe übergeben. Beliebige Exception-Texte können diese Inhalte ebenfalls enthalten: bekannte Fehler in sichere deutsche Ursachen überführen, sonst Fehlerklasse und Quellstelle verwenden. Eine reine Schlüsselmaskierung genügt nicht zum Schutz unbeschrifteter Geheimnisse.

Der Pilot begrenzt eine Nutzlast auf 4096 Bytes. Andere Grenzen müssen im jeweiligen Modul begründet werden. Debug-Ausgaben verwenden den nativen Debug-Kanal, keinen zusätzlichen persistenten Diagnosespeicher. Zusätzliche Netzwerkaufrufe, Quellwertabfragen, Aktionen oder Zustandsänderungen allein für Debug sind unzulässig. Ein Ausfall des Debug-Kanals darf die fachliche Verarbeitung nicht verhindern.

## Nachweise

Prüfungen umfassen erfolgreiche und abgelehnte Aktionen, empfangene und geschriebene Werte, Schnittstellenantworten und Fehler, ausgeglichene Start-/Endpaare, neue beziehungsweise gemeinsame Vorgangskennungen, unveränderte Rückgabewerte und Seiteneffekte sowie Geheimnisschutz. Ein gezielt gestörter Debug-Kanal muss die fachliche Verarbeitung weiter erlauben.

Die reale Symcon-Abnahme prüft zusätzlich Lesbarkeit, Datenmenge und Nachverfolgbarkeit im Debug-Fenster. Stub-Tests belegen weder echte Gerätewirkungen noch die Laufzeitkosten auf der Zielinstallation.
