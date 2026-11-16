<p align="center"><img src="icon.svg" alt="" width="140"></p>

<h1 align="center">Varv one</h1>

**Varv one** is a loop station that runs in the browser, built for the phone. You listen to the click and your loops in Bluetooth headphones and record with the phone's own microphone. Bluetooth delays everything you hear by a couple of hundred milliseconds, so anything you play along is recorded late. Varv corrects that: every recording is shifted back by a latency you set, or have the app measure for you, so it lands on the beat.

*Varv* is Swedish for lap, or one turn round the loop.

**Open it:** https://olleviotti.github.io/varv/. On an iPhone, open it in Safari, allow the microphone, and choose Add to Home Screen from the share menu. It then runs full screen, works offline, and keeps your saved projects.

## Guide

Short guide lines on the play screen, in edit mode and in settings explain each part when it first becomes relevant, and each one disappears for good once you have used what it describes. Settings has a button to show them again.

## Three views

The top bar is a single row: the bar and beat counter on the left, the Varv logo in the middle and the in and out meters on the right. Its bottom edge is amber while playing and the whole bar turns red while recording. The app has three views, reached by swiping (or the <kbd>E</kbd> and <kbd>S</kbd> keys); tapping the logo always brings you back to play.

- **Play** is the live view. Each track is a name and a tape strip showing its waveform. A new project starts with four empty tracks; the tracks share the screen height and shrink as more are added, down to a minimum, after which the list scrolls.
  - **Tap a strip** to mute or unmute the track.
  - **Hold a strip** to record one lap into that track, starting at its next lap; a red fill shows the hold, and the track gets a red frame and says "next lap", then "recording". When stopped, playback starts with the count-in first. Hold again to cancel.
  - **Tap a name** to solo the track.
- **Swipe right for Edit.** The track names travel to the right edge and the edit window comes in from the left. It opens on the track you last touched; tap another name to edit that one, or tap Master for the master effects. Double-tap any setting to return it to its default: sliders, EQ handles and switches anywhere, and the number on a stepper (tempo, beats, bars, latency). Settings locked by recordings stay as they are. Swipe left on the names, or tap the logo, to go back.
- **Swipe left for Settings,** which slide in under the top bar, grouped in cards with latency first: latency, loop length and tempo, project, performance recording, click, recording, mute timing and microphone. Swipe right, tap Done or tap the logo to go back.

## Latency correction

- **Per recording.** Every recording is shifted back by the latency in force when it was made. Each one keeps its own value, which you can nudge afterwards in steps of 1 or 10 ms while the loop plays, watching the hits line up with the beat lines.
- **Automatic measurement, exact.** The app plays ten clicks and listens for them through the microphone, using a matched filter tuned to the click, so no human timing is involved. Hold the phone's microphone against an earbud and tap Measure exactly. It finds a faint click buried in noise and reports nothing rather than a wrong value when it cannot hear the clicks.
- **Screen latency, for the sampler.** A note played on the screen is late by the headphone delay plus the time the touch takes to reach the app. Measure it once with **Measure by tapping**: the app plays sixteen clicks, you tap along on the beat as you hear it, and the offset of your taps (after the first three) is the screen latency. It sits under the headphone latency in Settings and can be nudged in 1 ms steps; until it is measured it is guessed as the headphone latency plus 70 ms.
- **Microphone choice.** The iPhone microphone is the default, even when headphones with a microphone are connected, and the app switches back to it if the system changes the input. On some iPhones and iPads, Safari moves the sound to the speaker when the phone's microphone starts; Varv then sets the audio session again, which brings the sound back to the headphones. `routetest.html` is a small page for checking how a device routes the sound. Another microphone, such as a USB interface, can be chosen in Settings.

## Loop length

- **Bars.** Tempo 40 to 240 bpm with tap tempo, 1 to 16 beats per bar and 1 to 32 bars per lap, with a click and a one-bar count-in.
- **Bars per track.** In Edit each track can have its own number of bars, for example a 4-bar melody over a 1-bar beat. It records on its own boundaries and its strip shows its own bars and playhead. The setting is fixed once the track holds a recording.
- **Free.** No tempo and no click. The first Record starts at once; play, then tap **End loop** to set the length (up to 30 seconds). Every track then has that length. Since nothing is playing during that first recording, it is not shifted for latency; later recordings are, so they land on the first one.

## Recording

- **One button.** Tap Record and it records lap after lap, each lap into the next empty track (or a new one), until you tap Record again; the lap in progress is then the last. The track waiting for the next lap is marked **auto**. A lap with nothing played in it is thrown away and the same track waits for the next lap, so the tracks fill in order, top down. Hold Record to start or stop playback. This all works from a single pedal button.

- **Hold a track** instead to record exactly one lap into that track.
- **Capture last** keeps the lap you just played even if you never pressed Record.
- **Undo** removes the latest recording. Removed recordings and deleted tracks stay in a bar at the bottom with a Restore button until you dismiss it.
- **Levels.** Input gain (−12 to +30 dB) and an optional 80 Hz low cut sit before the recording. Recordings are kept at the level they were played; automatic levelling is an option. The in and out meters in the top bar turn amber near full scale, red on clipping or when the output limiter has to work hard. Each track shows its own level under its name.
- A live strip shows what the microphone hears, already shifted by the current latency.

## Tracks

- Add tracks before you start, name them and give them their own effects.
- **Hold a track** to record into it from its next lap. The Record button and the pedal fill the empty tracks from the top, then create new ones.
- Recording again into a track that already holds audio adds another take on top (overdub). Each take has its own latency, reverse and remove. With **Overdub** off in Settings, the new take replaces the old one instead, from the moment it starts playing; the earlier takes stay on the track, silent (dimmed in Edit), and Undo brings the previous one back.
- **Mute timing:** mute and solo land on the next bar by default (in free mode: the next pass of the loop), so you can tap a little ahead. In Settings they can instead act immediately or on the next beat.
- Per track, in Edit: name, bars, volume, pan, graphical EQ, filter (darker or thinner), delay send and reverb send, plus the waveform and each take's latency, reverse and remove.
- **Transpose** a track in Edit, under Pitch: octaves (±2), semitones (±11) and a fine tuner in cents (±50). The tempo and the timing stay the same. Every recording on the track is shifted, and the play screen shows the setting under the track name. Double-tap a value to reset it. The shift is computed in the background from the stored recording, so changing it loses nothing; the old version keeps playing until the new one is ready.
- **Autotune** a track in Edit, under Autotune: it pulls a single voice or instrument to the nearest note of a key and scale (major, minor, major pentatonic, or all 12 notes). **Speed** is how fast a note is pulled in (hard gives the robotic effect, slower keeps vibrato and slides) and **Amount** how far. The key is what you hear, after any transposing. A note is held until another is clearly closer, so a voice between two notes does not flicker. Chords confuse it.

## Sampler

At the top of Edit, each track is set to record from the **Microphone** or to be a **Sampler**; the choice is fixed once the track holds recordings or laps. Switching back to Microphone keeps the sample aside for the session, so switching to Sampler again brings it back. On a sampler, tap **Record a sample**, play or sing one sound into the microphone and tap again (or press Record) to stop; it stops by itself after 8 seconds.

- **Auto trim** cuts the silence before and after the sound as soon as it is recorded: it starts 1.5 ms before the attack and ends where the sound has died away. The trim view shows the whole recording with the kept part lit; drag either edge to trim by hand, double-tap it or tap Auto trim to trim automatically again.
- **Pitch.** The pitch of the sample is detected when it is recorded, as a note with cents (YIN, as for autotune), so the keys play in tune from it. Sounds without a clear pitch, like most drums, count as C4. The root note can be moved by hand in semitones; double-tap it to go back to the detected one.
- **Edit options act on the sample.** The track's transpose and autotune are applied to the sample itself, not to each lap, and the sample can be reversed. Transposing keeps the sample's length and the keys move with it. With autotune on, the root is measured again after tuning. Every lap is rendered from the processed sample, so a change is heard on all of them, and recording a new sample keeps the laps already played.
- **Notes:** Full plays the whole sample on every note; Held stops it, with a short fade, when you let go.
- **The pad screen.** Hold a sampler track on the play screen, or tap Play on the screen in Edit, and the pad screen opens over the tracks: either **one big pad** that plays the sample as recorded, or **a keyboard** of one to four octaves stacked in rows, highest at the top, with the root note marked. Every finger plays its own note and sliding along the keys plays each one. The transport stays at the bottom; tap Done or the logo to close it.
- **Recording what you play.** Holding the track records one lap of what you play on the screen, from its next lap. With the pad screen open, Record records lap after lap into the sampler, each lap a take on top of the last (or replacing it, with Overdub off), and laps with nothing played are thrown away; Capture last keeps the lap you just played. While a recording is on (waiting for its lap, counting in or recording) the pads are silent, and framed in red, since anything heard live would be late; each note is placed at its touch time minus the screen latency and the lap plays in time from the next lap on. Otherwise the pads sound at once, to try the sample out.
- Each lap keeps the screen latency it was recorded with and can be nudged afterwards, like a take. The sample and the notes of every lap are saved with the project.

## Graphical EQ

Each track and the master have a three-band EQ drawn as its response curve. Drag the L, M or H handle sideways to set the frequency and up or down to set the level, from −12 to +12 dB; double-tap a handle to return it to its default level and frequency. The low and high bands are shelves and the mid band is a bell. The curve is the real response of the filters, the filter setting included.

## Scenes

Five scene buttons, A to E, sit just above the five transport buttons. Hold one to store which tracks are muted and soloed; tap it to bring that back, following the mute timing setting. A scene that matches the current state lights up. Scenes are saved with the project.

## Master effects

Under Master in the Edit view:

- Volume, graphical EQ and filter.
- Delay: time as 1/16, 1/8, dotted 1/8 or 1/4 note, or free in milliseconds; repeats, level and mix send.
- Reverb: size, level and mix send.
- Compressor: threshold and amount. The click goes through a matching neutral compressor, so click and tracks are delayed by the same few milliseconds and timing is unaffected.

## Projects

- **Everything is saved.** The first recording creates a project named after the date and time, and every change after that is saved automatically: tracks, takes, track settings, scenes, loop length, tempo and master effects. Rename it under Settings. After a reload, a Continue button reopens the last session.
- The raw recordings are stored, not the finished loops, so the latency of every take can still be changed after a project is reopened.
- Projects are stored in the browser on the device (IndexedDB) and are not synced anywhere.
- **Performance recording.** Records everything you hear, without the click, as an audio file. With the microphone included, what you play live is in it too, lined up with the loops by delaying the music by the latency. Recordings are kept under Settings, where you can save or share them.
- Export as a WAV file of the audible tracks, without effects or pan. With tracks of different lengths, the export runs until they all line up again.

## Live use

- The screen stays awake while playing. Large transport buttons: Start, Undo, Record, Capture last and Click on or off.
- Keys, and Bluetooth pedals that send them: <kbd>Space</kbd>, <kbd>R</kbd>, <kbd>Enter</kbd> or <kbd>→</kbd> work like the Record button (tap to record, hold to start or stop), <kbd>←</kbd> or <kbd>Backspace</kbd> undo, <kbd>C</kbd> capture last, <kbd>K</kbd> click, <kbd>1</kbd>–<kbd>9</kbd> mute a track and <kbd>Shift</kbd>+<kbd>1</kbd>–<kbd>9</kbd> solo it, <kbd>E</kbd> edit, <kbd>S</kbd> settings, <kbd>Esc</kbd> back to play, <kbd>P</kbd> performance recording.

## Technical notes

Everything lives in `index.html`, with no build step and no dependencies apart from two web fonts. Recording runs in an AudioWorklet that writes the microphone into a ring buffer indexed by the audio clock, which is what makes sample-accurate alignment possible. The page must be served over https for the microphone to work. `sw.js` makes the app work offline.

A touch on the screen is placed on the audio clock from the event's own time stamp, through `getOutputTimestamp()` where the browser has it; any fixed offset in that mapping is part of the screen latency measured by tapping, so it cancels out. The sampler keeps a log of these events, and a lap of notes collects from it everything played in its window, like a recording reads the microphone ring.

The transposer and the autotune share one engine: pitch detection with YIN, and a phase vocoder with phase locking whose ratio can change over time, processed as a loop so the seam stays smooth, followed by resampling; it runs in a Web Worker. Alignment, measurement, the gestures, the EQ, the transposer, the sampler, projects and the track features are verified with automated tests in Chrome using simulated audio.
