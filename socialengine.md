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

* user name & gender integration
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
<h3>Install the add-on</h3>

1. Login as admin into your SocialEngine PHP 4 Website and go to **Admin >> Manage >> Packages & Plugins**
<img src="{{site.github.url}}/assets/images/se/se_01.gif.png" class="img-responsive" />
2. Click on <kbd>Install New Packages</kbd> then on <kbd>Add Packages</kbd>
3. Browse to where you unzipped `avchat3_socialengineall_UNZIPFIRST.zip` and select the `module-avchat3-xxxx.tar` file from the `socialengine_4.x` folder.
4. Wait for it to be uploaded
5. Click <kbd>Continue</kbd> and follow the on-screen installation instructions until the package is installed.
6. Click <kbd>Manage Packages</kbd> (top left) and make sure the AVChat Module in the list is enabled.
<img src="{{site.github.url}}/assets/images/se/se_2.png" class="img-responsive" />
7. Click <kbd>Return to Admin Panel</kbd>
9. Users will see a new link in the menu that will take them to the video chat.

<h3>Install AVChat</h3>

1. Connect with an FTP client (like [WinSCP](http://winscp.net/eng/index.php) or [FileZilla](http://filezilla-project.org/)) to your website and go to the root of your website (usually in public_html).
2. Copy the `videochat` folder from the `socialengine_4.x` folder from the archive, to the root of your website.
3. In the new `videochat` folder copy the contents of the folder named `Files to upload to your web site` from the `AVChat 3.0.zip` archive.
<!--4. If the previous two steps are not completed an error message will appear: "The videochat folder or the AVChat files are missing from your SocialEngine installation."-->
5. CHMOD the `uploadedFiles` and `tokens` folders to `777`
<!--6. Create a new folder `tokens` (`videochat/tokens`) and CHMOD it to `777` (otherwise we might have token generation issues later on)-->

<h2 id="completing-the-installation">Complete installation</h2>
<h3>Connect AVChat to the media server app</h3>
1. Now back in the SE4 admin area go to **Settings > AVChat 3 Settings**
<img src="{{site.github.url}}/assets/images/se/se_04.gif.png" class="img-responsive" />
and enter the RTMP connection string to your `avchat30` application on the media server. It should look like this:
`rtmp://myFMSserver.com/avchat30/_definst_`
where `myFMSserver.com` is the domain name or ip of the your media server.
2. Click <kbd>Save Changes</kbd> at the bottom

Your AVChat installation is now configured to connect to the media server.

### Enter the chat and insert the license key

1. Go to **Admin -> Plugins -> Flash Video Chat** to enter the video chat, you will be asked for the license key:
<img src="{{site.github.url}}/assets/images/se/license_key.jpg" class="img-responsive" />
2. Enter the key (it's in your [client/trial area on nusofthq.com](https://nusofthq.com/c/)) and press <kbd>Submit</kbd>

</section>

<section class="bs-docs-section" markdown="1">
<h1 id="avchat-socialengine-application-features" class="page-header">Add-on Features</h1>
<h2 id="accessing-the-avchat-admin-area-socialengine">Access the AVChat admin area</h2>

The AVChat admin interface allows you to kick and ban users, view private discussions, log in as hidden, close, open and delete rooms, change the license key, etc.
SocialEngine PHP 4 has 5 default member levels:

* Public
* Default Level
* Moderators
* Admins
* Super Admins

By default Moderators, Admins and Super Admins have access to the AVChat admin interface.

Access to the AVChat admin interface and what admin features each member level gets can be controlled from: Manage -> Member Level AVChat 3 Permision.


<h2 id="open-avchat-in-a-popup-window-socialengine">Open AVChat in a pop up</h2>

By default AVChat 3 is embedded in your Socialengine page but you might want AVChat to open in a pop up window to make it easier for your users to browse your website while in the chat.
While logged in the admin area of SE4:

* Go to **Settings -> General AVChat 3 Settings**
* Set the **Open AVChat 3** in radio option to in popup
* Scroll to the bottom and click <kbd>Save Changes</kbd>


<h2 id="avchat-socialengine-ads">Placing ads around the video chat</h2>

Any ads can be placed around AVChat, including Google Ad-Sense.

You can place ads around:

* The chat area if the selected open method is Embeded.
* The Open chat button if the selected open method is Popup.

To place ads around AVChat (or around the Open Chat Button if open popup open method is selected), you need to edit this file: `application/modules/Avchat3/views/scripts/index/index.tpl`

Where you can place the ads:

1. On the top of the chat. In this case what you have to do is place the ads code before this line:
`<?php if($this->open_method == 1){ ?>`
2. In the right side of the chat. In this case you will have to use floated divs or tables to encapsulate the chat area and the ads.
3. On the bottom of the chat. In this case what you have to do is place the ads code after this line:
`<?php } ?>`
4. In the left side of the chat. In this case you will have to use floated divs or tables to encapsulate the chat area and the ads.
5. Or you can place the ads in any of the combined situations presented.


<h2 id="socialengine-member-levels">SocialEngine 4's member levels and AVChat</h2>

<h3>Social Engine member levels</h3>

SocialEngine 4 has 5 default member levels:

* Public
* Default Level
* Moderators
* Admins
* Super Admins

<h3>Who has access to AVChat by default</h3>

By default:

* Moderators, Admins and Super Admins have access to the AVChat admin interface
* Default Level has access to the AVChat user interface
* Public does not have access to AVChat

<h3>Permissions you can change from the Social Engine backend</h3>

The default setup can be changed from: **Manage -> Member Level AVChat 3 Permission**

<img src="{{site.github.url}}/assets/images/se/se_05.gif.png" class="img-responsive" />

But access to AVChat is not the only thing you can control. What makes this integration so great is that you can control in detail to what AVChat features each member level has access to without leaving the SE4 admin area.

See screenshot with all the permissions that you can control individually for each member level:
<img src="{{site.github.url}}/assets/images/se/full_se4_permissions_list.png" class="img-responsive" />


<h2 id="allowing-visitors-socialengine">Allowing visitors to join the video chat</h2>


By default the AVChat Module for SE4 does not allow visitors of your web site to enter the video chat. Only signed in users are allowed in the video chat.

By default SE4 considers visitors as part of its internal Public member level so to allow visitors in we need to allow access to AVChat for the Public member level:

1. Log in the admin area of SE4:
2. Go to **Manage -> Member Level AVChat 3 Settings**
3. Select **Public** in the **Member Level** drop down
4. The AVChat permissions for the Public member level will load
5. Set the **Allow Access AVChat** radio option to **Yes**, allowing access to AVChat
6. Scroll to the bottom and click <kbd>Save Changes</kbd>

Visitors will have the option to choose their user name and gender before joining the video chat.


<h2 id="change-page-title-socialengine">How to change the Flash Video Chat page title</h2>

The only way at this moment to change the title is by editing a file. In future updates we will add the option to change the title by editing a phrase in the SE4 phrase system.

What you have to do now to change the title:

1. Login into your FTP account with an FTP client
2. Go to `application/modules/Avchat3/Controllers/` and open in a text editor `IndexController.php`
3. Find this line `$this->view->avchat3_title = 'Flash Video Chat';` and change Flash Video Chat with what you want.
4. Save the file and that's it.

<h2 id="change-menu-title-socialengine">How to change the Flash Video Chat menu item title</h2>

1. Login as admin into your Social Engine PHP 4 website
2. Go to **Layout ->Menu Editor**
3. By default the Video Chat link is placed into the Main Navigation Menu. If you placed it into other menu, select the corresponding menu from the drop down. Find the Video Chat item, and click edit (see the screenshot below).
<img src="{{site.github.url}}/assets/images/se/se4_avchat3_menu_item.png" class="img-responsive" />
4. Type the new menu title in the "Label" field and save (see the screenshot below).
<img src="{{site.github.url}}/assets/images/se/se4_avchat_edit_menu_item.png" class="img-responsive" />


<h2 id="change-url-socialengine">How to change the default URL</h2>

This is a delicate task which requires editing a sensitive file, `application/index.php`.

<div class="alert alert-warning" role="alert"><p markdown="1">Before going further make sure that you BACKUP `application/index.php`</p></div>

Let's say that you want to access AVChat 3 by going to http://yourse4site.com/outstandingchat instead of http://yourse4site.com/avchat3. SE4 automatically creates the URL and it cannot be changed from the admin area. Editing the .htaccess file is a nightmare. So the easiest possible way is this:

1. Login into your FTP account with an FTP client
2. Go to `application` and open in a text editor `index.php`
3. **Before any code line** add these lines:

```php
if($\_SERVER['REQUEST_URI'] == '/outstandingchat'){
$\_SERVER['REQUEST_URI'] = '/avchat3';
}
```

Save the file and that's it. You can access now AVChat by going to http://youse4site.com/outstandingchat


* Do not use `videochat` as alias because `videochat` holds the AVChat 3 standalone files that are used by the AVChat 3 SE4 module.
* If you have Social Engine 4 installed in a folder like this http://yourse4site.com/se4folder/ then to change the URL you need to modify the code above:

```php
if($\_SERVER['REQUEST_URI'] == '/se4folder/outstandingchat'){
$\_SERVER['REQUEST_URI'] = '/se4folder/avchat3';
}
```

<h2 id="upgrade-avchat-module-socialengine">How to upgrade the AVChat module</h2>

SocialEngine Package Manager is responsible for all the packages in the SocialEngine system. It offers us an easy way for installing/upgrading a module or a widget. Next I will present a series of steps that can help you upgrade a module or widget easily.


1. Go to **ACP->Manage Packages & Plugins->Manage Packages->Install New Packages->Add Packages**;
2. **Choose Packages**: Select the new archive and after upload click Continue button;
3. **Run Pre-install Check**: You should see the following text: **Upgrade package "module-avchat3"[old_build_no] to [new_build_no]**. Here will also be shown the differences between the two archives. Click the <kbd>Continue</kbd> button;
4. **Enter FTP Info**: Enter your connection details and the click the <kbd>Continue</kbd> button;
5. **Run Permissions Check**: Here it will inform you about permissions beeing set and the number of files that will be copied during the installtion. Click the <kbd>Continue</kbd> button to go to next steps;
6. Copy Files. A message should inform you that all files were successfully copied.
7. **Update Database**. A message should inform you all necessary changes to the database have been made successfully. Click <kbd>Finalize Installation</kbd> button to complete the upgrade;
8. **Complete**: A message that informs you the installation was successfully should appear. From here you can return to **Package Manager** or to the **Dashboard**.

<h2 id="allowing-visitors-to-login-with-facebook">Allowing visitors to enter the chat using their Facebook profile</h2>

Only visitors will have the option of connecting with Facebook to AVChat.

Follow the chapter [Setup Facebook authentication](http://docs.avchat.net/standalone.html#setup-facebook-authentication) in order to obtain your `appid` that you will use in SocialEngine backend.

1. Go to SocialEngine backend: **Settings > AVChat 3 Settings**
2. You will find there the **Facebook App ID** field. Put there your personal Application ID.
3. Click <kbd>Save changes</kbd>


<h2 id="configuring-the-addon">Configuring the Add-on</h2>

The main way you can configure the Add-on is from the specific backend settings page found at `your_social_engine_site/admin/avchat3/settings/general`
<img src="{{site.github.url}}/assets/images/se/avchat-settings.png" class="img-responsive" />

Additionally to this the Add-on can be configured directly from AVChat's main config file (`avc_settings.xml`) and the rest of the configuration files described [here](http://docs.avchat.net/standalone.html#config-files)

</section>
