## Modulators

Functies voor modulaties.

- [modulate](#modulate)
- [modulateHue](#modulateHue)
- [modulateKaleid](#modulateKaleid)
- [modulatePixelate](#modulatePixelate)
- [modulateRepeat](#modulateRepeat)
- [modulateRepeatX](#modulateRepeatX)
- [modulateRepeatY](#modulateRepeatY)
- [modulateRotate](#modulateRotate)
- [modulateScale](#modulateScale)
- [modulateScrollX](#modulateScrollX)
- [modulateScrollY](#modulateScrollY)

### modulate

`.modulate( textuur, hoeveelheid )`

* `textuur`
  * `color` :: see [color `vec4`](#color-vec4)
  * `src` :: see [`src`](#src)
  * `shape` :: see [`shape`](#shape)
* `hoeveelheid` :: float (default `0.1`)

Modulate textuur.
Meer informatie over modulatie op: https://lumen-app.com/guide/modulation/

#### voorbeeld

```javascript
// chocolate whirlpool
voronoi()
  .color(0.9,0.25,0.15)
  .rotate( ({time})=>(time%360)/2 )
  .modulate(osc(25,0.1,0.5)
            .kaleid(50)
            .scale(({time})=>Math.sin(time*1)*0.5+1)
            .modulate(noise(0.6,0.5)),
            0.5)
  .out(o0)
```

### modulateHue

`.modulateHue( color, hoeveelheid )`

* `textuur`
  * `color` :: see [color `vec4`](#color-vec4)
  * `src` :: see [`src`](#src)
  * `shape` :: see [`shape`](#shape)
* `hoeveelheid` :: float (default `1.0`)

Wijzigt de coördinaten op basis van de tint van de tweede invoer.
Gebaseerd op: https://www.shadertoy.com/view/XtcSWM

#### voorbeeld

```javascript

```

### modulateKaleid

`.modulateKaleid( textuur )`

* `textuur`
  * `color` :: see [color `vec4`](#color-vec4)
  * `src` :: see [`src`](#src)
  * `shape` :: see [`shape`](#shape)


#### voorbeeld

```javascript
osc(9,-0.1,0.1)
  .modulateKaleid(osc(11,0.5,0),50)
  .scale(0.1,0.3)
  .modulate(noise(5,0.1))
  .mult(solid(1,1,0.3))
  .out(o0)
```

### modulatePixelate

`.modulatePixelate( multiple, offset )`

* `textuur`
  * `color` :: see [color `vec4`](#color-vec4)
  * `src` :: see [`src`](#src)
  * `shape` :: see [`shape`](#shape)
* `multiple` :: float (default `10.0`)
* `offset` :: float (default `3.0`)


#### voorbeeld

```javascript
// what lies beneath
voronoi(10,1,5).brightness(()=>Math.random()*0.15)
  .modulatePixelate(noise(25,0.5),100)
  .out(o0)
```

### modulateRepeat

`.modulateRepeat( textuur, repeatX, repeatY, offsetX, offsetY )`

* `textuur`
  * `color` :: see [color `vec4`](#color-vec4)
  * `src` :: see [`src`](#src)
  * `shape` :: see [`shape`](#shape)
* `repeatX` :: float (default `3.0`)
* `repeatY` :: float (default `3.0`)
* `offsetX` :: float (default `0.5`)
* `offsetY` :: float (default `0.5`)

#### voorbeeld

```javascript
shape(4,0.9)
  .mult(osc(3,0.5,1))
  .modulateRepeat(osc(10), 3.0, 3.0, 0.5, 0.5)
  .out(o0)
```

### modulateRepeatX

`.modulateRepeatX( textuur, reps, offset )`

* `textuur`
  * `color` :: see [color `vec4`](#color-vec4)
  * `src` :: see [`src`](#src)
  * `shape` :: see [`shape`](#shape)
* `reps` :: float (default `3.0`)
* `offset` :: float (default `0.5`)

#### voorbeeld

```javascript
// straight lines illusion
shape(4,0.9)
  .mult(osc(4,0.25,1))
  .modulateRepeatX(osc(10), 5.0, ({time}) => Math.sin(time) * 5)
  .scale(1,0.5,0.05)
  .out(o0)
```

### modulateRepeatY

`.modulateRepeatY( textuur, reps, offset )`

* `textuur`
  * `color` :: see [color `vec4`](#color-vec4)
  * `src` :: see [`src`](#src)
  * `shape` :: see [`shape`](#shape)
* `reps` :: float (default `3.0`)
* `offset` :: float (default `0.5`)

#### voorbeeld

```javascript
// morphing grid
shape(4,0.9)
  .mult(osc(4,0.25,1))
  .modulateRepeatY(osc(10), 5.0, ({time}) => Math.sin(time) * 5)
  .scale(1,0.5,0.05)
  .out(o0)
```

### modulateRotate

`.modulateRotate( textuur, multiple, offset )`

* `textuur`
  * `color` :: see [color `vec4`](#color-vec4)
  * `src` :: see [`src`](#src)
  * `shape` :: see [`shape`](#shape)
* `multiple` :: float (default `1.0`)
* `offset` :: float (default `0.0`)


#### voorbeeld

```javascript
// wormhole
voronoi(100,3,5)
  .modulateRotate(osc(1,0.5,0).kaleid(50).scale(0.5),15,0)
  .mult(osc(50,-0.1,8).kaleid(9))
  .out(o0)
```

### modulateScale

`.modulateScale( multiple, offset )`

* `textuur`
  * `color` :: see [color `vec4`](#color-vec4)
  * `src` :: see [`src`](#src)
  * `shape` :: see [`shape`](#shape)
* `multiple` :: float (default `1.0`)
* `offset` :: float (default `1.0`)


#### voorbeeld

```javascript
// cosmic radiation
gradient(5).repeat(50,50).kaleid([3,5,7,9].fast(0.5))
  .modulateScale(osc(4,-0.5,0).kaleid(50).scale(0.5),15,0)
  .out(o0)
```

### modulateScrollX

`.modulateScrollX( multiple, scrollX, speed )`

* `textuur`
  * `color` :: see [color `vec4`](#color-vec4)
  * `src` :: see [`src`](#src)
  * `shape` :: see [`shape`](#shape)
* `scrollX` :: float (default `0.5`)
* `speed` :: float (default `0.0`)

See also: [`scrollX`](#scrollx)

#### voorbeeld

```javascript
voronoi(25,0,0)
  .modulateScrollX(osc(10),0.5,0)
  .out(o0)
```
```javascript
// different scroll and speed
voronoi(25,0,0)
  .modulateScrollX(osc(10),0.5,0.25)
  .out(o0)
```

### modulateScrollY

`.modulateScrollY( textuur, scrollX, speed )`

* `textuur`
  * `color` :: see [color `vec4`](#color-vec4)
  * `src` :: see [`src`](#src)
  * `shape` :: see [`shape`](#shape)
* `scrollY` :: float (default `0.5`)
* `speed` :: float (default `0.0`)


#### voorbeeld

```javascript
// default
voronoi(25,0,0)
  .modulateScrollY(osc(10),0.5,0)
  .out(o0)
```

```javascript
// different scroll and speed
voronoi(25,0,0)
  .modulateScrollY(osc(10),0.5,0.25)
  .out(o0)
```
