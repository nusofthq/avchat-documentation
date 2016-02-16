
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

<h2 id="closing-avchat-pop-on-leave">How to close the pop up containing AVChat when clicking the [Leave] button</h2>

<h2 id="recording-video-streams">Recording the video streams</h2>

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
