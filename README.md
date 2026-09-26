# SymconDevelopment

`SymconDevelopment` ist die schlanke, zentrale Entwicklungsbasis für Burki24-Symcon-Projekte. Das Repository bündelt gemeinsame Arbeitsregeln, Qualitätsstandards, Entscheidungsvorlagen und wiederverwendbares Wissen, ohne die einzelnen Modul-Repositories mit kopierten Regelwerken zu belasten.

Die Basis ist von guten Ideen aus SAEF inspiriert, bleibt aber auf die bestehende Burki24-Infrastruktur zugeschnitten. Sie übernimmt keine SAEF-spezifischen Deployment-, Runtime-Mirror-, SSH-/PowerShell- oder MQTT-Frameworkteile.

## Verbindliche Grundlage

- Zielplattform: IP-Symcon 9 und PHP 8.5.
- Gemeinsame Helper liegen unter `libs/helper`; `.shared` wird nicht verwendet.
- Tests liegen unter `tests`; `.tests` wird nicht verwendet.
- Jedes Modul besitzt eine eigene `README.md`.
- Vorhandene Funktionen aus `Symcon_ModuleHelper` werden bevorzugt.
- Lokale Duplikate zentraler Helper sind nicht erlaubt.
- CI basiert auf `Symcon_ModuleCI` v1.0.0 und umfasst StylePHP, php-cs-fixer und `validate_structure`.
- Vor Änderungen werden die vorhandene Architektur, die Projektregeln und vergleichbare Implementierungen gelesen.
- Der dauerhafte Entwicklungszweig `dev` bleibt nach Pull Requests bestehen.

Die ausführlichen Regeln stehen in [AGENTS.md](AGENTS.md) und in den Dokumenten unter [`standards/`](standards/).

## Struktur

| Pfad | Zweck |
| --- | --- |
| `AGENTS.md` | Zentrale Arbeitsanweisung für Menschen und Coding-Agenten |
| `standards/` | Verbindliche technische und organisatorische Standards |
| `adr/` | Architekturentscheidungen mit Begründung und Folgen |
| `knowledge/` | Wiederverwendbare Erkenntnisse, Fehlerbilder und Lösungswege |
| `templates/` | Kurze Vorlagen für Projektanbindung und Moduldokumentation |
| `references/` | Kuratierte Referenzprojekte, Referenzimplementierungen und externe technische Dokumentation |

## Lokale Symcon-Dokumentation

Unter [`references/symcon/`](references/symcon/) liegen deutsch- und englischsprachige, projektübergreifend nutzbare Snapshots der offiziellen Symcon-Dokumentation. Dadurch können Menschen und Coding-Agenten Symcon-APIs und Plattformdetails lokal durchsuchen, ohne die vollständige Dokumentation in jedes Modul-Repository zu kopieren.

Der Snapshot ist eine datierte externe Referenz und keine verbindliche Arbeitsanweisung. Für zeitabhängige Aussagen bleibt die aktuelle offizielle Dokumentation maßgeblich. Herkunft, Stand und Aktualisierung sind in [`references/symcon/README.md`](references/symcon/README.md) beschrieben.

## Ein bestehendes Repository anbinden

Das Zielprojekt erhält nur eine kurze projektspezifische `AGENTS.md`. Ausgangspunkt ist [`templates/AGENTS.project.md`](templates/AGENTS.project.md). Sie verweist auf diese zentrale Basis und ergänzt ausschließlich projektspezifische Besonderheiten.

Empfohlene lokale Anordnung:

```text
workspace/
├── SymconDevelopment/
└── MeinSymconModul/
    └── AGENTS.md
```

Damit ist der relative Verweis `../SymconDevelopment/AGENTS.md` stabil. Falls Repositories anders angeordnet sind, muss der Pfad in der Projektdatei angepasst werden. Die zentrale Datei wird nicht in Zielprojekte kopiert; so entstehen keine auseinanderlaufenden Regelduplikate.

Bestehende Repositories werden erst nach einer separaten, projektspezifischen Prüfung angebunden. Dieses Repository verändert sie nicht automatisch.

## Geltungsreihenfolge

1. Sicherheits-, Plattform- und Repository-Vorgaben des jeweiligen Projekts
2. ausdrücklich dokumentierte projektspezifische Abweichungen in dessen `AGENTS.md`
3. die zentrale `AGENTS.md` und die Standards dieses Repositories
4. Knowledge-Artikel und Referenzen als unterstützende, nicht verbindliche Hinweise

Abweichungen von zentralen Regeln müssen begründet werden. Dauerhafte Architekturabweichungen gehören zusätzlich in ein ADR des betroffenen Projekts.

## Pflege

Änderungen an verbindlichen Standards erfolgen per Pull Request. Änderungen mit langfristigen Architekturfolgen erhalten ein ADR. Praxiswissen ohne normativen Charakter gehört nach `knowledge/`; Beispiele und externe Referenzen gehören nach `references/`.
