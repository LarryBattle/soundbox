# soundbox
A super simple JS library for playing sound effects and other audio.

 * Current size: `1.4kb`
 * Current minified size: `0.74kb`

[Demo](https://sbrl.github.io/soundbox/example.html)

Quick example:

```javascript
var soundbox = new SoundBox();
soundbox.load("beep-a", "beep-a.wav")
    .then(
        () => console.log("Loaded beep a!"),
        () => console.error("Failed to load keep a :-(")
    );
soundbox.load("beep-b", "beep-b.wav");
soundbox.load("beep-c", "beep-c.wav");
soundbox.load("victory", "victory.mp3");

soundbox.play("beep-a")
    .then(() => soundbox.play("beep-b"))
    .then(() => soundbox.play("beep-c"))
    .then(() => soundbox.play("victory"));
    
// The 3rd parameter is the volume: The callback can be omitted to enable promise mode
soundbox.play("beep", null, 0.8)
    .then(() => soundbox.play("victory"))
```

_(Full documentation below)_

## Download
The recommended way to obtain soundbox is via [npm](https://npmjs.org/) here: [sound-box](https://www.npmjs.com/package/sound-box) - To install it simply type `npm install sound-box`. Then you can include any of the 4 files described below from the `./node_modules/sound-box/` directory.

If npm isn't for you, then the latest master should be perfectly stable. If you want something that you know will work, try the latest [release](https://github.com/sbrl/soundbox/releases).

The following files are available via all release methods:
 * [soundbox.js](https://raw.githubusercontent.com/sbrl/soundbox/master/soundbox.js) - The main development version.
 * [soundbox.min.js](https://raw.githubusercontent.com/sbrl/soundbox/master/soundbox.min.js) - A minified version of the above.
 * [soundbox.jsm](https://raw.githubusercontent.com/sbrl/soundbox/master/soundbox.jsm) - An ES6 module-compatible version that's autogenerated. If you possibly can, I'd advise learning about about them. [This is a useful resource](https://jakearchibald.com/2017/es-modules-in-browsers/).
 * [soundbox.jsm](https://raw.githubusercontent.com/sbrl/soundbox/master/soundbox.min.jsm) - A minified version of the above.


## Usage

### Create a new instance:

```javascript
var soundbox = new SoundBox();
```

### Load a sound
Sound loading is done as follows. If a callback is not specified, promise mode is activated.

```javascript
// Promise mode
soundbox.load("alias", "path/to/filename").then(
    () => console.log("Loaded beep!"),
    () => console.error("Failed to load beep :-(")
);
soundbox.load("victory", "./sounds/yay.wav").then( /* .... */);
```

```javascript
// Callback mode
soundbox.load("alias", "path/to/filename", function() {
    console.log("Loaded beep!");
});
```

### Play a sound
Similarly, playing a sound takes 2 forms: callback and promise.

```javascript
// Promise mode
soundbox.play("beep-a")
    .then(() => soundbox.play("beep-b")) /* The .then() is optional of course */
    .then(() => soundbox.play("beep-c"))
    .then(() => soundbox.play("victory"));
```

```javascript
// Callback mode
soundbox.play("beep", function() {
	// Do stuff
});
```

#### Specify the volume
The volume can be specified when playing a sound, too. The volume should be a floating-point number between 0 (silent) and 1 (full volume, default).

Here's how:

```javascript
// Promise mode
soundbox.play("beep-a", null, 0.8)
    .then(() => /* .... */);
```

```javascript
// Callback mode
soundbox.play("beep", function() {
	// Do stuff
}, 0.5);
```

### Specify the default volume
If you'd like to change the default volume that sounds are played at, do this:

```javascript
soundbox.default_volume = 0.45; // Sets the default volume to 45%
```

#### Looping again and again
As of v0.3.7, looping support has been added. Use it like this:

```javascript
// Promise mode
soundbox.play("rocket", null, 0.8, true)
    .then(() => /* .... */);
```

```javascript
// Callback mode
soundbox.play("rocket", function() {
	// Do stuff
}, null, true); // A null volume = use the default volume. Supported in both modes of operation
```

### Stop all sounds
You can stop all currently playing sounds like this:

```javascript
soundbox.stop_all();
```

### Unload a sound
If you want to, you can unload a sound:

```javascript
soundbox.remove("sound_alias");
soundbox.remove("oops");
```

### Get the current version
Get the current version of SoundBox:

```javascript
console.log(`Soundbox is at ${SoundBox.version}`);
```

## Changelog
 - **v0.2:** Now with button mashing support!
 - **v0.3:** Added volume support! Converted for use as an ES6 module. If this doesn't suit you, then just remove the `import` and `export` statements to make it the way it was before.
 - **v0.3.1:** Added non-es6 version and build system to automate minification.
 - **v0.3.2:** Added `.stop_all()` and `default_volume`
 - **v0.3.3:** Fix a bug in `.stop_all()`
 - **v0.3.4:** Fix another bug in `.stop_all()`
 - **v0.3.5:** Update from `.jsm` to `.mjs` for file extension
 - **v0.3.6:** Fix `main` definition in `package.json`
 - **v0.3.7:** Update changelog in README
 - **v0.3.8:** Add optional `loop` parameter to `.play()`

## Real-World Usage
 - @MyTheValentinus has [created a mobile web app for playing sound-effects and other sounds](https://github.com/MyTheValentinus/soundbox)
 - @kdallas has used it as part of a [100 movies list](https://www.weblabsperth.com.au/100-movies/)
 - ...? _(Are you using soundbox? Let me know by opening an issue or contacting me and I'll add your project here!)_

## License
SoundBox.js is licensed under MIT:

```
The MIT License (MIT)

Copyright (c) 2015 Starbeamrainbowlabs

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
