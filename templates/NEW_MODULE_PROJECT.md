# Vorlage für ein neues Symcon-Modulprojekt

Diese Vorlage ist eine Entscheidungs- und Vollständigkeitscheckliste. Sie erzeugt bewusst kein blind kopierbares Universalmodul: GUIDs, Modulart, Verbindungen, Properties und Abhängigkeiten müssen für das konkrete Projekt festgelegt werden.

## 1. Auftrag klären

- Fachlicher Zweck: <!-- ein klarer Satz -->
- Gewünschte Module: <!-- Namen und Verantwortungen -->
- Öffentliche Schnittstellen: <!-- Methoden, Actions, Datenformate -->
- Externe Systeme: <!-- Geräte, Dienste, APIs -->
- Nicht im Umfang: <!-- bewusste Grenzen -->

Prüfe zuerst, ob das Modul in eine bestehende Bibliothek gehört oder ein eigenes Repository rechtfertigt.

## 2. Verträge festlegen

- Erzeuge neue, eindeutige GUIDs nach der gültigen Symcon-Konvention; kopiere keine IDs aus Referenzprojekten.
- Definiere stabile Modul- und Property-Namen, Idents, Variablentypen und Statuszustände.
- Entscheide, welche Variablen read-only, berechnet oder über `RequestAction()` steuerbar sind.
- Lege Parent-/Child-Verbindungen und öffentliche Methoden nur an, wenn der fachliche Datenfluss sie benötigt.
- Wähle native Variablendarstellungen; nutze Legacy-Profile nur bei begründetem Kompatibilitätsbedarf.

## 3. Erwartete Struktur

```text
Repository/
├── AGENTS.md
├── PROJECT_CONTEXT.md
├── README.md
├── CHANGELOG.md                  # aus templates/CHANGELOG.md
├── LICENSE                       # nach der Projektentscheidung
├── .gitignore
├── library.json
├── composer.json                 # falls von der gewählten Referenz benötigt
├── libs/
│   └── helper/                   # synchronisierte gemeinsame Helper
├── tests/
├── ModulName/
│   ├── module.json
│   ├── module.php
│   ├── form.json                 # wenn konfigurierbar
│   ├── locale.json               # wenn erforderlich
│   └── README.md
└── .github/
    └── workflows/
```

Optionale Dateien werden nur mit konkretem Zweck angelegt. Maßgeblich bleiben [`standards/MODULE_STRUCTURE.md`](../standards/MODULE_STRUCTURE.md) und eine aktuell freigegebene Burki24-Referenz.

## 4. Implementierungsreihenfolge

1. Lege Library- und Modulmetadaten mit neuen Identitäten an. Neue Module verwenden `IPSModuleStrict`; Signaturen und Helper-Kompatibilität werden nach [`standards/PHP_STYLE.md`](../standards/PHP_STYLE.md) geprüft.
2. Registriere Properties, Attribute, Timer und dauerhaft vorhandene Variablen deterministisch.
3. Implementiere `ApplyChanges()` idempotent und mit kontrollierter Konfigurationsvalidierung.
4. Implementiere Actions und öffentliche Methoden an ihren fachlichen Grenzen.
5. Ergänze das Konfigurationsformular und native Variablendarstellungen nach den zentralen Standards.
6. Binde nur tatsächlich benötigte Dateien aus `Symcon_ModuleHelper` über den vorgesehenen Consumer-Prozess ein.
7. Ergänze Tests, Benutzer-READMEs, Changelog, Projektkontext und CI. Diagnose- und Entwicklungshinweise gehören in die interne Dokumentation.

## 5. Mindestnachweise

- Metadaten und Formulare sind gültiges JSON.
- `validate_structure`, StylePHP und php-cs-fixer sind erfolgreich.
- Tests decken frische Konfiguration, wiederholtes `ApplyChanges()`, Actions sowie wichtige Fehlerfälle ab.
- Die vorgesehene PHP-8.5-/Symcon-9-Matrix ist über `Symcon_ModuleCI` v1.0.0 grün.
- Ein erforderlicher Praxistest unter IP-Symcon ist dokumentiert.
- Benutzer-READMEs beschreiben Voraussetzungen, Konfiguration, Variablen und sichtbares Verhalten nach [`standards/README_CONTENT.md`](../standards/README_CONTENT.md).
- Sichtbare Änderungen stehen im Changelog nach [`standards/CHANGELOG.md`](../standards/CHANGELOG.md).

## 6. Vor Veröffentlichung

- Keine Platzhalter, kopierten GUIDs, privaten ObjectIDs oder Zugangsdaten vorhanden.
- Keine lokalen Duplikate zentraler Helper vorhanden.
- Öffentliche Verträge und Migrationsfolgen geprüft.
- Branch- und Releaseablauf folgt [`standards/GIT_WORKFLOW.md`](../standards/GIT_WORKFLOW.md).
- Relevante Architekturentscheidungen sind als ADR dokumentiert.
- Release-Einträge im Changelog stimmen mit freigegebener Version, Veröffentlichungsdatum und sichtbarem Änderungsumfang überein.
