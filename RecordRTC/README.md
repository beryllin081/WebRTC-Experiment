#### RecordRTC: WebRTC audio/video recording / [Demo](https://www.webrtc-experiment.com/RecordRTC/)

**RecordRTC** is a library for cross-browser audio/video recording.

=

##### Features

1. You can record audio in WAV/OGG format
2. You can record video in WebM format
3. You can record video as animated GIF image

=

##### How to use RecordRTC?

```html
<script src="https://www.webrtc-experiment.com/RecordRTC.js"></script>
```

=

##### How to record audio?

```javascript
var recorder = RecordRTC(mediaStream);

// start recording audio
recorder.startRecording();

// stop recording audio
recorder.stopRecording(function(audioURL) {
   window.open(audioURL);
});
```

=

##### How to record video?

```javascript
var recorder = RecordRTC(mediaStream, {
   type: 'video',
   width: 320,
   height: 240
});

// start recording video
recorder.startRecording();

// stop recording video
recorder.stopRecording(function(videoURL) {
   window.open(videoURL);
});

// force saving recorded stream to disk
recorder.save();
```

=

##### How to record animated GIF image?

```javascript
var recorder = RecordRTC(mediaStream, {
   type: 'gif',
   
   width: 320,
   height: 240,
   
   frameRate: 200,
   quality: 10
});

// start recording gif
recorder.startRecording();

// stop recording gif
recorder.stopRecording(function(gifURL) {
   window.open(gifURL);
});
```

=

##### Get Data URL

```javascript
window.open( recorder.getDataURL() );
```

=

##### Get Blob object

```javascript
blob = recorder.getBlob();
```

=

##### POST on server

```javascript
blob = recorder.getBlob();

formData = new FormData();
formData.append('file-name', blob);

xhr.send(formData);
```

=

##### Get Virtual URL

```javascript
window.open( recorder.toURL() );
```

=

##### Save to Disk

```javascript
recorder.save();
```

=

##### WinXP?

No WinXP support. Try to use Vista, Windows 7 or Windows 8.

=

##### Stereo or Mono?

Audio recording fails for `mono` audio. So, try `stereo` audio only.

=

##### Possible issues/failures:

Do you know "RecordRTC" fails recording audio because following conditions fails:

1. Sample rate and channel configuration must be the same for input and output sides on Windows i.e. audio input/output devices mismatch
2. Only the Default microphone device can be used for capturing.
3. The requesting scheme is none of the following: http, https, chrome, extension's, or file (only works with `--allow-file-access-from-files`)
4. The browser cannot create/initialize the metadata database for the API under the profile directory

If you see this error message: `Uncaught Error: SecurityError: DOM Exception 18`; it means that you're using `HTTP`; whilst your webpage is loading worker file (i.e. `audio-recorder.js`) from `HTTPS`. Both files's (i.e. `RecordRTC.js` and `audio-recorder.js`) scheme MUST be same!

=

##### Saving to disk failures:

1. You're using chrome `incognito` mode
2. **RecordRTC** created **duplicate** temporary file
3. The requesting scheme is none of the following: `http`, `https`, `chrome`, extension's, or `file` (only works with `--allow-file-access-from-files`)
4. The browser cannot create/initialize the metadata database for the API under the profile directory

Click **Save to Disk** button; new tab will open; **right-click** over video and choose **Save video as...** option from context menu.

=

##### Web Audio APIs requirements

1. If you're on Windows, you have to be running Windows Vista or better (will not work on Windows XP).
2. On Windows, audio input hardware must be set to the same sample rate as audio output hardware.
3. On Mac and Windows, the audio input device must be at least stereo (i.e. a mono/single-channel USB microphone WILL NOT work).

=

##### Why stereo?

If you explorer chromium code; you'll see that some APIs can only be successfully called for `WAV` files with `stereo` audio.

Stereo audio is only supported for WAV files.

...still investigating the actual issue of failure with `mono` audio.

=

##### Browser Support

[RecordRTC Demo](https://www.webrtc-experiment.com/RecordRTC/) works fine on following web-browsers:

| Browser        | Support           |
| ------------- |-------------|
| Google Chrome | [Stable](https://www.google.com/intl/en_uk/chrome/browser/) / [Canary](https://www.google.com/intl/en/chrome/browser/canary.html) / [Beta](https://www.google.com/intl/en/chrome/browser/beta.html) / [Dev](https://www.google.com/intl/en/chrome/browser/index.html?extra=devchannel#eula) |
| Firefox | [Nightly](http://nightly.mozilla.org/) |

=

##### Credits

1. [Recorderjs](https://github.com/mattdiamond/Recorderjs) for audio recording
2. [whammy](https://github.com/antimatter15/whammy) for video recording
3. [jsGif](https://github.com/antimatter15/jsgif) for video recording

=

##### Spec & Reference

1. [Web Audio API](https://dvcs.w3.org/hg/audio/raw-file/tip/webaudio/specification.html)
2. [MediaRecorder](https://wiki.mozilla.org/Gecko:MediaRecorder)
3. [Canvas2D](http://www.w3.org/html/wg/drafts/2dcontext/html5_canvas/)
4. [MediaStream Recording](https://dvcs.w3.org/hg/dap/raw-file/tip/media-stream-capture/MediaRecorder.html)
5. [Media Capture and Streams](http://www.w3.org/TR/mediacapture-streams/)

=

##### License

[RecordRTC](https://www.webrtc-experiment.com/RecordRTC/) is released under [MIT licence](https://www.webrtc-experiment.com/licence/) . Copyright (c) 2013 [Muaz Khan](https://plus.google.com/100325991024054712503).
