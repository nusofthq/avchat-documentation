
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
