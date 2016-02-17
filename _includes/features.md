
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

<div class="alert alert-info" role="alert">Red5 will record the streams only in .flv format regardless of the video codec used.</div>

You will find the new `.flv` files in Red5/webapps/avchat30/streams/\_definst\_

The `.flv` files are named like this: username+ “\_”+ unique user id assigned by Red5 + “\_”+ timestamp (from when the user started publishing ).

On AMS/FMS

1. Edit `avchat30/settings.asc`
2. Set `recordAudioVideoStreams=true`
3. Reload the avchat30 AMS/FMS application using the AMS/FMS Management Console (or restart AMS/FMS)

FMS 3.5 or higher is required for recording in `.mp4` format and streaming with H.264 encoding.

<div class="alert alert-info" role="alert">FMS will automatically record .mp4 files if the video codec used is H.264 or .flv  files if Sorenson Spark is set.</div>

<div class="alert alert-warning" role="alert">For compatibility with the H.264 video codec, FMS requires the NellyMoser ASAO audio codec to be set. Using Speex may cause some files in some cases to not have audio.</div>

You will find the new .flv/.mp4  files in FMS/applications/avchat30/streams/\_definst\_.

The flv/mp4  files are named like this: username+ “\_”+ unique user id assigned by AMS/FMS + “\_”+ timestamp (from when the user connected to AMS/FMS).

On Wowza


1. Edit `Wowza/conf/avchat30/Application.xml`
2. On line 25 change `live-lowlatency` with `live-record` and save
3. Restart Wowza

Wowza will automatically record `.mp4`  files if the video codec used is `H.264` or `.flv` files if Sorenson Spark is set.

<div class="alert alert-warning" role="alert">Wowza doesn’t support adding the NellyMoser ASAO audio codec in a mp4 container. So if the audio-video profile .xml is set to record with H.264 video and NellyMoser ASAO audio, the resulting .mp4 won’t have any audio. To avoid this always use the Speex audio codec when using H.264 video encoding with Wowza.</div>

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

Playing back the files locally before passing them through the F4V Post Processor tool might not work.

FLV files with no meta data

Because of the way they are recorded, some .flv files will end up having no duration metadata, thus resulting in funny playback. To fix this run those flv files through [flvmdi](http://www.buraks.com/flvmdi/) or [flvtool2](https://github.com/unnu/flvtool2).

You can also use [FFmpeg](https://www.ffmpeg.org/) which provides a lot of functionality and it's quickly becoming the go to tool for video processing.

<h2 id="dynamic-bandwidth-usage-reduction">Dynamic bandwidth usage reduction explained</h2>

AVChat 3 , as all the other flash video chats out there, uses a media server (like Red5 and AMS) to stream audio and video between users. The audio and video data travels from the broadcaster user to the media server and from there to the receiver user.

Even tough there is no receiver (if there is no one watching) the stream still travels from the broadcaster to the media server, thus consuming bandwidth on the media server and on the broadcaster’s Internet connection.

This is where AVChat 3’s dynamic bandwidth usage reduction kicks in. When this feature is activated (it is on by default) the broadcaster streams audio and video to the media server ONLY WHEN IT HAS VIEWERS.

Here is bandwidth usage graph explaining how this feature works:

<img src="http://docs.avchat.net/assets/images/bw.png" class="img-responsive"/>

1. Users enters chats.
2. User starts the webcam and microphone but no audio and video data is sent yet to the media server.
3. Someone starts watching the broadcast and audio and video data starts being sent to the media server to be routed to the viewer.
4. The viewer stops watching the broadcast and the streaming of audio and video ends as well.

This feature will save a lot of bandwidth over time both on your media server (or media server hosting account) and on your users Internet connections.

To disable it (now why would you want to do that? :) ) edit `avc_setting.xml` and search for the `automaticallyReduceBandwidthUsage` variable. Set it to `0` to disable it.

<h2 id="ghost-users-detection">Ghost users and detection mechanism explained</h2>

Ghost users are a known issue with all media servers.

**What is a ghost user?**

A ghost user is a user who’s disconnection from the media server has not been detected by the media server, thus the media server thinks he is still connected.

In a chat you will know there are ghost users when you see 2-3 persons in the users list having the same user name or persons staying for unusual lenghts of time in the chat without activity.

**What causes ghost users?**

They happen when a user suddenly disconnects from the Internet while connected to a media server (for example by suddenly disconnecting your Ethernet cable or loosing WiFi signal) but in other occasions too like when the user is over a slow connection (mobile connections) or behind some weird combination of network hardware + server software. IE and the way it handles Flash content might also produce ghost users.

**How is AVChat 3 dealing with ghost users?**

1. Every 3 seconds the client  (swf file) sends a ping to the media server (this value can not be changed)
2. Every 10 seconds the media server (Red5/Wowza/AMS/FMS) check if all clients have sent a ping within the last 10 seconds (already 3 pings should have been sent by every client) and disconnects everyone who has not.

This means that no ghost user will ever stay in the chat for more than 20 seconds.

Starting with build 741 (April) you can control the above mechanism by changing the value of the `checkForGhostConnectionsEveryXSeconds` and `ghostUsersAreIdleForYSeconds` variables in `settings.asc` (AMS/FMS) or `avchat3.properties` (Red5 and Wowza). If your users seem to get disconnected for no apparent reason increase the value of `ghostUsersAreIdleForYSeconds` to 20 seconds for example. Both variables are set by default to 10 seconds.

<h2 id="external-users-list">External users list</h2>

**Overview**

In order to show on your website who is logged in the video chat, AVChat 3 generates 2 external files in the folder where it is installed:

* `users__definst_.txt` -> a text file containing the number of unique users connected to the video chat
* `users__definst_.xml` -> an XML file containing the list of rooms and users in each room

You will see these files ONLY AFTER THE FIRST USER (NOT ADMIN) LOGS IN THE VIDEO CHAT!

Starting with [build 2768](http://nusofthq.com/blog/avchat-august-update-build-2768/) the external users list is generated even if someone joins the chat through the admin interface.

You can use these 2 files to show on your website how many clients are logged in, the room structure or which clients are logged in.

How to actually code/do that is outside the scope of this documentation but anyone with minimum PHP or .NET experience  should be able to parse the XML/text file and post the contents on the website.

**How it works**

In detail:

1. User joins the video chat via `index.swf`, the path to the `writeuserslist.php` is automatically detected.
2. User joins a room, the media server sends the new  rooms/users structure to `writeuserslist.php` via POST (using the path detected at step 1).
3. `writeuserslist.php` receives the new info via POST and creates the 2 files on the web server.

One some of our integration kits `admin.swf` and `writeuserslist.php` are placed in separate folders, that’s why admins logging in do not trigger an attempt to detect the path to `writeuserslist.php`.

Admins and users are properly listed in the external `.xml` file as long as at least a user has logged in in the past so that the media server knows where `writeuserslist.php` is located.

You can also set the path manually (via the `settings.asc`/`avchat3.properties` files on the media server) and you should when:

+ You’re using `writeuserslist.asp` (or any other scripting language) instead of `writeuserslist.php`.
+ You’ve moved `writeuserslist.php` to a separate folder.
+ You have troubles with the external users list not being generated.

**Troubleshooting**

If the 2 files refuse to appear do these tasks in this order:

1. Log in the video chat through the user interface (not the admin interface/area)
2. Make sure the folder containing `writeuserslist.php` is `chmoded` to `755` so that `writeuserslist.php` can write/crate new files
3. Make sure calls to the new info is POST-ed from the media server to the web server (check Apache logs)
4. Make sure the folder where `writeuserslist.php` is located is not password protected!
5. Hard code the path to `writeuserslist.php`  in `settings.asc` (on AMS/FMS ) or in `avchat3.properties` (on Wowza/Red5) and restart the media server
6. Contact support: support@nusofthq.com

**Turning the feature off**

On AMS/FMS  edit `applications/avchat30/settings.asc`, set `application.writeUsersLists=false` and restart AMS/FMS.

On Red5 edit `webapps/avchat30/avchat3.properties`, set `writeUsersLists=false` and restart Red5.

On Wowza edit `conf/avchat30/avchat3.properties`, set `writeUsersLists=false` and restart Wowza.

This will turn off the feature and stop the media server from making POST calls to the web server.

<h2 id="textchat-transcripts">Where are the text chat transcripts</h2>

AVChat saves a history of all the text chat in all the rooms including private chats on the media server!

**On AMS/FMS**

They will be saved in the `FMS/applications/avchat30/logs/` folder and they will have this format: `_definst__r0_2010_12_20.txt`, where \_definst\_ is the application instance name, r0 is the room id, and 2010_12_20 is the date.

To disable it edit `applications/avchat30/settings.asc` and set `application.loggingEnabled=false`.

**On Red5**

They will be saved in `Red5/webapps/avchat30/avchat3_transcripts/` folder and they will have this format: `_definst__r0_2010_12_19_log.txt`.

To disable it edit `webapps/avchat30/avchat3.properties` and set `loggingEnabled=false`.

**On Wowza**

They will be saved in `Wowza\applications\avchat30\avchat3_transcripts` folder and they will have this format: `_definst__r0_2010_12_19_log.txt`.

To disable it edit `conf/avchat30/avchat3.properties` and set `loggingEnabled=false`.


<h2 id="deleting-textchat-logs">How to delete the text chat logs</h2>

You have 2 options here.

First of them and the most easier is to access the AVChat admin interface and click the little broom button in the down-right corner.

This action will delete all the exisiting messages from all rooms instantly.

<img src="http://docs.avchat.net/assets/images/eall.png" class="img-responsive"/>

The second option is to connect to your server by SSH, access the text chat transcripts folder, delete the files manually and restart the media server.

You will find the text chat transcripts by the filename which is in the format `r0textchat`.
The path to these files is:

* `avchat30/SharedObjects/_definst_` on Red5
* `avchat30/sharedobjects/_definst_` on FMS/AMS
* `applications/avchat30/sharedobjects/_definst_` on Wowza

The files extensions are:

* `.red5` on Red5
* `.fso` on FMS/AMS
* `.rso` on Wowza


<h2 id="deleting-empty-rooms-automatically">How to delete empty rooms automatically</h2>

Starting with [build 2160](http://nusofthq.com/blog/avchat-build-2160-has-arrived/) the delete empty rooms mechanism has been redone:

The media server now constantly checks for empty rooms and if:
* `deleteRoomsWhenTheyBecomeEmpty = true`
* the room is not protected (not included in the `doNotDeleteTheseRoomsWhenTheyBecomeEmpty`array) and
* is inactive for more than the number of hours set in the option `deleteEmptyInactiveRoomsOlderThan` then the room is deleted.

~~AVChat can be set up to remove empty rooms automatically as soon as the last person leaves the room.~~

By default this feature is turned off. To turn it on you need to edit the config file on the media server (`avchat3.properties on Red5/Wowza` and `settings.asc` on AMS/FMS) and set

`deleteRoomsWhenTheyBecomeEmpty=true`

You can also use the `doNotDeleteTheseRoomsWhenTheyBecomeEmpty` option to protect some rooms (like the main Lobby) from being removed like this:

Red5 & Wowza:

`doNotDeleteTheseRoomsWhenTheyBecomeEmpty=r1,r2`

FMS:

`application.doNotDeleteTheseRoomsWhenTheyBecomeEmpty=["r1","r2"]`

More details about each of the above config options and the exact syntax are in the config files. The location of the config files is detailed [here](http://docs.avchat.net/standalone#config-files).


<h2 id="edit-add-genders">How to edit/add genders</h2>


Starting with [build 1880](http://nusofthq.com/blog/new-avchat-november-build-1880-has-arrived) AVChat loads the genders from a `genders.xml` file. AVChat comes with a couple of predefined genders, but these can be edited or removed, and others can be added. As explained in the XML file, the only thing that should not be changed are the `IDs` of the male, admin, unknown and hidden genders, but other attributes of these genders can be changed such as the `iconUrl` or the `sortPriority`.

To add a new gender, simply add a new line in the XML file specifying all the attributes like so:

```xml
<gender id="female" label="Girl" iconUrl="gender_icons/girl.png" adminOnly="false" sortPriority="c" outlineColor ="0x577ce5" />
```

<div class="alert alert-warning" role="alert">Don't forget to add the icon image in the folder that you specified in the iconUrl attribute, otherwise the icon image won't load and won't be available to be displayed in AVChat. The recommended image icon size is 32x32px.</div>


<h2 id="login-area">Login area</h2>


Starting with [build 1880](http://nusofthq.com/blog/new-avchat-november-build-1880-has-arrived) AVChat 3 has a new and more customizable login area, with 2 main screens, which can be activated using the tab at the top : Enter as guest and Sign in & Register.

The default selected tab can be set using the setting in `avc_settings.xml` `selectedTabInLoginScreen`.

Also if the setting `showLoginError` is enabled the Enter as guest screen and corresponding tab disappear altogether.

The Enter as guest tab contains the textfield for the username, the gender selection that is customizable (see 6.12 for more details), the connect button and a new zone that allows the use of other existing accounts such as Facebook, for the authentication of users. This zone can also be enabled/disabled with `enableOtherAccountOptions` from `avc_settings.xml`.

The Sign in & Register tab contains the register and sign in buttons that redirect the users to the respective areas of the site.

To add the sign URL set `loginPageURL` in `avc_settings.xml`

To add the register URL set `registerPageURL` in `avc_settings.xml`.


<h2 id="setup-facebook-authentication">How to setup AVChat for Facebook authentication</h2>

Starting with [build 1880](http://nusofthq.com/blog/new-avchat-november-build-1880-has-arrived) AVChat 3 supports Facebook authentication.

This feature allows your users to connect to your AVChat area using their Facebook account.

Clicking the Facebook button in the login screen will open a popup asking for user's Facebook credentials. If he is already signed in on that browser, the connection will be done automatically.

<img src="http://docs.avchat.net/assets/images/fblogin.png" class="img-responsive"/>

AVChat 3 will now will use the name, profile picture and profile link from Facebook.

<img src="http://docs.avchat.net/assets/images/fb_profile.png" class="img-responsive"/>

This feature is controlled by the `enableOtherAccountOptions` setting located in the `avc_settings.xml` file.
If set to `0`, the feature will be disabled.

**There a few steps needed in order to set this up:**

1. Go to:  [https://developers.facebook.com/apps/](https://developers.facebook.com/apps/)
2. Create a new Facebook app for a website and enter a name for it.
3. In the new screen that shows up enter click <kbd>Create New Facebook APP ID</kbd>
4. Choose a category in the new screen and click <kbd>Create App ID</kbd>
5. You will be taken into a more advance setup screen but AVChat already has all the code needed so you can press <kbd>Skip Quick Start</kbd>
<img src="http://docs.avchat.net/assets/images/skip-start.png" class="img-responsive"/>
6. You wil be taken to your app Dashboard page. Click the <kbd>Settings</kbd> button
<img src="http://docs.avchat.net/assets/images/fb-dashboard.png" class="img-responsive"/>

7. Make sure a your site URL is typed in in the input, if not add it and click <kbd>Save Changes </kbd>
8. Open up the `index.html`
9. Find the line where the `appId` is specified and replace the existing app ID with the Facebook generated one for your personal app.
10. Save the file.

<div class="alert alert-info" role="alert">.Also note that in order for the Facebook based login to work for the admin interface (admin.swf and admin.html) the same modifications need to be made to admin.html</div>

<h2 id="badnicks-badwords">Badnicks & Badwords</h2>


AVChat 3 has 2 configuration files containing usernames and words which are not allowed to be used as nicknames or in the text chat.

We're talking about 2 separate files: `badnicks.xml` and `badwords.xml`.
Both files can be found in the main AVChat 3 installation folder.

**Bad nicks**

`badnicks.xml` - contains 2 groups of XML elements:

* `<nicks>` - the exact usernames defined there will not be allowed in chat
* `<widcards>` - usernames containing that wildcard string will not be allowed in chat.

Any username found either in the `<nicks>` or in the `<widcards>` tags will not be allowed in chat.

Bad nick example: `<bad>john</bad>` - meaning that any user trying to connect with username "john" will not be allowed.

Wildcard example: `<bad>adr</bad>` - meaning any user trying to connect with an username containing "adr" (adrian, adrienne) will not be allowed.

Only the user interface (`index.swf`) will check the member's username against the usernames in `badnicks.xml`. The admin interface (`admin.swf`) does not apply the check, so if the "admin" or "administrator" usernames are present in `badnicks.xml` they can be used in `admin.swf` but `index.swf` will not let users with these usernames go past the login screen.

**Bad words**

`badwords.xml` - contains 2 groups of XML elements as well:

* `<words>` - words defined there will not be allowed in chat
* `<widcards>` - words containing the wildcard will not be allowed.

If some user uses in chat a word from that list you have created, it will be replaced with asterisks (\***).

The badwords check also applies to admins.


<h2 id="rotating-messages">Rotating messages feature</h2>

AVChat 3 has a feature which gives the possibility for the owner to add info messages, text ads with links or any announcements.

This feature was added in [Build 1505](http://avchathq.com/blog/rotatting-text-messages-in-avchat-may-build-1505/) of AVChat 3 to give the website owner the ability to add info messages, text ads with links or any other announcements in the text chat.

**In detail**

The file which stores the messages is `rotate_messages.php` located in the AVChat 3 installation folder. It is called by AVChat 3 every `rotatingMessageTime` seconds (option in `avc_settings.xml`) and it sends to it a GET variable named `count` which stores the number of times it was called by that user.

The file comes by default with several messages. These can all be replaced and more can be added.

To replace the messages, open `rotate_messages.php` with a text editor and replace the text between the quotes, without affecting the PHP code.

Here’s the default file with the text that you should edit highlighted:

<img src="http://docs.avchat.net/assets/images/rotate_messages.png" class="img-responsive"/>

If you’ve edited the 6 default messages and you want to add more here’s what you need to do:

+ Duplicate the last case (case 0, lines 29-31 above) and replace 0 with 6 like this:

```php
case 6:
echo "<font color='#999999' face='Tahoma' size='11' ><b>A new message.</b></font>";
break;
```

+ On line 13 change the number 6 with 7 like this:
`switch ($count%7)`

As you can see, you can customize these messages using some HTML tags for color, font, size, etc. The supported list of HTML tags that can be used can be found [here](http://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/text/TextField.html#htmlText).

If you are an experienced web developer you can create your own `rotate_messages.php` file with messages being pulled out of a database, more complex logic, ads, etc. and point AVChat 3 to use it through the `rotatingMessageUrl` option located in `avc_settings.xml`.

**Other notes**


* `rotatingMessageUrl` in `avc_settings.xml` contains the path to `rotating_messages.php`
* To disable the feature open `avc_settings.xml` file with a text editor and set `rotatingMessageTime` to `0` (`<value>0</value>`)
* To increase the time between calls to `rotate_messages.php` open `avc_settings.xml` file with a text editor and set `rotatingMessageTime` to `120` (`<value>120</value>`) which means 2 minutes between calls or any other value in seconds.


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
