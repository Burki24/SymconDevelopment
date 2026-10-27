# Git-Workflow

## Zweige

- `dev` ist der dauerhafte Integrationszweig für laufende Entwicklung.
- Aufgaben werden in kurzlebigen, eindeutig benannten Feature- oder Fix-Branches umgesetzt.
- Pull Requests für laufende Entwicklung zielen auf `dev`, sofern die lokale Projektregel nichts ausdrücklich anderes festlegt.
- Nach dem Merge bleibt `dev` bestehen. Optionen zum automatischen Löschen gelten nur für den Quellbranch des Pull Requests, niemals für `dev`.
- `main` repräsentiert in den üblichen Burki24-Modul-Repositories den stabilen beziehungsweise veröffentlichten Stand.
- Zusätzliche dauerhafte Versionszweige werden ausschließlich nach der dokumentierten Praxis des jeweiligen Repositories verwendet.

## Release und Rücksynchronisierung

1. Bereite den Release-Stand auf `dev` vor und führe die vorgesehenen Prüfungen aus.
   Ordne die unveröffentlichten Changelog-Einträge der ausdrücklich bestätigten Version und dem Veröffentlichungsdatum zu; gleiche die Version mit `library.json` ab, gemäß [`CHANGELOG.md`](CHANGELOG.md).
2. Führe `dev` über einen geprüften Pull Request nach `main`.
3. Erstelle Tags und Releases nur vom geprüften stabilen Stand.
4. Synchronisiere das Merge-Ergebnis aus `main` anschließend zurück nach `dev`, damit beide Zweige denselben veröffentlichten Ausgangspunkt besitzen.

Die Rücksynchronisierung wird nicht durch Neuanlage oder Löschen von `dev` ersetzt. Projekte mit weiteren dauerhaften Zweigen beschreiben ihre Zielrichtung und Rücksynchronisierung ausdrücklich in der lokalen `AGENTS.md`.

## Änderungen vorbereiten

1. Prüfe Status, aktuellen Zweig und nicht zugehörige lokale Änderungen.
2. Aktualisiere die Arbeitsgrundlage nach dem im Projekt erlaubten Verfahren.
3. Halte die Änderung eng am Auftrag und vermische keine unabhängigen Aufräumarbeiten.
4. Führe die betroffenen Tests sowie Style- und Strukturprüfungen aus.
5. Prüfe den vollständigen Diff auf versehentliche Änderungen, Secrets und generierte Dateien.

### Automatisch verteilte Helper vor dem Modul-Commit

Lokale Helper-Testkopien dürfen nicht als konkurrierender Stand zum automatischen Helper-Sync im Arbeitsbaum verbleiben. Vor einem erforderlichen Pull gilt der verbindliche Ablauf unter [`HELPER_USAGE.md`](HELPER_USAGE.md#lokale-testbundles-und-automatische-verteilung): sichern, mit dem eingehenden Paket vergleichen, nur belegte redundante Teständerungen entfernen und alle übrigen Änderungen erhalten. Der Benutzer pullt den regulären Helper-Stand über GitHub Desktop, bevor er die darauf aufbauenden Moduländerungen committet und pusht. Ein pauschales Stash oder Verwerfen der Moduländerungen ersetzt diesen Abgleich nicht.

### Zeilenenden

- Neue und bearbeitete Textdateien werden standardmäßig mit LF geschrieben.
  Maßgeblich sind die für den konkreten Pfad wirksamen Repository-Attribute.
  Eine ausdrücklich vereinbarte CRLF-Ausnahme bleibt erhalten.
- Repositories legen den Standard in `.gitattributes` fest:

  ```gitattributes
  * text=auto eol=lf
  ```

  Vorhandene pfadspezifische Ausnahmen müssen weiterhin greifen. Insbesondere
  bleiben bytegenau ausgelieferte Fremdartefakte mit `-text` ausgenommen;
  Binärdateien werden nicht als Text normalisiert.
- Auch Skripte, Generatoren und Coding-Agenten schreiben Textdateien direkt
  mit den vereinbarten Zeilenenden. Für Editor-Konfigurationen gilt dieselbe
  Vorgabe. Sich auf eine spätere Git-Konvertierung zu verlassen, genügt nicht.
- Vor der Übergabe werden neue und geänderte Dateien auf ihre tatsächlichen
  Zeilenenden geprüft. Für getrackte Dateien zeigt `git ls-files --eol` Index,
  Arbeitsbaum und Attribute; neue Dateien sind zusätzlich direkt zu prüfen.
  Bei LF-Pfaden dürfen keine CRLF- oder gemischten Zeilenenden zurückbleiben.
  `git diff --check` ergänzt diese Prüfung, ersetzt sie aber nicht.
- Die Warnung über eine bevorstehende CRLF-/LF-Konvertierung wird durch korrekt
  geschriebene Dateien behoben. Globale Git-Einstellungen oder Warnungen werden
  dafür nicht geändert beziehungsweise unterdrückt. Es erfolgt keine pauschale
  Renormalisierung, kein Staging und kein Überschreiben fremder Änderungen.

## Commits und Pull Requests

- Commit und Push führt immer der Benutzer selbst über GitHub Desktop aus.
- Coding-Agenten bereiten Änderungen und deren Prüfung vor, erstellen aber keine Commits und führen keine Pushes aus. Das gilt für Git-Befehle ebenso wie für Tools, APIs und die Benutzeroberfläche. Eine Freigabe für Commit oder Push wird nicht angefragt.
- Nach Änderungen liefert der Coding-Agent ausschließlich die Commit-Texte zur manuellen Verwendung in GitHub Desktop: einen passenden Commit-Betreff (Summary) und eine Commit-Erklärung (Description), beide auf Englisch und getrennt kopierbar. Das gilt auch bei deutschsprachiger Unterhaltung oder Dokumentation. Erforderliche Ergebnis- und Prüfberichte bleiben davon unberührt.
- Die vorgeschlagenen Commit-Texte beschreiben einen thematisch geschlossenen Änderungsumfang. Ihre Bereitstellung berechtigt den Coding-Agenten nicht zur Ausführung von Commit oder Push.
- Auch reine Dokumentationsänderungen, Prüfberichte und Sammelabnahmen erhalten
  zwei getrennte kopierbare Textblöcke für Summary und Description. Wenn der
  Benutzer einzelne Test-PRs ablehnt oder erst später committen/pushen möchte,
  wird der gemeinsame Änderungsumfang beschrieben; die Texte werden trotzdem
  bereitgestellt.
- Ein Pull Request erklärt Problem, Lösung, Auswirkungen und Prüfungen.
- Architekturentscheidungen und notwendige Dokumentationsänderungen gehören in denselben fachlichen Zusammenhang.
- Fehlgeschlagene oder nicht ausgeführte Prüfungen werden nicht verschwiegen.
- Merge, Tagging, Release und Veröffentlichung erfolgen nur mit entsprechender Berechtigung und ausdrücklichem Auftrag. Commit und Push verbleiben immer beim Benutzer über GitHub Desktop.

## Konflikte und Abweichungen

Konflikte werden anhand der aktuellen Architektur gelöst, nicht durch pauschales Überschreiben. Dauerhafte Abweichungen von diesem Workflow werden in der lokalen `AGENTS.md` dokumentiert; Architekturfolgen erhalten bei Bedarf ein ADR.

Die Entscheidung für das dauerhafte Branch-Modell steht in [`ADR 0005`](../adr/0005-use-persistent-dev-main-workflow.md).
