The MediaStream can be from:

* A `getUserMedia()` call.
* The receiving end of a WebRTC call.
* A screen recording.
* Web Audio, once [this issue](https://codereview.chromium.org/1579693006) is implemented.

For `options` it's possible to specify the [MIME type](https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder/MediaRecorder) and, in the future, audio and video [bitrates](https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder/MediaRecorder).

MIME types have more or less specific values, combining container and codecs. For example:

* audio/webm
* video/webm
* video/webm;codecs=vp8
* video/webm;codecs=vp9
