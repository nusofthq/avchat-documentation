
All the AVChat documentation is on this page so if you're looking for something specific just hit <kbd>Ctrl+F</kbd> on your browser.

If you cannot find the answer you’re looking for here, we encourage you to try the [AVChat discussion forum](http://discuss.avchat.net).

<h2 id="how-avchat-works">How AVChat works</h2>

AVChat uses a media server to send audio, video and text chat between desktop users and text chat to and from mobile users.

![alt text](assets/images/how-avchat-works.png)

If we were to break down the exact process here is every step:

1. User goes to your web site and visits the page with the video chat on it.
2. The chat client (Flash swf on desktop) is loaded by the users browser, it initializes and it loads `avc_settings.php` from your web server together with other config files: the language file, the emoticons files, etc..
3. Once everything is loaded the user is asked for a user name and gender (if AVChat's not integrated).
4. Once the user provides that info the chat client attempts to connect to the media server using an `rtmp` connection over port `1935`.
5. Once connected to the media server the user can join rooms, send text messages, view other user's streams and start publishing their own audio video stream.
6. All data (audio, video, text) is sent from the user to the media server and from there it's directed as needed to all other users.

<h2 id="requirements">Requirements</h2>

To run AVChat 3 on your website you will need:

1. Web hosting for your chat/website
2. A media server

Your chat users need a modern Internet browser with Flash Player 11.1 or above installed.

The need for Flash Player 11.1 starts with AVChat build 2330 of AVChat which adds H.264 encoding support.

**Web hosting for your chat/website**

A web hosting account with PHP or ASP.NET support is needed. This is where the chat files will be placed and most probably where your web site is already located.

**A media server**

AVChat (and all Flash based video chat apps including the peer to peer ones) needs a media server to transport data (audio, video and text chat) betweenusers.

AVChat supports the 3 major media servers:

* [Red5](https://github.com/Red5/red5-server "Red5 Media Server") (free and open source)
* [Wowza](http://www.wowza.com "Wowza Media Server") (commercial)
* [Adobe Media Server](http://www.adobe.com/products/adobe-media-server-family.html "Adobe Media Server") (commercial)

AVChat (desktop) is compatible with:

* Red5 1.0.5+
* Wowza 1.7.x -> Wowza Streaming Engine 4
* Adobe Media Server 5 Starter, Professional and Extended and Flash Media Server 2, 3, 3.5, 4 and 4.5

AVChat (mobile) is compatible with:

* Red5 1.0.5+

Other compatibility notes:

* AVChat versions up to and including 3.5.2 are compatible with Red5 0.8 and 1.0RC1.
* Red5 1.0.5 needs at least Java JDK version 1.8
* Adobe Media Server *Standard* and Flash Media *Streaming Server* are not supported

**Setting up your own media server**

You can can install the above media server software on any VPS or dedicated/cloud server.

Any VPS, dedicated server or cloud server will work. If you don't have one yet we recommend getting one from these companies:

* [OVH - VPS servers starting at €3/month (datacenters in France)](http://www.ovh.com/fr/vps/vps-classic.xml)
* [Leaseweb - VPS servers starting at €5/month](https://www.leaseweb.com/cloud/public/virtual-server)
* [DigitalOcean - VPS servers starting at $5/month](https://www.digitalocean.com/?refcode=cd50d47eef55)

Each media server has it's own installation instructions. We can also install a media server for you, on your server, through our [Media Server Installation Service ($99)](http://avchat.net/services#installms).

**Media server porvided by us**

We're also offering [VPS servers with Red5 pre-installed](http://avchat.net/hosting) and configured for AVChat starting with $14.99/month. We can use servers in Toronto, San Francisco, New York, London, Amsterdam, Frankfurt and Singapore.

<!--
<h2 id="file-groups">AVChat archive structure</h2>
AVChat 3 has two groups of files:

* client side files, that go on your web server (html, js, xml, swf files, etc.)
* media server files (the media server app) that go on your media server (Red 5, AMS, Wowza). These handle all the logic of sending audio, video and text between users, etc...
-->


<h2 id="config-files">Configuration files</h2>

<h3>On the web server</h3>

**Main config file**

`avc_settings.xml` is the main configuration file for AVChat. You will find it in your AVChat installation folder on your web server.

`avc_settings.xml` has been introduced in [build 2060](http://nusofthq.com/blog/avchat-december-holiday-build-2060/ "AVChat build 2060") when all the settings from `avc_settings.php` and `avc_settings.aspx.cs` were removed from those 2 files and grouped into one single file: `avc_settings.xml`.

For simple ASP `avc_setting.asp` is still used before and after build 2060.

**Audio video quality**

**Themes**

**Translations**

<h3>On the media server</h3>

**Red5**

`avchat3.properties`, you will find it in `Red5/webapps/avchat30`

**Wowza**

`avchat3.properties` , you will find it in `Wowza/conf/avchat30`

**Adobe Media Server**

`settings.asc` , you will find it in `AMS/applications/avchat30`


<!--<div class="alert alert-info" role="alert">With this kind of setup 2 different versions of AVChat can be run at the same time by Red5. Just be carefull to connect the correct client to the correct server side application.</div>-->

<h2 id="file-structure">AVChat File Structure</h2>

AVChat ships as a zip archive that contains the following file/folder structure:

* ![folder icon](assets/images/folder-16.png) Files to upload to your website
  * ![folder icon](assets/images/folder-16.png) audio_video_quality_profiles (folder containing audio video quality files in .xml format)
  * ![folder icon](assets/images/folder-16.png) codebird-js
  * ![folder icon](assets/images/folder-16.png) emoticons (folder containing sets of emote icons)
  * ![folder icon](assets/images/folder-16.png) gender_icons
  * ![folder icon](assets/images/folder-16.png) report_snaps
  * ![folder icon](assets/images/folder-16.png) sounds (folder containing sounds used in the video chat in mp3 format)
  * ![folder icon](assets/images/folder-16.png) themes (subfolders dark and light each with a `style.xml`)
  * ![folder icon](assets/images/folder-16.png) tokens
  * ![folder icon](assets/images/folder-16.png) translations (folder containing UI translations in .xml)
  * ![folder icon](assets/images/folder-16.png) uploadedFiles (folder where files uploaded by users will go)
  * `admin.html` (html file that embeds admin.swf)
  * `admin.swf` (admin interface)
  * ajax-loading.gif
  * `avc_settings.asp`
  * `avc_settings.aspx`
  * `avc_settings.aspx.cs`
  * `avc_settings.php`
  * `avc_settings.xml` has been added started with [build 2060](http://nusofthq.com/blog/avchat-december-holiday-build-2060/ "AVChat build 2060")
  * `badnicks.xml` (xml file containing the bad usernames that are now allowed in the chat)
  * `badwords.xml` (xml file containing the bad words that are banned in the chat)
  * bg.png
  * `channel.html`
  * `dataEncryption.php`
  * favicon.ico
  * `file_types.xml` has been added starting with [build 2060](http://nusofthq.com/blog/avchat-december-holiday-build-2060/ "AVChat build 2060")
  * `fonts.xml` (list of fonts that can be used in the chat)
  * fullStar.png (default logo image that is shown over all video stream to   prevent them from being rebroadcasted)
  * `genders.xml`
  * `getRecordedVideosInfo.aspx`
  * `getRecordedVideosInfo.aspx.cs`
  * `getRecordedVideosInfo.php`
  * gift.png
  * `index.html` (html file that embeds index.swf)
  * `index.swf` (user interface)
  * `Mobile_Detect.php`
  * mobile-icon.png
  * mod_icon.png
  * nowebcam.png
  * ppvIcon.png
  * `ppvUpdate.aspx`
  * `ppvUpdate.aspx.cs`
  * `ppvUpdate.php`
  * `Preview.swf` (old background)
  * `report_snapshot_upload.aspx`
  * `report_snapshot_upload.aspx.cs`
  * `report_snapshot_upload.php`
  * `rotate_messages.aspx`
  * `rotate_messages.aspx.cs`
  * `rotate_messages.php`
  * search-14px.png
  * search-icon.png
  * `sendgift.aspx`
  * `sendgift.aspx.cs`
  * `sendgift.php`
  * `sendReport.aspx`
  * `sendReport.aspx.cs`
  * `sendReport.php`
  * `style.aspx`
  * `style.aspx.cs`
  * `style.php`
  * `style.css` (old css file that controls the colors and fonts used throughout the video chat). Starting with [build 2060](http://nusofthq.com/blog/avchat-december-holiday-build-2060/ "AVChat build 2060") style.css has been replaced with style.xml for users with PHP, style css is still used for users with ASP.NET and ASP
  * `swfobject.js`
  * `tinycon.min.js`
  * `token_request.aspx`
  * `token_request.aspx.cs`
  * `token_request.php`
  * `token_verify.aspx`
  * `token_verify.aspx.cs`
  * `token_verify.php`
  * `upload.asp`
  * `upload.aspx`
  * `upload.aspx.cs`
  * `upload.php`
  * `uploadclass.asp`
  * warning.png
  * `wget.aspx`
  * `wget.aspx.cs`
  * `wget.php`
  * `writeuserslist.aspx`
  * `writeuserslist.aspx.cs`
  * `writeuserslist.php`
* ![folder icon](assets/images/folder-16.png) Files to upload to your media server (FMS/AMS)
* ![folder icon](assets/images/folder-16.png) Files to upload to your media server (Red5 0.8)
* ![folder icon](assets/images/folder-16.png) Files to upload to your media server (Wowza)
