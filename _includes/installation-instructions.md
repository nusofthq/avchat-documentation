
<h2 id="standalone-installation-instructions">AVChat 3 Standalone installation instructions</h2>

First you need to download the AVChat archive from the client/trial area on nusofthq.com to your computer and extract its contents.

There are 2 sets of files in the AVChat archive, the avchat30 app which goes on your media server and the chat files which go on your web server.

**Setting up the avchat30 application on the media server**

<ul class="nav nav-tabs" id="serversTab">
  <li class="active"><a data-target="#red5" data-toggle="tab">Red5</a></li>
  <li><a data-target="#ams" data-toggle="tab">Adobe Media Server</a></li>
  <li><a data-target="#wowza" data-toggle="tab">Wowza</a></li>
</ul>

<div class="tab-content" markdown ="1">

  <div class="tab-pane active" id="red5">

Upload the `avchat30` folder from the **Files to upload to your media server (Red5)** folder to your Red5's **webapps** folder (C:\Program Files\Red5\webapps on Win, /opt/red5/webapps/ on Linux).

On Linux, chmod the new `avchat30` folder to 777.

Restart the Red5 server.

  </div>

  <div class="tab-pane" id="ams">

Upload the `avchat30` folder (you will find it in your AVChat archive in the **Files to upload to your media server (FMS) folder)** to the **applications** folder of your AMS installation.

Chmod the new `avchat30` folder to 777.

  </div>

  <div class="tab-pane" id="wowza">

Upload the `applications`, `lib` and `conf` folders from the **Files to upload to your media server (Wowza)** folder to the root folder of your Wowza Media Server installation.

Restart the Wowza server.

Starting with Wowza Streaming Engine 4, a new GUI has been added that allows you to control the server and individual applications. This can be accessed using a browserby going to http://WOWZA_SERVER_ADDRESS:8088/enginemanager/.

Wowza Streaming Engine 4 comes with the default stream prefix **mp4**. This needs to be changed to **flv**. Here's how:

1. Go to http://WOWZA_SERVER_ADDRESS:8088/enginemanager/
2. From the top menu click the [Server] page
3. In Server Setup click Edit
4. Change Default Stream Prefix from mp4 to flv
5. Save

  </div>

</div>

<script>
jQuery(function () {
    jQuery('#serversTab a:last').tab('show')
})
</script>


**Installing AVChat Standalone in a folder on your web site**

1. Create a new folder in your web site and upload the contents of **Files to upload to your web site** (from the AVChat archive received) to it.
2. Edit `avc_settings.xml` with a text editor, and set the `<value>` of the first XML tag - `<connectionstring>` to: `<value>rtmp://my-media-server.com/avchat30/_definst_</value>` where `my-media-server.com` is the domain name or ip of the server where your media server is installed.
3. CHMOD the **uploadedFiles** folder to 777 (otherwise the upload function might not work).
4. CHMOD the tokens folder to 777.
5. Go to http://yoursite.com/your_new_video_chat_folder/, log in and enter your license key in the dialog box that shows up after the connection is established.
![alt text](http://docs.avchat.net/assets/images/license_key.jpg)
6. To access the admin interface go to http://yoursite.com/your_new_video_chat_folder/admin.html. We strongly suggest you rename `admin.html` and `admin.swf` files for security reasons.

If you're on a ASP.NET server and it doesn't run PHP you need to configure AVChat to use the .aspx server side files.

<h2 id="using-different-medias-server-apps">Using different media server apps for 2 or more AVChat 3 installations</h2>

<h2 id="using-different-app-instances">Using different app instances for 2 or more AVChat 3 installations</h2>

<h2 id="switching-between-config-files">Switching between the PHP and ASPX configuration files in AVChat</h2>

<h2 id="change-license-key">How to change the license key</h2>

<h2 id="reset-license-key">How to reset the license key</h2>

<h2 id="installed-version">What AVChat build/version I have installed?</h2>

<h2 id="what-we-need-for-installation">What we need if you want us to perform the AVChat 3 installation</h2>

<h2 id="what-we-need-for-installation-media-server">What we need if you want us to perform the media server (Red5/AMS/Wowza) installation</h2>

<h2 id="switch-from-trial-to-licensed">Switching from a trial version of AVChat 3 to a licensed version</h2>

<h2 id="installing-mobile-version">Installing the mobile version of AVChat 3</h2>
