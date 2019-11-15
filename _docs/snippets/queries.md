---
title: Queries
authors:
  - tbaddade
prio: null
---

# Queries

* [Paginierung auf alphabetisch basierende Datensätze](queries.md#paginierung-abc)
  * [vorheriger Datensatz](queries.md#paginierung-abc-vorheriger-datensatz)
  * [nächster Datensatz](queries.md#paginierung-abc-naechster-datensatz)
* [Paginierung auf Datum basierende Datensätze](queries.md#paginierung-datum)
  * [vorheriger Datensatz](queries.md#paginierung-datum-vorheriger-datensatz)
  * [nächster Datensatz](queries.md#paginierung-datum-naechster-datensatz)
* [Query inkl. einer "Bitte auswählen" Option](queries.md#option-please-select)

## Blättern auf alphabetisch basierende Datensätze

Die Methoden basieren auf Yorm und gehören in eine Class wie zum Beispiel

```php
class Project extends rex_yform_manager_dataset
{
}
```

### vorherigen Datensatz holen

```php
public function getPrevious()
{
    $query = self::query()
        ->where('status', '1')
        ->where(sprogfield('title'), $this->getTitle(), '<')
        ->orderBy(sprogfield('title'), 'DESC');
    return $query->findOne();
}
```

### nächsten Datensatz holen

```php
public function getNext()
{
    $query = self::query()
        ->where('status', '1')
        ->where(sprogfield('title'), $this->getTitle(), '>')
        ->orderBy(sprogfield('title'), 'ASC');
    return $query->findOne();
}
```

## Blättern auf Datum basierende Datensätze zu erstellen \(News\)

Die Methoden basieren auf Yorm und gehören in eine Class wie zum Beispiel

```php
class News extends rex_yform_manager_dataset
{
}
```

Die Queries lassen sich aber auch sehr einfach für eine normale DB-Abfrage adaptieren.

### vorherigen Datensatz holen

```php
public function getPrevious()
{
    $query = self::query()
        ->where('status', '1')
        ->whereRaw('id != :id and (date > :date or date = :date and id > :id)',
            ['id' => $this->id, 'date' => $this->date])
        ->orderBy('date', 'ASC')
        ->orderBy('id', 'ASC');
    return $query->findOne();
}
```

### nächsten Datensatz holen

```php
public function getNext()
{
    $query = self::query()
        ->where('status', '1')
        ->whereRaw('id != :id and (date < :date or date = :date and id < :id)',
            ['id' => $this->id, 'date' => $this->date])
        ->orderBy('date', 'DESC')
        ->orderBy('id', 'DESC');
    return $query->findOne();
}
```

## Query inkl. einer "Bitte auswählen" Option

Nützlich bei `select`-Feldtypen im **MetaInfo** AddOn oder im **YFormbuilder**

```php
SELECT name, filename AS id FROM rex_project_icon UNION SELECT ' Bitte wählen' AS name, "" AS id ORDER BY name
```

### Beispielausgabe in der Sidebar eines Artikels

```markup
<select name="art_icon" size="1" class="form-control" id="rex-metainfo-art_icon">
    <option value=""> Bitte wählen</option>
    <option value="file_a">A</option>
    <option value="file_b">B</option>
</select>
```

> Hinweis: `select` via **MetaInfo** erstellt

