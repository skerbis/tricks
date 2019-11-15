---
title: Kategorie einer REDAXO Instanz (Quelle) in eine andere Instanz (Ziel) kopieren
authors:
  - tbaddade
prio: null
---

# Kategorie einer REDAXO Instanz \(Quelle\) in eine andere Instanz \(Ziel\) kopieren

## Voraussetzung

* Sequel Pro 

## Vorbereitung

* Backup der Ziel-DB erstellen
* Dump aus der Quell-DB holen und in Sequel Pro in separater DB einspielen
* Datenbankverbindung zu der Ziel-DB aufbauen
* Module und Templates wurden manuell kopiert und die Id per Hand in der Ziel-DB neu gesetzt

## Und los

### Alle Artikel einer bestimmten Kategorie holen

```sql
SELECT *
FROM rex_article
WHERE id = "11322" OR path LIKE "|11322|%"
```

1. Ergebnis als CSV exportieren
2. Wechsel in die Ziel-DB 
3. Tabelle rex\_article auswählen
4. Ablage - Importieren
5. CSV-Datei importieren
6. Spalten überprüfen und ggf. welche ignorieren
7. Import starten

### Alle Slices einer bestimmten Kategorie holen

```sql
SELECT s.*
FROM rex_article_slice AS s 
    LEFT JOIN rex_article AS a 
        ON s.article_id = a.id
WHERE a.id = "11322" 
    OR  a.path LIKE "|11322|%"
```

1. Ergebnis als CSV exportieren
2. Wechsel in die Ziel-DB 
3. Tabelle rex\_article\_slice auswählen
4. Ablage - Importieren
5. CSV-Datei importieren
6. Spalten überprüfen und ggf. welche ignorieren
7. Import starten

### Alle verwendeten Medien holen

1. nachstehendes Skript als Modul anlegen und die Root-Id anpassen
2. Artikel anlegen und das Modul wählen
3. Zeit mitbringen, kann dauern
4. Es werden jetzt alle verwendete Medien in den Ordner "/media\_export" kopiert \(liegt im root neben medie bzw. redaxo\)
5. den ausgegebenen Query kopieren und in Sequel Pro der Quell-DB absetzen
6. Ergebnis exportieren
7. Wechsel in die Ziel-DB und CSV-Datei auswählen, Einstellungen setzen und den Button "öffnen" klicken
8. Hier die category\_id entweder lassen oder manuell einen Wert eintragen \(alle Import-Dateien könnten in einer separaten Kategorie gespeichert werden\)
9. Falls die Kategorie-Id nicht angepasst wird, müssten auch die Medienkaegorien exportiert werden.

```php
<?php
$rootId = 11322;

/**
 * @param $filename
 * @param $rootId
 *
 * @return bool|string
 */
function mediaIsInUse($filename, $rootId = 0)
{
    $sql = rex_sql::factory();

    // FIXME move structure stuff into structure addon
    $values = [];
    for ($i = 1; $i < 21; ++$i) {
        $values[] = 'value' . $i . ' REGEXP ' . $sql->escape('(^|[^[:alnum:]+_-])'.$filename);
    }

    $files = [];
    $filelists = [];
    $escapedFilename = $sql->escape($filename);
    for ($i = 1; $i < 11; ++$i) {
        $files[] = 'media' . $i . ' = ' . $escapedFilename;
        $filelists[] = 'FIND_IN_SET(' . $escapedFilename . ', medialist' . $i . ')';
    }

    $where = '';
    $where .= implode(' OR ', $files) . ' OR ';
    $where .= implode(' OR ', $filelists) . ' OR ';
    $where .= implode(' OR ', $values);

    $from = '';
    if ($rootId > 0) {
        $from = 'LEFT JOIN ' . rex::getTablePrefix() . 'article AS a ON s.article_id = a.id ';
        $where = '(a.id = "' . $rootId . '" OR a.path LIKE "|' . $rootId . '|%") AND (' . $where . ')';
    }

    $query = '
    SELECT DISTINCT 
        s.article_id, 
        s.clang_id 
    FROM ' . rex::getTablePrefix() . 'article_slice AS s ' . $from . '
    WHERE ' . $where;

    $warning = [];
    $res = $sql->getArray($query);
    if ($sql->getRows() > 0) {
        return true;
    }

    return false;
}

$files = [];
$query = 'SELECT * FROM ' . rex::getTablePrefix() . 'media';

$sql = rex_sql::factory();
$items = $sql->getArray($query);
if (count($items)) {
    foreach ($items as $item) {
        $filename = $item['filename'];
        if (mediaIsInUse($filename, $rootId)) {
            $files[] = $filename;
        }
    }
}

if (count($files)) {
    $where = [];
    foreach ($files as $file) {
        $where[] = 'filename = "' . $file . '"';
        rex_file::copy(rex_path::frontend() . 'media/' . $file, rex_path::frontend() . 'media_export/' . $file);
    }

    $query = 'SELECT * FROM ' . rex::getTablePrefix() . 'media WHERE ' . implode(' OR ', $where);
    echo '<pre>' . $query . '</pre>';
}
```

