
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

<img src="http://docs.avchat.net/assets/images/fbProfile.png" class="img-responsive"/>

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
<img src="http://docs.avchat.net/assets/images/app-dashboard.png" class="img-responsive"/>

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

You can disable the register tab using the setting `enableRegisterTab` and found in the `avc_settings.xml` file.

To disable the tab:

1. Open the file with a text editor.
2. Search for `enableRegisterTab`.
3. Set it's `<value>` tag to `0`.
4. Save the file and upload it back to the server.

Example:

```xml
<enableRegisterTab>
	<title>enableRegisterTab</title>
	<name>Enable register tab</name>
	<type>boolean</type>
	<desc>controls the status (enabled, disabled) of the Register and Sign-in tab (the second tab)</desc>
	<values>0 for disabled, 1 for enabled</values>
	<default>1</default>
	<value>0</value>
</enableRegisterTab>
```

You can also translate the tab's label and it's content to use it in some other purpose.
The text used in this tab can be found in `translations/en.xml` file located in the AVChat installation folder.

<h2 id="reporting-users">Report user feature</h2>

**Sending a report**

Starting with [build 2760](http://nusofthq.com/blog/avchat-august-build-2760/) a user can be reported by any other user if necessary. This options is easily accessed by pressing the <kbd>Report this user</kbd> button located in a user's side menu.

<img src="http://docs.avchat.net/assets/images/report.png" class="img-responsive"/>

The same button can also be accessed directly from the user's web-cam window.

<img src="http://docs.avchat.net/assets/images/reportFromCam.png" class="img-responsive"/>

Once pressed a window opens that allows the following:

* Selecting a report reason
* Adding more information of why the user is reported in the limit of 200 characters
<img src="http://docs.avchat.net/assets/images/reportW.png" class="img-responsive"/>

Pressing <kbd>Report</kbd> will send the report, <kbd>Cancel</kbd> will cancel the sending.

Upon sending the report, automatically, two screenshots are taken:

* A screenshot of the text-chat area
* A screenshot of the reported user's web-cam

These screenshots are sent to the web-server and can be found in the AVChat installation directory in the folder named report_snaps. The filename is composed of the user's siteId and the screenshot type (CAM or TEXT), so a screenshot will be named like so: `userSitedId_CAM.jpg` and `userSitedId_TEXT.jpg`

All of the information of the report is also available through a PHP API, the file `sendReport.php`. This file can be configured to send an automatic email with the data of the reported user along with links to the two above mentioned screenshots. By default the code for the email sending is commented. It can also be customized to be used in any other way it is seen fit.

The email address will have to be set manually, by opening the file with any text editor and editing the following line of code:
`$to = "webmaster@example.com";`

The default mail that it is sent will look similar to this:

<img src="http://docs.avchat.net/assets/images/reportMail.png" class="img-responsive"/>

**Viewing a report**

All of the reports can be seen using the AVChat administrator area -> Reports panel. The number between the parentheses is a notification for the total number of reports.

<img src="http://docs.avchat.net/assets/images/reportsPanel.png" class="img-responsive"/>

The notifications work in the following way:
Upon entering the chat as admin, the [Reports] button will show the total number of reports like so: Reports (10). When a new reports is received and the reported users window is not opened, the total number of NEW reports will be displayed in the top right corner of the [Reports] button like so:

<img src="http://docs.avchat.net/assets/images/reportNotif.png" class="img-responsive"/>

Pressing the <kbd>Report</kbd> button will open a new window and the notifications for the total number of NEW reports disappears.
The new window displays all of the reports sent. Here you have the following options:

* View the camera snapshot for a particular report (this is only active if a screenshot of the reported user's webcam was taken).
* View the text-chat snapshot for a particular report
* Copy username (copy the username of the reported user)
* Copy user IP (copy the IP of the reported user)
* Remove a report
* Close (closes the window)

<img src="http://docs.avchat.net/assets/images/reportList.png" class="img-responsive"/>

Removing a report will permenantly delete it.

Additionally the report feature can be disabled by setting `enableReportSending` to `0`. Also an admin can be blocked to see the reports by setting `adminCanSeeReports` to `0`. By default they are both enabled (set to `1`).

<h2 id="pay-per-view-api">Pay Per View API</h2>

Starting with [build 3078](http://nusofthq.com/blog/avchat-october-build-3078-has-been-released/) the Pay Per View API has been introduced, API that deprecates the old `freeVideoTime` setting and functionality.

The API offers a series of settings and functionalities, which will be detailed later, that enable you to create and integrate a costum build payment solution based on several criteria for example:how much does a user stay in chat, how many minutes can he watch other streams.

The API comes in 2 parts: settings that can be controlled from the `avc_settings.xml` file and the actual API for JavaScript, PHP and .NET.

**The settings in avc_settings.xml detailed**

The API is intended to be used with an integrated version of AVChat and makes use of the following settings in `avc_settings.xml`:


1. `PPVEnabled` - This setting controls whether or not the PPV feature is enabled, and also depending on that, the status of the PPV button. When disabled the PPV button is not shown in the status bar.
2. `PPVAmount` - This setting holds the amount of time or credits, depending on the `PPVType` setting. The `PPVAmount` starts to decrease as soon as the user enters the chat or as soon as he starts viewing a webcam (depending on `PPVTrigger`) with a ratio equal to `PPVRatio`/second. The remaining `PPVAmount` is then sent (every second) to the JS function onPPVUpdate which can be usually be found in index.html and `admin.html` and to `ppvUpdate.php` and `ppvUpdate.aspx`.
3. `PPVType` - This setting controls what `PPVAmount` represents (time, money, credits). When set to time the `PPVAmount` will be shown in the chat time formated (i.e. 15:32).
4. `PPVTrigger` - This setting indicates what triggers the `PPVAmount` to decrease. When set to `viewing_webcams` the `PPVAmount` starts to decrease as soon as you start viewing someone, viewing 2 or more cams will NOT decrease the timer faster. When set to `connected` the `PPVAmount` starts to decrease as soon as you enter the chat.
5. `PPVRatio` - This setting controls the ratio at which the `PPVAmount` is decreased every second. When set to 0.5 for example there will be a 0.5 credits or seconds decreased every second.
6. `PPVLink` - This setting holds the URL for the page from which more time/credits may be purchased for more video stream access. Pressing the PPV button will open the PPV Link.
7. `PPVIcon` - This setting provides the URL to the icon loaded in the PPV button located in the status bar. The icon size should be 16x16.

The PPV Button mentioned above is a new button added in the status bar that displays dynamically the amount of time/credits left if PPV is enabled. Here's how it looks:
<img src="http://docs.avchat.net/assets/images/PPVButton.png" class="img-responsive"/>

**The API**

The API comes in 3 flavors:
* a Javascript API, represented by the function `onPPVUpdate` (found in `index.html` and `admin.html`).
* a PHP file `ppvUpdate.php`
* a .NET file `ppvUpdate.aspx`

All of the above are called every second that passes while viewing a stream or being in chat, depending on the trigger set, by the AVChat client, with the following parameters:
* `ppvAmountLeft`: the amount of time/money/credits left for a particular user.
* `ppvInitialAmount`: the initial amount of time/money/credits that a user had.
* `ppvRatio`: the rate at which the ppvAmountLeft is decreased.
* `userSiteId`: the siteId value as sent by avc_settings.xxx
* `sessionTimeStamp`: the timestamp from the last login.

**Working with the API**

All of this information feed and parameters will have to be stored and updated in the database of the site in which AVChat will be integrated.

A general workflow will look something like this:

1. Registered site user enters AVChat.
2. AVChat starts churning down data to the API based on the settings set in `avc_settings.xml`.
3. Parameters passed to the API will have to be taken and stored/updated in site database.
4. Based on the information stored a custom made script will have to update the `PPVAmount` setting so that when a user re-enters chat the correct amount of time/credits left will be used.

**Controlling the API**

The API can be controlled by the setting `PPVEnabled`. Depending on the value set here just parts of the API can be enabled.

**Enabling just the JavaScript API**

To only enable the JavaScript API set `PPVEnabled` to `1`.

**Enabling just the PHP/.NET API**

To only enable the PHP/.NET API set `PPVEnabled` to `2`.

**Enabling both JavaScript and PHP/.NET API**

To enable both JavaScript and PHP/.NET API set `PPVEnabled` to `3`.

<h2 id="avchat-twitter-authentication">How to setup AVChat for Twitter authentication</h2>

**The Twitter authentication explained**

Starting with [build 2915](http://avchat.net/support/documentation) AVChat supports Twitter authentication.

This feature allows your users to connect to AVChat using their Twitter account.

Clicking the Twitter logo in the login screen will open up a popup asking for the user's Twitter credentials in order the authorize the app for that particular account.

<img src="http://docs.avchat.net/assets/images/twAuth.png" class="img-responsive"/>

Upon given permission AVChat will automatically login using the user's Twitter profile name and profile picture. Opening the user's profile from the user side menu will lead you to the user's Twitter profile.

<img src="http://docs.avchat.net/assets/images/twProfile.png" class="img-responsive"/>

This feature is controlled by the setting `enableOtherAccountOptions` located in the `avc_settings.xml` file. If set to `0`, the feature will be disabled.

**Setting it up**

Here are the steps that will guide you on how to set this up:

1. Go to [https://dev.twitter.com/apps](https://dev.twitter.com/apps)
2. Create a Twitter application by clicking "Create a new application" (you must have a Twitter account, if not create one prior to this).
3. Enter the Name, Description, Website URL (your website) and the Callback URL (this will be a placeholder for the actual callback URL but it is needed. You can enter the same website URL completed earlier).
4. Agree with the terms, enter the CAPTCHA and click "Create your Twitter application".
5. You will receive a message at the top of the page that the application was succesfully created and be redirected to a new page that lists all the details for the created application.
<img src="http://docs.avchat.net/assets/images/twDetails.png" class="img-responsive"/>
6. Open up `index.html`(that can be found in your AVChat installation folder) with any text editor.
7. Find the lines similar to this: `var consumerKey = "U3yvRmc....";` and `var consumerSecret = "YtlvlqRTXjdjmK.....";` and replace those values with the ones generated by Twitter for your own application (marked in the image above by the green rectangle).
8. Find the line similar to this var `pathToAVChat = "http://avchat.net/demos/avchat30";` and replace the value with the link to your AVChat installation.
9. Save and close the file.

<div class="alert alert-info" role="alert">Also note that in order for the Twitter based login to work for the admin interface (admin.swf and admin.html) the same modifications need to be made to admin.html</div>

<h2 id="editing-columns">How to edit columns in the rooms panel</h2>

This feature allows you to edit the info displayed regarding a room in the rooms panel. The values represent the table heads for each column:

<img src="http://docs.avchat.net/assets/images/rooms_list_th.png" class="img-responsive"/>

In the above image, you can see that small arrow icon annotated with green. Users are able to sort the rooms in the rooms list by that option.

For example, clicking the name once (as in the example), will sort the rooms alphabetically, by name (from A to Z). Clicking it once again will reverse the sort (from Z to A).

Same procedure for the rest of the colums.

Also, you can remove some of the columns so that you will only display the name of the room, having only the "name" label in the `<value>` node, like:
`<value>name</value>`

How to do it:

* Open `avc_settings.xml` - you can find it in your AVChat installation folder.
* Search for `columnsInRoomsPanel` (line 1116).
* Based on the values in the `<default>` node (name, users, private, owner, created), set the `<value>` node to what you need.
* Save the file and upload it back to the server.

```xml
<columnsInRoomsPanel>
   <title>columnsInRoomsPanel</title>
   <name>Columns in rooms panel</name>
   <type>string</type>
   <desc>a string that allows you to configure and edit the columns shown by the rooms list inside the rooms panel.</desc>
   <default>name users private owner created</default>
   <examples></examples>
   <value>name users private owner created</value>
</sortRoomListOn>
```

<h2 id="autostart-webcam">How to make the webcams auto start</h2>

Perhaps you're using AVChat for live conferences where people will use audio/video by default and you want to eliminate some steps, to make AVChat more user friendly.

In this matter, you can set the webcams to open automatically for each user, after connecting.

There are 2 possibilities here:

After connecting, each user will start seeing all other public streams automatically.

How to set this:

*	Open `avc_settings.xml` - you can find it in your AVChat installation folder
* search for `autoStartCameras` (line 426)
* set it's `<value>` node to `1` which enables it
* save the file and upload it back to the server

```xml
<autoStartCameras>
   <title>autoStartCameras</title>
   <name>Autostart cameras</name>
   <type>boolean</type>
   <desc>if set to 1 the user will start to view PUBLIC cams automatically as soon as they are started, admins with the permission to view private streams will also view private streams automatically</desc>
   <examples>0 for disabled, 1 for enabled</examples>
   <default>0</default>
   <value>1</value>
</autoStartCameras>
```

After connecting, each user will start streaming, with or without microphone.

How to set this:

* Open `avc_settings.xml` - you can find it in your AVChat installation folder
* Search for `autoStartMyCamera` (line 435)
* Set it's `<value>` node to `1` which enables it
* Save the file and upload it back to the server

```xml
<autoStartMyCamera>
   <title>autoStartMyCamera</title>
   <name>Autostart my camera</name>
   <type>eboolean</type>
   <desc>if set to 2, when a user has a webcam, immediatley after joining the first room, his camera will start broadcasting (the mic will start muted if the user has one).if set to 1, when a user has a webcam/microphone, immediatley after joining the first room, his camera/mic will start broadcasting. If set to 0, the user will have to press the 'Start my camera/mic' buttons to start it . This setting also takes into consideration the allowAudioStreaming and allowVideoStreaming variables</desc>
   <examples>0, 1, 2</examples>
   <default>0</default>
   <value>1</value>
</autoStartCameras>
```

<h2 id="allow-block-video-streaming">Allowing/blocking audio and video streaming</h2>

AVChat acts like a group chat with audio and video, but you can disable one of these 2 functionalities anytime, for any of your purposes.

By default, both features are enabled. Here's how to control both of them:

Disabling video streaming:

1. Open `avc_settings.xml` with a text editor
2. Search for `allowVideoStreaming` (line 110)
3. Set it's `<value>` node to `0`
4. Save the file and upload it back to the server

This way, users will be able to use only the microphone.

Disabling audio streaming:

1. Open `avc_settings.xml` with a text editor
2. Search for `allowAudioStreaming` (line 119)
3. Set it's `<value>` node to `0`
4. Save the file and upload it back to the server

This way, users will be able to use only the webcam, if `allowVideoStreaming` is enabled.

Having both disabled will make AVChat work as text chat only.

<h2 id="disabling-mobile-version">Restricting access from a desktop PC to  the mobile version</h2>

The mobile version is HTML5 and Javascript based, so it can be easily be accessed from any browser including desktop browsers.

If you purchased the mobile version of AVChat and installed it and you want the users to be able to access the mobile version only from a mobile device, here are the steps needed to do so:

* Open `avc_settings.xml` with a text editor
* Search for `enableHtmlClientForDesktopBrowser` (line 1458)
* Set it's `<value>` node to `0`
* Save the file and upload it back to the server

<h2 id="audio-video-only">How to disable the mobile version only</h2>

If you purchased the mobile version of AVChat and installed it, but you need to disable it for some reason, just remove or rename the `ws` folder from your AVChat installation folder.

<h2 id="audio-video-only">Configure AVChat to function with audio and video only (AVChat 3.5.1 and older)</h2>

<div class="alert alert-warning" role="alert">This setting has been deprecated starting with AVChat 3.5.2 build 3542.</div>

For more details on what has been changed you can read the [blogpost](http://avchat.net/blog/avchat-3-5-2-update-now-released/).

AVChat can be set to function in video-only mode (just audio/video streams with no text-chat).

This feature is intended for users that want to utilize AVChat for specific seminars and presentations. When this is activated only the users-list will be available, and the user’s camera will automatically start.

Also user-side menu specific text-chat options will be no longer available.

This feature is controlled by the setting `enableAudioVideoOnlyMode` also present `avc_settings.xml`.

How to set it:

* Open `avc_settings.xml` with a text editor
* Search for `enableAudioVideoOnlyMode` (line 1548)
* Set it's `<value>` node to `1`
* Save the file and upload it back to the server


<h2 id="audio-video-only">Configure AVChat to function with audio and video only (AVChat 3.5.2 and newer)</h2>

In [AVChat 3.5.2]([blogpost](http://avchat.net/blog/avchat-3-5-2-update-now-released/) we've introduced a new setting `hideTextChat` which controls whether or not the text chat area is shown. The older setting `enableAudioVideoOnlyMode` has been removed completely, but it’s functionality can still be obtained combining some settings together including the newly added `hideTextChat`.

How to set it:

* Open `avc_settings.xml` with a text editor
* Search for `hideTextChat`
* Set it's `<value>` node to `1`
* Save the file and upload it back to the server

The idea behind this change was to eliminate any kind of possible conflicts that would’ve occurred if `enableAudioVideoOnlyMode` was activated and other settings like `allowVideoStreaming` was also set separately. To give you an idea on how AVChat can be setup to obtain the same or similar effects you can view the [Live stream setup documentation](http://docs.avchat.net/standalone#setup-for-livestreaming).

<h2 id="showing-hiding-rooms">How to hide/show some of the existing rooms</h2>

There might be a situation when you don't want to show all the rooms to your users, but also not delete them, to prevent others joining some of your rooms.

This is easy, there are 2 possibilities here: hiding rooms or showing only some of them.

Also user-side menu specific text-chat options will be no longer available.

How to show only some of the existing rooms:

* Open `avc_settings.xml` - you can find it in your AVChat installation folder
* Search for `showOnlyRooms` (line 1702)
* Insert the room ID or rooms IDs you want to be shown in the `<value>` node (r0 for a single room and [r1,r2,r3] for multiple rooms)
* Save the file and upload it back to the server

How to hide some of the existing rooms:

* Open `avc_settings.xml` - you can find it in your AVChat installation folder
* Search for `hideTheseRooms` (line 1766)
* insert the room ID or rooms IDs you want to be shown in the `<value>` node (r0 for a single room and [r1,r2,r3] for multiple rooms)
* Save the file and upload it back to the server


<h2 id="rooms-music-player">Rooms music player</h2>

Every room can have it's own music playlist with music tracks from Youtube.

Upon entering the respective room the music player will automatically start to play the songs.

This feature is controlled by the new setting `enableMusicForRooms` found in `avc_settings.xml`.

It comes enabled by default, here's how to disable it:

* Open `avc_settings.xml` - you can find it in your AVChat installation folder
* Search for `enableMusicForRooms` (line 1755)
* Set it's `<value>` node to `0`
* Save the file and upload it back to the server


<h2 id="enabling-webcam-docking">How to enable webcam docking</h2>

Webcams can be aligned automatically above the text chat area when other streams are opened, like in the picture below:

<img src="http://docs.avchat.net/assets/images/docking1.jpg" class="img-responsive"/>

This feature comes disabled by default, here's how to enable it:

* Open `avc_settings.xml` - you can find it in your AVChat installation folder
* Search for `enableWebcamDocking` (line 1784)
* Set it's `<value>` node to 1
* Save the file and upload it back to the server


<h2 id="setup-realtime-translation">How to setup Real-Time Translation with Google's Translate API</h2>

Starting with AVChat [build 3396](https://nusofthq.com/blog/long-awaited-new-avchat-build-3396-is-here/) we have implemented a mechanism that permits AVChat to detect the language the browser is setup for. Based on this and using Google’s Translate API you can now translate on the fly messages from another language, from a user that has the browser setup in french for example, to your preferred language, assuming as well that your browser is setup in your particular language.

A small translate link will appear on the side of the text message, pressing it will show the translation for that particular message in a smaller grey font beneath the original text, as shown in the images below:

<img src="http://docs.avchat.net/assets/images/french_text.jpg" class="img-responsive"/>

<img src="http://docs.avchat.net/assets/images/english_text.jpg" class="img-responsive"/>

But in order to achieve this you must first have a Google API Key. Here are the steps needed to obtain one:

1. Go to [https://console.developers.google.com](https://console.developers.google.com) and create a Google account if you don't have one.
2. After creating you account go to the Projects page by clicking on the Projects link in the left-side menu.
3. Create a new project by clicking on the Create Project button and name it however you wish.
4. Wait for a couple of seconds while the project is created.

Now that you've setup your project it's time to enable the Translate API for it:

1. With your project selected in the menu on the left, select `API Manager`.
2. In the list of APIs, select `Translate API` from the `Other popular APIs` catergory, and make sure it is enabled.
3. In the sidebar on the left, select Credentials.
4. In this page click on the <kbd>Create credentials</kbd> button and select `API Key`.
5. In the dialog box that opens up select `Browser key`.
6. Http referers can also be setup like mentioned in the next window:
  <img src="http://docs.avchat.net/assets/images/googleAPIkeyCreation.png" class="img-responsive"/>
7. Give it a name and specify the referers from which to accept request and then click <kbd>Create</kbd>
8. An API Key will be generated. Copy it and set it in the `avc_settings.xml` setting `googleAPIkey`.
9. Save and close `avc_settings.xml`.

There is one more thing that needs to be done before the setup is ready. Google Translate API v2 requires billing information for your account before you can start using the service. To enable billing for your project, do the following:

1. With the project selected, in the sidebar on the left, select <kbd>Billing</kbd>.
2. Select Enable billing
3. Select your location and then fill in the form.

That's it, now AVChat will translate text messages on the fly, provided the user's browsers are setup for different languages.

<h2 id="setup-for-livestreaming">How to setup AVChat for Live streaming</h2>

AVChat can be setup for live streaming of events or interactive courses for example. This is easily done when you have AVChat integrated with a CMS like Wordpress or Joomla, where you can setup a particular user group to be able to broadcast, and another "viewers" user group to only be able to view other streams. The particular settings you would need to setup will be detailed later.

In case you have a standalone installation of AVChat, the same effect can be achieved by having two different installation folders (two instances of AVChat installed on the webserver, connected to the same instance on the media server. One installation will fill the role of the broadcaster and the other of the viewer.

The following settings apply in both of the cases (integrated AVChat and standalone)

The **broadcaster role** will have the following setup:

1. `allowVideoStreaming` set to `1`
2. `allowAudioStreaming` set to `1`
3. `autoStartMyCamera` set to `1`
4. `autoStartCameras` set to `0`
5. `allowPrivateStreaming` set to `0`


The **viewer role** will have the following setup:

1. `allowVideoStreaming` set to `0`
2. `allowAudioStreaming` set to `0`
3. `autoStartMyCamera `set to `0`
4. `autoStartCameras` set to `1`

It is recommended that the cameras are set to be docked: `enableWebcamDocking` set to 1

Additional changes can be made. You can hide the users list for both broadcaster and viewer role by setting `hideUsersList` to `1`.

Starting with [AVChat 3.5.2](http://avchat.net/blog/avchat-3-5-2-update-now-released/) The entire text chat area can be hidden as well separately using the setting `hideTextChat` set to `1`.

<h2 id="accessing-videos-via-http">Accessing the videos via http from the avchat30/streams/\_definst\_ folder (Red5 only)</h2>

When recording using the Red5 media server the video files are created in `Red5/webapps/avchat30/streams/_definst_`. Starting with [AVChat 3.6](http://avchat.net/support/documentation#) the streams folder can be exposed - via Red5's Tomcat web server - to be accessible via http (from the browser) at http://RED5_SERVER_ADDRESS:5080/avchat30/streams/

This will help you greatly if you want to:

* Play the files through HTML5 or progressive download
* Download the files locally
* Move the files to a different server

You will need to do the following steps:

1. Go to `Red5/webapps/avchat30/WEB-INF/` on your media server.
2. Open `web.xml` with a text editor.
3. Delete the tag `<security-constraint>` along with it's contents.
4. Uncomment the other `<security-constraint>` tag, where it reads.
5. Save and exit.
6. Restart Red5.

If you now go to http://RED5_SERVER_ADDRESS:5080/avchat30/streams/ in your web browser you will see a list of all the video files. Clicking them will download them or play them in the browser.

<img src="http://docs.avchat.net/assets/images/listings_on.png" class="img-responsive"/>

This open directory listing can be a security issue (you don't want to expose all the recorded videos to anyone snooping around). To turn off the directory listing do the following:

1. Go to Red5/conf/ on your media server.
2. Open web.xml with a text editor.
3. Search for this code:

		<init-param>
		   <param-name>listings</param-name>
		   <param-value>true</param-value>
		</init-param>

4. Set the listings value to false like this:

		<init-param>
		   <param-name>listings</param-name>
		   <param-value>false</param-value>
		</init-param>

5. Save and exit.
6. Restart Red5.

Directory listing will now be turned off.

<img src="http://docs.avchat.net/assets/images/listings_off.png" class="img-responsive"/>

You will still be able to access the file and download it or play it if you know it's name (absolute http path).

<h2 id="stream-recording-api-red5">How to setup AVChat's Stream Recording API (Red5 only)</h2>

Starting with [AVChat 3.6](http://avchat.net/blog/avchat-3-6-brings-a-new-mobile-version-and-red5-1-0-5-compatibility) a new stream recording API is available. The API is represented by the `getRecordedVideosInfo` file (PHP or .NET variant) located on the webserver side in the AVChat installation folder.

The way this works is if the media server (Red5 in this case) is setup to record the live streams, each time a stream is started or closed, the media server calls the webserver side file g`etRecordedVideosInfo` sending the following information about the stream: `streamname`, the `siteId` of the user that made the recorded `videostream`, the `username` of the user that made the recorded videostream.

This API is disabled by default as it is works together with the media-server side setting `recordAudioVideoStreams`

So in order to enable this feature you must do the following steps:

1. Edit `avchat30/avchat3.properties` and set `recordAudioVideoStreams` to `true`.
2. In the Red5 installation directory go to the `conf` folder and edit `red5.properties`.
3. Search for the following setting `fileconsumer.delayed.write` and set it to `false`.
4. Restart Red5.

By default Red5 tries to automatically detect the location of the `getRecordedVideosInfo.php` file. If the file is moved to any other folder other than the AVChat installation folder or if the `.aspx` file is used instead, the location needs to be set manually using the new media-server side setting `sendRecordingsInfoScriptURL` from `avchat3.properties`.


<h2 id="autocreate-rooms">The auto-create rooms mechanism</h2>

Starting with [AVChat 3.6.3](http://avchat.net/blog/avchat-3-6-3-update/) the mechanism for automatic room creation has changed. The server-side setting (Red5 and AMS) autoCreate`defaultRooms` has been deprecated and removed. Its functionality has been integrated into the `defaultRooms` setting. Leaving the value of this setting empty will disable the auto-creation mechanism.

The `defaultRooms` setting comes with a predefined room, The Lobby, which will enable the creation of this room for all new instances of AVChat. Already existing instances will not have rooms created automatically.

To create rooms automatically you need to add ROOM OBJECTS to the `defaultRooms` settings. You can add one or multiple rooms.

**On Red5**

Example for one room:

`defaultRooms=[The Lobby,Main room for everyone,,0,,This is an automated created room]`

To create more than 1 default room add another room object to the `defaultRooms` array and separate the room objects with a semicolumn:

`defaultRooms`=[The Lobby,Main room for everyone,,0,,This is an automated created room];[Super Room, The description,1234,0,,This is an automated created room]`

**On AMS**

Example for one room:

`application.defaultRooms=[{name:"The Lobby(auto)",description:"The Main Room",password:"",maxusers:50,ownerName:"",ownerId:"",siteId:"",ip:"127.0.0.1",clientId:"",welcomeMessage:"This is an autocreated room",playListArray:""}];`

To create more than 1 default room add another room object to the `defaultRooms` array and separate the room objects with a comma:

`application.defaultRooms=[{name:"The Lobby(auto)",description:"The Main Room",password:"",maxusers:50,ownerName:"",ownerId:"",siteId:"",ip:"127.0.0.1",clientId:"",welcomeMessage:"This is an autocreated room",playListArray:""}, {...another room object...}]`
