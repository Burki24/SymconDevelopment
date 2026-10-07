# ADR 0001: Symcon-Dokumentation zentral vorhalten

- Status: Ersetzt
- Datum: 2026-09-26
- Entscheider: Burki24
- Ersetzt: –
- Ersetzt durch: [`ADR 0006`](0006-use-official-symcon-llms-sources.md)

Dieses ADR dokumentiert die frühere Snapshot-Strategie und ist nicht mehr anzuwenden. Die aktive Entscheidung steht in ADR 0006.

## Kontext

Mehrere Burki24-Symcon-Projekte benötigen regelmäßig dieselben Informationen zu Symcon-APIs, Funktionen und Plattformverhalten. Eine ausschließliche Onlinesuche kostet Zeit und erschwert die gezielte projektübergreifende Volltextsuche. Kopien in jedem Modul-Repository würden dagegen auseinanderlaufen und die einzelnen Projekte unnötig vergrößern.

Symcon stellt die vollständige Dokumentation in deutscher und englischer Sprache als für Sprachmodelle aufbereitete Textdateien bereit. Die Inhalte sind externe Dokumentation und dürfen weder als projektspezifische Arbeitsanweisung noch als Ersatz für die Analyse des vorhandenen Codes behandelt werden.

## Entscheidung

Das private Repository `SymconDevelopment` hält unter `references/symcon/` je einen unveränderten deutschen und englischen Snapshot der offiziellen Symcon-Dokumentation vor.

- Die deutsche Fassung ist der übliche Einstieg; die englische Fassung dient zusätzlich für exakte Fachbegriffe, Quervergleiche und unklare Übersetzungen.
- Die zentrale `AGENTS.md` weist angebundene Projekte an, diese lokalen Snapshots zuerst gezielt zu durchsuchen.
- Die Snapshots werden nicht in einzelne Modul-Repositories kopiert.
- Herkunft, Erzeugungsstand, Dateigröße, Zeilenzahl und SHA-256 werden dokumentiert.
- Zeitabhängige Aussagen werden bei Bedarf gegen die aktuelle offizielle Dokumentation geprüft.
- Die Arbeitskopien bleiben im privaten Repository und werden nicht öffentlich weiterveröffentlicht.

Nicht Teil dieser Entscheidung sind eine automatische Aktualisierung, ein Dokumentations-Mirror oder Änderungen an bestehenden Modul-Repositories.

## Alternativen

- **Ausschließlich online suchen:** vermeidet lokale Dateien, ist aber langsamer, weniger reproduzierbar und von der Erreichbarkeit sowie der Suchfunktion der Website abhängig.
- **Dokumentation in jedes Projekt kopieren:** ermöglicht lokale Suche, erzeugt jedoch redundante, potenziell unterschiedliche Stände.
- **Eigenes Dokumentations-Repository anlegen:** trennt Fremdinhalte stärker, erhöht für zwei Referenzdateien aber Verwaltungs- und Anbindungsaufwand ohne zusätzlichen Nutzen.
- **Nur eine Sprache speichern:** benötigt weniger Platz, erschwert aber Quervergleiche und die Suche nach abweichenden Fachbegriffen.

## Folgen

Alle angebundenen Projekte erhalten über eine einzige lokale Quelle denselben Dokumentationsstand. Die Volltextsuche funktioniert ohne Webzugriff und ohne lokale Duplikate in den Modul-Repositories.

Das Repository wächst um rund 6,8 MB. Die Snapshots müssen bewusst aktualisiert werden und können zwischen Aktualisierungen veralten. Bei einem Update sind beide Sprachfassungen sowie ihre Metadaten zu prüfen. Das Repository muss privat bleiben, solange die externen Dokumentationsdateien darin enthalten sind.

## Nachweise

- Offizielle Indizes: <https://www.symcon.de/de/llms.txt> und <https://www.symcon.de/en/llms.txt>
- Deutscher Snapshot vom 26.09.2026: SHA-256 `B8D1A22C8B687B8BDBC0573B80214DB45B3DD5DF5C49EA02156B0A0BDFB732EA`
- Englischer Snapshot vom 26.09.2026: SHA-256 `F29A6EC65185F81F0CFC2FCBA02168F94A576C9BE334DB8D3FF54C700AB7F516`
- Beide Arbeitskopien wurden bytegenau mit den bereitgestellten Quelldateien verglichen.
