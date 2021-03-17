# Hydra

Dit is een Nederlandse documentatie van Hydra. Officiële documentatie in het Engels is te vinden via: [github.com/ojack/hydra](https://github.com/ojack/hydra)


---
Wat is Hydra?

Hydra is een set tools voor het livecoderen van netwerkbeelden. Geïnspireerd door analoge modulaire synthesizers, zijn deze tools een verkenning van het gebruik van streaming via internet voor het routeren van videobronnen en -outputs in realtime.

Hydra gebruikt meerdere framebuffers om dynamisch te mixen, samen te stellen en samen te werken tussen verbonden browser-visuele-streams. Coördinaten- en kleurtransformaties kunnen op elke uitvoer worden toegepast via gekoppelde functies.

Opmerking: Hydra is in ontwikkeling. Werkt momenteel alleen op Chrome of Chromium, op computers met WebGL.


---


## Beginnen

Ga naar https://hydra-editor.glitch.me

* CTRL-Enter: voer 1 regel code uit
* CTRL-Shift-Enter: voer alle code uit op het scherm
* ALT-Enter: voer een blok code uit
* CTRL-Shift-H: verberg of laat de code zien
* CTRL-Shift-F: maak de code op doormiddel van [Prettier](https://prettier.io/)
* CTRL-Shift-S: Sla een screenshot op en download als een file
* CTRL-Shift-G: Deel op Twitter (als het beschikbaar is). Deelt naar [@hydra_patterns](https://twitter.com/hydra_patterns)


Op [@hydra_patterns](https://twitter.com/hydra_patterns) vind je patronen die door andere gedeeld zijn. Voor inspiratie en om makkelijk aan de slag te gaan.


#### Basic functions
render an oscillator with parameters frequency, sync, and rgb offset:
```
osc(20, 0.1, 0.8).out()
```

rotate the oscillator 0.8 radians:
```
osc(20, 0.1, 0.8).rotate(0.8).out()
```
pixelate the output of the above function:
```
osc(20, 0.1, 0.8).rotate(0.8).pixelate(20, 30).out()
```
show webcam output:
```
s0.initCam() // initialize a webcam in source buffer s0
src(s0).out() // render source buffer s0
```
If you have more than one camera connected, you can select the camera using an index:
```
s0.initCam(1) // initialize a webcam in source buffer s0
```
webcam kaleidoscope:
```
s0.initCam() // initialize a webcam in source buffer s0
src(s0).kaleid(4).out() // render the webcam to a kaleidoscope
```

You can also composite multiple sources together:
```
osc(10)
  .rotate(0.5)
  .diff(osc(200))
  .out()
```

By default, the environment contains four separate output buffers that can each render different graphics.  The outputs are accessed by the variables o0, o1, o2, and o3.

to render to output buffer o1:
```
osc().out(o1)
render(o1) // render the contents of o1
```
If no output is specified in out(), the graphics are rendered to buffer o0.
to show all render buffers at once:
```
render()
```

The output buffers can then be mixed and composited to produce what is shown on the screen.
```
s0.initCam() // initialize a webcam in source buffer s0
src(s0).out(o0) // set the source of o0 to render the buffer containing the webcam
osc(10, 0.2, 0.8).diff(o0).out(o1) // initialize a gradient in output buffer o1, composite with the contents of o0
render(o1) // render o1 to the screen
```

The composite functions blend(), diff(), mult(), and add() perform arithmetic operations to combine the input texture color with the base texture color, similar to photoshop blend modes.

modulate(texture, amount) uses the red and green channels of the input texture to modify the x and y coordinates of the base texture. More about modulation at: https://lumen-app.com/guide/modulation/
```
osc(21, 0).modulate(o1).out(o0)
osc(40).rotate(1.57).out(o1)
```

use a video as a source:
```
s0.initVideo("https://media.giphy.com/media/AS9LIFttYzkc0/giphy.mp4")
src(s0).out()
```


use an image as a source:
```
s0.initImage("https://upload.wikimedia.org/wikipedia/commons/2/25/Hydra-Foto.jpg")
src(s0).out()
```

#### Passing functions as variables
Each parameter can be defined as a function rather than a static variable. For example,
```
osc(function(){return 100 * Math.sin(time * 0.1)}).out()
```
modifies the oscillator frequency as a function of time. (Time is a global variable that represents the milliseconds that have passed since loading the page). This can be written more concisely using es6 syntax:
```
osc(() => (100 * Math.sin(time * 0.1))).out()
```

## Desktop capture
To use screen capture or a browser tab as an input texture, you must first install the chrome extension for screensharing, and restart chrome. Desktop capture can be useful for inputing graphics from another application, or a video or website in another browser tab. It can also be used to create interesting feedback effects.

To install, go to chrome://extensions
Click "Load unpacked extension", and select the "extensions" folder in "screen-capture-extension" in this repo. Restart chrome. The extension should work from now on without needing to reinstall.

select a screen tab to use as input texture:
```
s0.initScreen()
```

render screen tab:
```
s0.initScreen()
src(s0).out()
```

## Connecting to remote streams
Any hydra instance can use other instances/windows containing hydra as input sources, as long as they are connected to the internet and not blocked by a firewall. Hydra uses webrtc (real time webstreaming) under the hood to share video streams between open windows. The included module rtc-patch-bay manages connections between connected windows, and can also be used as a standalone module to convert any website into a source within hydra. (See standalone camera source below for example.)

To begin, open hydra simultaneously in two separate windows.
In one of the windows, set a name for the given patch-bay source:
```
pb.setName("myGraphics")
```
The title of the window should change to the name entered in setName().

From the other window, initiate "myGraphics" as a source stream.
```
s0.initStream("myGraphics")
```
render to screen:
```
s0.initStream("myGraphics")
src(s0).out()
```
The connections sometimes take a few seconds to be established; open the browser console to see progress.
To list available sources, type the following in the console:
```
pb.list()
```

## Running locally
To run locally, you must have nodejs and npm installed. Install from: https://nodejs.org/en/

open terminal and enter directory
```
cd hydra
```
install dependencies:
```
npm install -d
```
run server
```
npm run start
```
go to https://localhost:8000 in the browser

## Audio Responsiveness (experimental)
FFT functionality is available via an audio object accessed via "a". The editor uses https://github.com/meyda/meyda for audio analysis.
To show the fft bins,
```
a.show()
```
Set number of fft bins:
```
a.setBins(6)
```
Access the value of the leftmost (lowest frequency) bin:
```
a.fft[0]
```
Use the value to control a variable:
```
osc(10, 0, () => (a.fft[0]*4))
  .out()
```
It is possible to calibrate the responsiveness by changing the minimum and maximum value detected. (Represented by blur lines over the fft). To set minimum value detected:
```
a.setCutoff(4)
```

Setting the scale changes the range that is detected.
```
a.setScale(2)
```
The fft[<index>] will return a value between 0 and 1, where 0 represents the cutoff and 1 corresponds to the maximum.

You can set smoothing between audio level readings (values between 0 and 1). 0 corresponds to no smoothing (more jumpy, faster reaction time), while 1 means that the value will never change.
```
a.setSmooth(0.8)
```
To hide the audio waveform:
```
a.hide()
```
## MIDI (experimental)

MIDI controllers can work with Hydra via WebMIDI an example workflow is at [/docs/midi.md](https://github.com/ojack/hydra/blob/master/docs/midi.md) .

## API

There is an updated list of functions at [/docs/funcs.md](https://github.com/ojack/hydra/blob/master/docs/funcs.md).

As well as in the [source code for hydra-synth](https://github.com/ojack/hydra-synth/blob/master/src/composable-glsl-functions.js).

#### Changelog between v0 and v1:
* Syntax change from 'o0.osc()' to 'osc().out(o0)'. Note: old syntax still works
* multiple generator functions can be composited into each other:
`osc(10)
  .rotate(0.5)
  .diff(osc(200).rotate(0.2))
  .out()`
* Buffer can be an input to itself:
`osc(40, 0.1, 1)
  .modulate(src(o0), 0.1)
  .scale(1.1)
  .rotate(0.04)
  .out(o0)`
* Multiple cameras can be specified using s0.initCam(1)
* synth logic exists as a separate module, hydra-synth
* added preliminary fft capability
* fixed some bugs in editor and camera

 #### Libraries and tools used:
 * [Regl: functional webgl](http://regl.party/)
 * glitch.io: hosting for sandbox signalling server
 * codemirror: browser-based text editor
 * simple-peer

 ## Inspiration:
 * Space-Time Dynamics in Video Feedback (1984). [video](https://www.youtube.com/watch?v=B4Kn3djJMCE) and [paper](http://csc.ucdavis.edu/~cmg/papers/Crutchfield.PhysicaD1984.pdf) by Jim Crutchfield about using analog video feedback to model complex systems.
 * [Satellite Arts Project (1977) - Kit Galloway and Sherrie Rabinowitz](http://www.ecafe.com/getty/SA/)
 * [Sandin Image Processor](http://www.audiovisualizers.com/toolshak/vidsynth/sandin/sandin.htm)
 * [kynd - reactive buffers experiment](https://kynd.github.io/reactive_buffers_experiment/)

 #### Related projects:
 * [Lumen app (osx application)](https://lumen-app.com/)
 * [Vsynth (package for MaxMSP)](https://cycling74.com/forums/vsynth-package)
 * [VEDA (VJ system within atom)](https://veda.gl/)
 * [The Force](https://videodromm.com/The_Force/)
