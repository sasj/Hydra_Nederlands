
## les 2
Hydra -> [hydra.ojack.xyz](https://hydra.ojack.xyz)


## -> Vorige les


```javascript
//osc (frequentie, synchroniseren, RGB kleur offset)
osc(20,0.1,0.5)
.out()
```

```javascript
osc(20, 0.1, 0.8)
.rotate(0.8,0.1)
.out()
```


### Lijst - array

```javascript
[1,2,4,5]
```

```javascript
osc([20,40,100], 0.1, 0.8)
.rotate(0.8,0.2)
.out()
```

:arrow_right: Verander de waardes


### Kleur

`Overzicht-functies -> funcs_color`  
Ga naar [Kleur functies](../overzicht-functies/funcs_color.md)

:arrow_right: Zoek op de functie omkeren - invert


## :camera: :movie_camera: :camera: webcam :camera: :movie_camera: :camera:

`s0` = de S van source oftewel bron
`initCam()` = functie dat het webcam beeld pakt


```javascript
s0.initCam() // webcam naar s0

src(s0)
.out()
```
het kan zijn dat je een pop-up krijgt om gebruik van de camera toe te laten.



---
### -> Opdracht 1

Voeg nu functies toe die het beeld manipuleren.

#### voorbeeld:

```javascript
s0.initCam() // webcam naar s0

src(s0)
.rotate(0.2,0.5)
.kaleid(2)
.out()
```
