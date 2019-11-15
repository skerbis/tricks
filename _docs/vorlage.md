---
title: Seitenüberschrift
authors: []
prio: null
---

# Seitenüberschrift

* [Kopfbereich](vorlage.md#kopfbereich)
* [Überschriften](vorlage.md#ueberschriften)
* [Links](vorlage.md#links)
* [Bilder](vorlage.md#bilder)
* [Listen](vorlage.md#listen)
* [Tabellen](vorlage.md#tabellen)
* [Code](vorlage.md#code)
* [Hinweise](vorlage.md#hinweise)
* [Anker 3](vorlage.md#anker-3)
  * [Anker 3a](vorlage.md#anker-3a)
  * [Anker 3b](vorlage.md#anker-3b)
  * [Anker 3c](vorlage.md#anker-3c)
* [Anker 4](vorlage.md#anker-4)

## Kopfbereich

1. Seitenüberschrift als h1 auszeichnen
2. TOC Liste mit Anker erstellen, Die erste Ebene wird im Text mit `h2` die zweite Ebene mit `h3` ausgezeichnet

**Beispiel**

```text
# Seitenüberschrift

- [Überschrift](#anker-zur-ueberschrift)
- [Anker 2](#anker-2)
    - [Anker 2a](#anker2a)
- [Anker 3](#anker-3)
    - [Anker 3a](#anker-3a)
    - [Anker 3b](#anker-3b)
    - [Anker 3c](#anker-3c)
- [Anker 4](#anker-4)
```

## Überschriften mit Anker setzen

**Beispiel**

```text
<a name="anker-zur-ueberschrift"></a>
## Überschrift
```

## Links

Links bitte immer mit Beschreibung angeben

**Beispiel**

```text
[REDAXO Loader - REDAXO laden und entpacken](install_redaxo_loader.md)
```

## Bilder

Bilder bitte im Ordner `/screenshots` hinterlegen. Damit sie danach sowohl auf der Tricks-Website als auch in der Artikelansicht auf GitHub funktionieren, müssen sie mit absoluter URL referenziert werden. Die Basis-URL dafür lautet **`https://raw.githubusercontent.com/FriendsOfREDAXO/tricks/master/screenshots/`**, und ein Bild würdest du etwa so referenzieren:

```text
![Bild 1](https://raw.githubusercontent.com/FriendsOfREDAXO/tricks/master/screenshots/bild1.jpg "Bild 1")
```

## Listen

**Beispiel**

* Listenpunkt 1
* Listenpunkt 2
* Listenpunkt 3
* Listenpunkt 4

## Tabellen

**Beispiel**

```text
Alt                   | Neu
--------------------- | -----------------------
`$REX['SERVERNAME']`  |  `rex::getServername()`
```

## Code

```text
Zur Code-Auszeichnung bitte ``` verwenden
```

**Beispiel Code Block**

```php
<?php
$article = rex_article::get();
```

**Beispiel Code Inline**

Code innerhalb eines Text wird `ganz normal` ausgezeichnet

## Hinweise

Hinweise werden später blau unterlegt.

> **Hinweis:** Zweitens: ich habe erklärt mit diese zwei Spieler: nach Dortmund brauchen vielleicht Halbzeit Pause. Ich habe auch andere Mannschaften gesehen in Europa nach diese Mittwoch. Ich habe gesehen auch zwei Tage die Training.
>
> **Hinweis:** Zweitens: ich habe erklärt mit diese zwei Spieler: nach Dortmund brauchen vielleicht Halbzeit Pause. Ich habe auch andere Mannschaften gesehen in Europa nach diese Mittwoch. Ich habe gesehen auch zwei Tage die Training.

