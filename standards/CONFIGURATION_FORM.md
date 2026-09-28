# Konfigurationsformulare

## Ziel

Konfigurationsformulare bilden die persistente Modulkonfiguration verständlich und reproduzierbar ab. Sie bleiben möglichst statisch, validierbar und frei von unnötigen Laufzeitabhängigkeiten.

## Grundstruktur

- Verwende eine `form.json` als lesbare Ausgangsbasis, wenn das Modul ein Konfigurationsformular besitzt.
- Nutze die von der Zielversion unterstützten offiziellen Elementfelder. Für normale Eingabeelemente ist `caption` die sichtbare Beschriftung; elementspezifische Felder werden nicht mechanisch umbenannt.
- Der `name` eines persistenten Eingabeelements entspricht der registrierten Property und bleibt nach Veröffentlichung stabil.
- Trenne persistente Einstellungen unter `elements` von Diagnose-, Test- und Bedienaktionen unter `actions`.
- Beschriftungen und Meldungen müssen dem vorhandenen Lokalisierungskonzept des Projekts folgen.

## Statisch vor dynamisch

Ein statisches Formular ist der Standard. `GetConfigurationForm()` wird nur eingesetzt, wenn Inhalte von Instanzzustand, vorhandenen Objekten oder anderen zur Laufzeit ermittelten Daten abhängen.

Wenn `Symcon_ModuleHelper` im Projekt eingebunden ist, wird für dynamische Formulare der vorhandene `ConfigurationFormHelper` bevorzugt. Er lädt und validiert die modulbezogene `form.json` und serialisiert die ergänzte Struktur einheitlich. Eine lokale Kopie dieser Logik ist nicht zulässig.

Dynamische Ergänzungen müssen:

- auf einer gültigen statischen Ausgangsstruktur aufbauen;
- stabile Feldnamen und Listenschlüssel verwenden;
- leere, fehlende und fehlerhafte Laufzeitdaten verständlich darstellen;
- ohne unbeabsichtigte Änderung persistenter Properties wiederholt aufrufbar sein;
- externe Zugriffe beim bloßen Öffnen des Formulars vermeiden oder klar begrenzen;
- Fehler als hilfreichen Formularzustand anzeigen, statt ein ungültiges Formular zurückzugeben.

## Interaktion

- `visible` und `enabled` steuern ausschließlich die Bedienoberfläche; `ApplyChanges()` validiert unabhängig davon alle relevanten Properties.
- `IPS_UpdateFormField()` aktualisiert den geöffneten Dialog, ersetzt aber keine persistente Konfiguration oder fachliche Validierung.
- `onChange`, `onClick` und vergleichbare Skripte bleiben klein und delegieren komplexe Arbeit an klar benannte Modulmethoden.
- Aktionsskripte behandeln übergebene Werte defensiv und dürfen keine Zugangsdaten, Tokens oder vollständigen externen Antworten ausgeben.
- Potenziell destruktive Aktionen benötigen eine eindeutige Beschriftung, eine angemessene Bestätigung und eine klar begrenzte Wirkung.

## Verträge und Kompatibilität

Property-Namen, Datentypen und Defaultwerte sind öffentliche Konfigurationsverträge. Eine Umbenennung oder Typänderung erfolgt nicht allein durch Anpassung der `form.json`, sondern benötigt eine Migration nach [`MIGRATIONS.md`](MIGRATIONS.md).

Ein neues Formular darf bestehende gespeicherte Werte nicht unbemerkt durch neue Defaults ersetzen. Entfernte oder versteckte Felder werden darauf geprüft, ob ihre Properties weiterhin gelesen, migriert oder bewusst aufgegeben werden.

## Prüfung

Mindestens zu prüfen sind:

- `form.json` ist gültiges JSON mit der erwarteten Wurzelstruktur;
- jedes persistente Feld besitzt eine passende registrierte Property;
- `GetConfigurationForm()` liefert auch bei fehlenden optionalen Laufzeitdaten gültiges JSON;
- dynamische Listen und Sichtbarkeiten sind für leere und gefüllte Zustände nachvollziehbar;
- `ApplyChanges()` weist ungültige oder unvollständige Konfiguration kontrolliert ab;
- sichtbare Texte sind gemäß Projektkonvention lokalisierbar.

API-Details und verfügbare Elemente werden über die [offiziellen Symcon-Dokumentationseinstiege](../references/symcon/README.md) nachgeschlagen. Der zentrale Helper-Vertrag ist unter [`references/Symcon_ModuleHelper.md`](../references/Symcon_ModuleHelper.md) beschrieben.
