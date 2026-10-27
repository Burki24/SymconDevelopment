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

## Dynamische Formularbreite

Formulare nutzen die verfügbare Breite der Symcon-Konsole. Übergeordnete
Container wie `ExpansionPanel` erhalten grundsätzlich keine feste Pixelbreite;
ohne `width` können sie sich an den verfügbaren Platz anpassen. Vorschauen und
andere flächige Inhalte verwenden bei Bedarf eine relative Breite (zum
Beispiel `100%`). Eine feste Breite ist nur für einzelne Bedienelemente oder
Spalten zulässig, wenn sie deren Lesbarkeit verbessert. Begründete Ausnahmen
für Container werden im Projekt dokumentiert.

Die Breitenregel verspricht kein automatisches Umbrechen jeder Feldgruppe:
Feldanordnung und lange Beschriftungen werden zusätzlich in schmalen und
breiten Konsolenansichten auf Überlauf, Abschneiden und Bedienbarkeit geprüft.

## Farbzuordnung in Kachel- und IPSView-Designern

Diese Vorgabe gilt libraryübergreifend für alle Module mit konfigurierbaren
Farben: Jeder Kachel- und IPSView-Designer enthält eine modulbezogene,
beschriftete Beispielgrafik mit verständlicher Legende. Sie zeigt, welcher
sichtbare Bereich durch welches Farbfeld gesteuert wird. Bei mehreren
Darstellungsvarianten werden deren gemeinsame und abweichende Zuordnungen
erkennbar; eine beliebige allgemeine Farbpalette genügt nicht.

**Jede Grafik wird an das zugehörige Modul und dessen tatsächliche Kachel- bzw.
IPSView-HTML-Darstellung angepasst.** Aufbau, sichtbare Elemente, Zustände und
Farbzuordnungen müssen zur konkreten Ausgabe passen. Beispielsweise erhält eine
Alarmdarstellung eine passende Alarmansicht, ein Kalender seine Kalenderansicht
und ein Diagrammmodul den jeweiligen Diagrammtyp. Eine Gerätekarte aus der
Anwesenheit darf nicht allein durch Umbenennen der Legende für ein anderes Modul
übernommen werden. Gemeinsame Helper und Gestaltungsmittel sind wiederverwendbar;
das erläuterte Motiv und die Zuordnung zu den tatsächlich verwendeten HTML-/CSS-
Bereichen bleiben modulbezogen. Ändert sich die Ausgabe, wird die Grafik im
selben Änderungszusammenhang abgeglichen und nötigenfalls aktualisiert.

- Bild und Textlegende verwenden **exakt dieselben lokalisierten Feldnamen**
  wie der Designer. In der deutschen Oberfläche stehen die deutschen
  Bezeichnungen im Vordergrund, etwa „View-Hintergrund“, „Label-Schrift“ oder
  „Akzentfarbe“. Englische/technische Property-Namen und Farbrollen dürfen
  kleiner oder in Klammern ergänzt werden, ersetzen diese Feldnamen aber nicht.
- Bezeichnungen aus zentralen Helpern werden aus deren Übersetzungskatalogen
  bezogen. Keine abweichenden Begriffe erfinden und keine parallelen Kopien
  zentraler Übersetzungen pflegen. Vorbereitete Bildressourcen müssen gegen
  die zugehörigen Katalogbezeichnungen geprüft werden.
- Hintergrund, Bedienelemente, Textarten, semantische Statusfarben, Auswahl,
  Rahmen und Schatten werden erklärt, soweit die Ausgabe sie tatsächlich nutzt.
  Abgeleitete Mischfarben oder Deckkräfte werden als Ableitungen benannt und
  keinem erfundenen eigenen Farbfeld zugeordnet. Nicht verwendete Designerfarben
  werden ausdrücklich von den wirksamen Farben unterschieden.
- Eine feste schematische Farbkarte ist zulässig und als solche zu kennzeichnen.
  Sie darf nicht als Live-Vorschau aktueller oder ungespeicherter Einstellungen
  erscheinen. Die Zuordnung muss für eigene Farben und Hell-/Dunkelstile stimmen.
- Die Grafik bleibt bei schmaler und breiter Konsole lesbar, nutzt flexible
  Breiten und enthält keine privaten Geräte-, Konto- oder Installationsdaten.
  Ihre Anzeige benötigt keine externen Bilddienste und verändert keine
  Konfiguration oder Gerätezustände.
- Vorhandene zentrale SVG-/Formular-/Asset-Helper werden gemäß
  [HELPER_USAGE.md](HELPER_USAGE.md) wiederverwendet. Modulbezogene Bildinhalte
  bleiben beim Modul; diese Vorgabe ändert die Zentralisierungsregeln nicht.

Neue und überarbeitete Designer erfüllen diese Vorgabe. Bestehende Designer
aller Libraries werden in gesonderten Folgearbeiten geprüft und entsprechend
ergänzt; die Aufnahme der Regel bedeutet keine bereits erfolgte Umsetzung oder
Abnahme in anderen Libraries. Fortschritt und Praxisabnahme werden jeweils im
zuständigen Projektkontext festgehalten. Die nachgewiesene Farbzuordnung von
SymconiCloud Anwesenheit dient als Referenz, nicht als unveränderte Kopiervorlage.

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
- übergeordnete Container passen sich an schmale und breite Konsolenansichten an; Ausnahmen mit fester Breite sind begründet.
- Designer-Farbkarten stimmen mit den verwendeten Farbfeldern und deren
  lokalisierten Bezeichnungen überein; Bildressourcen und Textlegenden werden
  gemäß [TESTING.md](TESTING.md#designer-farbkarten-und-lokalisierung) geprüft.

API-Details und verfügbare Elemente werden über die [offiziellen Symcon-Dokumentationseinstiege](../references/symcon/README.md) nachgeschlagen. Der zentrale Helper-Vertrag ist unter [`references/Symcon_ModuleHelper.md`](../references/Symcon_ModuleHelper.md) beschrieben.
