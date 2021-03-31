## Bronnen / Sources

Bronnen worden als basis gebruikt om visuele inhoud te produceren. Het is als ware een beginpunt van een blok code.

- [kleur verloop - gradient](#gradient)
- [ruis - noise](#noise)
- [osc](#osc)
- [uit - out](#out)
- [weergeven - render](#render)
- [vorm - shape](#shape)
- [solide - solid](#solid)
- [src](#src)
- [src - camera](#src_-_camera)
- [voronoi](#voronoi)

---
### kleur verloop gradient

`gradient( snelheid )`

* `snelheid` :: float (standaardwaarde `x`)

#### voorbeeld

```javascript
gradient(2)
.out()
```
---
### ruis - noise

`noise( schaal, offset )`

* `schaal` :: int (standaardwaarde `10.0`)
* `offset` :: float (standaardwaarde `0.1`)

Genereer [Perlin noise](https://en.wikipedia.org/wiki/Perlin_noise).

#### voorbeeld

```javascript
// ruis verandering tussen verschillende schalen en offsets
noise( ({time}) => Math.sin(time/10)*50 , ({time}) => Math.sin(time/2)/500 )
    .out()
```
---
### osc

`osc (frequentie, synchroniseren, RGB kleur offset)`

* `frequentie` :: float (standaardwaarde `60.0`)
* `synchroniseren` :: float (standaardwaarde `0.1`)
* `RGB kleur offset` :: float (standaardwaarde `0.0`)

#### voorbeeld

```javascript
// frequentie
osc( [1,10,50,100,250,500].fast(2) )
  .out()
```
```javascript
// frequentie 2
osc( ({time}) => Math.sin(time/10) * 100 )
.out()
```
```javascript
// synchroniseren
osc( 10, [-10,-1,-0.1,0,0.1,1,10], 0 )
.out()
```
```javascript
// RGB kleur offset
osc(10,0.1, ({time}) => Math.sin(time/10) * 100 )
.out()
```
---
### uit - out

`.out( buffer )`

* `buffer`
  * `osc`: `o0`, `o1`, `o2`, `o3`
  * `src`: `s0`, `s1`, `s2`, `s3`

#### voorbeeld

```javascript
// Basis
osc(20,0.1,0.5)
.out()
```

```javascript
// stuur vier oscillatoren naar verschillende buffers
// en laat ze samen komen
osc( [1,10,50,100,250,500].fast(2) ).out(o0) // frequentie
osc( ({time}) => Math.sin(time/10) * 100 ).out(o1) // frequentie 2
osc( 10, [-10,-1,-0.1,0,0.1,1,10], 0 ).out(o2) // sync
osc(10,0.1, ({time}) => Math.sin(time/10) * 100 ) // kleur offset
  .modulate(o1,0.05)
  .modulate(o2,0.05)
  .modulate(o3,0.05)
  .out(o3)
render(o3)
```
---
### weergeven - render

`render( buffer )`

* `buffer`: buffer (standaardwaarde `o0`)
---
#### voorbeeld

```javascript
osc( [1,10,50,100,250,500].fast(2) ).out(o0) // frequentie
osc( ({time}) => Math.sin(time/10) * 100 ).out(o1) // frequentie 2
osc( 10, [-10,-1,-0.1,0,0.1,1,10], 0 ).out(o2) // sync
osc(10,0.1, ({time}) => Math.sin(time/10) * 100 ).out(o3) // kleur offset

render(o0) // verander naar  o1, o2, or o3
```

```javascript
// alle vier de buffers op het scherm
osc( [1,10,50,100,250,500].fast(2) ).out(o0) // frequentie
osc( ({time}) => Math.sin(time/10) * 100 ).out(o1) // frequentie 2
osc( 10, [-10,-1,-0.1,0,0.1,1,10], 0 ).out(o2) // sync
osc(10,0.1, ({time}) => Math.sin(time/10) * 100 ).out(o3) // kleur offset
render()
```
---
### vorm - shape

`shape( zijkanten, straal, gladstrijken)`

* `zijkanten` :: int (standaardwaarde `3.0`)
* `straal` :: float (standaardwaarde `0.3`)
* `gladstrijken` :: float (standaardwaarde `0.01`)

#### voorbeeld

```javascript
// wazige cirkel omkeren
shape(100,0.01,1)
.invert(({time})=>Math.sin(time)*2)
.out()
```

```javascript
// een regenboog bal
shape(5,0.5,0.1).repeat(19,19)
  .mult(osc(10,1,2))
  .rotate( ({time}) => time%360 )
  .scrollX(1,-0.25)
  .mult(shape(15,0.3,0.01)
        .rotate( ({time}) => time%360 )
        .scrollX(1,-0.25))
  .out()
```
---
### solide - solid

`solid( r, g, b, a )`

* `r` :: float (standaardwaarde `0.0`)
* `g` :: float (standaardwaarde `0.0`)
* `b` :: float (standaardwaarde `0.0`)
* `a` :: float (standaardwaarde `1.0`)

#### voorbeeld

```javascript
// door rood, groen en blauw lopen
solid([1,0,0],[0,1,0],[0,0,1],1)
.out()
```
---
### src

`src( invoer )`

* `invoer` :: invoer (voorbeelden: `o0`, `s1`)


---
### src - camera

activeer camera
's0.initCam()'

#### voorbeeld:

```javascript
s0.initCam() // webcam naar s0

src(s0)
.rotate(0.2,0.5)
.kaleid(2)
.out()
```


---
### voronoi

`voronoi( schaal, snelheid, mengen )`

* `schaal` :: float (standaardwaarde `5`)
* `snelheid` :: float (standaardwaarde `0.3`)
* `mengen` :: float (standaardwaarde `0.3`)

Genereer [voronoi vormen](https://en.wikipedia.org/wiki/Voronoi_diagram).

#### voorbeeld

```javascript
// standaardwaarde
voronoi(5,0.3,0.3)
.out()
```

```javascript
// fireflies
voronoi(25,2,10)
.color(1,1,0)
.brightness(0.1
.out()
```
