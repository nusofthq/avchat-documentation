---
layout: default
title: AVChat Module for PHPFox 3.8
description: Documentation covering the AVChat module for PHPFox 3.8.
isHome: false
hide: true
---

<section class="bs-docs-section" markdown="1">
  <h1 id="overview" class="page-header">Overview</h1>
  <p class="lead">The AVChat Module for PHPFox 3.8 (Nebula) handles the integration between a PHPFox 3.8 web site and the AVChat video chat software.</p>

  If you're looking for something specific just hit <kbd>Ctrl+F</kbd> on your browser.
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="installation-instructions" class="page-header">Installation Instructions</h1>
<h2 id="download-avchat-and-phpfox38-module">Download & extract archives</h2>
Download these 2 archives from your [private client/trial area](https://nusofthq.com/c/) to your computer:

1. `AVChat 3.0.zip` contains AVChat
2. `avchat3_phpfox30x_module.zip` contains the PHPFox module

Extract the 2 archives somewhere on your computer.

<h2 id="installing-the-media-server-app">Media Server Application</h2>
Once we've downloaded &amp; unzipped everything the next thing we need to do is to setup the media server app to which AVChat will connect to.

AVChat uses a media server to send all the audio video and text data between users. AVChat supports the 3 major media servers:

* Red5
* Adobe Media Server
* Wowza

Here's how to install the `avchat30` app on each one of them:

{% include media-server-app.md %}

<h2 id="installing-the-module-and-avchat-on-phpfox38">Module & AVChat installation</h2>
<h3>Upload files to your website</h3>
Connect using an FTP client to your website and:

1. upload the `include` and `module` folders from the PHPFox module archive to your website root
2. upload the contents of the `Files to upload to your web site` folder from  the AVChat archive to `/module/avchat3/include/plugin/`

<div class="bs-callout bs-callout-info" id="callout-tables-responsive-overflow"> <h4>Folder permissions</h4> <p markdown="1">If your website's hosted on a Linux server go to `/module/avchat3/include/plugin/` and CHMOD the `uploadedFiles` and `tokens` folders to 777.</p> </div>

<h2 id="completing-the-installation">Complete installation</h2>
<h3>Activate the module</h3>
Now open your PHPFox's `AdminCP` area in a web browser, and go to `Extensions->Import Products`.

<img src="{{site.github.url}}/assets/images/phpfox/extensions-import-products.png" class="img-responsive" />

You will be prompted to install `AVChat3 Module for phpFox 3`. Click the Install link. The module will install and you'll receive a confirmation message:

>Product successfully installed.

<h3>Connect AVChat to the media server app</h3>
Now go to `Settings->Manage Settings` and click on the `General AVChat 3 Settings` link. The AVChat 3 settings page will load.

<img src="{{site.github.url}}/assets/images/phpfox/connection-string.png" class="img-responsive" />

In the `RTMP Connectionstring` section insert your connection string for the media server app ( it should look like this `rtmp://media-server-ip/avchat30/_definst_` ). Scroll to the bottom and click <kbd>Submit</kbd>.

Your AVChat copy is now configured to connect to the media server.

<h3>Enter the chat, connect and insert the license key</h3>
There's a new `Video Chat` link in the PHPFox menu, click on it.
<img src="{{site.github.url}}/assets/images/phpfox/avchat-link-in-menu.png" class="img-responsive" />
The page with AVChat on it will load and AVChat's login screen will show up.

**Your username will be automatically filled and the gender will be pre-selected:**

<img src="{{site.github.url}}/assets/images/phpfox/avchat-connect.png" class="img-responsive" />
Click `[Connect]`. AVChat will now connect to the media server and ask you for the license key.

Enter the key (It's in your [private client/trial area](https://nusofthq.com/c/)) and press `[Submit]`.
</section>

<section class="bs-docs-section" markdown="1">
<h1 id="avchat-phpfox38-module-features" class="page-header">Module Features</h1>
<h2 id="accessing-the-avchat-admin-area-phpfox38">Access the AVChat admin area</h2>
If you want to log in as hidden, kick/ban users, close/delete rooms, view users IP's and a lot of other cool stuff that admins do, you'll have to use the AVChat admin interface.

**By default, users that are part of the Administrators and Staff user groups have access to the admin area of AVChat.**

While logged in click the Video Chat link in the main menu. The AVChat admin interface will automatically load if you have access to it.

<h2 id="open-avchat-in-a-popup-window-phpfox38">Open AVChat in a pop up</h2>

You might want AVChat to open in a pop up window to make it easier for your users to browse your website while in the chat.

1. From Admin CP click on `Settings -> Manage Settings`
2. Click on `General AVChat 3 Settings`
<img src="{{site.github.url}}/assets/images/phpfox/admin-manage-settings.png" class="img-responsive" />
3. Under `Open Method` select `popup`
4. Click on <kbd>Submit</kbd> at the bottom of the page

<h2 id="avchat-phpfox38-permissions">Limiting features to certain user groups</h2>
<h3>PHPFox user groups</h3>
Each user in PHPFox belongs to a user group.

PHPFox ships with 4 default user groups that can not be removed
  * *Administrators*
  * *Staff* or logged in users
  * *Registered User*
  * *Guest*

<h3>Limiting AVChat features</h3>

To control what AVChat features (creating rooms, sending PM's, viewing webcams, etc.) are available to each user group do the following from the AdminCP:

1. go to `Users -> Manage User Groups`.
2. click the arrow in front of the user group you want to change AVChat permissions for and select `Manage User Settings`.
3. select `Avchat3` in the list to the left. The permissions for AVChat 3 will load up.
4. change the permissions for that user group and click `SAVE` at the bottom.

<h2 id="location-of-avchat-files">Location of AVChat &amp; module files</h2>
All the AVChat  files including:

* all the module files
* `index.swf` and `admin.swf`
* language files
* themes
* audio/video quality profile files
* `avc_settings.xml`
* `integration.php`


are located in `/module/avchat3/include/plugin/`.

</section>
