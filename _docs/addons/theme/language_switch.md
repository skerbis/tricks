---
title: Language Switcher
authors: []
prio: null
---

# Theme AddOn - Language Switcher

> Benötigt das [Theme Addon](https://github.com/FriendsOfREDAXO/theme)

* [Was macht es?](language_switch.md#was-macht-es)
* [Die Funktion](language_switch.md#die-funktion)
* [Einbinden in Theme](language_switch.md#einbinden-in-theme)
* [Ausgabe im Template](language_switch.md#ausgabe-im-template)
* [Theme Debug Module](language_switch.md#theme-debug-module)

## Was macht es?

Eine kleine Funktion um die Sprachen im Frontend als stylebare Liste auszugeben.

## Die Funktion

Lege eine Datei namens `clang_switch.php` im [Theme Addon](https://github.com/FriendsOfREDAXO/theme) im Ordner `theme/private/inc/frontend` an.

**Inhalt der Datei**

```php
<?php
/* ----- Language Switch -----
$showCurLang : true / false - if the current language shall be displayed
$wrappingList: true / false - adds wrapping ul with extra css if given
$countryCode : true / false - Shows Country Code as Name
$css_extra   : adds extra css classes
   ----- Language Switch ----- */

if(!function_exists("getLangNav"))
{
    function getLangNav($showCurLang = true, $wrappingList = true, $countryCode = true, $css_extra = '')
    {
        $langOutput = '';

        $langOutput  .= ($wrappingList ? '<ul class="lang--nav '.$css_extra.'">' : '');
        foreach(rex_clang::getAll() as $lang) {
            if(rex_clang::getCurrentId() == $lang->getId()) {
                if($showCurLang) {
                    $langOutput .= '<li class="lang--item lang--item__active lang--'.$lang->getCode().'">'.($countryCode ? $lang->getCode() : $lang->getName()).'</li>';
                }
            }
            else {
                if($lang->isOnline() && rex_article::getCurrent($lang->getId())->isOnline()) {
                    $langOutput .= '<li class="lang--item lang--item__inactive lang--'.$lang->getCode().'"><a title="'.$lang->getName().'" href="'.rex_getUrl('',$lang->getId()).'">'.($countryCode ? $lang->getCode() : $lang->getName()).'</a></li>';
                }
            }
        }
        $langOutput .= ($wrappingList ? '</ul>' : '');
        //return languagelist
        return $langOutput;
    }
}
```

## Einbinden in Theme

Anschließend wird die Datei `clang_switch.php` in die `functions.php` im Ordner `theme/private/inc`ein.

**z.B so:**

```php
<?php

if (!rex::isBackend()) {
    // Frontend 

    include('frontend/clang_switch.php');

} else {
    // Backend 

    //get REDAXO config file
    $configFile = rex_path::coreData('config.yml');
    $config = rex_file::getConfig($configFile);

    if (isset($config['debug']) && $config['debug'] === true) {
        // Optional Debug Module Function - Infos: https://github.com/FriendsOfREDAXO/tricks/blob/master/theme_debug_module.md
        //include('backend/debug_module.php');
    }
}
```

## Ausgabe im Template

Jetzt kann die Ausgabe der Funktion an beliebiger Stelle im Template ausgegeben werden.

```php
<?php

echo getLangNav(true, true, true, 'my--class');
```

## Theme Debug Module

Eine kleine Funktion um die Inhalte der REX\_VALUES auszugeben. Vor allem hilfreich beim Einsatz von [mform](https://github.com/FriendsOfREDAXO/mform) und [mblock](https://github.com/FriendsOfREDAXO/mblock). Zur Anleitung: [Theme Debug Module](https://github.com/FriendsOfREDAXO/tricks/blob/master/theme_debug_module.md)

