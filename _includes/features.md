
<h2 id="bandwidth-explained">Bandwidth usage explained</h2>

The bandwidth usage/month depends on many factors and can never be guessed without several days of actual running the video chat software on your website:

* number of people online watching cams and how much time they spend watching
* number of people online broadcasting cams and how much time they spend broadcasting
* how many cams a user can see at once
* audio/video quality (128,256,512kbits/s etc…)

For example a user broadcasting its webcam for 30 minutes at 256kbits/s will use  57Mbytes of bandwdith (256kbits/s * 60 seconds * 30 minutes=57Mbytes).

Another user viewing the first one for 30 minutes will use the same amount: 57Mbytes. Total: 114Mbytes for a 30 minute 1 to 1 video chat session.

**Reducing bandwidth usage**

AVChat 3 offers several ways to reduce the monthly bandwidth used on the media server:

* [the automatic bandwidth reduction](http://docs.avchat.net/standalone#dynamic-bandwidth-usage-reduction) feature which is on by default
* you can [lower the audio/video quality for the streams](http://docs.avchat.net/standalone#quality-profiles-explained) so that they use less bandwidth
* you can limit the amount of time/day users can view web cams
* you can limit the amount of web cams users can view at once (4 by default)


<h2 id="delay-latency-display-for-streams">Delay/Latency display for live video streams</h2>

In the side menu for other people’s web cams, AVChat 3 now shows an estimation of how much it takes for the video and audio data to travel from the broadcaster to the viewer (through the media server) . We call this value round-trip time but its also known as latency.

<img src="http://docs.avchat.net/assets/images/rtt.png" class="img-responsive"/>

The value is not always 100% exact but it is a really good estimation!

For one to many broadcasts the trip time value  is not important, live TV broadcasts generally  have a 5-15 seconds delay to give broadcasters time to censor any audio needing censorship

A low trip time is really important when the audio/video communication goes both ways, for example when 2 people are in a video conference. Imagine what would happen if when talking with someone over the phone it would take 5 seconds for your voice to travel from you to the other person.

The trip time in AVChat 3 is influenced by:

* How close the broadcaster and the viewer are to the media server
* Sound quality (paradoxically the higher the better)
* The Internet connection of the broadcaster and the viewer

Round-trip time values you are likely to get when your video chat users are close to the media server and have good, low latency, Internet connections:

* 200 ms on audio+video streams
* 50ms on video only streams

This showing of the round-trip time is controlled by `showVideoFpsInfo` from `avc_settings.xml`. By default it is disabled.

<h2 id="hide-who-is-typing-box">How to hide the who-is-typing box</h2>

<img src="http://docs.avchat.net/assets/images/whoIsTyping.png" class="img-responsive"/>

In `avc_settings.xml` you will find the following setting:

```xml
<showWhoIsTyping>
	<title>showWhoIsTyping</title>
	<name>Show who is typing</name>
	<type>boolean</type>
	<desc>if set to 0, the who is typing bar in the text chat area will not be shown anymore</desc>
	<examples>0 for hidden , 1 for visible</examples>
	<default>1</default>
	<value>1</value>
</showWhoIsTyping>
```

Set it to 0 and the who-is-typing box will not be shown anymore in the chat.

<h2 id="closing-avchat-pop-on-leave">How to close the pop up containing AVChat when clicking the <kbd>Leave</kbd> button</h2>

When AVChat 3 is opened in a pop up window you can use the <kbd>Leave</kbd> button to close the pop up window:

1. Edit `avc_settings.xml`
2. Set `disconnectButtonEnabled` `<value>` to 1;
3. Set `disconnectButtonLink` `<value>` to `javascript:window.close();`

By default clicking <kbd>Leave</kbd> takes you to a new web page instead of closing the window.

<img src="http://docs.avchat.net/assets/images/leave-btn.png" class="img-responsive"/>

<h2 id="recording-video-streams">Recording the video streams</h2>

AVChat 3 uses a media server (like Red5, AMS/FMS and Wowza) to stream audio and video between users. The audio and video data travels from the broadcaster user to the media server and from there to the receiver/viewer. While it passes  through the media server the audio and video data can be captured and stored in `.flv` file,  or, starting with build 2330, in `.mp4` files. The file type that will be created depends on the video codec being used (`Sorenson Spark` or `H.264`).

**Codecs being used**

The audio data will be encoded with the `NellyMoser` or `Speex` codec (depending on your audio settings) and the video data will be encoded with the `Sorenson Spark`  video codec.  Starting with [build 2330](http://avchat.net/blog/avchat-build-2330-introduces-h-264-support/) the `H.264` codec has also been added for video encoding.

The audio and video encoding is done by Flash Player (before it sends the data to the media server) and Flash Player can only encode with those codecs. Flash Player 11.1 or above is required for `H.264` support.

So when the audio and video data hits the media server it is already encoded, the media server just saves the data into `.flv` or `.mp4` files depending on the video codec.

**Enabling audio/video streams recording**

The feature is disabled by default because it tends to use large amounts of space over the time.

On Red5:

1. Edit `avchat30/avchat3.properties`
2. Set `recordAudioVideoStreams=true`
3. Restart Red5

<div class="alert alert-info" role="alert">Red5 will record the streams only in `.flv` format regardless of the video codec used.</div>

You will find the new `.flv` files in Red5/webapps/avchat30/streams/\_definst\_

The `.flv` files are named like this: username+ “\_”+ unique user id assigned by Red5 + “\_”+ timestamp (from when the user started publishing ).

On AMS/FMS

1. Edit `avchat30/settings.asc`
2. Set `recordAudioVideoStreams=true`
3. Reload the avchat30 AMS/FMS application using the AMS/FMS Management Console (or restart AMS/FMS)

FMS 3.5 or higher is required for recording in `.mp4` format and streaming with H.264 encoding.

<div class="alert alert-info" role="alert">FMS will automatically record `.mp4` files if the video codec used is H.264 or `.flv`  files if Sorenson Spark is set.</div>

<div class="alert alert-warning" role="alert">For compatibility with the `H.264` video codec, FMS requires the `NellyMoser ASAO` audio codec to be set. Using `Speex` may cause some files in some cases to not have audio.</div>

You will find the new .flv/.mp4  files in FMS/applications/avchat30/streams/\_definst\_.

The flv/mp4  files are named like this: username+ “\_”+ unique user id assigned by AMS/FMS + “\_”+ timestamp (from when the user connected to AMS/FMS).

On Wowza


1. Edit `Wowza/conf/avchat30/Application.xml`
2. On line 25 change `live-lowlatency` with `live-record` and save
3. Restart Wowza

Wowza will automatically record `.mp4`  files if the video codec used is `H.264` or `.flv` files if Sorenson Spark is set.

<div class="alert alert-warning" role="alert">Wowza doesn’t support adding the `NellyMoser ASAO` audio codec in a `mp4` container. So if the audio-video profile `.xml` is set to record with `H.264` video and `NellyMoser ASAO` audio, the resulting `.mp4` won’t have any audio. To avoid this always use the `Speex` audio codec when using `H.264` video encoding with Wowza.</div>

You will find the new .flv/.mp4  files in this folder: `Wowza/content/`.

As oppsed to AMS/FMS and Red5, by default, the flv/mp4 files are not grouped in folders by application and application-instance like this:

+ Wowza/content/avchat30/\_definst\_
+ Wowza/content/avchat30/\_siteB

To group them like that you need to:

1. Edit `Wowza/conf/avchat30/Application.xml`
2. On line 26 change the default folder path
`${com.wowza.wms.AppHome}/content`
with
`${com.wowza.wms.AppHome}/content/${com.wowza.wms.context.Application}/${com.wowza.wms.context.ApplicationInstance}`
3. Save and restart Wowza.

The .flv/.mp4  files are named like this: username+ “\_”+ unique user id assigned by Wowza.

**Audio video quality**

The media server records whatever gets sent from the client `.swf` file, so to increase the audio/video quality of the recordings you need to increase the audio/video quality used inside the video chat software.

Because you are recording audio/video streams that are destined for live viewing, the quality of the recordings  is not as high as the quality that you get with a dedicated Flash video recording software like our [Flash Video Recorder](https://hdfvr.com). Live streams are maintained as “live” as possible by Flash Player and the media server by dropping video frames and even stopping the video data from being sent to the media server because audio data has higher priority than video data (this will only happen over slow connections tough where audio+video data just doesn’t fit through in a “live” way).

When you have [auto bandwidth reduction](http://docs.avchat.net/standalone#dynamic-bandwidth-usage-reduction) turned on (it’s on by default) streams are passed through the media server only when there is someone watching the respective stream. So even tough user X is broadcasting, his stream will only be recorded if he has one or more viewers. The stream recording process will also stop when user X has no more viewers. You can turn off [auto bandwidth reduction](http://docs.avchat.net/standalone#dynamic-bandwidth-usage-reduction).

**H.264 vs Sorenson Spark**

Advantages:

1. H.264 requires `less bandwidth` than Sorenson Spark
2. H.264 causes `less delay` when streaming between the broadcaster and the receiver
3. H.264 provides `better image quality`, `smoother framerates` and `sharper edges and details`.

Disadvantages:

H.264 is more `CPU intensive` than Sorenson Spark.  Having a lot of streams running at once may cause the AVChat client to have performance drawbacks for users with slower hardware.

**Playing back the recorded files**

FLV

To play back the .flv or .mp4 files on your desktop you can use [VLC](https://www.videolan.org/vlc/index.html).

To play back the .flv or .mp4  files on your website directly from the media server you can use any flash video player for websites that supports streaming. We recommend [JW Player](https://www.jwplayer.com/) or [Flow Player](https://flowplayer.org/). You can also move the video files from your media server to your web server and deliver them to your users via progressive download.

MP4 files recorded with Adobe Media Server

Flash Media Server version 3.5 and later and Adobe Flash Media Live Encoder 3 and later can record content in MPEG-4 (F4V) format using an industry-standard recording technology known as “fragments” or “moof atoms.” Some MPEG-4 compatible tools and players do not support moof atoms and therefore cannot recognize files recorded by Adobe Media Server (previously known as Flash Media Server). [The F4V Post Processor](http://www.adobe.com/products/adobe-media-server-family/tool-downloads.html) tool aggregates the information from all the moof atoms into a single moov atom and outputs a new file. Use the F4V Post Processor tool to prepare F4V files for editing in Adobe Premiere® Pro software, delivery over HTTP, or in video players that support H.264 and AAC formats. This tool can be used in Windows or Linux.

Playing back the files locally before passing them trough the F4V Post Processor tool might not work.

FLV files with no meta data

Because of the way they are recorded, some .flv files will end up having no duration metadata, thus resulting in funny playback. To fix this run those flv files through [flvmdi](http://www.buraks.com/flvmdi/) or [flvtool2](https://github.com/unnu/flvtool2).

<div class="alert alert-info" role="alert" markdown="1">You can also use [FFmpeg](https://www.ffmpeg.org/) which provides a lot of functionality and it's quickly becoming the go to tool for video processing.</div>

<h2 id="dynamic-bandwidth-usage-reduction">Dynamic bandwidth usage reduction explained</h2>

<h2 id="ghost-users-detection">Ghost users and detection mechanism explained</h2>

<h2 id="external-users-list">External users list</h2>

<h2 id="textchat-transcripts">Where are the text chat transcripts</h2>

<h2 id="deleting-textchat-logs">How to delete the text chat logs</h2>

<h2 id="deleting-empty-rooms-automatically">How to delete empty rooms automatically</h2>

<h2 id="edit-add-genders">How to edit/add genders</h2>

<h2 id="login-area">Login area</h2>

<h2 id="setup-facebook-authentication">How to setup AVChat for Facebook authentication</h2>

<h2 id="badnicks-badwords">Badnicks & Badwords</h2>

<h2 id="rotating-messages">Rotating messages feature</h2>

<h2 id="register-tab-disable">Register & Sign in tab disable/enable</h2>

<h2 id="reporting-users">Report user feature</h2>

<h2 id="pay-per-view-api">Pay Per View API</h2>

<h2 id="avchat-twitter-authentication">How to setup AVChat for Twitter authentication</h2>

<h2 id="editing-columns">How to edit columns in the rooms panel</h2>

<h2 id="autostart-webcam">How to make the webcams auto start</h2>

<h2 id="allow-block-video-streaming">Allowing/blocking audio and video streaming</h2>

<h2 id="disabling-mobile-version">How to disable the mobile version</h2>

<h2 id="audio-video-only">Configure AVChat to function with audio and video only</h2>

<h2 id="showing-hiding-rooms">How to hide/show some of the existing rooms</h2>

<h2 id="rooms-music-player">Rooms music player</h2>

<h2 id="enabling-webcam-docking">How to enable webcam docking</h2>

<h2 id="setup-realtime-translation">How to setup Real-Time Translation with Google's Translate API</h2>

<h2 id="setup-for-livestreaming">How to setup AVChat for Live streaming</h2>

<h2 id="accessing-videos-via-http">Accessing the videos via http from the avchat30/streams/\_definst\_ folder (Red5 only)</h2>

<h2 id="stream-recording-api-red5">How to setup AVChat's Stream Recording API (Red5 only)</h2>

<h2 id="autocreate-rooms">The auto-create rooms mechanism</h2>
