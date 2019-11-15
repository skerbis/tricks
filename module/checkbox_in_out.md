---
title: Checkbox im Modul
authors: []
prio: null
---

# Checkbox im Modul

## Input

```markup
<input type="hidden" name="REX_INPUT_VALUE[1]" value="0">
<input type="checkbox" name="REX_INPUT_VALUE[1]" value="1" REX_VALUE[id=1 instead=checked]>
```

## Output

```php
<?php 
if(REX_VALUE[1])
    {
      echo "checked...";
```

