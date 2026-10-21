# Architektur der Entwicklungsbasis

`SymconDevelopment` ist eine gemeinsame Engineering- und Wissensbasis für eigenständige Burki24-Symcon-Repositories. Es ist weder eine Laufzeitabhängigkeit noch ein Deployment-Framework. Zielprojekte binden die Basis ausschließlich über eine kurze lokale `AGENTS.md` an.

## Informationsschichten

| Schicht | Aufgabe | Verbindlichkeit |
| --- | --- | --- |
| `AGENTS.md` | Leserichtung, Arbeitsregeln und Grenzen | verbindlich für ausdrücklich angebundene Projekte |
| `principles/` | stabile Begründungen und Leitlinien | verbindliche Entscheidungsgrundlage |
| `standards/` | konkrete gemeinsame Entwicklungsregeln | verbindlich, soweit ein Projekt keine begründete Abweichung dokumentiert |
| `adr/` | langfristige Entscheidungen und ihre Folgen | verbindlich innerhalb ihres Geltungsbereichs |
| `knowledge/` | wiederverwendbare Diagnose- und Lösungserfahrung | unterstützend, nicht normativ |
| `templates/` | anpassbare Startpunkte und Checklisten | unterstützend, Platzhalter sind vor Nutzung zu ersetzen |
| `references/` | geprüfte Beispiele und externe Dokumentation | unterstützend, niemals blind zu kopieren |

Die vorhandene Architektur des Zielprojekts bleibt Teil der maßgeblichen Arbeitsgrundlage. Eine zentrale Regel rechtfertigt keine unbeabsichtigte Migration eines bestehenden öffentlichen Vertrags.

## Leserichtung im Zielprojekt

```text
lokale AGENTS.md
    ↓
zentrale AGENTS.md und principles/
    ↓
Projektkontext, README und relevante ADRs
    ↓
relevante standards/
    ↓
vorhandene Helper, Implementierung, Tests und CI
    ↓
bei Bedarf knowledge/ und references/
```

Es wird nur der für die konkrete Aufgabe benötigte Kontext geladen. Die offizielle Symcon-`llms.txt` dient als Index; verlinkte Markdown-Seiten werden gezielt und nur bei Bedarf geladen.

## Wissensfluss

1. Eine projektspezifische Erkenntnis wird zunächst im betroffenen Repository nachgewiesen.
2. Wiederholt sich das Muster oder ist es erkennbar projektübergreifend, wird es als Knowledge-Artikel festgehalten.
3. Entsteht daraus eine verbindliche Regel, wird der passende Standard geändert.
4. Verändert die Regel langfristig Architektur oder Zuständigkeiten, wird zusätzlich ein ADR erstellt.
5. Funktionen, die mehrere Module benötigen, werden mit geklärtem Vertrag zentral in `Symcon_ModuleHelper` umgesetzt und von den betroffenen Modulen eingebunden. Vor jeder Umsetzung sind die vorhandenen Helper zu prüfen.

So wächst die Basis aus belegter Praxis und nicht aus vorsorglich erfundenen Abstraktionen.

## Technische Abgrenzung

Die ausführbaren Bausteine verbleiben in ihren zuständigen Repositories:

- `Symcon_ModuleHelper` besitzt gemeinsame Modulfunktionen einschließlich PHP-Helpern und wiederverwendbaren Visualisierungs- und Layoutbausteinen in HTML, CSS und JavaScript.
- `Symcon_ModuleCI` besitzt die gemeinsame CI-Basis.
- Modul-Repositories besitzen ihre fachliche Implementierung, Tests und projektspezifischen Entscheidungen.

SAEF dient ausschließlich als konzeptionelle Inspiration. Deployment-Frameworks, Runtime-Mirrors, Filesets, SSH-/PowerShell-Orchestrierung, MQTT-Frameworkschichten sowie SAEF-eigene Helper gehören nicht zu dieser Architektur.
