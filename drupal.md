---
layout: default
title: AVChat Module for Drupal 5/6
description: The documentation for the AVChat module for Drupal.
isHome: false
hide: true
---

<section class="bs-docs-section" markdown="1">
  <h1 id="overview" class="page-header">Overview</h1>
  <p class="lead">The AVChat Module for Drupal 5 and 6 handles the integration between a Drupal 5 or 6 web site and the AVChat video chat software.</p>

<div class="bs-callout bs-callout-warning" id="callout-tables-responsive-overflow"> <h4>End of life</h4> <p markdown="1">**Drupal 5** has reached end of life Jan 5th 2011 and is no longer supported. **Drupal 6** has reached end of life on February 24th 2016 and will no longer be supported. If you are looking to start a new Drupal website, you should use Drupal 7 or 8 instead.</p> </div>



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

1. upload the `avchat3` folder from `avchat3_drupal_modules.zip/drupal6.x_component` to `/sites/all/modules/`
2. upload the contents of the `Files to upload to your web site` folder from  the AVChat archive to `/sites/all/modules/avchat3/`

<div class="bs-callout bs-callout-info" id="callout-tables-responsive-overflow"> <h4>Folder permissions</h4> <p markdown="1">If your website's hosted on a Linux server CHMOD the `uploadedFiles` and `tokens` folders to 777.</p> </div>

Edit `avc_settings.xml` and change the value of the `connectionstring` node to the connection string for your new avchat30 app on the media server:

<pre>
&lt;connectionstring&gt;
  &lt;value&gt;rtmp://media-server-ip/avchat30/_definst_&lt;/value&gt;
&lt;/connectionstring&gt;
</pre>
<h2 id="installing-the-module">Complete installation</h2>
Now open your Drupal's admin area in a web browser, go to `Administer > Site Building > Modules > List` and enable the `AVChat 3.x Module` .

Two new menu items will show up in your Drupal menu:

* AVChat Video Chat (User)
* AVChat Video Chat (Admin)

Click on either of them, you will be taken to a new web page where AVChat will load in the browser and will ask for a username. Type one and click `[Enter Chat]`. AVChat will now connect to the media server and ask you for the license key.

Enter the key (It's in your [private client/trial area](https://nusofthq.com/c/)) and press `[Submit]`.
</section>


<section class="bs-docs-section" markdown="1">
<h1 id="installation-instructions" class="page-header">Module Features</h1>
<h2 id="accessing-the-avchat-admin-area">Access the AVChat admin area</h2>
The AVChat admin interface allows you to kick and ban users, view private discussions, log in as hidden, close, open and delete rooms, change the license key, etc. .

By default, Drupal 5 and 6 come with two user roles:

 * Anonymous user: this role is used for users that don't have a user account or that are not authenticated.
 * Authenticated user: this role is automatically granted to all logged in users.

In Drupal 5 and 6 there is a <em>super administrator</em> account who has access to the AVChat admin interface by default.

To give other people access to the AVChat admin interface do the following:

1. Go to `Administer -> User Management -> Permissions`
2. Under the `avchat3 module` select which user roles you want to "access avchat3 admin interface" .

Unce a user has access to the admin area of AVChat (super administrators or members with a user role that grants them access) he just has to log in and click on the `AVChat Video Chat (Admin)` menu item.

<h2 id="open-avchat-in-a-popup-window">Open AVChat in a pop up</h2>

You might want AVChat to open in a pop up window to make ti easier for your users to browse your website while in the chat.

**Drupal 5:**

Feature not available.

**Drupal 6:**

1. Go to `Administer -> Site configuration -> AVChat 3.0 Drupal 6.x Module Settings`
2. Set `Chat will open` to `in popup` and save

<h2 id="permissions">Limiting features to certain user roles</h2>
By default Drupal 5 and 6 come with two user roles:

* **anonymous users** or visitors
* **authenticated users** or logged in users

and a **super administrator** account which does not belong to any user role.

On top of that you can add your own custom user roles from `Administer -> User Management -> Roles`.
<h3>Limiting AVChat features</h3>

To control what AVChat features (creating rooms, sending PM's, viewing webcams, etc.) are available to each user role go to the Permissions page `Administer -> User Management ->Permissions -> avchat3 module` .

All user roles will be shown horizontally while all the AVChat features you can turn on and off will be shown vertically.

<h2 id="location-of-avchat-files">Allowing visitors to enter AVChat</h2>
1. Go to `Administer -> User management -> Permissions -> avchat3 module`
2. Scroll down to the `access avchat3 user interface` column
3. Check the `anonymous user` and save

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
