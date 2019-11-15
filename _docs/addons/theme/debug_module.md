---
title: 'Function debug_module($value, ''String'')'
authors:
  - elricco
  - marcohanke
prio: null
---

# Theme AddOn - Function debug\_module\($value, 'String'\)

> Benötigt das [Theme Addon](https://github.com/FriendsOfREDAXO/theme)

* [Was macht es?](debug_module.md#was-macht-es)
* [Die Funktion](debug_module.md#die-funktion)
* [Einbinden in Theme](debug_module.md#einbinden-in-theme)
* [Ausgabe im Modul](debug_module.md#ausgabe-im-modul)
* [Theme Language Switch](debug_module.md#theme-language-switch)

## Was macht es?

Eine kleine Funktion um die Inhalte der REX\_VALUES auszugeben. Vor allem hilfreich beim Einsatz von [mform](https://github.com/FriendsOfREDAXO/mform) und [mblock](https://github.com/FriendsOfREDAXO/mblock). Die Funktion gibt entweder ein `dump($value)` oder `print_r($value)` bei Core Version &lt; 5.3.0 aus.

## Die Funktion

Lege eine Datei namens `debug_module.php` im [Theme Addon](https://github.com/FriendsOfREDAXO/theme) im Ordner `theme/private/inc/backend` an.

**Inhalt der Datei**

```php
<?php
if(!function_exists("debug_module"))
{
    function debug_module($value,$label = 'VALUE')
    {
        //get core version
        $coreVersion = rex_config::get('core', 'version');
        //build debug
        if ($coreVersion < '5.3.0') {
            //return debug
            echo '<h6>'.$label.'</h6>'.
                '<pre>' .
                print_r($value,1) .
                '</pre>';
        } else {
            //return debug
            echo '<h6>'.$label.'</h6>';
                dump($value);
        }
    }
}
```

## Einbinden in Theme

Anschließend wird die Datei `debug_module.php` in die `functions.php` im Ordner `theme/private/inc`ein.

**z.B so:**

```php
<?php

if (!rex::isBackend()) {
    // Frontend

    // Optional language switch - Infos: https://friendsofredaxo.github.io/tricks/addons/theme/language_switch
    //include('frontend/clang_switch.php');

} else {
    // Backend

    //get REDAXO config file
    $configFile = rex_path::coreData('config.yml');
    $config = rex_file::getConfig($configFile);

    //when debug is set and true, include function(s)
    if (isset($config['debug']) && $config['debug'] === true) {
        include('backend/debug_module.php');
    }
}
```

## Ausgabe im Modul

Und nun kann -immer wenn der Haken bei `Debug-Modus` unter `System` drin ist- die Ausgabe im Backend des Moduls ein und ausgeschaltet werden. Ausgegeben wird es im Modul dann z.B.:

```php
<?php

//get config from mform
$owlConfiguration = rex_var::toArray("REX_VALUE[20]");

//fetch items from mform
$items = rex_var::toArray("REX_VALUE[1]");

//when function is present
if(function_exists('debug_module')) {
    //show debug module output
    debug_module($items);
    debug_module($owlConfiguration, 'Configuration');
    debug_module("REX_VALUE[5]", 'REX_VALUE 5');
}
```

## Theme Language Switch \(optional\)

Ein Sprachschalter, den man in im Frontend an beliebiger Stelle einbinden kann: [Theme Language Switch](https://friendsofredaxo.github.io/tricks/addons/theme/language_switch)

