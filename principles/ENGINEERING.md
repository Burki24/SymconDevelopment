# Engineering-Prinzipien

## 1. Zuverlässigkeit vor Bequemlichkeit

Symcon-Module steuern und beobachten reale Systeme. Vorhersagbares Verhalten, sichere Fehlerpfade und verständliche Zustände sind wichtiger als eine besonders kurze oder schnelle Implementierung.

## 2. Vorhandene Architektur vor neuer Abstraktion

Vor jeder Änderung werden die bestehende Struktur, öffentliche Verträge, Helper, Tests und vergleichbare Implementierungen gelesen. Neue Abstraktionen entstehen nur, wenn sie einen belegten wiederkehrenden Bedarf besser lösen als die vorhandenen Bausteine.

## 3. Verträge bleiben stabil

Properties, Idents, öffentliche Methoden, Statuscodes, persistierte Werte und sichtbares Verhalten sind Verträge. Änderungen benötigen eine bewusste Kompatibilitätsentscheidung und, falls erforderlich, eine Migration.

## 4. Konfiguration ist deterministisch und idempotent

Wiederholtes Anwenden derselben Konfiguration darf keine Duplikate oder unnötigen Seiteneffekte erzeugen. Automatisch verwaltete Objekte haben eine klare Zuständigkeit und stabile technische Identitäten.

Bei konfigurierten Quellvariablen steht die Variablen-ID als technische
Identität an erster Stelle. Namen, Pfade und sichtbare Gruppierungen können
gleich sein oder sich ändern, ohne Quellen zu vereinen oder zu verwerfen;
Details regelt [`SOURCE_VARIABLE_IDENTITY.md`](../standards/SOURCE_VARIABLE_IDENTITY.md).

## 5. Eine kanonische Quelle pro gemeinsamer Fähigkeit

Gemeinsame PHP-Funktionen gehören in `Symcon_ModuleHelper`, gemeinsame CI-Logik in `Symcon_ModuleCI` und gemeinsame Regeln in dieses Repository. Lokale Kopien gemeinsamer Bausteine werden nicht als Abkürzung verwendet.

## 6. Kleine, nachvollziehbare Änderungen

Eine Änderung löst ein klar abgegrenztes Problem. Fachliche Anpassungen, Migrationen, Formatierung und Infrastrukturänderungen werden nur kombiniert, wenn sie untrennbar zusammengehören.

## 7. Nachweise vor Behauptungen

Tests, Style- und Strukturprüfungen belegen nur den jeweils geprüften Bereich. Abschlussberichte unterscheiden ausgeführte Nachweise, nicht geprüfte Risiken und begründete Annahmen.

## 8. Entscheidungen und Wissen bleiben auffindbar

Langfristige Entscheidungen erhalten ein ADR. Wiederverwendbare Diagnose- und Lösungserfahrung wird in der Knowledge Base festgehalten. Dokumentation ist Bestandteil einer fachlichen Änderung, nicht nachgelagerte Dekoration.

## 9. Private Daten bleiben außerhalb des Repositories

Zugangsdaten, Tokens und installationsbezogene Interna werden nicht in Code, Beispiele, Logs oder Git-Historie übernommen. Auch private Repositories sind kein sicherer Ablageort für Geheimnisse.

## 10. Komplexität muss sich verdienen

Optionale Frameworkschichten, Helper oder Automationen werden erst eingeführt, wenn ihr Nutzen durch konkrete Projekte belegt ist. Ein einmaliger Anwendungsfall bleibt in der Regel lokal.
