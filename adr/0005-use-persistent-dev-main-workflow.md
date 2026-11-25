# ADR 0005: Dauerhaftes dev/main-Branch-Modell verwenden

- Status: Angenommen
- Datum: 2026-09-26
- Entscheider: Burki24
- Ersetzt: –
- Ersetzt durch: –

## Kontext

Die Burki24-Repositories benötigen einen stabilen veröffentlichten Stand und zugleich einen dauerhaften Integrationszweig für laufende Entwicklung. Wird `dev` nach einem Release-Pull-Request gelöscht oder nicht mit dem Merge-Ergebnis synchronisiert, entstehen unnötige Neuanlagen, Abweichungen und Folgekonflikte.

## Entscheidung

- `main` repräsentiert den stabilen beziehungsweise veröffentlichten Stand.
- `dev` ist der dauerhafte Arbeits- und Integrationszweig. Alle Aufgaben werden direkt auf `dev` bearbeitet.
- Ein Release wird über einen Pull Request von `dev` nach `main` vorbereitet und geprüft.
- Nach dem Merge wird das Ergebnis aus `main`, einschließlich des Merge-Commits, wieder nach `dev` synchronisiert.
- `dev` bleibt nach Merges bestehen und ist vom automatischen Löschen ausgenommen.
- Tags und Releases werden vom geprüften stabilen Stand erstellt.

Projekte mit zusätzlichen dauerhaften Versionszweigen dokumentieren Zielrichtung und Rücksynchronisierung in ihrer lokalen `AGENTS.md`.

## Alternativen

- **Nur `main`:** vereinfacht die Branch-Struktur, vermischt aber laufende Integration und stabilen Veröffentlichungsstand.
- **Kurzlebiger `dev`:** erzeugt nach jedem Release unnötige Wiederherstellung und verliert die dauerhafte Integrationslinie.
- **GitFlow mit weiteren permanenten Zweigen:** bietet mehr Trennung, ist für die vorhandenen Modulprojekte ohne belegten Bedarf zu schwergewichtig.

## Folgen

Der Veröffentlichungsstand bleibt klar von laufender Arbeit getrennt. Nach jedem Release ist eine bewusste Rücksynchronisierung erforderlich. Pull-Request- und Branch-Schutzregeln müssen `dev` als dauerhaften Branch behandeln.

## Nachweise

- [`standards/GIT_WORKFLOW.md`](../standards/GIT_WORKFLOW.md)
- bewährter Release- und Rücksynchronisierungsablauf in den angebundenen Burki24-Repositories
