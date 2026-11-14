# Varv

A loop station in the browser with latency compensation per layer. Made for listening in Bluetooth headphones while recording with the phone's microphone.

- Click with count-in, tempo, time signature and 1 to 8 bars per lap
- Every lap becomes its own layer, shifted back by the set latency; the latency can be adjusted afterwards per layer
- Latency can be measured, either exactly (the app listens for its own clicks) or by clapping along
- Per layer: mute, volume, three-band EQ, filter, delay, reverb, reverse and delete
- Master: EQ, filter, delay (time, feedback, level), reverb (size, level) and compressor
- Capture the last lap after the fact, undo the latest layer, restore deleted layers, export the lap as WAV
- Keys and Bluetooth pedal: space, R or right arrow, left arrow, C, K, 1 to 9

Everything lives in `index.html`. The page must be opened over https for the microphone to work.
