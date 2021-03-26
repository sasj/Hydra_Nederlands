
## les 1

Benodigheden
- Chrome of Chromium browser
- Deze documentatie


## Begin

Ga naar [hydra.ojack.xyz](https://hydra.ojack.xyz)
Je krijgt een scherm met uitleg over Hydra. Sluit het venster (wanneer je het gelezen hebt). Je ziet nu een voorbeeld schets, deze kan elke keer verschillend zijn.

De code van het voorbeeld wordt gelijk uitgevoerd.

Rechts boven zie je een aantal knoppen:  
![voer code uit](afbeeldingen/play.png) = voer code uit / play  

![upload](afbeeldingen/upload.png) = upload naar [Hydra_patterns op Twitter](https://twitter.com/hydra_patterns)

![clear](afbeeldingen/clear.png) = verwijder alle code

![voer code uit](afbeeldingen/example.png) = een willekeurig voorbeeld   

![change](afbeeldingen/change.png) = verander willekeurige waardes

![info](afbeeldingen/info.png) = informatie startscherm

Belangrijke toets combinaties

* CTRL-Enter: voer 1 regel code uit
* CTRL-Shift-Enter: voer alle code uit op het scherm
* ALT-Enter: voer een blok code uit



### :arrow_right: doen:
- bestudeer verschillende voorbeelden. Kan je zelf bedenken wat verschillende functies doen?



## Basis functies

Als eerst gaan we aan de slag met een oscillator.


```javascript
osc(20)
.out()
```
We beginnen het maken van een oscillator doormiddel de functie `osc()`  
`.out` zorgt er voor dat het beeld op het scherm getoond wordt.

De `osc` krijgt hier 1 input, het getal 20.   
:arrow_right: verander deze waarde en kijk wat er gebeurd

---
```javascript
//osc (frequentie, synchroniseren, RGB kleur offset)
osc(20,0.1,0.5)
.out();

```
We geven bij het eerste voorbeeld 1 argument, maar de functie `osc()` kan 3 argumenten ontvangen.
- frequentie = de hoeveelheid golven
- synchronisatie = snelheid
- RGB kleur offset = kleurwaarde

:arrow_right: verander de 3 waardes en kijk wat er gebeurd

---
#### draaien
```javascript
osc(20, 0.1, 0.8)
.rotate(0.8)
.out()
```

Functies kan worden toegevoegd tussen `osc()` en `.out()`, hier hebben we een voorbeeld met de `rotate()` functie. Om een functie toe te voegen zetten we eerst een punt.

de `rotate()` functie kan 1 of 2 waardes ontvangen.

`.rotate( hoek, snelheid )`

* `hoek` :: float (standaardwaarde `10.0`)
* `snelheid` :: float (standaardwaarde `0.0`)

```javascript
osc(20, 0.1, 0.8)
.rotate(0.8,0.1)
.out()
```

:arrow_right: Verander de waardes weer

### Lijst - array

```javascript
[1,2,4,5]
```

```javascript
osc([20,40,100], 0.1, 0.8)
.rotate(0.8,0.2)
.out()
```



---
### :dart: Opdracht 1

Ga naar [overzicht-functies/funcs_geometry.md](../overzicht-functies/funcs_geometry.md)

Pas de functie kaleidoscoop toe.


### :dart: Opdracht 2: verder spelen

Kijk verder in het overzicht van de functies. Ook bij kleur / color.
