
<h2 id="file-groups">AVChat 3 groups of files</h2>

AVChat 3 has two groups of files:

* client side files, that go on your web server (html, js, xml, swf files, etc.) and are loaded by your web site users in their browsers
* media server files that go on your media server (Red5,FMIS,Wowza) these handle all the logic of sending messages between users, banning IPs, accepting connections, etc...



<h2 id="config-files">Configuration files</h2>

AVChat has 2 main configuration files:

1. `avc_settings.xxx` which you will find in your AVChat installation folder on your web server (its's part of the client side files) Starting with [build 2060](http://nusofthq.com/blog/avchat-december-holiday-build-2060/ "AVChat build 2060")  all the settings from `avc_settings.php` and `avc_settings.aspx.cs` were moved to a new file `avc_settings.xml` from which they are imported. For simple ASP avc_setting.asp remains unchanged:
2. the media server app config file:
  * `settings.asc` on FMS/AMS, you will find it in `/applications/avchat30` on FMS or `/FMSApps/avchat30` on AMS
  * `avchat3.properties` on Red5, you will find it in `/webapps/avchat30`
  * `avchat3.properties` on Wowza , you will find it in `Wowza/conf/avchat30`

There are other less important config files (like the video quality .xml file or the logback_avchat30.xml file on Red5 that specifies where the log files should be created) but we will cover them below as needed.

<h2 id="file-structure">File Structure</h2>

AVChat ships in an archive that looks like this:

* Files to upload to your website
  * audio_video_quality_profiles (folder containing audio video quality files in .xml format)
  * codebird-js
  * emoticons (folder containing sets of emote icons)
  * gender_icons
  * report_snaps
  * sounds (folder containing sounds used in the video chat in mp3 format)
  * themes (subfolders dark and light each with a `style.xml`)
  * tokens
  * translations (folder containing UI translations in .xml)
  * uploadedFiles (folder where files uploaded by users will go)
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
* Files to upload to your media server (FMS/AMS)
* Files to upload to your media server (Red5 0.8)
* Files to upload to your media server (Wowza)



<h2 id="how-avchat-works">How AVChat works</h2>

1. User goes to your web site and visits the page with the video chat embedded.
2. The chat client (Flash swf) is loaded by the users browser, it initializes and it loads avc_settings.xxx from your web server together with other config files: the language file, the emoticons files and some other config files.
3. Once everything is loaded the user is asked for a user name and gender (if AVChat's not integrated).
4. Once the user provides that info the chat client attempts to connect to the media server using an rtmp connection over port 1935.
5. Once connected to the media server the user can join rooms, send text messages, view other user's streams and start publishing their own audio video stream.
6. All data (audio, video, text) is sent from the user to the media server and from there it's directed as needed to all other users.

![alt text](http://docs.avchat.net/assets/images/fcs.jpg "Logo Title Text 1")

<h2 id="requirements">Requirements</h2>

To run AVChat 3 on your website you will need:

1. Web hosting for your chat/website
2. A media server

Your chat users need a modern Internet browser with Flash Player 11.1 or above installed.

The need for Flash Player 11.1 starts with AVChat build 2330 of AVChat which adds H.264 encoding support.

<h3 id="web-hosting"> Web hosting for your chat/website</h3>

A web hosting account with PHP or ASP.NET support is needed. This is where the chat files will be placed and most probably where your web site is already located.

<h3 id="media-server"> A media server</h3>

AVChat (and all Flash based video chat apps including the peer to peer ones) needs a media server to transport data (audio, video and text chat) between your chat users.

There are 3 media servers:

* [Red5](https://github.com/Red5/red5-server "Red5 Media Server") (free open source)
* [Wowza](http://www.wowza.com "Wowza Media Server") (commercial, free trial)
* [Adobe Media Server](http://www.adobe.com/products/adobe-media-server-family.html "Adobe Media Server") (commercial, free edition)

AVChat (desktop) is compatible with:

* Red5 1.0.5+
* Wowza 1.7.x -> Wowza Streaming Engine 4
* Adobe Media Server 5 Starter, Professional and Extended
* Flash Media Server 2, 3, 3.5, 4 and 4.5

AVChat (mobile version) is compatible with:

* Red5 1.0.5+

Other compatibility notes:

* AVChat versions up to and including 3.5.2 are compatible with Red5 0.8 and 1.0RC1.
* Red5 1.0.5 specifically needs at least Java JDK version 1.8
* Adobe Media Server Standard is not supported
* Flash Media Streaming Server is not supported

<h3 id="setting-up-own-media-server">Setting up your own media server</h3>

You can can install the above media server software on any VPS or dedicated/cloud server.

Any VPS, dedicated server or cloud server will work. If you don't have one yet we recommend getting one from these companies:

* [OVH - VPS servers starting at €3/month (datacenters in France)](http://www.ovh.com/fr/vps/vps-classic.xml)
* [Leaseweb - VPS servers starting at €5/month](https://www.leaseweb.com/cloud/public/virtual-server)
* [DigitalOcean - VPS servers starting at $5/month](https://www.digitalocean.com/?refcode=cd50d47eef55)

Each media server has it's own installation instructions but we can install a media server for you through our [Media Server Installation Service ($99)](http://avchat.net/services#installms).

We're also offering [VPS servers with Red5 pre-installed](http://avchat.net/hosting) and configured for AVChat starting with $14.99/month. We use servers in San Francisco, New York, Amsterdam, Singapore and more.
