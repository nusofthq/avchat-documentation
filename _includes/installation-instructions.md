
<h2 id="standalone-installation-instructions">AVChat 3 Standalone installation instructions</h2>

First you need to download the AVChat archive from the client/trial area on nusofthq.com to your computer and extract its contents.

There are 2 sets of files in the AVChat archive, the avchat30 app which goes on your media server and the chat files which go on your web server.

**Setting up the avchat30 application on the media server**

{% include media-server-app.md %}

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
