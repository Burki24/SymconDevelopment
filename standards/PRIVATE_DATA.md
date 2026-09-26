# Private Daten und Geheimnisse

## Grundsatz

Repositories, Beispiele, Test-Fixtures, Logs und Diagnosedaten enthalten keine Geheimnisse oder privaten Installationsdetails. Das gilt auch für private GitHub-Repositories, da Inhalte über Historie, Forks, Artefakte oder spätere Sichtbarkeitsänderungen erhalten bleiben können.

## Nicht versionieren

Insbesondere nicht einchecken:

- Passwörter, API-Schlüssel, OAuth-Secrets, Tokens und private Schlüssel;
- reale interne IP-Adressen, Hostnamen und nicht öffentliche Endpunkte;
- persönliche oder installationsbezogene Symcon-ObjectIDs;
- private MQTT-Topics, Gerätekennungen und Standortinformationen;
- vollständige externe Antworten mit Personen-, Konto- oder Gerätedaten;
- lokale Systembeschreibungen, Backups und exportierte Konfigurationen;
- produktive `.env`-, Authentifizierungs- oder Credential-Dateien.

Testdaten und Beispiele verwenden erkennbare Platzhalter oder synthetische Werte. Eine Anonymisierung muss auch zusammengesetzte Logs, Screenshots und JSON-Payloads berücksichtigen.

## Zulässige Ablage

Geheimnisse werden über die vom Zielsystem vorgesehenen Mechanismen verwaltet, beispielsweise GitHub Secrets oder geschützte Symcon-Konfiguration. Lokale Dateien werden nur verwendet, wenn das Projekt dies vorsieht und sie zuverlässig ignoriert werden.

Für lokale, nicht versionierte Arbeitsdaten sind je nach Projekt beispielsweise `private/`, `*.local.*` oder `.env*` möglich. Diese Namen sind keine Sicherheitsgrenze: Vor jedem Commit bleibt der vollständige Diff auf sensible Inhalte zu prüfen.

## Code, Logs und Diagnose

- Zugangsdaten werden nicht in URLs, Fehlermeldungen oder Debug-Ausgaben aufgenommen.
- Externe Payloads werden nur ausschnittsweise und bereinigt protokolliert.
- Diagnosespeicher bleiben begrenzt und enthalten nur den zur Fehleranalyse notwendigen Kontext.
- Konfigurations-Hashes sind Fingerabdrücke, keine Geheimnis- oder Integritätsmechanismen; sensible Rohwerte gehören nicht in Diagnoseausgaben.
- Pull-Request-Beschreibungen und CI-Artefakte werden wie Repository-Inhalte behandelt.

## Vorfall

Wurde ein Geheimnis eingecheckt, genügt das Entfernen aus der aktuellen Datei nicht. Das Geheimnis wird unverzüglich widerrufen oder rotiert; anschließend werden Reichweite, Historie, Logs und Artefakte geprüft. Eine notwendige Historienbereinigung erfolgt nur als gesonderte, ausdrücklich freigegebene Maßnahme.
