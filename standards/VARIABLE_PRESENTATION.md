# Variablendarstellungen

## Ziel

Variablen besitzen neben Typ und Wert einen sichtbaren Vertrag: Bedeutung, Einheit, Wertebereich, Bedienbarkeit und Darstellung müssen zusammenpassen. IP-Symcon-9-Darstellungen werden für neue oder bewusst modernisierte Module gegenüber neu eingeführten Legacy-Profilen bevorzugt.

Bestehende Variablenprofile bleiben ein unterstützter Kompatibilitätsvertrag. Sie werden nicht ohne Migrationsentscheidung entfernt oder ersetzt.

## Verbindliche Trennung

- **Ident und Typ** bestimmen die technische Identität und den gespeicherten Wert.
- **Darstellung** beschreibt die Visualisierung und zulässige Bedienoberfläche.
- **Action** bestimmt, wie eine Benutzeränderung fachlich verarbeitet wird.

Eine Darstellungsänderung darf nicht beiläufig Ident, Variablentyp, Wertebedeutung oder gespeicherte Historie ändern.

## Verwendung gemeinsamer Darstellungen

Wenn `Symcon_ModuleHelper` im Projekt eingebunden ist, werden passende Methoden aus `VariablePresentationHelper` verwendet. Der Helper stellt generische native Darstellungen bereit, unter anderem für Boolean-, Text-, Zahlen-, Temperatur-, Prozent-, Slider-, Helligkeits-, Farb-, Dauer-, Schalter-, Rollladen-, Aufzählungs-, Webinhalt- und Datum/Uhrzeit-Werte.

- Erzeuge keine lokale Kopie einer vorhandenen Presentation-Methode.
- Geräte-, Protokoll- oder Providerlogik bleibt im fachlich zuständigen Modul.
- Neue zentrale Methoden benötigen einen generischen Vertrag und mehrere reale Anwendungsfälle.
- Übersetzbare Beschriftungen werden vom aufrufenden Modul nach dessen Lokalisierungskonzept bereitgestellt.

## Lebenszyklus

- Dauerhaft vorhandene Variablen werden nach der vorhandenen Modulkonvention registriert.
- Bedingt sichtbare oder konfigurationsabhängige Variablen werden deterministisch gepflegt, typischerweise über die vorhandenen `MaintainVariable*`-Muster.
- Wiederholtes `ApplyChanges()` darf weder Variablen duplizieren noch unnötig Darstellungen wechseln.
- Stabile Idents bleiben bei Umbenennungen sichtbarer Bezeichnungen erhalten.
- Das Entfernen einer verwalteten Variable wird auf Datenverlust, Archivhistorie und Rückwärtskompatibilität geprüft.

## Bedienbare Variablen

Eine steuerbare Variable erhält eine Action und verarbeitet Benutzeränderungen über `RequestAction()`. Direkte Wertänderungen dürfen die fachliche Action-Schicht nicht umgehen.

`SetValue*()` ist für modul- oder skripteigene Status-, Cache- und Ergebnisvariablen vorgesehen. Bei Variablen fremder Instanzen oder Geräte wird deren öffentlicher Action-Vertrag verwendet.

## Migration von Profilen

Eine Umstellung von einem Legacy-Profil auf eine native Darstellung ist eine sichtbare Änderung. Vor der Migration sind mindestens zu prüfen:

- Wertebereich, Schrittweite, Einheit und Nachkommastellen;
- Assoziationen, Icons und Farben;
- Action-Verhalten und Bedienbarkeit;
- benutzerdefinierte oder installationsabhängige Profile;
- Visualisierungen und Tests, die das bisherige Profil erwarten.

Kompatible Altinstallationen dürfen nicht stillschweigend ihre semantische Darstellung verlieren. Die Migrationsentscheidung und gegebenenfalls ein Übergangsverhalten werden dokumentiert.

## Prüfung

- Variablentyp, Darstellung und fachliche Wertebedeutung stimmen überein.
- Read-only- und steuerbare Variablen sind klar unterschieden.
- `RequestAction()` behandelt gültige und ungültige Werte kontrolliert.
- Wiederholtes Anwenden der Konfiguration bleibt idempotent.
- Tests prüfen den Presentation-Vertrag und nicht nur die Existenz der Variable.
- Modul-README dokumentiert sichtbare Variablen, Einheiten, Actions und relevante Änderungen.

Verfügbare native Darstellungen werden über die [offiziellen Symcon-Dokumentationseinstiege](../references/symcon/README.md) geprüft. Der aktuelle gemeinsame Helper-Vertrag ist unter [`references/Symcon_ModuleHelper.md`](../references/Symcon_ModuleHelper.md) katalogisiert.
