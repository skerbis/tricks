---
title: 'YForm Tablemanager: Hochgeladene Dateien schützen / Medienpool updaten'
authors:
  - pschuchmann
prio: null
---

# YForm Tablemanager: Hochgeladene Dateien schützen / Medienpool updaten

Mit dem EP `REX_YFORM_SAVED` lassen sich die aktuellen Daten eines Datensatzes auslesen. Möchte man nun zeitgleich Änderungen oder Anpassungen in einer anderen Tabelle ausführen, kann das mit dem folgenden Code erreicht werden. Ein möglicher Anwendungsfall:

* YForm Tabelle mit Medienfeldern
* YCom Media Auth Plugin zum Schutz der hochgeladenen Medien

Die Medien werden in der angelegten YForm Tabelle gespeichert. Aber um die Dateien zu schützen, müssen die zugehörigen Datensätze in der Tabelle `rex_media` angepasst werden.

## Extensionpoint 'REX\_YFORM\_SAVED' erweitern, entweder in der boot.php des project Addons oder im eigenen Addon

```php
rex_extension::register('REX_YFORM_SAVED', ['klasse', 'methode'], rex_extension::LATE);
```

## Methode deklarieren

```php
class klasse {
    public function methode($ep) {

    //Tabellenname aus $ep holen
    $table = $ep->getParam('table');

    //Code nur ausführen für festgelegte yform_tabelle
    if ($table == rex::getTable('yform_tabelle')) {

      //Id und Datensatz holen
      $id = $ep->getParam('id');
      $dataset = rex_yform_manager_dataset::get($id, $table)->getData();

      //Beispiel für angelegte Medienfelder in yform_tabelle
      $media_files   = [];
      $media_files[] = $dataset['media'];
      $media_files[] = $dataset['media_web_1'];
      $media_files[] = $dataset['media_web_2'];
      $media_files[] = $dataset['media_web_3'];
      $media_files[] = $dataset['media_web_4'];
      $media_files = array_filter($media_files);

      //Update auf rex_media Tabelle. Um die Medien zu betrachten zu können, muss der Nutzer eingeloggt sein und wenigstens einer Gruppe zugehörig sein mit Id 1 und/oder 2.
      foreach ($media_files as $media_file) {
        $sql = rex_sql::factory();
        $sql = $sql->setDebug(false);
        $sql = $sql->setTable(rex::getTable('media'));
        $sql = $sql->setWhere(['filename' => $media_file]);
        $sql = $sql->setValues(['ycom_auth_type' => '1']);
        $sql = $sql->setValues(['ycom_group_type' => '2']);
        $sql = $sql->setValues(['ycom_groups' => '1,2']);
        $sql->update();

        //Generiere Cache Datei für das Medium
        rex_media_cache::generate($media_file);
      }

    }

    return;

    }
}
```

