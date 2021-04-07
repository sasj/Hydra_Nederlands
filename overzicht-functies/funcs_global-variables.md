## Globale variabelen - Global variables

Handige variabelen die globaal zijn gedefinieerd en binnen functies als parameter kunnen worden gebruikt.

- [muis - mouse](#muis_-_mouse)
- [tijd - time](#tijd_-_time)

### muis - mouse

`mouse`

* `.x` :: x positie van de muis
* `.y` :: y positie van de muis

#### Voorbeeld

Regel de oscillatorfrequentie met de muispositie:

```javascript
osc(() => mouse.x)
.out()
```

### tijd - time

`time`

* `time` :: de huidige tijd

#### Voorbeeld

Bestuur de oscillator met behulp van een sinusgolf op basis van de huidige tijd:

```javascript
osc( ({time}) => Math.sin(time) )
.out()
```
