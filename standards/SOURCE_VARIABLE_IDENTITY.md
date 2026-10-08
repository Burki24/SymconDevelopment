# Identität konfigurierter Quellvariablen

## Grundsatz

Bei Verweisen auf bestehende IP-Symcon-Variablen ist die **Variablen-ID** die
einzige technische Identität der Quelle. Das gilt für alle
Module, insbesondere für Konfiguration, Deduplizierung, Datenfluss,
Aktualisierungen, Caches und die Zuordnung in Visualisierungen.

Variablenname, Objektpfad, übergeordnete Instanz, Kategorie, Datenreihenname,
Einheit und sonstige Beschriftungen sind keine Ersatzschlüssel. Mehrere
Variablen dürfen denselben Namen und Pfadbestandteile besitzen; sie bleiben
anhand ihrer unterschiedlichen Variablen-IDs getrennte Quellen. Eine
Instanz-ID identifiziert die Instanz, nicht eine ihrer möglicherweise mehreren
Variablen.

## Darstellung und fachliche Gruppierung

- Ein ausdrücklich konfigurierter Anzeigename hat Vorrang. Ohne solchen Namen
  wird der aktuelle Symcon-Name der referenzierten Variablen angezeigt.
  Sichtbare Bezeichnungen ändern die Quellenidentität nicht.
- Gleichlautende Bezeichnungen dürfen keine Quelle verwerfen, zusammenführen
  oder eine gültige Konfiguration ungültig machen.
- Variablen- und Instanz-IDs bleiben ausschließlich intern. Sie werden nicht
  automatisch an Beschriftungen angehängt und erscheinen nicht in Ansichten.
  Auch bei gleichen sichtbaren Namen bleiben die Quellen über ihre IDs
  getrennt. Ein Objektpfad wird nicht zur Identitätsbestimmung herangezogen.
- Ausdrücklich konfigurierte Kategorien oder Datenreihen können eine
  **fachliche Gruppierung** definieren. Diese Gruppierung ist von der
  technischen Identität jedes enthaltenen Variablenwerts zu trennen; auch
  innerhalb einer Gruppe darf kein Wert allein wegen gleicher Namen verloren
  gehen.

## Lebenszyklus und Prüfung

Die Variablen-ID ist innerhalb der jeweiligen Symcon-Installation stabil,
aber keine installationsübergreifende Identität. Import, Migration oder
Wiederherstellung zwischen Installationen benötigen deshalb eine ausdrücklich
definierte Zuordnung; IDs werden nicht blind auf fremde Installationen
übertragen.

Tests decken mindestens zwei verschiedene Variablen-IDs mit gleichem Namen
und gleicher fachlicher Gruppierung ab. Sie prüfen, dass beide Werte getrennt
erhalten bleiben und eine Umbenennung von Variable oder Elternobjekt die
technische Zuordnung nicht verändert. Sichtbare Namen enthalten keine
automatisch ergänzten IDs; ein konfigurierter Anzeigename hat Vorrang.
