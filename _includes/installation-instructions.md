
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

You might have 2 installations of AVChat, either on the same domain or on different domains that you want to connect to the same media server.

**Introduction**

AVChat is made of 2 parts:

* the client side files that go on your web server (html, xml, swf files, etc.)
* the media server application (by default avchat30) that goes on your media server (Red5, AMS, Wowza)

The connection string inside the avc_settings.xxx is made out of 4 parts and when combined it looks like this: `rtmp://my-media-server.com/avchat30/\_definst\_` .

* rtmp is the protocol used to communicate between the AVChat client and the media server.
* my-media-server.com is the address where you host your Media Server (AMS, RED5, Wowza), it can also be an ip.
* avchat30 this is the (default) name of the application on the media server to which your users will connect.
* **\_definst\_** is the instance of the avchat30 app to which we connect (AMS for example supports multiple instances).

To connect 2 installations of the AVChat client to the same media server, you will basically have to:

1. duplicate the avchat30 app on the media server
2. connect the second installation of AVChat to the new avchat30 app by changing the connection string.

On Red5 and Wowza it's slightly more complicated so make sure you read the long versions below:

**Long version: Flash Media Interactive Server(AMS)**

On AMS the process is pretty straight forward.

All the app files for AVChat are placed inside the AMS/applications/**avchat30** folder. To create a new avchat30 app:

1. duplicate the avchat30 folder and
2. rename the new one to avchat30_siteX (or to any other name that fits you).

You should now have 2 folders in your AMS/applications folder:

* applications/**avchat30**
* applications/**avchat30_siteX**

That's all!

To connect AVChat to the new AMS app use:
rtmp://my-media-server.com/**avchat30_siteX**/\_definst\_ in `avc_settings.xml`.

<div class="alert alert-info" role="alert">With this kind of setup 2 different versions of AVChat can be run at the same time by FMS/AMS. Just be careful to connect the correct client to the correct server side application.</div>

**Long version: Red5**

All the app files for AVChat are placed inside the Red5/webapps/avchat30 folder. To create a new avchat30 app:

1. duplicate the **avchat30** folder and
2. rename the new one to **avchat30_siteX** (or to any other name that fits you).
3. edit avchat30_siteX/WEB_INF/`red5-web.properties` and change: `webapp.contextPath=/avchat30` to `webapp.contextPath=/avchat30_siteX`
4. edit avchat30_siteX/WEB_INF/`web.xml` and change
```
<context-param>
<param-name>webAppRootKey</param-name>
<param-value>/avchat30</param-value>
```
to
```
<context-param>
<param-name>webAppRootKey</param-name>
<param-value>/avchat30_siteX</param-value>
</context-param>
```
5. rename this file:
webapps/avchat30_siteX/WEB-INF/classes/`logback_avchat30.xml`
to
webapps/avchat30_siteX/WEB-INF/classes/`logback_avchat30_siteX.xml`
6. edit
webapps/avchat30_siteX/WEB-INFclasses/`logback_avchat30_siteX.xml`
and change:
```
<jmxConfigurator contextName="avchat30" />
```
to
```
<jmxConfigurator contextName="avchat30_siteX" />
```
and
```
<fileNamePattern>log/avchat30.%d{yyyy-MM-dd}.log</fileNamePattern>
```
to
```
<fileNamePattern>log/avchat30_siteX.%d{yyyy-MM-dd}.log</fileNamePattern>
```

Steps 5 and 6 will ensure we will get separate logs for each app.

That's all!

To connect AVChat to the new Red5 app use:
rtmp://my-media-server.com/avchat30_siteX/\_definst\_ in `avc_settings.xml` .

<div class="alert alert-info" role="alert">With this kind of setup 2 different versions of AVChat can be run at the same time by Red5. Just be carefull to connect the correct client to the correct server side application.</div>

**Long version: Wowza**

This one is very simple!

Just duplicate the **Wowza/applications/avchat30** folder and rename it to **avchat30_siteX**. Do the same thing with the **Wowza/conf/avchat30** folder: duplicate it and rename it to **avchat30_siteX**.

That's all!

To connect AVChat to the initial app/folder use:
rtmp://my-media-server.com/avchat30/\_definst\_ in `avc_settings.xml` .

To connect AVChat to the second app/folder use:
rtmp://my-media-server.com/avchat30_siteX/\_definst\_ in `avc_settings.xml` .

<div class="alert alert-info" role="alert">Wowza does NOT support running of 2 different versions of AVChat at the same time. The steps provided above only allow the setup of multiple apps of the SAME version.</div>

<h2 id="using-different-app-instances">Using different app instances for 2 or more AVChat 3 installations</h2>



There is also a 'quick and dirty' version of setting up multiple installations of AVChat to work on the same media server.

This version involves using application instances and can be used the same way with all of the 3 media-servers (FMS/AMS, Wowza and Red5).

To tell the media server to create a new instance of the same application simply edit the connection string of the second AVChat installation by changing **\_definst\_** to any other specific name like **newInstance**.

So the final result will be:

* One AVChat installation will have the default connection string type: **rtmp://my-media-server.com/avchat30/\_definst\_**
* The second AVChat installation will have the modified connection string: **rtmp://my-media-server.com/avchat30/newInstance**

Now each installation will connect to it's own instance of the media server side AVChat application.

<div class="alert alert-info" role="alert">By using this kind of setup both AVChat installations will use the same media server settings files (settings.asc/avchat3.properties). Also it is possible that at least one of the installations won't correctly update the external users list.</div>


<h2 id="switching-between-config-files">Switching between the PHP and ASPX configuration files in AVChat</h2>

<h2 id="change-license-key">How to change the license key</h2>

<h2 id="reset-license-key">How to reset the license key</h2>

<h2 id="installed-version">What AVChat build/version I have installed?</h2>

<h2 id="what-we-need-for-installation">What we need if you want us to perform the AVChat 3 installation</h2>

<h2 id="what-we-need-for-installation-media-server">What we need if you want us to perform the media server (Red5/AMS/Wowza) installation</h2>

<h2 id="switch-from-trial-to-licensed">Switching from a trial version of AVChat 3 to a licensed version</h2>

<h2 id="installing-mobile-version">Installing the mobile version of AVChat 3</h2>
