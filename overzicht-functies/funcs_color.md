## Kleur (Color)

Functies voor het bewerken van kleur

- [helderheid - brightness](#helderheid-(brightness))
- [contrast - contrast](#contrast)
- [kleur `vec4` - color `vec4`](#color-vec4)
- [colorama - colorama](#colorama)
- [omkeren - invert](#invert)
- [lichtintensiteit - luma](#luma)
- [waarden beperken - posterize](#posterize)
- [verzadiging - saturate](#saturate)
- [verschuiving - shift](#shift)
- [drempel - thresh](#thresh)

### helderheid (brightness)

`.brightness( hoeveelheid )`

* `hoeveelheid` :: float (standaardwaarde `0.4`)

#### Voorbeeld

```javascript
osc(20,0,2)
  .brightness( 0.3 )
  .out()
```

### contrast (contrast)

`.contrast( hoeveelheid )`

* `hoeveelheid` :: float (standaardwaarde `1.6`)

Een grotere`hoeveelheid` maaks een hoger contrast

#### Voorbeeld

```javascript
// 20Hz oscillator met contrastinterpolatie tussen 0,0-5,0
osc(20)
.contrast( ({time}) => Math.sin(time) * 5 )
.out()
```

### kleur `vec4` (color `vec4`)

`.color( r, g, b )`

* `r` :: float
* `g` :: float
* `b` :: float

Geef de textuur een kleur.

#### Voorbeeld

```javascript
// 20Hz oscillator bron
// kleurvolgorde van rood, groen, blauw, wit, zwart
// output naar buffer o0
osc(20)
.color([1,0,0,1,0],[0,1,0,1,0],[0,0,1,1,0])
.out()
```

### colorama (colorama)

`.colorama( hoeveelheid )`

* `hoeveelheid` :: float (standaardwaarde `0.005`)

Verschuift HSV waardes.

#### Voorbeeld

```javascript
// 20Hz oscillator bron
// kleur reeks in Rood, Groen, Blauw, Wit, Zwart
// colorama reeks van 0.005, 0.5, 1.0 met 1/8 snelheid
osc(20)
  .color([1,0,0,1,0],[0,1,0,1,0],[0,0,1,1,0])
  .colorama([0.005,0.33,0.66,1.0].fast(0.125))
  .out()
```

```javascript
//
noise(3,0.1)
.colorama( ({time}) => Math.sin(time/5) )
.out()
```

### omkeren - invert

`.invert( hoeveelheid )`

* `hoeveelheid` :: float (standaardwaarde `1.0`)

Kleur omkeren.

#### Voorbeeld

```javascript
// kleur zal omgekeerd worden wanneer het 0 is.
solid(1,1,1)
.invert([0,1])
.out(o0)
```

### lichtintensiteit (luma)

`.luma( drempel, tolerantie )`

* `drempel` :: float (standaardwaarde `0.5`)
* `tolerantie` :: float (standaardwaarde `0.1`)

#### Voorbeeld

```javascript
// standaardwaarde
osc(10,0,1)
.luma(0.5,0.1)
.out()
```

```javascript
osc(10,0,[0,0.5,1,2])
.luma([0.1,0.25,0.75,1].fast(0.25),0.1)
.out()
```

### waarde beperken - posterize

`.posterize( bins, gamma )`

* `bins` :: float (standaardwaarde `3.0`)
* `gamma` :: float (standaardwaarde `0.6`)

#### Voorbeeld

```javascript
gradient(0)
.posterize( [1, 5, 15, 30] , 0.5 )
.out()
```

### verzadeging - saturate

`.saturate( hoeveelheid )`

* `hoeveelheid` :: float (standaardwaarde `2.0`)

#### Voorbeeld

```javascript
osc(10,0,1)
.saturate( ({time}) => Math.sin(time) * 10 )
.out()
```

### verschuiving (shift)

`.shift( r, g, b, a )`

* `r` :: float (standaardwaarde `0.5`)
* `g` :: float (standaardwaarde `0.5`)
* `b` :: float (standaardwaarde `0.5`)
* `a` :: float (standaardwaarde `0.5`)

#### Voorbeeld

```javascript

```

### thresh

`.thresh( drempel, tolerantie )`

* `drempel` :: float (standaardwaarde `0.5`)
* `tolerantie` :: float (standaardwaarde `0.04`)

#### Voorbeeld

```javascript
// standaardwaarde
noise(3,0.1)
.thresh(0.5,0.04)
.out(o0)
```

```javascript
noise(3,0.1)
  .thresh( ({time})=>Math.sin(time/2) , [0.04,0.25,0.75,1].fast(0.25) )
  .out(o0)
```
