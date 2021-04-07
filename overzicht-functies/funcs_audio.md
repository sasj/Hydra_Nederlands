## Geluid - Audio

Functies om audio invoer te gebruiken waar de visuals op reageren.

- [algemeen](#algemeen)
- [1. audio informatie](#audio-informatie)
- [show](#show)
- [hide](#hide)
- [setBins](#setbins)
- [setCutoff](#setcutoff)
- [setScale](#setScale)
- [setSmooth](#setSmooth)
- [2. audio als variabel](#2.-audio-als-ariabel)
---
### algemeen

Er zijn twee verschillende categorieën voor audio.
1. audio informatie weergeven en aanpassen
2. audio gebruiken als variabel om de visuals te manipuleren.

Mogelijk vraagt jouw browser toestemming om microfoon te gebruiken.

---
### 1. audio informatie
Voor het gebruik van de audio functies gebruiken we toegewezen variabele naam 'a' (de a van audio).


---
### show
Hiermee laat je de bins zien van de audio input. Standaard is dat 4 balkjes rechts onderin.

`.show()`
```javascript
a.show();
```

### hide
zorg dat de audio visualisatie rechts onder verdwijnt.

`.hide()`

```javascript
a.hide();
```


### setBins
Hiermee kan je de aantal bins veranderen, standaardwaarde is 4 en kan je al veel mee, maar je kan bijv. ook 6 of 18 gebruiken.
Per bin is een bepaalde frequentie bereik ingesteld. Als je meer bins hebt zorgt dat ervoor dat per bin het bereik kleiner wordt, waardoor je specifieker bepaalde frequenties kan adresseren.

`.setBins( bins )`

* `bins` :: integer (standaardwaarde `4`)

```javascript
a.setBins(6);
```

### setCutoff
Wijzig tot waar de geluidsdetectie mag worden gebruikt.

`.setCutoff( frequency )`

* `frequency` :: float (standaardwaarde `x`)

```javascript
a.setCutoff(6)
```

### setScale
Wijzig het bereik van de audio input.

`.setScale( amount )`

* `amount` :: float (standaardwaarde `x`)

```javascript
a.setScale(3)
```


### setSmooth
Maak de fft-waarden vlakker, hierdoor is het meer of minder gevoelig voor snelle veranderingen.  
De waardes zijn tussen 0 en 1.
0 = het meest gevoelig
1 = het meest vlak.

`.setSmooth( hoeveelheid )`

* `amount` :: float (standaardwaarde `x`)

```javascript
a.setSmooth(0.3)
```


---
## 2. audio als variabel
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
