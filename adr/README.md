# Architecture Decision Records

ADRs dokumentieren Entscheidungen, die langfristig Architektur, Kompatibilität, Abhängigkeiten oder mehrere Repositories betreffen. Sie halten nicht nur das Ergebnis, sondern auch Kontext, Alternativen und Folgen fest.

## Katalog

| ADR | Status | Entscheidung |
| --- | --- | --- |
| [`0001`](0001-central-symcon-documentation.md) | Ersetzt | Symcon-Dokumentation zentral und zweisprachig vorhalten |
| [`0002`](0002-lean-saef-adaptation.md) | Angenommen | SAEF schlank und konzeptionell adaptieren |
| [`0003`](0003-use-symcon-modulehelper.md) | Angenommen | `Symcon_ModuleHelper` als kanonische Helper-Quelle verwenden |
| [`0004`](0004-use-symcon-moduleci.md) | Angenommen | `Symcon_ModuleCI` als gemeinsame CI-Basis verwenden |
| [`0005`](0005-use-persistent-dev-main-workflow.md) | Angenommen | dauerhaftes `dev`/`main`-Branch-Modell verwenden |
| [`0006`](0006-use-official-symcon-llms-sources.md) | Angenommen | offiziell gepflegte Symcon-`llms.txt`-Quellen direkt verwenden |

## Benennung

```text
NNNN-kurzer-titel.md
```

Die Nummern steigen fortlaufend. [`0000-template.md`](0000-template.md) dient als Vorlage und wird für eine neue Entscheidung kopiert.

## Status

Verwende einen klaren Status: `Vorgeschlagen`, `Angenommen`, `Abgelehnt`, `Ersetzt` oder `Veraltet`. Wird ein ADR ersetzt, verlinken beide Dokumente aufeinander.

## Wann kein ADR nötig ist

Kleine Implementierungsdetails, temporäre Untersuchungen und reine Fehlerbehebungen ohne langfristige Architekturwirkung gehören in Issue, Pull Request oder Knowledge-Artikel.
