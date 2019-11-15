---
title: HTTP Status Codes 410 umsetzen
authors:
  - dtpop
prio: null
---

# HTTP Status Codes 410 umsetzen

* [Einleitung](errorcode_410.md#einleitung)
* [Problem](errorcode_410.md#problem)
* [htaccess](errorcode_410.md#htaccess)
* [Template](errorcode_410.md#template)
* [Hinweise](errorcode_410.md#hinweise)

## Einleitung

So, will auch mal hier meinen ersten Tipp rein schreiben. Ich war eine Zeit lang dran, deswegen muss ich mir jetzt mal eine Notiz dazu machen. Vielleicht kann es ja noch jemand brauchen. Würde mich freuen.

## Problem

Es sollen für verschiedene Seiten http Status Codes 410 übermittelt werden. yrewrite kann das nicht. Ich habe versucht yrewrite dazu zu bekommen, indem ich die Auswahl ergänzt habe. Das hat dann nicht funktioniert. Nächster Versuch, das ganze klassisch über die htaccess zu lösen hat auch nicht funktioniert, es wurde der Status Code nicht übertragen respektive überschrieben. Ein erster Erfolg hat sich eingestellt, indem ich die 410er Fehlerseite als statische html Seite abgelegt und definiert habe. Aber wer will das schon. Verschiedene Versuche in der boot.php über den Extensionpoint OUTPUT\_FILTER haben auch nicht zum Ziel geführt. Auch hier wurde der Status Code rigide neu gesetzt, ein 410er war nicht zu übertragen. So - Probleme haben wir alle genug, deswegen jetzt zur Lösung.

## htaccess

```text
ErrorDocument 410 /index.php?article_id=125 # ist ja klar, das Fehlerdokument muss definiert werden, als Artikel Id die Id des anzuzeigenden Artikels eintragen
```

Ich habe mich hier zur Url mit article\_id entschieden. Man könnte auch die schöne yrewrite url eintragen. Funktioniert aber nicht mehr, wenn einer auf die Idee kommt den Artikel umzubenennen.

Dann müssen die ganzen Weiterleitungen noch eingetragen werden.

```text
    Redirect 410 /alteurl/eins
    Redirect 410 /alteurl/zwei
```

## Template

Nun wird zwar die korrekte Fehlerseite angezeigt, aber leider nicht der richtige Status Code. Und jetzt haltet euch fest, jetzt kommt wirklich der ultimative Trick. Ans Ende vom Template kommt genau diese eine Zeile:

```php
<?php if (REX_ARTICLE_ID == 125) exit ?>
```

Die 125 ist natürlich durch die eigene 410er Fehlerseiten Id zu ersetzen.

## Hinweise

> **Hinweis:** Bitte selber gut testen. Das hier wurde mit Redaxo 5.5 umgesetzt. Möglicherweise gibt es in yrewrite mal eine Ergänzung und dieser Hack ist dann nicht mehr nötig.

