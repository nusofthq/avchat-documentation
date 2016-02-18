---
layout: default
title: AVChat SocialEngine 4 Add-on
description: Documentation covering the AVChat add-on for SocialEngine 4
isHome: false
hide: true
---

<section class="bs-docs-section" markdown="1">
  <h1 id="overview" class="page-header">Overview</h1>
  <p class="lead">The AVChat Video Chat Add-on for SocialEngine 4 handles the integration between your SocialEngine 4 community and our AVChat software:</p>

* user name integration
* profile url integration
* profile image integration
* placement of video chat within the web site (user and admin interface)
* control video chat permissions for each SocialEngine PHP 4 member levels  directly from the SE4 admin area

The AVChat Module for SE4 is one of the best most advanced integration we have done! Why? because directly in SE4's admin area you can control access to AVChat and its features based on the level of the user

If you like the AVChat Module for SocialEngine PHP 4 don't forget to [rate it and review it in the SE Community Addons area](http://www.socialengine.com/customize/se4/mod-page?mod_id=187). You can also view our [Developer Profile on socialengine.com](http://www.socialengine.com/customize/se4/developer?dev_id=4292).

If you cannot find the answer you’re looking for here, we encourage you to try our [FAQ](http://avchat.net/faq) or [forums](http://discuss.avchat.net/). There's also more documentation regarding AVChat in the [documentation area for the main standalone version](http://docs.avchat.net/standalone).

If you're looking for something specific just hit <kbd>Ctrl+F</kbd> on your browser.
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="installation-instructions" class="page-header">Installation Instructions</h1>
<h2 id="download-avchat-and-socialengine-application">Download & extract archives</h2>
Download these 2 archives from your [private client/trial area](https://nusofthq.com/c/) to your computer:

1. `AVChat 3.0.zip` contains AVChat
2. `avchat3_socialengineall.zip` contains the SocialEngine add-on

Extract the 2 archives somewhere on your computer.

<h2 id="installing-the-media-server-app">Media Server Application</h2>
Once we've downloaded &amp; unzipped everything the next thing we need to do is to setup the media server app to which AVChat will connect to.

AVChat uses a media server to send all the audio video and text data between users. AVChat supports the 3 major media servers:

* Red5
* Adobe Media Server
* Wowza

Here's how to install the `avchat30` app on each one of them:

{% include media-server-app.md %}

<h2 id="installing-the-application-and-avchat-on-socialengine">SocialEngine 4 add-on &amp; AVChat installation</h2>

1. Connect with an FTP client (like [WinSCP](http://winscp.net/eng/index.php) or [FileZilla](http://filezilla-project.org/)) to your website and go to the root of your website (usually in public_html).
2. Copy the `videochat` folder from the `socialengine_4.x` folder from the archive, to the root of your website.
3. Now in the new `videochat` folder copy the contents of the folder named `Files to upload to your web site` from the `AVChat 3.0.zip` archive.
4. If the previous two steps are not completed an error message will appear: "The videochat folder or the AVChat files are missing from your SocialEngine installation."
5. CHMOD the `videochat/uploadedFiles` folder to `777` (otherwise the upload function might not work)
6. Create a new folder `tokens` (`videochat/tokens`) and CHMOD it to `777` (otherwise we might have token generation issues later on)
7. Now back in the SE4 admin area go to Admin -> Plugins -> Flash Video Chat to enter the video chat, you will be asked for the license key:
<img src="{{site.github.url}}/assets/images/se/license_key.jpg" class="img-responsive" />
8. Enter the key (it's in your client/trial area) and press <kbd>Submit</kbd>

<h2 id="completing-the-installation">Complete installation</h2>
<h3>Install the add-on</h3>

1. Login as admin into your SocialEngine PHP 4 Website and go to Admin >> Manage >> Packages & Plugins
<img src="{{site.github.url}}/assets/images/se/se_01.gif.png" class="img-responsive" />
2. Click on <kbd>Install New Packages</kbd> then on <kbd>Add Packages</kbd>
3. Browse to where you unzipped `avchat3_socialengineall_UNZIPFIRST.zip` and select the `module-avchat3-xxxx.tar` file from the `socialengine_4.x` folder.
4. Wait for it to be uploaded
5. Click <kbd>Continue</kbd> and follow the on-screen installation instructions until the package is installed.
6. Click <kbd>Manage Packages</kbd> (top left) and make sure the AVChat Module in the list is enabled.
<img src="{{site.github.url}}/assets/images/se/se_2.gif" class="img-responsive" />
7. Click <kbd>Return to Admin Panel</kbd>
9. Users will see a new link in the menu that will take them to the video chat.

<h3>Connect AVChat to the media server app</h3>

1. Go to Settings >> AVChat 3 Settings
<img src="{{site.github.url}}/assets/images/se/se_04.gif.png" class="img-responsive" />
and enter the RTMP connection string to your `avchat30` application on the media server. It should look like this:
`rtmp://myFMSserver.com/avchat30/_definst_`
where `myFMSserver.com` is the domain name or ip of the your media server.
2. Click <kbd>Save Changes</kbd> at the bottom

Your AVChat installation is now configured to connect to the media server.

<h3>Allow access to the chat</h3>
From the Admin CP:

1. Go to **Users -> Group Permissions**
2. Click the group you want to have access to AVChat
3. Scroll down to the **AVChat 3 Video Chat - User Permissions** section and click **Allow** (green box)
4. Scroll to the end and click <kbd>Update Permissions</kbd>

Repeat 2-4 for each group you want to have access to the chat. Make sure you allow access to the *Administrative* user group since you're part of it.

<h3>Enter the chat and insert the license key</h3>

1. Go to the forum's front end. There's a new **Video Chat** link in xenForo's main menu, click on it.

2. The page with AVChat on it will load and AVChat's login screen will show up. **Your username will be automatically filled.**

3. Click <kbd>Enter Chat</kbd>. AVChat will now connect to the media server and ask you for the license key.

4. Enter the key (It's in your [private client/trial area](https://nusofthq.com/c/)) and press <kbd>Submit</kbd>.
</section>

<section class="bs-docs-section" markdown="1">
<h1 id="avchat-xenforo-application-features" class="page-header">Add-on Features</h1>
<h2 id="accessing-the-avchat-admin-area-xenforo">Access the AVChat admin area</h2>
If you want to log in as hidden, kick/ban users, close/delete rooms, view users IP's and a lot of other cool stuff that admins do, you'll have to use the AVChat admin interface.

**By default no xenForo user group has access to the video chat as admin. You will need to configure this permission for each group.**

While logged in the Admin CP do the following:

 * Click on **Users** in the top menu
 * Click on the user group you want to give AVChat admin access to
 * On the following page search for **AVChat 3 Video Chat - User Permissions** and you will see AVChat's permissions list
 * Check **Allow** (the green box) for **Can access chat as admin**
 * Scroll to the bottom and click on <kbd>Update Permissions</kbd>


Now, whenever a user belonging to that user group will access the chat, the AVChat admin interface will now load, instead of the one for regular members.

<h2 id="open-avchat-in-a-popup-window-xenforo">Open AVChat in a pop up</h2>

By default AVChat 3 is embedded in your xenForo page but you might want AVChat to open in a pop up window to make it easier for your users to browse your website while in the chat.

1. From Admin CP go to **Home -> Options**
2. Search for **AVChat 3 Video Chat Options** and click on it
2. Select **Popup** for **Display Mode**
3. Scroll to the bottom and click <kbd>Save Changes</kbd>

<h2 id="avchat-xenforo-permissions">Limiting features to certain user groups</h2>
<h3>xenForo user groups</h3>

xenForo ships with 4 user groups:

  * *Administrative*
  * *Moderating*
  * *Registered*
  * *Unregistered / Unconfirmed*

<img src="{{site.github.url}}/assets/images/xenforo/user-groups.png" class="img-responsive" />


<h3>Limiting AVChat features</h3>

To control what AVChat features (creating rooms, sending PM's, viewing webcams, etc.) are available to each user group do the following from the AdminCP:

1. go to **Users** and the click on **User Group Permissions** in the left sidebar.
2. click on the user group you want to edit and then search for **AVChat 3 Video Chat - User Permissions**
3. change the AVChat permissions for that user group and click <kbd>Update Permissions</kbd> at the bottom.

<!--
<h2 id="location-of-avchat-files">Preventing visitors (guests) from accessing the video chat</h2>

From the  AdminCP:

1. Go to `Members` and click on `Manage Member Groups`
2. Click on `Guests` then on the `AVChat 3` tab
3. Select `No` for `Can access chat`
4. Scroll to the bottom and click <kbd>Complete Edit</kbd>

Visitors will still see the `Video Chat` link but they will be asked to sign in or register.

<img src="{{site.github.url}}/assets/images/xenforo/visitor-register-signing.png" class="img-responsive" />
-->

<h2 id="allow-chat-access-to-visitors">Allowing visitors access to the video chat</h2>

The xenForo addon does not allow any user group to access the chat by default. Every group (including *Unregistered / Unconfirmed* which covers visitors) need to be given permission from the group's permissions page.

From the Admin CP:

1. go to **Users -> Group Permissions**
2. click on the **Unregistered / Unconfirmed**
3. Scroll down to **AVChat 3 Video Chat - User Permissions** and select **Allow** (the green box) for **Can access chat**
4. Scroll down and click <kbd>Update Permissions</kbd>

<div class="alert alert-info" role="alert">
<p markdown="1">When a user group doesn't have permission to access the chat they still see the `Video Chat` link in the menu but on the chat page they're asked to register or sign in.</p>
</div>


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
