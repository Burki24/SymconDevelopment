# Referenzimplementierungen

Dieses Verzeichnis katalogisiert geprüfte Burki24-Projekte oder konkrete Implementierungen, die als Beispiel dienen. Referenzen sind nicht automatisch verbindlich und werden nicht blind kopiert.

## Katalog

- [`Symcon_ModuleHelper`](Symcon_ModuleHelper.md): zentrale Helper-Quelle, Manifest- und Consumer-Synchronisierung sowie projektspezifische Abgrenzung von den allgemeinen Modulstandards
- [`Symcon-Dokumentation`](symcon/README.md): lokale deutsche und englische Snapshots der offiziellen Dokumentation zur projektübergreifenden Volltextsuche

Jeder Eintrag sollte enthalten:

- Repository und möglichst unveränderliche Version, Tag oder Commit
- relevanter Pfad oder relevanter Baustein
- wofür die Implementierung als Referenz gilt
- zuletzt geprüfte Plattform- und Abhängigkeitsversionen
- bekannte Grenzen oder bewusst nicht zu übernehmende Teile

Bevor eine Referenz verwendet wird, werden ihr Vertrag, ihre Aktualität und ihre Eignung für das Zielprojekt geprüft. Verbindliche Regeln stehen ausschließlich in `AGENTS.md`, `standards/` oder einem angenommenen ADR.

SAEF kann als konzeptionelle Inspirationsquelle genannt werden. SAEF-spezifische Deployment-, Runtime-Mirror-, SSH-/PowerShell- oder MQTT-Frameworkteile gehören nicht zu den Burki24-Referenzmustern dieser Basis.
