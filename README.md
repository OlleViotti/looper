<p align="center"><img src="icon.svg" alt="" width="140"></p>

<h1 align="center">Varv</h1>

**Varv** is a loop station that runs in the browser, built for the phone. You listen to the click and your loops in Bluetooth headphones and record with the phone's own microphone. Bluetooth delays everything you hear by a couple of hundred milliseconds, so anything you play along is recorded late. Varv corrects that: every recording is shifted back by a latency you set, or have the app measure for you, so it lands on the beat.

*Varv* is Swedish for lap, or one turn round the loop.

**Open it:** https://olleviotti.github.io/looper/. On an iPhone, open it in Safari, allow the microphone, and choose Add to Home Screen from the share menu. It then runs full screen, works offline, and keeps your saved projects.

## Latency correction

- **Per recording.** Every recording is shifted back by the latency in force when it was made. Each one keeps its own value, which you can nudge afterwards in steps of 1 or 10 ms while the loop plays, watching the hits line up with the beat lines.
- **Setups.** Save one latency value per combination of headphones and microphone, for example AirPods and wired, and switch between them.
- **Automatic measurement, exact.** The app plays ten clicks and listens for them through the microphone, using a matched filter tuned to the click, so no human timing is involved. Hold the phone's microphone against an earbud. It finds a faint click buried in noise and reports nothing rather than a wrong value when it cannot hear the clicks.
- **Measurement by clapping.** Clap along with ten clicks. People clap slightly ahead of a click, so this reads somewhat short; the app says so.
- **Microphone choice.** By default the app records with the phone's own microphone even when headphones are connected, and switches back to it if the system changes the input.

## Recording

- Click with a count-in of one bar, tempo 40 to 240 bpm with tap tempo, 2 to 7 beats per bar and 1, 2, 4 or 8 bars per lap.
- **One lap** records a single lap. **Continuous** records every lap until you tap again; silent laps are thrown away.
- **Capture last** keeps the lap you just played even if you never pressed Record.
- **Undo** removes the latest recording. Removed recordings and deleted tracks stay in a bar at the bottom with a Restore button until you dismiss it.
- A level meter and a live strip show what the microphone hears, already shifted by the current latency.

## Tracks

- Add tracks before you start, name them and give them their own effects.
- **Arm** a track to record into it. With no track armed, Record fills the empty tracks from the top, then creates new ones. The status bar always says where the next recording will go.
- Recording again into a track that already holds audio adds another take on top (overdub). Each take has its own latency, reverse and remove.
- Large **Arm**, **Solo** and **Mute** buttons on every track, made for live use.
- Per track: volume, pan, three-band EQ (low, mid, high), filter (darker or thinner), delay send and reverb send.

## Master effects

- Volume, three-band EQ and filter.
- Delay: time as 1/16, 1/8, dotted 1/8 or 1/4 note, or free in milliseconds; feedback, level and mix send.
- Reverb: size, level and mix send.
- Compressor: threshold and amount. The click goes through a matching neutral compressor, so click and tracks are delayed by the same few milliseconds and timing is unaffected.

## Projects

- Save the session as a named project: tracks, takes, track settings, tempo and master effects. Once saved, changes are saved automatically.
- The raw recordings are stored, not the finished loops, so the latency of every take can still be changed after a project is reopened.
- Projects are stored in the browser on the device (IndexedDB) and are not synced anywhere.
- Export the current lap as a WAV file of the audible tracks, without effects or pan.

## Live use

- The screen stays awake while playing. Large transport buttons: Start, Undo, Record, Capture last and Click on or off.
- Keys, and Bluetooth pedals that send them: <kbd>Space</kbd> start and stop, <kbd>R</kbd>, <kbd>Enter</kbd> or <kbd>→</kbd> record, <kbd>←</kbd> undo, <kbd>C</kbd> capture last, <kbd>K</kbd> click, <kbd>1</kbd> to <kbd>9</kbd> mute a track.

## Technical notes

Everything lives in `index.html`, with no build step and no dependencies apart from two web fonts. Recording runs in an AudioWorklet that writes the microphone into a ring buffer indexed by the audio clock, which is what makes sample-accurate alignment possible. The page must be served over https for the microphone to work. `sw.js` makes the app work offline.

Alignment, measurement, projects and the track features are verified with automated tests in Chrome using simulated audio.
