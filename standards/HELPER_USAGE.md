# Verwendung gemeinsamer Helper

## Leitregel

Vor einer neuen lokalen Hilfsfunktion wird geprüft, ob `Symcon_ModuleHelper` oder ein vorhandener Baustein unter `libs/helper` die Aufgabe bereits erfüllt. Wiederverwendung ist der Standard; lokale Duplikate zentraler Helper sind nicht zulässig.

## Entscheidungsfolge

1. Suche im betroffenen Modul und Repository nach bestehendem Verhalten.
2. Prüfe die eingebundene Version und API von `Symcon_ModuleHelper`.
3. Prüfe vergleichbare Burki24-Module auf eine freigegebene Nutzung.
4. Verwende die bestehende Funktion, wenn ihr Vertrag passt.
5. Fehlt eine allgemein nutzbare Funktion, schlage eine getrennte Ergänzung im zuständigen Helper-Repository vor.
6. Implementiere lokal nur dann, wenn die Logik wirklich modulspezifisch ist; benenne und teste diese fachliche Zuständigkeit klar.

## Keine Duplikate

Als Duplikat gilt auch leicht umbenannter oder nur minimal veränderter Helper-Code mit demselben fachlichen Vertrag. Ein kurzfristiges Kopieren „bis später“ ist keine akzeptierte Integrationsstrategie.

Wenn eine neue Helper-Version im Zielprojekt noch nicht verfügbar ist, werden Abhängigkeit, Versionsanforderung und Migrationsreihenfolge geklärt. Es wird kein stiller Fallback durch Kopieren eingebaut.

## Ablage

- Repositoryweit geteilter Code: `libs/helper`
- Modulinterne, ausschließlich fachliche Logik: im Modul nach dessen vorhandener Struktur
- Tests und Testhilfen: `tests` nach bestehender Testkonvention
- Kein `.shared`, kein `.tests`

## Prüfung

Bei Änderungen an gemeinsamem Verhalten sind alle bekannten Aufrufer, ihre Eingabeformen und ihre Fehlererwartungen zu prüfen. Öffentliche Verträge werden nicht unbeabsichtigt über eine Helper-Änderung verschoben.

Bei Modulen mit `IPSModuleStrict` werden zusätzlich die Signaturen eingebundener Traits gegen die echte Basisklasse geprüft. Eine Freigabe für `IPSModule` belegt nicht automatisch Strict-Kompatibilität. Fehlende Kompatibilität wird als eigene Helper-Änderung behandelt; Tests vorhandener Consumer und ein erforderlicher Laufzeitnachweis gehören dazu. Hintergrund: [`knowledge/strict-module-helper-compatibility.md`](../knowledge/strict-module-helper-compatibility.md).

Die zugrunde liegende Zuständigkeitsentscheidung steht in [`ADR 0003`](../adr/0003-use-symcon-modulehelper.md).
