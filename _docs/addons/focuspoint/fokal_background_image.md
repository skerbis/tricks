---
title: Hintergrundbild mit Focuspoint
authors:
  - marcohanke
  - skerbis
  - christophboecker
prio: null
---

# Hintergrundbild mit Focuspoint

> _Hinweis:_ Das Hintergrundbild darf NICHT mit dem MediaManager-Effekt `Fokuspoint` beschnitten werden, es sollte höchstens auf die entsprechende Maximalgröße skaliert werden. Voraussetzung: Installiertes Focuspoint-AddOn und im Medienpool hinterlegte Koordinaten.

Mit folgendem Code kann man ein Bild als Hintergrundbild einbinden, wobei der Fokuspoint aus dem Medienpool berücksichtigt wird. Somit ist unabhängig vom Browserfenster immer der gewünschte Ausschnitt zu sehen.

```php
<?php
$style = '';

//Abfrage ob Medium vorhanden
if ('REX_MEDIA[id=1]' != '') {
    $file_name = 'REX_MEDIA[id=1]';

    // Focuspoint-Werte auslesen und als Variablen $x und $y speichern
    // (Fallback auf `50% 50%` ist in `getFocus()` enthalten)
    list($x,$y) = focuspoint_media::get($file_name)->getFocus();

    // Inline-CSS-Ausgabe mit entsprechendem Medientyp und Focuspoint-Koordinaten
    $style = 'style="background-image: url(/mediatypes/1200/'.$file_name.'); background-size: cover; background-position:'.$x.'% '.$y.'%;';
}
```

```markup
<!-- Ausgabe des Styles innerhalb eines div -->
<div <?= $style ?>></div>
```

