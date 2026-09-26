# Modulstruktur

## Ziel

Symcon-Repositories sollen vertraut, prüfbar und ohne projektspezifische Sonderpfade aufgebaut sein. Vor einer Strukturänderung ist immer die vorhandene Architektur zu lesen.

## Erwartetes Grundbild

```text
Repository/
├── library.json
├── README.md
├── composer.json                 # falls im Projekt verwendet
├── libs/
│   └── helper/                   # gemeinsame Helper und Einbindungen
├── tests/                        # Tests für Bibliothek und Module
├── ModulName/
│   ├── module.json
│   ├── module.php
│   ├── form.json                 # wenn das Modul ein Konfigurationsformular hat
│   ├── locale.json               # wenn Lokalisierung benötigt wird
│   └── README.md
└── .github/
    └── workflows/                # CI-Konfiguration
```

Die reale Struktur des jeweiligen Repositories bleibt maßgeblich. Optionale Dateien werden nur angelegt, wenn das Modul sie tatsächlich benötigt.

## Verbindliche Regeln

- Verwende `libs/helper` für gemeinsam genutzte Hilfsbausteine. Lege kein `.shared` an.
- Verwende `tests` für Tests. Lege kein `.tests` an.
- Jedes veröffentlichte Modul besitzt eine eigene `README.md` mit Zweck, Voraussetzungen, Konfiguration und sichtbarem Verhalten.
- Bewahre die vorhandene Benennung und Aufteilung eines Repositories, solange keine begründete Migration beschlossen wurde.
- Nutze vorhandene zentrale Helper, insbesondere `Symcon_ModuleHelper`; kopiere deren Funktionen nicht in Module.
- Neue gemeinsame Abstraktionen benötigen mindestens zwei konkrete Anwendungsfälle oder eine bereits beschlossene zentrale Zuständigkeit.
- Generierte Dateien, Abhängigkeiten und lokale Werkzeuge gehören nicht ohne vorhandene Projektkonvention in das Repository.

## Vor einer Änderung prüfen

1. Welche Module und öffentlichen Verträge sind betroffen?
2. Gibt es bereits eine vergleichbare Implementierung?
3. Welche Helper und Traits werden heute eingebunden?
4. Welche Struktur erwartet `validate_structure`?
5. Welche Tests und Modul-READMEs müssen gemeinsam angepasst werden?

Strukturelle Migrationen werden nicht nebenbei vorgenommen. Sie benötigen einen eigenen Umfang, einen Kompatibilitätsplan und bei dauerhaften Architekturfolgen ein ADR.
