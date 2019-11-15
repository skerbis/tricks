---
title: Hilfsfunktionen
authors: []
prio: null
---

# Hilfsfunktionen

In REDAXO sind zahlreiche Hilfsfunktionen enthalten, mit denen man in Modulen, Templates, AddOns etc. arbeiten kann.

## rex\_markdown

So kann ein Markdown-Text geparst werden. Die Funktion `parse` ist nicht statisch.

```php
echo rex_markdown::factory()->parse($text)
```

## rex\_addon und rex\_config

Wenn man weiß, dass ein Array in einem `rex_addon`- oder `rex_config`-Wert existiert, kann man dieses auch direkt abfragen, z. B. so in der Art:

```php
rex_addon::get('addonname')->getProperty('arrayroot')['key']['subkey']

rex_config::get('key')->getProperty('arrayroot')['key']['subkey']
```

