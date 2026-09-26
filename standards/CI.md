# Continuous Integration

## Gemeinsame Basis

Burki24-Symcon-Repositories verwenden `Symcon_ModuleCI` v1.0.0. Neue oder aktualisierte Workflows orientieren sich an einer bereits freigegebenen Burki24-Implementierung und pinnen die vorgesehene Version eindeutig.

Die CI muss mindestens die im Projekt konfigurierten Varianten dieser Prüfungen abdecken:

- StylePHP
- php-cs-fixer im Prüfmodus
- `validate_structure`
- vorhandene Tests unter `tests`

Versions-, PHP- oder Symcon-Matrizen werden aus dem jeweiligen Repository und der freigegebenen ModuleCI-Konfiguration übernommen; sie werden nicht in diesem allgemeinen Standard erfunden.

## Änderungsregeln

- Lies bestehende Workflows und `composer.json`, bevor du CI änderst.
- Aktualisiere keine Actions, Abhängigkeiten oder Matrizen beiläufig zusammen mit einer fachlichen Änderung.
- Halte lokale Prüfkommandos und CI-Verhalten möglichst deckungsgleich.
- Entferne keine Prüfung, um einen Pull Request grün zu machen. Kläre Ursache und Zuständigkeit.
- Behandle Warnungen, fehlende Artefakte und übersprungene Tests sichtbar.
- Secrets werden weder in Workflow-Dateien noch in Logs oder Beispielen hinterlegt.

## Abgrenzung

Die CI prüft Quellcode, Struktur und Tests. Deployment, Runtime-Mirror, Fileset-Verteilung, SSH-/PowerShell-Orchestrierung und MQTT-Infrastruktur sind nicht Bestandteil dieser Entwicklungsbasis.

## Nachweis im Pull Request

Der Pull Request beschreibt:

- welche lokalen Prüfungen gelaufen sind;
- welche CI-Prüfungen erwartet werden;
- warum eine Prüfung gegebenenfalls nicht ausführbar oder nicht relevant war;
- ob die Änderung die unterstützte Plattform IP-Symcon 9 / PHP 8.5 berührt.

Die Entscheidung für die gemeinsame CI-Basis steht in [`ADR 0004`](../adr/0004-use-symcon-moduleci.md).
