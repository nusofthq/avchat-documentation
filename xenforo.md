---
layout: default
title: AVChat xenForo Add-on
description: Documentation covering the AVChat add-on for xenForo
isHome: false
hide: true
---

<section class="bs-docs-section" markdown="1">
  <h1 id="overview" class="page-header">Overview</h1>
  <p class="lead">The AVChat Video Chat Add-on for xenForo handles the integration between your xenForo community and our AVChat software:</p>

 * username and gender integration
 * profile url integration
 * profile picture integration
 * Facebook and Twitter integration
 * placement of video chat within the web site (user and admin interface)
 * control what features each user group from xenForo has access to
 * control AVChat 3 general settings from the xenForo admin area

If you're looking for something specific just hit <kbd>Ctrl+F</kbd> on your browser.
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="installation-instructions" class="page-header">Installation Instructions</h1>
<h2 id="download-avchat-and-ipboard34-application">Download & extract archives</h2>
Download these 2 archives from your [private client/trial area](https://nusofthq.com/c/) to your computer:

1. `AVChat 3.0.zip` contains AVChat
2. `avchat3_video_chat_xenforo_addon.zip` contains the xenForo add-on

Extract the 2 archives somewhere on your computer.

<h2 id="installing-the-media-server-app">Media Server Application</h2>
Once we've downloaded &amp; unzipped everything the next thing we need to do is to setup the media server app to which AVChat will connect to.

AVChat uses a media server to send all the audio video and text data between users. AVChat supports the 3 major media servers:

* Red5
* Adobe Media Server
* Wowza

Here's how to install the `avchat30` app on each one of them:

{% include media-server-app.md %}

<h2 id="installing-the-application-and-avchat-on-ipboard34">xenForo add-on &amp; AVChat installation</h2>
<h3>Upload files to your website</h3>
Connect using an FTP client to your website and:

1. upload the `library` and `videochat` folders from the xenForo's archive to your forum's root folder
2. upload the contents of the `Files to upload to your web site` folder (except `admin.html` and `index.html` ) from the AVChat archive to `/videochat/`
3. Edit the `.htaccess`in your forum's root folder and replace the following lines:

{% highlight ActionScript %}
RewriteRule
^(data/|js/|styles/|install/|favicon\.ico|crossdomain\.xml|robots\.txt) - [NC,L]
{% endhighlight %}
with:

{% highlight ActionScript %}
RewriteRule
^(data/|js/|styles/|install/|favicon\.ico|crossdomain\.xml|robots\.txt|videochat/|index_popup\.php) - [NC,L]
{% endhighlight %}

<div class="bs-callout bs-callout-info" id="callout-tables-responsive-overflow"> <h4>Folder permissions</h4> <p markdown="1">If your website's hosted on a Linux server CHMOD the `/videochat/uploadedFiles` and `/videochat/tokens` folders to 777.</p> </div>

<h2 id="completing-the-installation">Complete installation</h2>
<h3>Install the add-on</h3>
In the xenForos's `Admin CP` area click on `Install Add-on` in the left side menu. On the Install New Add-on page click on <kbd>Choose&nbsp;File</kbd> and select the `addon-AVChat3VideoChat.xml` from the xenForo add-on archive. Click <kbd>Install Add-on</kbd>

<h3>Connect AVChat to the media server app</h3>
In Admin CP's top menu  go to `Home -> Options`. Select `AVChat 3 Video Chat Options` from the list.

In the `RTMP Connectionstring` section insert your connection string for the media server app ( it should look like this `rtmp://media-server-ip/avchat30/_definst_` ). Scroll to the bottom and click <kbd>Save Changes</kbd>.

Your AVChat copy is now configured to connect to the media server.

<h3>Enter the chat and insert the license key</h3>
There's a new `Video Chat` link in xenForo's front end menu, click on it.

The page with AVChat on it will load and AVChat's login screen will show up.

**Your username will be automatically filled:**

Click `[Enter Chat]`. AVChat will now connect to the media server and ask you for the license key.

Enter the key (It's in your [private client/trial area](https://nusofthq.com/c/)) and press `[Submit]`.
</section>

<section class="bs-docs-section" markdown="1">
<h1 id="avchat-ipboard34-application-features" class="page-header">Add-on Features</h1>
<h2 id="accessing-the-avchat-admin-area-ipboard34">Access the AVChat admin area</h2>
If you want to log in as hidden, kick/ban users, close/delete rooms, view users IP's and a lot of other cool stuff that admins do, you'll have to use the AVChat admin interface.

**By default no xenForo user group has access to the video chat as admin. You will need to configure this permission for each user group.**

While logged in the Admin CP do the following:

 * Click on `Users` in the top menu
 * Click on the user group you want to give AVChat admin access to
 * On the following page search for `AVChat 3 Video Chat - User Permissions` and you will see AVChat's permissions list
 * Check `Allow` (the green box) for `Can access chat as admin`
 * Scroll to the bottom and click on <kbd>Update Permissions</kbd>


Now, whenever a user belonging to that user group will access the chat, the AVChat admin interface will now load, instead of the one for regular members.

<h2 id="open-avchat-in-a-popup-window-ipboard34">Open AVChat in a pop up</h2>

By default AVChat 3 is embedded in your xenForo page but you might want AVChat to open in a pop up window to make it easier for your users to browse your website while in the chat.

1. From Admin CP go to `Home -> Options`
2. Search for `AVChat 3 Video Chat Options` and click on it
2. Select `Popup` for `Display Mode`
3. Scroll to the bottom and click <kbd>Save Changes</kbd>

<h2 id="avchat-ipboard34-permissions">Limiting features to certain user groups</h2>
<h3>xenForo 3 user groups</h3>

xenForo 3 ships with 4 user groups:

  * *Administrative*
  * *Moderating*
  * *Registered*
  * *Unregistered / Unconfirmed*

<h3>Limiting AVChat features</h3>

To control what AVChat features (creating rooms, sending PM's, viewing webcams, etc.) are available to each user group do the following from the AdminCP:

1. go to `Users` and the click on `User Group Permissions` in the left sidebar.
2. click on the user group you want to edit and then search for `AVChat 3 Video Chat - User Permissions`
3. change the AVChat permissions for that user group and click <kbd>Update Permissions</kbd> at the bottom.

<!--
<h2 id="location-of-avchat-files">Preventing visitors (guests) from accessing the video chat</h2>

From the  AdminCP:

1. Go to `Members` and click on `Manage Member Groups`
2. Click on `Guests` then on the `AVChat 3` tab
3. Select `No` for `Can access chat`
4. Scroll to the bottom and click <kbd>Complete Edit</kbd>

Visitors will still see the `Video Chat` link but they will be asked to sign in or register.

<img src="{{site.github.url}}/assets/images/ipboard/visitor-register-signing.png" class="img-responsive" />
-->

<h2 id="location-of-avchat-files">Location of AVChat &amp; add-on files</h2>
All the AVChat  files including:

* all the add-on files
* `index.swf` and `admin.swf`
* language files
* themes
* audio/video quality profile files
* `avc_settings.xml`
* `integration.php`

are located in `/videochat/`.

</section>
