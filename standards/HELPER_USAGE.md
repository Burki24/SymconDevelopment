# Verwendung gemeinsamer Helper

## Leitregel

Vor einer neuen lokalen Hilfsfunktion wird geprüft, ob `Symcon_ModuleHelper` oder ein vorhandener Baustein unter `libs/helper` die Aufgabe bereits erfüllt. Wiederverwendung ist der Standard; lokale Duplikate zentraler Helper sind nicht zulässig.

## Entscheidungsfolge

1. Suche im betroffenen Modul und Repository nach bestehendem Verhalten.
2. Prüfe die eingebundene Version und API von `Symcon_ModuleHelper`.
3. Prüfe vergleichbare Burki24-Module auf eine freigegebene Nutzung.
4. Verwende die bestehende Funktion, wenn ihr Vertrag passt.
5. Fehlt eine allgemein nutzbare Funktion, schlage eine getrennte Ergänzung im zuständigen Helper-Repository vor.
6. Implementiere lokal nur dann, wenn die Logik wirklich modulspezifisch ist; benenne und teste diese fachliche Zuständigkeit klar.

## Keine Duplikate

Als Duplikat gilt auch leicht umbenannter oder nur minimal veränderter Helper-Code mit demselben fachlichen Vertrag. Ein kurzfristiges Kopieren „bis später“ ist keine akzeptierte Integrationsstrategie.

Wenn eine neue Helper-Version im Zielprojekt noch nicht verfügbar ist, werden Abhängigkeit, Versionsanforderung und Migrationsreihenfolge geklärt. Es wird kein stiller Fallback durch Kopieren eingebaut.

## Lokale Testbundles und automatische Verteilung

Die automatische Verteilung liefert den verbindlichen Consumer-Stand einschließlich Helpern, Abhängigkeiten, Ressourcen und generierten Metadaten. Ein lokales Testbundle aus der kanonischen Quelle ist ein vorläufiger Prüfstand, keine zweite Veröffentlichungsquelle. Es wird unverändert über das vorhandene Bundle-Verfahren erzeugt; Versionen, Hashes oder Herkunftsangaben werden nicht von Hand als veröffentlichter Stand ausgegeben.

### Vorbeugung bei lokalen Tests

1. Prüfe und sichere vor dem Einspielen eines Testbundles den Arbeitsbaum, den Index und die ursprünglichen betroffenen Dateien. Bereits vorhandene Änderungen müssen eindeutig von den eigenen Teständerungen unterscheidbar bleiben.
2. Verwende möglichst eine isolierte Testumgebung. Wird der normale Arbeitsbaum vorübergehend verwendet, stelle nach der Prüfung den gesicherten Ausgangsstand der ausschließlich für den Test ausgetauschten Dateien wieder her, auch bei fehlgeschlagenen Prüfungen. Fachliche Moduländerungen bleiben erhalten.
3. Übergib keine noch offenen lokalen Helper-Testkopien für einen anschließend erforderlichen Pull. Veröffentliche zunächst die zentrale Helper-Änderung über den Benutzerworkflow und lasse die automatische Verteilung den Consumer-Stand liefern. Weise auf noch ausstehende Verteilung oder Pulls und die dadurch noch nicht erfüllte Modulabhängigkeit hin.

### Bereits blockierter Pull

1. Erfasse lokalen Branch, `HEAD`, Index und sämtliche lokalen Änderungen. Sichere die betroffenen Dateien und den Diff außerhalb des versionierten Inhalts; schließe unversionierte Dateien ein. Ein pauschales Stash oder Verwerfen aller Moduländerungen ist keine Standardlösung.
2. Vergleiche anhand eines aktuell gefetchten Remote-Stands die lokalen Testdateien mit dem eingehenden Verteilungscommit und der zugehörigen kanonischen Helper-Version. Prüfe auch Abhängigkeiten, Ressourcen, Hashmanifest und generierte Dokumentation. Unterschiede bei Version oder Herkunft dürfen nur dann als Metadatenunterschied gelten, wenn die funktionale Gleichheit tatsächlich nachgewiesen ist.
3. Entferne ausschließlich nachweislich redundante, selbst eingebrachte und ungestagte Helper-Teständerungen. Setze nur diese Dateien auf ihren unveränderten Stand vor dem Test zurück; `HEAD` ist nur bei zuvor sauberen Dateien der richtige Ausgangspunkt. Fachliche Moduländerungen und sonstige vorhandene Arbeit dürfen sich dabei nicht ändern. Bei zusätzlichen funktionalen Unterschieden, fremden Änderungen oder bereits gestagten beziehungsweise committeten Testständen ist zunächst eine gezielte Konfliktlösung erforderlich; nichts pauschal zurücksetzen oder die Historie umschreiben.
4. Prüfe den erwarteten Stand nach dem Pull mit den erhaltenen Moduländerungen und dem vollständigen eingehenden Helper-Paket. Nutze eine isolierte Umgebung oder spiele das Paket nur vorübergehend ein und stelle anschließend den bereinigten Ausgangsstand zuverlässig wieder her. Unterscheide im Ergebnisbericht ausdrücklich zwischen diesem geprüften Stand und dem noch nicht gepullten Arbeitsbaum.
5. Kontrolliere vor der Übergabe, dass die blockierenden Teständerungen entfernt sind, alle übrigen Änderungen unverändert erhalten bleiben und Index sowie `HEAD` durch die Bereinigung unverändert sind. Der Benutzer führt Fetch/Pull und anschließend Commit/Push über GitHub Desktop aus. Nach dem Pull sind Helper-Integrität und betroffene Modultests am tatsächlichen Integrationsstand erneut zu prüfen.

Für das Entfernen redundanter Testkopien ist kein eigener Helper-Commit im Modul erforderlich. Die fachlichen Moduländerungen werden erst mit dem regulär verteilten Helper-Stand übergeben; dessen Metadaten werden nicht durch einen lokalen Testgenerator erneut überschrieben.

## Ablage

- Repositoryweit geteilter Code: `libs/helper`
- Modulinterne, ausschließlich fachliche Logik: im Modul nach dessen vorhandener Struktur
- Tests und Testhilfen: `tests` nach bestehender Testkonvention
- Kein `.shared`, kein `.tests`

## Prüfung

Bei Änderungen an gemeinsamem Verhalten sind alle bekannten Aufrufer, ihre Eingabeformen und ihre Fehlererwartungen zu prüfen. Öffentliche Verträge werden nicht unbeabsichtigt über eine Helper-Änderung verschoben.

Bei Modulen mit `IPSModuleStrict` werden zusätzlich die Signaturen eingebundener Traits gegen die echte Basisklasse geprüft. Eine Freigabe für `IPSModule` belegt nicht automatisch Strict-Kompatibilität. Fehlende Kompatibilität wird als eigene Helper-Änderung behandelt; Tests vorhandener Consumer und ein erforderlicher Laufzeitnachweis gehören dazu. Hintergrund: [`knowledge/strict-module-helper-compatibility.md`](../knowledge/strict-module-helper-compatibility.md).

Die zugrunde liegende Zuständigkeitsentscheidung steht in [`ADR 0003`](../adr/0003-use-symcon-modulehelper.md).
