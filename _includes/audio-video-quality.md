
AVChat (through Flash Player) captures raw audio and video data from your web cam and microphone, encodes it, and sends it to the media server from where it is sent to the other users.

For encoding the video data AVChat can use `Sorenson Spark` and `H.264`. For encoding audio data AVChat can use the `Speex` and the `NellyMoser ASAO` audio codecs.

AVChat puts no limits on the audio video quality experienced by your users and in that spirit it opens up all the available audio and video settings to you to play with. You can change the video resolution, picture quality, frame rate and sound quality.

Read below to learn how to play with all those settings and more.


<h2 id="quality-profiles-explained">Audio/video quality profile files explained</h2>

In the installation folder of AVChat you will find a folder named `audio_video_quality_profiles`. It contains several XML files. We call these XML files audio video quality profiles.

Each XML file contains the settings (resolution, frames per second, picture and sound quality, etc.) used to encode the video/audio data that's coming from your computer's webcam and microphone. AVChat ships with several such profile files that you can use out of the box each configured to give you the best possible audio and video quality at a certain data rate from 96kbits/s to 768kbits/s.

The default audio/video profile used by AVChat is `512k_high_motion_medium_picture_quality_high_sound_quality.xml`. This profile will consume (for one stream) maximum 469kbits/s for video and 42 Kbits/s for audio, total: 511kbits/s.

To make AVChat use another audio/video quality profile file for when users start broadcasting their web cam and microphone you need to change the value of the `miccamsettingsurl` variable inside `avc_settings.xml` to point to the XML file of your choice.

You can also make your own quality profiles or edit the existing ones.


<h2 id="editing-existing-quality-profiles">Editing existing quality profile files</h2>

Each of the quality profile files has the exact same XML structure:

```xml
<item>
   <nm>128 ISDN</nm>
   <df>0</df>
   <bytes>16000</bytes>
   <q>0</q>
   <fps>7</fps>
   <kfps>28</kfps>
   <w>200</w>
   <h>150</h>
   <displayWidth>256</displayWidth>
   <displayHeight>192</displayHeight>
   <snd>speex6</snd>
   <sndSilencelevel>0</sndSilencelevel>
   <vcodec>sorenson</vcodec>
</item>
```

Each node/value pair explained:

**Video settings**
* `<bytes>` This is the maximum amount of bytes that the video (not audio) can consume per second. If it is set to 0, the video stream from the user to the media server will consume as much bandwidth as possible to maintain the picture quality. Multiply by 8 to get the value in bits.
* `<q>` This is the picture quality. If set to 0 it will use as much quality as possible, without exceeding the <bytes> value. Maximum is 100 but that will consume EXCESSIVE bandwidth. A value between 85-95 will produce really good picture quality!
* `<fps>` This defines the video frame rate. 10, 15, 30 fps, etc... . Some old web cams can only capture up to 15fps.
* `<kfps>` Key frames. This tells AVChat that every <kfps> frames a full frame will be sent to the media server . The rest of the frames contain just the changes from the previous frame.
* `<w>` The desired width of the captured video in pixels
* `<h>` The desired height of the captured video in pixels
* `<displayWidth>` The desired width of the video display
* `<displayHeight>` The desired height of the video display
* `<othersDisplayScale>` controls the scale of the video that is represented by an incoming stream ( the stream you are watching). By default it size of the video window will be that of the native resolution the broadcaster is transmiting in. If that size creates a window too large for example ( 1280 x 720 ), this can be scaled down by using a lower value for othersDisplayScale i.e. 0.25
* `<vcodec>` The video codec used to encode the live stream, with possible values being `sorenson` or `h264`. Use the h264 value to encode video with H.264 codec (Main Profile with Level 3_1 are used, for more details click [here](http://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Profiles)) (This setting has been added in [build 2330](http://nusofthq.com/blog/avchat-build-2330-introduces-h-264-support/))

**Audio settings**
* `<snd>` The sound rate. The higher the better but it also consume more bandwidth.

  The snd tag controls the quality/bandwidth of audio.Flash Player supports encoding sound in 2 codecs: `NellyMoser` and `Speex`.

  Speex is newer,better and open source, that's why its used by default.

  Possible values:
  *  44 : NellyMoser, highest quality
  *  22 : NellyMoser, medium high quality
  *  11 : NellyMoser, medium low quality
  *  8 : NellyMoser, low quality
  *  5 : NellyMoser, lowest quality
  *  speex10 : Speex, default value for this profile, highest quality, uses 42.2kbits/s of bandwidth
  *  speex9 : 34.2kbits/s
  *  speex8 : 27.8kbits/s
  *  speex7 : 23.8kbits/s
  *  speex6 : Speex, uses 20.6kbits/s of bandwidth
  *  speex5 : 16.8kbits/s
  *  speex4 : 12.8kbits/s
  *  speex3 : Speex, low quality, lowest usable quality, uses 9.80kbits/s
  *  speex2 : 7.75kbits/s
  *  speex1 : 5.75kbits/s
  *  speex0 : Speex, lowest quality, not really usable, uses 3.95kbits/s
* `<sndSilencelevel>` Takes values from 0 to 100. Flash Player will consider any sound that is lower than the value of this tag as "silence" and thus will not send any data to the media server. Use 100 if you want to never send audio to the media server. Use 0 if you always want to send to the media server whatever the mic captures (even noise). We recommend using 0 since if you use the default (10) Flash Player will stop broadcasting sound when you stop speaking. Even though this seems like a cool feature that cuts bandwidth in reality the listeners will frequently get the feeling that you've been cut off.

**Misc settings**
* `<nm>` This is the name of the connection type. The value of this tag is not used in AVChat.
* `<df>` If set to 1, this will be the connection type that will be used by default. The value of this tag is not used in AVChat.

To edit a quality profile file open it in Notepad or any other text editor, change the value that you want to change, save it back to the web server. Now reload AVChat in the browser and start your webcam, you should see the changes in effect.

<h2 id="making-custom-quality-profiles">Making your own quality profile file</h2>


To make your own audio video quality profile, duplicate one of the existing XML quality files, give it a unique name and edit it with a text editor. To use it, upload it to your web server and set the value of the `miccamsettingsurl` variable in the `avc_settings.php/aspx.cs` configuration file to it.

You can use one quality profile file with higher quality video for "gold" users and one with lower quality video for "free" users for example.
