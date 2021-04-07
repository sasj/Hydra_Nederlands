
## les 4
Hydra -> [hydra.ojack.xyz](https://hydra.ojack.xyz)


## Audio reactief!

Audio functies: [overzicht-functies/funcs_audio.md](overzicht-functies/funcs_audio.md)


Voor het gebruik van de audio functies gebruiken we toegewezen variabele naam 'a' (de a van audio).

---
#### eerste kijken wat voor input we krijgen.

`.show()`

```javascript
a.show();
```

---
#### meerdere bins

`.setBins( bins )`

* `bins` :: integer (standaardwaarde `4`)

```javascript
a.setBins(6);
```


---
## audio als variabel
De verschillende waardes van de bins kan worden gebruikt om het beeld aan te passen en te laten reageren op geluid.

'a' variabele wordt weer gebruikt.  
'.fft[x]' vragen we de waarde van een bin aan. Tussen '[ ]' komt een getal van de bin die we willen gebruiken. Als de standaardwaarde van het aantal bins niet veranderd is, zijn er 4 bins. Belangrijk om te onthouden is dat de eerste bin met het nummer 0 begint. Bins de we kunnen aanroepen zijn dus '0' '1' '2' '3'.

'a.fft[0]'
om te zorgen dat de waarde altijd blijft updaten gaan we de waarde in een functie zetten.
' () => a.fft[0]'


```javascript
a.show()

osc(10)
.rotate( () => a.fft[3])
.out()
```




---
### -> Vandaag verder

Gebruik de audio input als waarde in verschillende functies.
