---
title: Interne Linkliste mit REX_LINKLIST
authors: []
prio: null
---

# Interne Linkliste mit REX\_LINKLIST

* [Beschreibung](interne_linkliste.md#beschreibung)
* [Moduleingabe](interne_linkliste.md#moduleingabe)
* [Modulausgabe](interne_linkliste.md#modulausgabe)

## Beschreibung

Einzelne Artikel können durch den Redakteur ausgewählt werden und so als Liste ausgegeben werden. Das Modul erstellt ein Bootstrap-Panel mit einer Artikelliste.

## Moduleingabe

```markup
<fieldset class="form-horizontal">
    <div class="form-group">
        <label class="col-sm-2 control-label">Interne Links</label>
        <div class="col-sm-10">
            REX_LINKLIST[id="1" widget="1"]
        </div>
    </div>
</fieldset>
```

In der REX\_Linklist werden die Werte \(Artikel-IDs\) kommasepariert gespeichert.

## Modulausgabe

In der Modulausgabe werden die Werte mitels explode \([http://php.net/manual/de/function.explode.php](http://php.net/manual/de/function.explode.php)\) in einer foreach-Schleife ausgelesen. Anhand der ID holt man sich den Datensatz des Artikels. Wenn nur ein Link erzeugt werden soll, bietet sich die direkte Umwandlung des Datensatzes in einen Link mittels `->toLink()` an.

```php
<?php
if ("REX_LINKIST[1]" != "") {
  $menu = array();
  foreach(explode(',', 'REX_LINKLIST[1]') as $articleId) {

    // Artikeldatensatz auslesen
    $article = rex_article::get($articleId);
    if ($article) {

      // Erstelle Link aus aktuellem Artikel
      $menu[$articleId] = $article->toLink();
    }
  }

  // Ausgabe mit implode: http://php.net/manual/de/function.implode.php
  if (! empty($menu)) {
    echo '<ul><li>', implode('</li><li>', $menu), '</li></ul>';
  }
}
```

