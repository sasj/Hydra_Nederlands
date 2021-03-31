## Operatoren

Functies voor het uitvoeren van bewerkingen op bronnen.

- [toevoegen - add](#toevoegen---add)
- [mengen - blend](#mengen---blend)
- [verschil - diff](#verschil---diff)
- [laag - layer](#laag---layer)
- [maskeren - mask](#maskeren---mask)
- [vermenigvuldigen - mult](#vermenigvuldigen---mult)

### toevoegen - add

`.add( textuur, Hoeveelheid )`

* `textuur`
  * `kleur`
  * `src`
  * `shape`
* `Hoeveelheid` :: float (standaardwaarde `0.5`)

Voeg texturen toe.

#### Voorbeeld

```javascript
shape()
.scale(0.5)
.add(shape(4),[0,0.25,0.5,0.75,1])
.out()

osc(9,0.1,1)
.add(osc(13,0.5,5))
.out()
```

### mengen - blend

`.blend( textuur, Hoeveelheid )`

* `textuur`
  * `kleur`
  * `src`
  * `shape`
* `Hoeveelheid` :: float (standaardwaarde `0.5`)

Meng texturen.

#### Voorbeeld

```javascript
shape()
.scale(0.5)
.blend(shape(4),[0,0.25,0.5,0.75,1])
.out()

osc(9,0.1,1)
.blend(osc(13,0.5,5))
.out()
```

### verschil - diff

`.diff( textuur )`

* `textuur`
  * `kleur`
  * `src`
  * `shape`

Geeft het verschil van de textuur terug.

#### Voorbeeld

```javascript
osc(9,0.1,1)
  .diff(osc(13,0.5,5))
  .out()

osc(1,1,2)
  .diff(shape(6,1.1,0.01)
        .scale(({time})=>Math.sin(time)*0.05 + 0.9)
        .kaleid(15)
        .rotate(({time})=>time%360))
  .out()
```

### laag - layer

`.layer( textuur )`

* `textuur`
  * `kleur`
  * `src`
  * `shape`

Overlap textuur gebaseerd op alpha waarde

#### Voorbeeld

```javascript
solid(1,0,0,1)
.layer(shape(4)
.kleur(0,1,0,({time})=>Math.sin(time*2)))
.out()
```

### maskeren - mask

`.mask( textuur, herhalingen, offset )`

* `textuur`
  * `kleur`
  * `src`
  * `shape`
* `herhalingen` :: float (standaardwaarde `3.0`)
* `offset` :: float (standaardwaarde `0.5`)

#### Voorbeeld

```javascript
// standaardwaarde
gradient(5).mask(voronoi(),3,0.5).invert([0,1]).out()

// algae pulse
osc(10,-0.25,1).kleur(0,0,1).saturate(2).kaleid(50)
  .mask(noise(25,2).modulateScale(noise(0.25,0.05)))
  .modulateScale(osc(6,-0.5,2).kaleid(50))
  .mult(osc(3,-0.25,2).kaleid(50))
  .scale(0.5,0.5,0.75)
  .out()
```

### vermenigvuldigen - mult

`.mult( textuur, Hoeveelheid )`

* `textuur`
  * `kleur` :: see [kleur `vec4`](#kleur-vec4)
  * `src` :: see [`src`](#src)
  * `shape` :: see [`shape`](#shape)
* `Hoeveelheid` :: float (standaardwaarde `1.0`)

Vermenigvuldig en vervaag textuur met de `Hoeveelheid`.

#### Voorbeeld

```javascript
osc(9,0.1,2)
.mult(osc(13,0.5,5))
.out()
```
