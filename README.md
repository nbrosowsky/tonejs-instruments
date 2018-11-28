# tonejs-instruments

I've been playing around with audio samples and [Tone.js](https://tonejs.github.io/) but was finding it tedious to keep writing code to load the same instrument samples.
So I decided to put together a little code that makes it easier for me to load the instruments and a repository for all the samples I'm using.

This code produces a SampleLibrary object with all the info about the samples and a quick load function.

##### [DEMO (all instruments)](https://nbrosowsky.github.io/tonejs-instruments/demo.html)
**Note: this demo loads all the samples from all the instruments and may be slow loading. If your internet connection is slow, I suggest the demo below, which loads four randomly chosen instruments.

##### [DEMO (four random instruments)](https://nbrosowsky.github.io/tonejs-instruments/demo-min.html)

## Basic Usage

You can load instrument samples by calling SampleLibrary.load() and passing an object with the settings. 
Only the "instrument" setting is necessary to load an instrument. By default, instruments are not automatically connected to the master out.

```javascript
// passing a single instrument name loads one instrument and returns the tone.js object
var piano = SampleLibrary.load({
  instruments: "piano"
  });
  
 piano.toMaster();
 piano.triggerAttack("A3");

// passing an array of instrument names will load all the instruments listed returning a new object, 
// each property a tone.js object
var instruments = SampleLibrary.load({
  instruments: ["piano","harmonium","violin"]
  });

// waits for instrument sound files to load from /samples/
Tone.Buffer.on('load', function() {
     // play instrument sound
     instruments['piano'].toMaster();
     instruments['piano'].triggerAttack("A3");
     });

```

## Optional arguments

File extension:
```javascript
// By default, the file extension for the samples is set to .mp3 with .ogg as a fallback. 
// You can change this by setting the "ext" when you load:
var piano = SampleLibrary.load({
  instruments: "piano",
  ext: ".wav"
  });

// follows the Tone.js formatting for fallbacks
var piano = SampleLibrary.load({
  instruments: "piano",
  ext: ".[wav|mp3|ogg]"
  });

```

Reduce the number of samples loaded
```javascript
// The number of samples per instrument varies quite a bit (a few have more than 60)
// To reduce the number loaded set "minify" to true
// If > 16 samples, it loads every second
// If > 32 samples, it loads every fourth
// If > 48 samples, it loads every sixth

var piano = SampleLibrary.load({
  instruments: "piano",
  minify: true
  });
  
```

## About the samples

These instrument samples come from a variety of public domain sources (see the sample-source-info.txt for more information)

All the samples have been edited for consistency: trimming silence, on/off ramp, volume-matching, normalizing, noise removal, and some pitch-correction where necessary.

Included instruments:
- bass-electric
- bassoon
- cello
- clarinet
- contrabass
- flute
- french-horn
- guitar-acoustic
- guitar-electric
- harmonium
- harp
- organ
- piano
- saxophone
- trombone
- trumpet
- tuba
- violin
- xylophone

## To do:
- Add drumkits
- Add Synths

## LICENSE

Code: MIT License (see LICENSE.md)

Samples: [CC-by 3.0](https://creativecommons.org/licenses/by/3.0/)
