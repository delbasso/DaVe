# Base44 Import Anleitung

## Ziel

Die App `Agrardatenkatalog BW` hat jetzt eine vorbereitete Seite `Anforderungssuche` und passende Entitäten.

Diese lokalen Dateien passen zu den neuen Base44-Entitäten:

- `output/base44_import_tables/SourceDocument.csv`
- `output/base44_import_tables/AtomicRequirement.csv`
- `output/base44_import_tables/RequirementCategoryAssignment.csv`
- `output/base44_import_tables/RequirementRelation.csv`
- `output/base44_import_tables/DataCatalogEntry.csv`
- `output/base44_import_tables/base44_import_tables.xlsx`

## Empfohlene Import-Reihenfolge

### Einfachster Weg: JSON-Import in der App

Wenn die Base44-Seite `Import Anforderungskatalog` bzw. der Importbereich in `Anforderungssuche` sichtbar ist:

1. Datei öffnen:
   `output/base44_seed/base44_requirement_seed.json`
2. Inhalt kopieren.
3. In der App in das JSON-Importfeld einfügen.
4. `Vorschau prüfen` klicken.
5. Prüfen, ob etwa diese Counts erscheinen:
   - `atomic_requirements`: 119
   - `data_collections`: 70
   - `source_documents`: 70
6. `Import starten` klicken.

### Alternativer Weg: Tabellenimport

1. `SourceDocument`
2. `AtomicRequirement`
3. `RequirementCategoryAssignment`
4. `RequirementRelation`
5. `DataCatalogEntry`

## Hinweise zu Feldumwandlungen

Einige Felder wurden für Base44 vereinfacht:

- `evidence_required` ist in Base44 ein Ja/Nein-Feld.
  Deshalb steht dort `true`, wenn ein Nachweistext vorhanden ist.

- `requirement_type` wurde auf die Base44-Werte gemappt:
  - `pflicht`
  - `bedingt`
  - `freiwillig`

- `secondary_categories` steht im CSV als Semikolon-Liste.
  Wenn Base44 ein Array erwartet, kann die App diese Liste später beim Import splitten.

- `confidence` wurde von Text auf Zahl gemappt:
  - `hoch` -> `0.9`
  - `mittel` -> `0.65`
  - `niedrig` -> `0.4`

- Die 70 Datenerhebungen aus dem Metadatenkatalog werden als `DataCatalogEntry` exportiert.
  Wichtige Felder:
  - `dct:subject`: Kurztitel der Datenerhebung
  - `dct:description`: Beschreibung
  - `dct:source`: Grundlagendokument
  - `dct:isPartOf`: zugehöriger Prozess / Datensammlung
  - `dcat:frequency`: Frequenz

## Base44 Editor

`https://app.base44.com/apps/693fe406f8910a81b9d72b57/editor/preview`

## Morgen testen

1. Base44 Editor öffnen.
2. Prüfen, ob die Seite `Anforderungssuche` sichtbar ist.
3. Wenn Import möglich ist, zuerst `SourceDocument.csv`, dann `AtomicRequirement.csv` importieren.
4. Danach `DataCatalogEntry.csv` importieren.
5. Suche mit `Stickstoff`, `Pflanzenschutz`, `Aufbewahrung`, `Direktzahlungen FIONA jährlich` testen.

Falls der Import in Base44 nicht direkt angeboten wird, kann der JSON-Export als Grundlage für eine Backend-Funktion genutzt werden:

`output/base44_seed/base44_requirement_seed.json`

## Weaviate-Hinweis

In Weaviate liegt wegen des aktuellen 1-Collection-Limits alles in `AtomicRequirement`.

Die Trefferarten werden über `record_type` unterschieden:

- `record_type = atomic_requirement`
- `record_type = data_collection`
