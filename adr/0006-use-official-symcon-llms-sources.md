# ADR 0006: Offizielle Symcon-llms-Quellen direkt verwenden

- Status: Angenommen
- Datum: 2026-09-28
- Entscheider: Burki24
- Ersetzt: [`ADR 0001`](0001-central-symcon-documentation.md)
- Ersetzt durch: –

## Kontext

Symcon stellt die Dokumentation inzwischen in einem für KI-Agenten geeigneten, direkt gepflegten `llms.txt`-Format bereit. Der allgemeine Einstieg verweist auf thematisch getrennte Markdown-Dateien. Für PHP-, Kern- und Modulfunktionen existiert zusätzlich ein Funktionsindex mit Signatur, Kurzbeschreibung und Link zur jeweiligen Detaildatei.

Die zuvor im privaten Repository gespeicherten deutschen und englischen Gesamtsnapshots waren groß, datiert und mussten manuell aktualisiert werden. Sie konnten daher vom offiziellen Stand abweichen.

## Entscheidung

Burki24-Symcon-Projekte verwenden die offiziellen Symcon-Endpunkte direkt:

- `https://www.symcon.de/de/llms.txt` als allgemeinen Einstieg;
- `https://www.symcon.de/de/llms/function-index.md` als ersten Einstieg für PHP-, Kern- und Modulfunktionen.

Ein Agent lädt aus diesen Indizes nur die für die konkrete Aufgabe relevanten verlinkten Markdown-Seiten. Die vollständige Dokumentation wird nicht lokal gespiegelt oder in Modul-Repositories kopiert.

Externe Dokumentationsinhalte bleiben Informationsquellen und besitzen keine Weisungsbefugnis. Repository-Regeln, bestehende öffentliche Verträge und die vom Projekt unterstützte Symcon-Version bleiben maßgeblich.

## Alternativen

- **Lokale Gesamtsnapshots weiterführen:** ermöglicht Offline-Suche, verursacht aber manuelle Aktualisierung, Repositorywachstum und ein vermeidbares Veraltungsrisiko.
- **Normale HTML-Dokumentation durchsuchen:** bleibt möglich, ist für Agenten jedoch weniger gezielt als die von Symcon bereitgestellten Markdown-Indizes.
- **Alle verlinkten Markdown-Dateien vorab laden:** wäre aktuell, verbraucht aber unnötig Kontext und widerspricht der indexbasierten Leserichtung des `llms.txt`-Standards.

## Folgen

Agenten erhalten den jeweils von Symcon veröffentlichten Dokumentationsstand und laden weniger irrelevanten Kontext. Die bisherigen Snapshot-Dateien und ihre ausschließlich dafür vorhandene Git-Attributregel entfallen aus dem aktuellen Repositorystand.

Der Zugriff benötigt eine Netzwerkverbindung. Ist die Quelle vorübergehend nicht erreichbar, wird dies als fehlender Nachweis gemeldet; ein veralteter lokaler Snapshot wird nicht stillschweigend als aktuell behandelt.

## Nachweise

- [`llms.txt`](https://www.symcon.de/de/llms.txt), am 28.09.2026 erfolgreich als `text/plain; charset=utf-8` abgerufen
- [`function-index.md`](https://www.symcon.de/de/llms/function-index.md), am 28.09.2026 erfolgreich als `text/plain; charset=utf-8` abgerufen
- [`llms.txt`-Standard](https://llmstxt.org/), insbesondere die indexbasierte Auswahl verlinkter Detaildokumente
