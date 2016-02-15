---
layout: default
title: AVChat Module for Drupal 7
description: The documentation for the AVChat module for Drupal.
isHome: false
hide: true
---

<section class="bs-docs-section" markdown="1">
  <h1 id="overview" class="page-header">Overview</h1>
  <p class="lead">The AVChat Module for Drupal 7 handles the integration between a Drupal 7 web site and the AVChat video chat software.</p>

  If you're looking for something specific just hit <kbd>Ctrl+F</kbd> on your browser.
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="installation-instructions" class="page-header">Installation Instructions</h1>
<h2 id="installing-the-module">Download & extract archives</h2>
Download these 2 archives from your [private client/trial area](https://nusofthq.com/c/) to your computer:

1. `AVChat 3.0.zip` contains AVChat
2. `avchat3_drupal_modules.zip` contains the Drupal modules

Extract the 2 archives somewhere on your computer.

<h2 id="installing-the-module">Media Server Application</h2>
Once we've downloaded everything the 1st thing we need to do is to setup the media server app to which AVChat will connect to.

AVChat uses a media server to send all the audio video and text data between users. AVChat supports the 3 major media servers:

* Red5
* Adobe Media Server
* Wowza

Here's how to install the `avchat30` app on each one of them:

{% include media-server-app.md %}

<h2 id="installing-the-module">Module & AVChat installation</h2>
Connect using an FTP client to your website and:

1. upload the `avchat3` folder from `avchat3_drupal_modules.zip/drupal7.x_module` to `/sites/all/modules/`
2. upload the contents of the `Files to upload to your web site` folder from  the AVChat archive to `/sites/all/modules/avchat3/`

<div class="bs-callout bs-callout-info" id="callout-tables-responsive-overflow"> <h4>Folder permissions</h4> <p markdown="1">If your website's hosted on a Linux server CHMOD the `uploadedFiles` and `tokens` folders to 777.</p> </div>

Edit `/sites/default/settings.php`, search for `# $cookie_domain = '.example.com'`;, remove the `#` sign and replace `.example.com` with your domain name.

<h2 id="installing-the-module">Complete installation</h2>
Now open your Drupal's admin area in a web browser, go to `Modules > List > CHAT Section` and enable the `AVChat 3 Module` .

Two new menu items will show up in your Drupal menus:

* "Flash Video Chat" in the main menu
* "AVChat 3 Module Settings" in the admin menu

Click on ` AVChat 3 Module Settings`, a list of AVChat 3 settings will show up including the RTMP connection string field.

Set it to the connection string for your new media server app like this:

* `rtmp://media-server-ip/avchat30/_definst_`

Click on `Flash Video Chat` to open the page with AVChat on it. The pre-filled AVChat login screen will show up, click `[Connect]`. AVChat will now connect to the media server and ask you for the license key.

Enter the key (It's in your [private client/trial area](https://nusofthq.com/c/)) and press `[Submit]`.


<div class="bs-callout bs-callout-info" id="callout-tables-responsive-overflow"> <h4>Deep integration</h4> <p markdown="1">When accessing AVChat logged in to the website the user name in the AVChat login section will be automatically filled with your Drupal username. If the user role you belong to has the permission to access AVChat 3 as admin, the admin interface of AVChat 3 will be loaded.</p> </div>
</section>


<section class="bs-docs-section" markdown="1">
  <h1 id="installation-instructions" class="page-header">Module Features</h1>
  <h2 id="accessing-the-avchat-admin-area">Access the AVChat admin area</h2>
The AVChat admin interface allows you to kick and ban users, view private discussions, log in as hidden, close, open and delete rooms, change the license key, etc. .

Drupal 7 comes with three user roles:

 * Anonymous user: this role is used for users that don't have a user account or that are not authenticated.
 * Authenticated user: this role is automatically granted to all logged in users.
 * Administrator

To give other people access to the AVChat admin interface do the following:

1. Go to `Modules -> AVChat3 Module`
1. Click on the `Permissions` link
2. Select which user roles you want to "access avchat3 admin interface" .

Unce a user has access to the admin area of AVChat he just has to log in and click on the ` Flash Video Chat` link. AVChat's admin interface is automatically loaded.

<h2 id="open-avchat-in-a-popup-window">Open AVChat in a pop up</h2>

You might want AVChat to open in a pop up window to make it easier for your users to browse your website while in the chat.

1. Go to `Admin Menu -> AVChat 3 Module Settings`
2. Set `Chat will open` to `in popup` and save

  <h2 id="permissions">Limiting features to certain user roles</h2>
  By default Drupal 7 comes with 3 user roles:

  * **anonymous users** or visitors
  * **authenticated users** or logged in users
  * **administrator**

On top of that you can add your own custom user roles from `Admin Menu -> People -> Permissions -> Roles`.
<h3>Limiting AVChat features</h3>

To control what AVChat features (creating rooms, sending PM's, viewing webcams, etc.) are available to each user role go to the Permissions page `Admin Menu -> People -> Permissions` .

All user roles will be shown horizontally while all the AVChat features you can turn on and off will be shown vertically.

<h2 id="location-of-avchat-files">Allowing visitors to enter AVChat</h2>
1. Go to `Modules -> AVChat3 Module`
2. Click on `Permissions`
3. Click on the `access avchat3 user interface` option corresponding to the `anonymous user` column.


<h2 id="location-of-avchat-files">Location of AVChat files</h2>
All the AVChat  files including:

* all the module files
* index.swf and admin.swf
* language files
* audio/video quality profile files
* avc_settings.xml


are located in `sites/all/modules/avchat3`.

<h2 id="location-of-avchat-files">GPL License</h2>
The AVChat Module for Drupal is licensed under the GNU General Public License, version 2.

Once you purchase the module you can modify it and distribute it as long as you keep it under the GPL.

We are not affiliated with or endorsed by the Drupal Project or its trademark owners.
</section>
