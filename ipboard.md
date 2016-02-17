---
layout: default
title: AVChat Application for IP.Board 3
description: Documentation covering the AVChat Application for IP.Board.
isHome: false
hide: true
---

<section class="bs-docs-section" markdown="1">
  <h1 id="overview" class="page-header">Overview</h1>
  <p class="lead">The AVChat Application for IP.Board 3 handles the integration between your IP.Board 3 web site and our AVChat software:</p>

 * username and gender integration
 * profile url integration
 * profile picture integration
 * Facebook and Twitter integration
 * placement of video chat within the web site (user and admin interface)
 * control what features each member group from IP.Board has access to
 * control AVChat 3 general settings from IP.Board AdminCP area

<div class="bs-callout bs-callout-warning" id="callout-tables-responsive-overflow">
<h4>IP.Board 3.4 End of Support</h4>
<p markdown="1">[Invision Power](https://www.invisionpower.com), the company behind IP.Board, [have announced](https://community.invisionpower.com/blogs/entry/9745-ipboard-34-end-of-support/) in December 2015 the following product cycle for IP.Board 3.4:
</p>
<ul>
<li>March 1, 2016 - End of advanced technical support and development. Basic / limited technical support will continue.</li>
<li>June 1, 2016 - End of all technical support. Only security updates will be provided.</li>
<li>April 1, 2017 - Complete product End of Life (EOL)</li>
 </ul>
</div>
If you're looking for something specific just hit <kbd>Ctrl+F</kbd> on your browser.
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="installation-instructions" class="page-header">Installation Instructions</h1>
<h2 id="download-avchat-and-ipboard34-application">Download & extract archives</h2>
Download these 2 archives from your [private client/trial area](https://nusofthq.com/c/) to your computer:

1. `AVChat 3.0.zip` contains AVChat
2. `avchat3_ipboard_3.x_application.zip` contains the IP.Board Application

Extract the 2 archives somewhere on your computer. Here's their contents:

<img src="{{site.github.url}}/assets/images/ipboard/folder-structure.gif" class="img-responsive" />

<h2 id="installing-the-media-server-app">Media Server Application</h2>
Once we've downloaded &amp; unzipped everything the next thing we need to do is to setup the media server app to which AVChat will connect to.

AVChat uses a media server to send all the audio video and text data between users. AVChat supports the 3 major media servers:

* Red5
* Adobe Media Server
* Wowza

Here's how to install the `avchat30` app on each one of them:

{% include media-server-app.md %}

<h2 id="installing-the-application-and-avchat-on-ipboard34">IP.Board App &amp; AVChat installation</h2>
<h3>Upload files to your website</h3>
Connect using an FTP client to your website and:

1. upload the `videochat` and `admin` folders from the IP.Board archive to your forum's root folder
2. upload the contents of the `Files to upload to your web site` folder (except `admin.html` and `index.html` ) from the AVChat archive to `/videochat/`
<img src="{{site.github.url}}/assets/images/ipboard/copying-avchat-files.png" class="img-responsive" />

<div class="bs-callout bs-callout-info" id="callout-tables-responsive-overflow"> <h4>Folder permissions</h4> <p markdown="1">If your website's hosted on a Linux server CHMOD the `/videochat/uploadedFiles` and `/videochat/tokens` folders to 777.</p> </div>

<h2 id="completing-the-installation">Complete installation</h2>
<h3>Activate the App</h3>
Now go to your IP.Boards's `AdminCP > System` area in a web browser, and click on `Manage Applications & Modules` in the left sidebar.

<img src="{{site.github.url}}/assets/images/ipboard/ipboard-manage-apps.png" class="img-responsive" />

On the Manage Apps page, in the right section under `Applications Not Installed`, the AVChat 3 app will show up. Click <kbd>Install</kbd> and then <kbd>Continue</kbd>.

The app will now install. Once it's done installing a confirmation message will show up:

>This installation is now complete

A new link `Video Chat` will show up in the forum's front end main menu. Clicking on it will bring up the AVChat login screen but AVChat won't yet connect to the media server because it does not know where it is. Onward!

<h3>Connect AVChat to the media server app</h3>
In AdminCP's top menu click on `Other Apps -> AVChat 3`. The AVChat 3 settings page will load.

<img src="{{site.github.url}}/assets/images/ipboard/avchat-3-settings.png" class="img-responsive" />

In the `RTMP Connectionstring` section insert your connection string for the media server app ( it should look like this `rtmp://media-server-ip/avchat30/_definst_` ). Scroll to the bottom and click <kbd>Submit</kbd>.

Your AVChat copy is now configured to connect to the media server.

<h3>Enter the chat and insert the license key</h3>
There's a new `Video Chat` link in IP.Board's front end menu, click on it.

The page with AVChat on it will load and AVChat's login screen will show up.

**Your username will be automatically filled:**

<img src="{{site.github.url}}/assets/images/ipboard/avchat-login-screen-ipboard.png" class="img-responsive" />
Click `[Enter Chat]`. AVChat will now connect to the media server and ask you for the license key.

Enter the key (It's in your [private client/trial area](https://nusofthq.com/c/)) and press `[Submit]`.
</section>

<section class="bs-docs-section" markdown="1">
<h1 id="avchat-ipboard34-application-features" class="page-header">Application Features</h1>
<h2 id="accessing-the-avchat-admin-area-ipboard34">Access the AVChat admin area</h2>
If you want to log in as hidden, kick/ban users, close/delete rooms, view users IP's and a lot of other cool stuff that admins do, you'll have to use the AVChat admin interface.

**By default no IP.Board member group has access to the video chat as admin. You will need to configure this permission for each member group.**

While logged in the AdminCP do the following:

 * Click on `Members` in the top menu  
 * In the left sidebar click on `Manage Member Groups`
 * Click on the member group you want to give AVChat admin access to
 * Click on the AVChat 3 tab, the AVChat permissions for that member group will load
 * Check `Yes` for `Can access chat as admin`
 * Scroll to the bottom and click on <kbd>Complete Edit</kbd>


Now, whenever a user belonging to that member group will access the chat, the AVChat admin interface will now load, instead of the one for regular members.

<h2 id="open-avchat-in-a-popup-window-ipboard34">Open AVChat in a pop up</h2>

By default AVChat 3 is embedded in your IP.Board page but you might want AVChat to open in a pop up window to make it easier for your users to browse your website while in the chat.

1. From AdminCP click on `Other Apps -> AVChat 3`
2. For `Open Method` select `popup`
3. Scroll to the bottom and click <kbd>Save</kbd>

<h2 id="avchat-ipboard34-permissions">Limiting features to certain member groups</h2>
<h3>IP.Board 3 member groups</h3>

IP.Board 3 ships with 6 member groups:

  * *Administrators*
  * *Banned*
  * *Guests*
  * *Members*
  * *Moderators*
  * *Validating*

<img src="{{site.github.url}}/assets/images/ipboard/member-groups.png" class="img-responsive" />

<h3>Limiting AVChat features</h3>

To control what AVChat features (creating rooms, sending PM's, viewing webcams, etc.) are available to each member group do the following from the AdminCP:

1. go to `Members` and the click on `Manage Members Groups` in the left sidebar.
2. click on the member group you want to edit and then on the `AVChat 3` tab.
3. change the AVChat permissions for that member group and click `Complete Edit` at the bottom.

<img src="{{site.github.url}}/assets/images/ipboard/avchat-member-permissions.png" class="img-responsive" />

<h2 id="location-of-avchat-files">Preventing visitors (guests) from accessing the video chat</h2>

From the  AdminCP:

1. Go to `Members` and click on `Manage Member Groups`
2. Click on `Guests` then on the `AVChat 3` tab
3. Select `No` for `Can access chat`
4. Scroll to the bottom and click <kbd>Complete Edit</kbd>

Visitors will still see the `Video Chat` link but they will be asked to sign in or register.

<img src="{{site.github.url}}/assets/images/ipboard/visitor-register-signing.png" class="img-responsive" />


<h2 id="location-of-avchat-files">Location of AVChat &amp; module files</h2>
All the AVChat  files including:

* all the module files
* `index.swf` and `admin.swf`
* language files
* themes
* audio/video quality profile files
* `avc_settings.xml`
* `integration.php`

are located in `/videochat/`.

</section>
