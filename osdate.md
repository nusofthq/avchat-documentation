---
layout: default
title: AVChat osDate add-on
description: Documentation covering the AVChat add-on for osDate
isHome: false
hide: true
---

<section class="bs-docs-section" markdown="1">
  <h1 id="overview" class="page-header">Overview</h1>
  <p class="lead">The AVChat Plugin for osDate handles the integration between your osDate web site and our AVChat software. Here's what it will do:</p>

* user name integration
* profile url integration
* profile image integration
* placement of video chat within the web site (user and admin interface)
* show how many users are in the video chat on every page of your web site
* choose which Membership Types have access to the video chat

If you cannot find the answer you’re looking for here, we encourage you to try our [FAQ](http://avchat.net/faq) or [forums](http://discuss.avchat.net/). There's also more documentation regarding AVChat in the [documentation area for the main standalone version](http://docs.avchat.net/standalone).

If you're looking for something specific just hit <kbd>Ctrl+F</kbd> on your browser.
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="installation-instructions" class="page-header">Installation Instructions</h1>
<h2 id="download-avchat-and-osdate-application">Download & extract archives</h2>
Download these 2 archives from your [private client/trial area](https://nusofthq.com/c/) to your computer:

1. `AVChat 3.0.zip` contains AVChat
2. `avchat3_osdate21x_component.zip` (includes the actual osDate Plugin)

Extract the 2 archives somewhere on your computer.

<h2 id="installing-the-media-server-app">Media Server Application</h2>
Once we've downloaded &amp; unzipped everything the next thing we need to do is to setup the media server app to which AVChat will connect to.

AVChat uses a media server to send all the audio video and text data between users. AVChat supports the 3 major media servers:

* Red5
* Adobe Media Server
* Wowza

Here's how to install the `avchat30` app on each one of them:

{% include media-server-app.md %}

<h2 id="installing-the-application-and-avchat-on-osdate">osDate add-on &amp; AVChat installation</h2>
<h3>Install AVChat</h3>

1. Extract the `avchat3_osdate21x_component.zip` archive and upload the AVChat3 folder inside it to your web site's `plugins` folder.
2. Now go to the folder where you unzipped the latest AVChat3 archive and copy all the content from `Files to upload to your website` to your site `plugins/AVChat3/includes/` folder
3. Now open `plugins/AVChat3/includes/avc_settings.xml` in a text editor and set the `<value>` of the `<connectionstring>` tag
`<value>rtmp://media-server-ip-address/avchat30/_definst_</value>`
4. Chmod the `plugins/AVChat3/includes/uploadedFiles` folder to 777 (otherwise the upload function might not work)
5. Chmod the `tokens` folder (`plugins/AVChat3/includes/tokens`) to 777

<h3>Install the add-on</h3>

1. Log in as an admin in your osDate web site, go to **Tools > Plugins > AVChat 3** and click <kbd>Install</kbd> .
2. Refresh the page and Go to **Plugins > AVChat 3**, log in using a username and enter your license key (it's in your client/trial area on avchathq.com) in the dialog box that shows up after you connect:

<img src="{{site.github.url}}/assets/images/osDate/license_key.jpg" class="img-responsive" />

</section>

<section class="bs-docs-section" markdown="1">
<h1 id="avchat-osDate-application-features" class="page-header">Add-on Features</h1>
<h2 id="accessing-the-avchat-admin-area-osDate">Access the AVChat admin area</h2>

From the osDate admin area go to **Plugins > AVChat 3**

<h2 id="osDate-member-levels">osDate's user levels and AVChat</h2>

You can configure who has access to the video chat by going to: **Tools > Plugins > AVChat 3 > Edit** .

<h2 id="allowing-visitors-osDate">Allowing visitors to join the video chat</h2>


By default the AVChat Plugin for osDate does not allow visitors of your web site to enter the video chat. Only signed in users are allowed in the video chat.

To allow visitors/guests to join the video chat login via FTP to your web site and edit this file: `[your site root]/plugins/avchat3/includes/integration.php` .

At the end of the file set `$avconfig['showLoginError']=0`;

Save the file and upload it back to your web site.

</section>
