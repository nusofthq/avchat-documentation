
<p class="lead" markdown="1">AVChat (through Flash Player) captures raw audio and video data from your web cam and microphone, encodes it, and sends it to the media server from where it is sent to the other users. AVChat puts no limits on the audio video quality experienced by your users and in that spirit it opens up all the available audio and video settings for you to play with. You can change the video resolution, picture quality, frame rate, sound rate and a lot more.</p>

For encoding video AVChat can use the **Sorenson Spark** and **H.264** codecs. For encoding audio AVChat can use the **Speex** and **Nellymoser ASAO** audio codecs.

<h2 id="quality-profiles-explained">Audio/video quality profile files explained</h2>

In the installation folder of AVChat you will find a folder named `audio_video_quality_profiles`. It contains several XML files. We call these XML files **audio video quality profiles** because they define a certain set of audio and video quality settings.

Each XML file contains the parameters (resolution, frames per second, picture and sound quality, etc.) used to encode the video/audio data that's coming from your computer's webcam and microphone. AVChat ships with several such profile files that you can use out of the box each configured to give you the best possible audio and video quality at several data rates from 96kbits/s to 768kbits/s.

The default audio/video profile used by AVChat is `512k_high_motion_medium_picture_quality_high_sound_quality.xml`. This profile will consume (for one stream) maximum 469kbits/s for video and 42 Kbits/s for audio, total: 511kbits/s.

To make AVChat standalone use another audio/video quality profile file you need to change the value of the `miccamsettingsurl` variable inside `avc_settings.xml` to point to the XML file of your choice. You can also make your own quality profiles or edit the existing ones.

<h2 id="editing-existing-quality-profiles">Editing existing quality profile files</h2>

Each of the quality profile files has the exact same XML structure:

{% highlight xml %}
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
{% endhighlight %}

Each node/value pair explained:

### Video settings


<dl class="dl-horizontal">
  <dt>bytes</dt>
  <dd>The maximum amount of bytes that the video (excluding audio) can use per second. If set to 0, the video encoder will allocate as much data/s as possible to maintain the picture quality. Multiply by 8 to get the value in bits.</dd>
  <dt>q</dt>
  <dd>The picture quality. If set to 0 the encoder will use as much quality as possible, without exceeding the **bytes** value. Maximum is 100 but that will consume excessive bandwidth. A value between 85-95 will result in great picture quality without the high bandwidth usage.</dd>
  <dt>fps</dt>
  <dd>The video frame rate. 10, 15, 30 fps, etc... . Some old web cams can only capture up to 15fps.</dd>
  <dt>kfps</dt>
  <dd>Key frames. This tells AVChat that every **kfps** frames a full frame will be encoded in the video stream. The rest of the frames contain just the changes from the previous frame.</dd>
  <dt>w</dt>
  <dd>The desired width of the captured video in pixels</dd>
  <dt>h</dt>
  <dd>The desired height of the captured video in pixels</dd>
  <dt>displayWidth</dt>
  <dd>The desired width of the video display</dd>
  <dt>displayHeight</dt>
  <dd>The desired height of the video display</dd>
  <dt>othersDisplayScale</dt>
  <dd>controls the scale of the video that is represented by an incoming stream ( the stream you are watching). By default it size of the video window will be that of the native resolution the broadcaster is transmiting in. If that size creates a window too large for example ( 1280 x 720 ), this can be scaled down by using a lower value for othersDisplayScale i.e. 0.25</dd>
  <dt>vcodec</dt>
  <dd markdown="1">
  The video codec used to encode the live stream, with possible values being `sorenson` or `h264`. Use the h264 value to encode video with H.264 video codec (Main Profile with Level 3_1 are used
  </dd>
</dl>

### Audio settings

<dl class="dl-horizontal">
  <dt>snd</dt>
  <dd markdown="1">

  The `snd` tag controls the audio codec and sample rate/bandwidth of audio. Flash Player supports encoding sound in 2 codecs:
  * Nellymoser ASAO
  * Speex

  When using the **Nellymoser ASAO** codec you can choose between five different microphone sample rate values: 5, 8, 11, 22 and 44.

  **Speex** on the other hand has a fixed sampling rate of 16kHz. Speex allows control of the quality by offering us 11 different encoding quality options, from 0 to 10. Each setting translates to a different bitrate.

  Possible values for `snd`:

  *  44 : Nellymoser, 44kHz sample rate (highest quality for Nellymoser)
  *  22 : Nellymoser, 22kHz sample rate
  *  11 : Nellymoser, 11kHz sample rate
  *  8 : Nellymoser, 8kHz sample rate (low quality)
  *  5 : Nellymoser, 5kHz sample rate (lowest quality)
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

  </dd>
  <dt>sndSilencelevel</dt>
  <dd>Takes values from 0 to 100. Flash Player will consider any sound that is lower than the value of this tag as "silence" and thus will not send any data to the media server. Use 100 if you want to never send audio to the media server. Use 0 if you always want to send to the media server whatever the mic captures (even noise). We recommend using 0 since if you use the default (10) Flash Player will stop broadcasting sound when you stop speaking. Even though this seems like a cool feature that cuts bandwidth in reality the listeners will frequently get the feeling that you've been cut off.</dd>
</dl>

To edit a quality profile file open it in Notepad or any other text editor, change the value that you want to change, save it back to the web server. Now reload AVChat in the browser and start your webcam, you should now see the changes.

<h2 id="making-custom-quality-profiles">Making your own quality profile file</h2>


To make your own audio video quality profile, duplicate one of the existing XML quality files, give it a unique name and edit it with a text editor. To use it, upload it to your web server and set the value of the `miccamsettingsurl` variable in `avc_settings.xml` configuration file to it.
