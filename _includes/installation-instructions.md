
<h2 id="standalone-installation-instructions">AVChat 3 standalone installation instructions</h2>

First you need to download the AVChat archive from the [client/trial area on nusofthq.com](https://nusofthq.com/c/) to your computer and extract it's contents.

There are 2 sets of files in the AVChat archive:

* the chat client files which go on your web server
* the server side `avchat30` app for each media server (Red5/AMS/Wowza)

### Setting up the `avchat30` application on the media server


{% include media-server-app.md %}


### Installing AVChat standalone in a folder on your web site

1. Create a new `chat` folder in your web site and upload the contents of `Files to upload to your web site` from the AVChat archive to it.
2. Edit `avc_settings.xml` with a text editor, and set the `<value>` of the first XML tag - `<connectionstring>` to: `<value>rtmp://my-media-server.com/avchat30/_definst_</value>` where `my-media-server.com` is the domain name or ip of the server where your media server is installed.
3. CHMOD the `uploadedFiles` and `tokens` folder to 777 (otherwise the upload adn token authentication functions might not work).
5. Go to http://yoursite.com/chat/, enter the chat and, when prompted, enter the license key.
<img src="http://docs.avchat.net/assets/images/license_key.jpg" class="img-responsive"/>
6. To access the admin interface go to http://yoursite.com/chat/admin.html.

<div class="alert alert-warning" role="alert"><p markdown="1">Since this is a standalone installation we strongly suggest you rename the `admin.html` and `admin.swf` files for security reasons. Don't forget to edit the renamed `admin.html` to point to the renamed `admin.swf`.</p></div>

If you're using ASP.NET on the web server, and it doesn't run PHP, you need to [configure AVChat to use the .aspx server side files](#switching-between-config-files).

<h2 id="switching-between-config-files">Switching between the PHP and ASPX configuration files in AVChat</h2>

You have the possibility to switch the type of the configuration files used by AVChat to communicate with the web server (load the settings, request tokens, etc...).

Switching to other types of config files (like the .aspx ones also provided with AVChat) can be done via the `sscode` flash var explained below.

By default AVChat uses the PHP set of files (`avc_settings.php`, `token_request.php`, etc.) so we need to tell it to use the .aspx set of files. To do that we will use the `sscode` flash var.

1. Open up `index.html` and `admin.html` in a text editor and find the following variable: `sscode :"php"`, and replace with:
`sscode :"aspx"`, like this:
<img src="http://docs.avchat.net/assets/images/sscodeaspx.jpg" class="img-responsive"/>
2. Edit `avc_settings.xml` and set the and set the `<value>` of the `<stylecssurl>` tag to style.aspx like this `<value>style.aspx</value>`:
<img src="http://docs.avchat.net/assets/images/stylecss.jpg" class="img-responsive"/>

The `sscode` flash var, if not specified, defaults to `php`.

Instead of `aspx` you can use any other extension (.rb, .asp, etc) as long as the corresponding files exist in the video chat folder.

<h2 id="using-different-medias-server-apps">Connecting different AVChat installations to the same media server.</h2>

When you have AVChat installed in 2 different locations (different folders or different websites) there are 3 ways to connect them to the same media server :

1. Connect them to the same app and app instance (users from one location will interact with users from a different location)
2. Connect them to the same app but different instance (separate rooms and users but same sahred application level config file)
3. Connect them to a different `avchat30` app (totally independent)

<!--
### Introduction

AVChat is made of 2 parts:

* the client side files that go on your web server (html, xml, swf files, etc.)
* the media server application (by default `avchat30`) that goes on your media server (Red5, AMS, Wowza)

The connection string inside the avc_settings.xxx is made out of 4 parts and when combined it looks like this: `rtmp://my-media-server.com/avchat30/\_definst\_` .

* rtmp is the protocol used to communicate between the AVChat client and the media server.
* my-media-server.com is the address where you host your media server (AMS, RED5, Wowza), it can also be an ip.
* `avchat30`  is the (default) name of the application on the media server to which your users will connect.
* `\_definst\_` is the instance of the `avchat30` app to which we connect
-->

### Solution 1: Using the same app instance for 2 or more AVChat 3 installations

As long as you use the same connection string, users from different installations of AVChat can interact with each other in the same rooms.

<div class="alert alert-warning" role="alert"><p>
Because the <em>application instance</em> running on the media server tries to detect the URL of the AVChat installation on the web server, the following features will only work with one of the AVChat copies:

<ul><li>external users &amp; rooms list</li>
<li>token authentication</li>
<li>reports</li>
<li>record API (feature exists only on Red5)</li></ul>
</p></div>

### Solution 2: Using different app instances for 2 or more AVChat 3 installations

There is a quick way of setting up multiple **separate** installations of AVChat to work with the same media server app. It involves using *application instances* and can be used the same way with all 3 media-servers (AMS, Wowza and Red5).

The default application instance for all media servers is `_definst_` . To force AVChat to connect to a new instance simply edit the connection string and change `_definst_` to any other instance name like `siteB` or `userK`, the new connection string should look like `rtmp://my-media-server.com/avchat30/siteB`.

<div class="alert alert-warning" role="alert"><p markdown="1">By using *application instances*, both AVChat installations will use the same media server app and thus the same settings files (`settings.asc` on AMS and `avchat3.properties` on Red5/Wowza) so be careful if you hardcode any paths or if you change any options in those 2 files because it will affect both installations. For more freedom use different application folders as outlined below.</p></div>

### Solution 3: Using different apps for 2 or more AVChat 3 installations (totally independent)

<!--
To connect 2 installations of the AVChat client to different `avchat30` apps on the same media server, you will basically have to:

1. duplicate the `avchat30` app on the media server
2. connect the second installation of AVChat to the new `avchat30` app by changing the connection string.-->

#### Adobe Media Server

On AMS the process is pretty straight forward. All the app files are placed inside the `AMS/applications/avchat30` folder. To create a new `avchat30` app:

1. duplicate the `avchat30` folder
2. rename the new one to `avchat30_siteX` (or to any other name that fits you).

You should now have 2 folders application folders:

* `avchat30`
* `avchat30_siteX`

To connect the second installation of AVChat to the new AMS app use this connection string in `avc_settings.xml`: `rtmp://my-media-server.com/avchat30_siteX/_definst_`.

<div class="alert alert-info" role="alert">With this kind of setup 2 different versions of AVChat (3.5 and 3.6 for example) can be run at the same time by AMS. Just be careful to connect the correct AVChat copy to the correct media server application.</div>

#### Red5

All the app files for AVChat are placed inside the `Red5/webapps/avchat30` folder. To create a new `avchat30` app:

1. duplicate the `avchat30` folder and
2. rename the new one to `avchat30_siteX` (or to any other name that fits you).

Now in the `avchat30_siteX/WEB_INF/` folder:

1. edit `red5-web.properties` and change: `webapp.contextPath=/avchat30` to `webapp.contextPath=/avchat30_siteX`
2. edit `web.xml` and change

        <context-param>
        <param-name>webAppRootKey</param-name>
        <param-value>/avchat30</param-value>
        </context-param>
to
        <context-param>
        <param-name>webAppRootKey</param-name>
        <param-value>/avchat30_siteX</param-value>
        </context-param>
3. rename `logback_avchat30.xml` located in `Red5/webapps/avchat30_siteX/WEB-INF/classes/` to `logback_avchat30_siteX.xml`
4. now edit it and change:

        <jmxConfigurator contextName="avchat30" />
to

        <jmxConfigurator contextName="avchat30_siteX" />
and

        <fileNamePattern>log/avchat30.%d{yyyy-MM-dd}.log</fileNamePattern>
to

        <fileNamePattern>log/avchat30_siteX.%d{yyyy-MM-dd}.log</fileNamePattern>


Steps 3 and 4 will ensure we will get separate logs for each app.

To connect AVChat to the new Red5 app use the following connection string in `avc_settings.xml` : `rtmp://my-media-server.com/avchat30_siteX/_definst_`  .

<div class="alert alert-info" role="alert">With this kind of setup 2 different versions of AVChat (3.5 and 3.6 for example) can be run at the same time by Red5. Just be careful to connect the correct client to the correct server side application.</div>

#### Wowza

This one is very simple:

1. duplicate the `Wowza/applications/avchat30` folder and rename it to `avchat30_siteX`.
2. duplicate the `Wowza/conf/avchat30` folder and rename it to `avchat30_siteX`.


To connect AVChat to the new Wowza app use the following connection string in `avc_settings.xml` : `rtmp://my-media-server.com/avchat30_siteX/_definst_`  .

<div class="alert alert-warning" role="alert">Wowza does not support running of 2 different versions of AVChat at the same time. The steps provided above only allow the setup of multiple `avchat30` apps of the same version/build.</div>

<h2 id="change-license-key">How to change the license key</h2>

Here are 3 setiations where you will have to change the AVChat license key:

* Switch from trial to non-trial key or to a new trial key.
* Switch the domain on which the software will be used.
* Upgrade from Lite (20 users) to Basic (40 users).

**What do I have to do?**

1. Log in the video chat using the admin interface (`admin.html` or `admin.swf`)
2. Click the <kbd>Settings</kbd> button at the top
3. In the window that shows up, delete the old key from the text field and insert the new key
4. Press the <kbd>Change Key</kbd> button
5. If successful, you should now see the new limits/expiration date/domain above the license key text field <img src="http://docs.avchat.net/assets/images/licensekey.jpg" class="img-responsive"/>

<h2 id="reset-license-key">How to reset the license key</h2>


If something goes awfully wrong and you find yourself locked out of the video chat (you’ve inserted a key for a domain to which you do not have yet access or has not yet been registered ) you can reset the license key by following these simple steps:

1. Delete this file
  * on Red5: red5/webapps/avchat30/persistence/SharedObject/\_definst\_/`licensekey.red5`
  * on AMS: fms/applications/avchat30/sharedobjects/\_definst\_/`licensekey.fso`
  * on Wowza: wowza/applications/avchat30/sharedobjects/\_definst\_/`licensekey.rso`
2. Restart Red5, AMS or Wowza
3. Enter the video chat and you will be asked for the key again.


<h2 id="installed-version">What AVChat version and build do I have installed?</h2>

To see what AVChat version and build you have installed you need to right click any element in the video chat. The first item in the menu that shows up conatins the version number (3.6 in this case) and the build number (3648):

![alt text](http://docs.avchat.net/assets/images/build.png)

**Why is the build number important?**

The build number allows you to check if you have the latest version of our software. If your build number is 3078 and on the blog we announce a new release with the build number 3097, then it means you should consider upgrading your installation.

Each increment in the build number might represent any of the following things:

* bug fix
* new feature
* new file
* new entry in the translation file
* new setting in the config files

You should check the release notes for the exact new features and bug fixes in each build.

**Build numbers on our live AVChat demo**

[Our online AVChat demo](http://avchat.net/demos/avchat30) is frequently updated, so even tough the latest build available for download might be 3097, the demo might have a higher build number. We update the demo more frequently to test new features and UI changes before we release these changes to customers.

<h2 id="what-we-need-for-installation">What we need to install AVChat 3</h2>

Here's what we need to install AVChat:

1. FTP access to the web site (or folder) where AVChat will be installed
2. If you've purchased [an integration kit](http://avchat.net/integrations/) we will need admin acess to the admin area of your CMS (Joomla!, Drupal, etc.).
3. root ssh access to the vps/dedicated server where the media server (Red5/AMS/Wowza) is installed (on Windows servers Remote Desktop access will do)

If you don't have a media server we offer VPS media server hosting services starting from $14.99/month. More info [here](http://avchat.net/hosting).

Please open a support ticket from [your client area](https://nusofthq.com/c/) and send us the data. Our team will handle the installation.

AVChat installations are generally made in the same day if all the data above is correct and complete.

<h2 id="what-we-need-for-installation-media-server">What we need to install a media server</h2>

We offer [Media Sever Installation Service](http://avchat.net/services#installms) for a $99 one time fee.

Here's what we need to install a media server:

1. root ssh access to the vps/cloud server where you want the media server (Red5/AMS/Wowza) to be installed if have a Linux Server, or Remote Desktop if you have a Windows server.
2. AMS or Wowza license key if any.

Please send the data to [support](support@nusofthq.com) after purchase.

Media server installations are generally made in the same day if all the data provided is correct and complete. Our tech support hours are 8am to 6:3pm GMT.

<h2 id="switch-from-trial-to-licensed">Switching from a trial version of AVChat 3 to a purchased version</h2>

If you have a trial version of AVChat installed and have purchased a license, switching to production is very easy:

1. Download the purchased version of AVChat and unzip it
3. Copy and replace `index.swf` and `admin.swf` from the extracted archive to your trial AVChat installation folder.

[Also don't forget to replace the trial license key, with the purchased one](http://docs.avchat.net/standalone#change-license-key).

That's it! You are now running the licensed version of AVChat.

<div class="alert alert-info" role="alert">Be careful that the trial version you had installed and the licensed version you bought correspond.</div>

<h2 id="installing-mobile-version">Installing the mobile version of AVChat 3</h2>

### AVChat 3.6 and newer

Starting with [AVChat 3.6](http://avchat.net/blog/avchat-3-6-brings-a-new-mobile-version-and-red5-1-0-5-compatibility/) the mobile version of AVChat only works on Red5 1.0.5 and up. The new mobile HTML 5 client introduced in AVChat 3.6 uses WebSockets to communicate and Red5 is the only media server supporting this technology.

Here's how to set it up:

On the media server/Red5:

1. Download json-smart-2.0-RC3.jar library from [here](https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/json-smart/json-smart-2.0-RC3.jar) and put in the `Red5/plugins` folder (applies to both Red5 1.0.5 and 1.0.6)
2. Open `Red5/conf/red5.properties` and scroll dow to the `#WebSocket` section
4. Change the `ws.host` default value (`0.0.0.0`) with your media server IP address
5. Save the file and restart Red5

On the webserver:

1. Download the mobile archive from your private client area at [https://nusofthq.com](https://nusofthq.com) and unzip
2. Copy the `ws` folder to your AVChat installation directory.

### AVChat 3.5 and older

On the media server side, inside the settings file, the web server IP needs to be defined.

Here's how to set it:

On Adobe Media Server:

* open `settings.asc` file (you will find it in `AMS/applications/avchat30`)
* search for `webServerIP`
* replace the existing IP (`127.0.0.1`) with your website's IP ([use this tool](http://mxtoolbox.com/DNSLookup.aspx) to find out the ip)

On Red5:

* open `avchat3.properties` file (you will find it in `/Red5/webapps/avchat30`)
* search for `webServerIP`
* replace the existing IP (`127.0.0.1`) with your website's IP ([use this tool](http://mxtoolbox.com/DNSLookup.aspx) to find out the ip)
