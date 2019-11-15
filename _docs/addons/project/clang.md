---
title: Tipps für Sprachen in REDAXO
authors: []
prio: null
---

# Tipps für Sprachen in REDAXO

## Datum in korrekter Sprache ausgeben

**Szenario**

Die REDAXO-Website verfügt über verschiedene Sprachen. Ein Datum ist im MYSQL-Format hinterlegt und soll in Abhängigkeit der Sprache korrekt formatiert ausgegeben werden.

**Lösung**

`setlocale()` in PHP mit Sprach-Metainfos setzen.

**Schritt-für-Schritt-Anleitung**

Die Funktion `setlocale()` benötigt eine Kombination aus `Language Code` und `Country Code`.

1. Im Addon **Meta Infos** unter **Sprachen** ein neues Feld `clang_country` einfügen:

   ```yaml
      Spaltenname: country
      Feldbezeichnung: Country Code (ISO 3166)
      Feldtyp: Text
      Feldattribut (optional): pattern="[A-Z]{2}"
   ```

2. In **System** unter Sprachen die gewünschten Sprachen anlegen und dabei in den Feldern **Code** \(für `Language Code`\) und **Country Code** den korrekten Sprach- und Region-Codes eintragen, z.B. `de` und `DE`, `de` und `AT`, `en` und `GB` oder `en` und `US`.

   _Eine vollständige Liste an korrekten Country-Codes gibt es auf oracle.com:_ [_Language Codes_](https://docs.oracle.com/cd/E13214_01/wli/docs92/xref/xqisocodes.html#wp1252447) _und_ [_Country Codes_](https://docs.oracle.com/cd/E13214_01/wli/docs92/xref/xqisocodes.html#wp1250799)

3. Im **project-Addon** in der `boot.php` folgenden Code einfügen:

   ```php
      $clang = rex_clang::getCurrent();
      setlocale(LC_TIME, $clang->getCode()."_".$clang->getValue('country').".utf8");
   ```

4. Nun ist der aktuelle Sprachcode überal gesetzt und ein Datum kann ganz einfach mit `strftime()` formatiert werden, z. B.

   ```php
      strftime('%d. %B %Y', strtotime($event['date_begin'])) // Ergibt 03. Februar 2013
   ```

