<p align="center"><img src="icon.svg" alt="" width="140"></p>

<h1 align="center">Varv</h1>

**Varv** is a loop station that runs in the browser, built for the phone. You listen to the click and your loops in Bluetooth headphones and record with the phone's own microphone. Bluetooth delays everything you hear by a couple of hundred milliseconds, so anything you play along is recorded late. Varv corrects that: every recording is shifted back by a latency you set, or have the app measure for you, so it lands on the beat.

*Varv* is Swedish for lap, or one turn round the loop.

**Open it:** https://olleviotti.github.io/looper/. On an iPhone, open it in Safari, allow the microphone, and choose Add to Home Screen from the share menu. It then runs full screen, works offline, and keeps your saved projects.

## Three views

The app has three views, reached by swiping or with the two buttons in the header.

- **Play** is the live view. Each track is a name and a tape strip showing its waveform.
  - **Tap a strip** to mute or unmute the track.
  - **Hold a strip** to arm it; a red fill shows the hold, and the armed track gets a red frame.
  - **Tap a name** to solo the track.
- **Swipe right for Edit.** The track names travel to the right edge and the edit window comes in from the left. Tap a name to edit that track, or tap Master for the master effects. Swipe left on the names, or tap the edit button, to go back.
- **Swipe left for Settings:** loop length, tempo, latency, project, click, recording, mute timing and microphone. Swipe right or tap Done to go back.

## Latency correction

- **Per recording.** Every recording is shifted back by the latency in force when it was made. Each one keeps its own value, which you can nudge afterwards in steps of 1 or 10 ms while the loop plays, watching the hits line up with the beat lines.
- **Automatic measurement, exact.** The app plays ten clicks and listens for them through the microphone, using a matched filter tuned to the click, so no human timing is involved. Hold the phone's microphone against an earbud and tap Measure exactly. It finds a faint click buried in noise and reports nothing rather than a wrong value when it cannot hear the clicks.
- **Microphone choice.** By default the app records with the phone's own microphone even when headphones are connected, and switches back to it if the system changes the input.

## Loop length

- **Bars.** Tempo 40 to 240 bpm with tap tempo, 1 to 16 beats per bar and 1 to 32 bars per lap, with a click and a one-bar count-in.
- **Bars per track.** In Edit each track can have its own number of bars, for example a 4-bar melody over a 1-bar beat. It records on its own boundaries and its strip shows its own bars and playhead. The setting is fixed once the track holds a recording.
- **Free.** No tempo and no click. The first Record starts at once; play, then tap **End loop** to set the length (up to 30 seconds). Every track then has that length. Since nothing is playing during that first recording, it is not shifted for latency; later recordings are, so they land on the first one.

## Recording

- **One lap** records a single lap. **Continuous** records every lap until you tap again; silent laps are thrown away.
- **Capture last** keeps the lap you just played even if you never pressed Record.
- **Undo** removes the latest recording. Removed recordings and deleted tracks stay in a bar at the bottom with a Restore button until you dismiss it.
- A level meter and a live strip show what the microphone hears, already shifted by the current latency.

## Tracks

- Add tracks before you start, name them and give them their own effects.
- **Arm** a track (hold its strip) to record into it. With no track armed, Record fills the empty tracks from the top, then creates new ones. The status bar always says where the next recording will go.
- Recording again into a track that already holds audio adds another take on top (overdub). Each take has its own latency, reverse and remove.
- **Mute timing:** mute and solo act immediately by default. In Settings they can instead land on the next beat or the next bar (in free mode: the next pass of the loop), so you can tap a little ahead.
- Per track, in Edit: name, arm, solo and mute buttons, volume, pan, graphical EQ, filter (darker or thinner), delay send and reverb send, plus the waveform and each take's latency, reverse and remove.

## Graphical EQ

Each track and the master have a three-band EQ drawn as its response curve. Drag the L, M or H handle sideways to set the frequency and up or down to set the level, from −12 to +12 dB; double-tap a handle to flatten it. The low and high bands are shelves and the mid band is a bell. The curve is the real response of the filters, the filter setting included.

## Master effects

Under Master in the Edit view:

- Volume, graphical EQ and filter.
- Delay: time as 1/16, 1/8, dotted 1/8 or 1/4 note, or free in milliseconds; repeats, level and mix send.
- Reverb: size, level and mix send.
- Compressor: threshold and amount. The click goes through a matching neutral compressor, so click and tracks are delayed by the same few milliseconds and timing is unaffected.

## Projects

- Save the session as a named project: tracks, takes, track settings, loop length, tempo and master effects. Once saved, changes are saved automatically.
- The raw recordings are stored, not the finished loops, so the latency of every take can still be changed after a project is reopened.
- Projects are stored in the browser on the device (IndexedDB) and are not synced anywhere.
- Export as a WAV file of the audible tracks, without effects or pan. With tracks of different lengths, the export runs until they all line up again.

## Live use

- The screen stays awake while playing. Large transport buttons: Start, Undo, Record, Capture last and Click on or off.
- Keys, and Bluetooth pedals that send them: <kbd>Space</kbd> start and stop, <kbd>R</kbd>, <kbd>Enter</kbd> or <kbd>→</kbd> record, <kbd>←</kbd> undo, <kbd>C</kbd> capture last, <kbd>K</kbd> click, <kbd>1</kbd> to <kbd>9</kbd> mute a track, <kbd>E</kbd> edit, <kbd>S</kbd> settings.

## Technical notes

Everything lives in `index.html`, with no build step and no dependencies apart from two web fonts. Recording runs in an AudioWorklet that writes the microphone into a ring buffer indexed by the audio clock, which is what makes sample-accurate alignment possible. The page must be served over https for the microphone to work. `sw.js` makes the app work offline.

Alignment, measurement, the gestures, the EQ, projects and the track features are verified with automated tests in Chrome using simulated audio.
