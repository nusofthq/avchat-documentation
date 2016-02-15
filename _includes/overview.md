
<h2 id="file-groups">AVChat 3 groups of files</h2>

AVChat 3 has two groups of files:

* client side files, that go on your web server (html, js, xml, swf files, etc.) and are loaded by your web site users in their browsers
* media server files that go on your media server (Red5,FMIS,Wowza) these handle all the logic of sending messages between users, banning IPs, accepting connections, etc...



<h2 id="config-files">Configuration files</h2>

AVChat has 2 main configuration files:

1. **avc_settings.xxx** which you will find in your AVChat installation folder on your web server (its's part of the client side files) Starting with build 2060 all the settings from **avc_settings.php** and **avc_settings.aspx.cs** were moved to a new file **avc_settings.xml** from which they are imported. For simple ASP avc_setting.asp remains unchanged:
2. the media server app config file:
..* **settings.asc** on FMS/AMS, you will find it in **/applications/avchat30** on FMS or **/FMSApps/avchat30** on AMS
..* **avchat3.properties** on Red5, you will find it in **/webapps/avchat30**
..* **avchat3.properties** on Wowza , you will find it in **Wowza/conf/avchat30**

There are other less important config files (like the video quality .xml file or the logback_avchat30.xml file on Red5 that specifies where the log files should be created) but we will cover them below as needed.

<h2 id="file-structure">File Structure</h2>

<h2 id="how-avchat-works">How AVChat works</h2>

<h2 id="requirements">Requirements</h2>
