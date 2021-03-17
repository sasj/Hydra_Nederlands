## Geometry

Functies voor het bewerken van de geometrie

- [kaleidoscoop - kaleid](#kaleid)
- [pixels - pixelate](#pixelate)
- [herhaal repeat](#repeat)
- [herhaal horizontaal - repeatX](#repeatX)
- [herhaal verticaal - repeatY](#repeatY)
- [draaien - rotate](#rotate)
- [schaal - scale](#scale)
- [verplaats horizontaal - scrollX](#scrollX)
- [verplaats verticaal - scrollY](#scrollY)

### kaleidoscoop - kaleid

`.kaleid( x vlakken )`

* `x vlakken` :: float (standaardwaarde `4.0`)

Kaleidoscoop effect met `x vlakken` herhaling.

#### Voorbeeld

```javascript
osc(25,-0.1,0.5)
.kaleid(50)
.out()
```

### pixels - pixelate

`.pixelate( x, y )`

* `pixelX` :: float (standaardwaarde `20.0`)
* `pixelY` :: float (standaardwaarde `20.0`)

Pixel textuur met `pixelX` delen horizontaal en `pixelY` delen verticaal.

#### Voorbeeld

```javascript
// standaardwaarde
osc(20,0.1,0.6)
.pixelate(20,20)
.out()
```

### herhaal - repeat

`.repeat( x herhalingX, x herhalingY, afstand X, afstand Y )`

* `herhaling X` :: float (standaardwaarde `3.0`)
* `herhaling Y` :: float (standaardwaarde `3.0`)
* `afstand X` :: float (standaardwaarde `0.0`)
* `afstand Y` :: float (standaardwaarde `0.0`)


#### Voorbeeld

```javascript
// standaardwaarde
osc(40,0.05,10)
.repeat(3.0, 3.0, 0.0, 0.0)
.out()
```


### repeatX

`.repeatX( x herhaling, afstand )`

* `x herhaling` :: float (standaardwaarde `3.0`)
* `afstand` :: float (standaardwaarde `0.0`)

#### Voorbeeld

```javascript
// standaardwaarde
osc(40,0.05,10)
.repeatX(3.0, 0.0)
.out()
```

```javascript
osc(5,0,1)
  .rotate(1.57)
  .repeatX([1,2,5,10], ({time}) => Math.sin(time))
  .out()
```

### Herhaling Y - repeatY

`.repeatY( herhaling, afstand )`

* `herhaling` :: float (standaardwaarde `3.0`)
* `afstand` :: float (standaardwaarde `0.0`)

#### Voorbeeld

```javascript
// standaardwaarde
osc(5,0,1)
.repeatY(3.0, 0.0)
.out()
```

```javascript
osc(5,0,1)
  .repeatY([1,2,5,10], ({time}) => Math.sin(time))
  .out()
```

### draaien - rotate

`.rotate( hoek, snelheid )`

* `hoek` :: float (standaardwaarde `10.0`)
* `snelheid` :: float (standaardwaarde `0.0`)

Draai het beeld

#### Voorbeeld

```javascript
osc(50)
.rotate( 1, 0.2 )
.out()
```


```javascript
osc(10,1,1)
    .rotate( ({time}) => time%360, ({time}) => Math.sin(time*0.1)*0.05 )
    .out()
```

### schaal - scale

`.scale( grootte, xMult, yMult )`

* `grootte` :: float (standaardwaarde `1.5`)
* `xMult` :: float (standaardwaarde `1.0`)
* `yMult` :: float (standaardwaarde `1.0`)

Schaal het beeld

#### Voorbeeld

```javascript
// standaardwaarde
osc(10,1,1)
.scale(1.5)
.out()
```

```javascript
shape(4)
.rotate(0.5,0.2)
.pixelate(30,40)
.scale(1.0,2.3,1.5)
.out()
```

### verplaats horizontaal scrollX

`.scrollX( verplaats X, snelheid )`

* `verplaats X` :: float (standaardwaarde `0.5`)
* `snelheid` :: float (standaardwaarde `0.0`)

#### Voorbeeld

```javascript
// standaardwaarde
osc(10,0,1)
.scrollX(0.5,0)
.out()
```
```javascript
// x position
osc(10,0,1)
  .scrollX([0,0.25,0.5,0.75,1])
  .out()
```
```javascript
// scroll speed
gradient(1)
  .scrollX(0, ({time}) => Math.sin(time*0.05)*0.05 )
  .out()
  ```
  ```javascript
gradient(0.125)
  .scrollX(0, ({time}) => Math.sin(time*0.05)*0.05 )
  .scrollY(0, ({time}) => Math.sin(time*0.01)*-0.07 )
  .pixelate([5,2,10],[15,8])
  .scale(0.15)
  .modulate(noise(1,0.25))
  .out()
```

### verplaats horizontaal - scrollY

`.scrollY( verplaats Y, snelheid )`

* `verplaats Y` :: float (standaardwaarde `0.5`)
* `snelheid` :: float (standaardwaarde `0.0`)

#### Voorbeeld

```javascript
// standaardwaarde
osc(10,0,1)
  .scrollY(0.5,0)
  .out()
```
```javascript
// y position
osc(10,0,1)
.scrollY([0,0.25,0.5,0.75,1]
  .fast(4),0)
  .out()
```
```javascript
// scroll speed
gradient(1)
.scrollY(0, ({time}) => Math.sin(time*0.05)*0.05 )
.out()
```

```javascript
gradient(0.125)
  .scrollX(0, ({time}) => Math.sin(time*0.05)*0.05 )
  .scrollY(0, ({time}) => Math.sin(time*0.01)*-0.07 )
  .pixelate([5,2,10],[15,8])
  .scale(0.15)
  .modulate(noise(1,0.25))
  .out()
```
