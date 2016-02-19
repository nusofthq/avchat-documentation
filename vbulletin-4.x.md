---
layout: default
title: AVChat vBulletin 4.x add-on
description: Documentation covering the AVChat add-on for vBulletin 4.x
isHome: false
hide: true
---

<section class="bs-docs-section" markdown="1">
  <h1 id="overview" class="page-header">Overview</h1>
  <p class="lead">The AVChat Video Chat Product for vBulletin 4.x integrates AVChat with your existing vBulletin 4.x web site and users database:</p>


* Username integration: users will have the same username and gender in the web site and in the video chat.
* Avatar integration: the avatar pictures are automatically used inside the video chat.
* Direct access to the admin area for Administrators, Moderators and Super Moderators. They have access to the admin area of AVChat 3 from where you can do all sorts of powerful things like kick and ban.
* Different permissions for different usergroups, You can control the video chat features independently for each usergroup. You can also control to what admin features (kick,ban,etc...) do Administrators, Moderators and Super Moderators have access to.
* Access user profiles directly from the video chat: you can access the profiles of users directly from the video chat.
* Simple install, it installs as any other vBulletin 4.x Product.
* One click away from users, a link to the video chat is placed in the main menu in the user area.


If you cannot find the answer you’re looking for here, we encourage you to try our [FAQ](http://avchat.net/faq) or [forums](http://discuss.avchat.net/). There's also more documentation regarding AVChat in the [documentation area for the main standalone version](http://docs.avchat.net/standalone).

If you're looking for something specific just hit <kbd>Ctrl+F</kbd> on your browser.
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="installation-instructions" class="page-header">Installation Instructions</h1>
<h2 id="download-avchat-and-vbulletin-application">Download & extract archives</h2>
Download these 2 archives from your [private client/trial area](https://nusofthq.com/c/) to your computer:

1. `AVChat 3.0.zip` contains AVChat
2. `avchat3_vbulletin_38x_and_4x_product.zip` (contains the AVChat Product for vBulletin 4.x)

Extract the 2 archives somewhere on your computer.

<h2 id="installing-the-media-server-app">Media Server Application</h2>
Once we've downloaded &amp; unzipped everything the next thing we need to do is to setup the media server app to which AVChat will connect to.

AVChat uses a media server to send all the audio video and text data between users. AVChat supports the 3 major media servers:

* Red5
* Adobe Media Server
* Wowza

Here's how to install the `avchat30` app on each one of them:

{% include media-server-app.md %}

<h2 id="installing-the-application-and-avchat-on-vbulletin">vBulletin 4.x add-on &amp; AVChat installation</h2>
<h3>Install AVChat</h3>

1. Unpack the `avchat3_vbulletin_38x_and_4x_product.zip` archive.
2. Copy the `videochat` and the `includes` folder into the root of your vBulletin 4.x installation.
3. Now go to the folder where you unzipped the latest AVChat3 archive and copy all the content from `Files to upload to your website` to the `videochat` folder that you just copied
4. Edit `videochat/avc_settings.xml` in a text editor and set the `<value>` of the `<connectionstring>` tag
`<value>rtmp://media-server-ip-address/avchat30/_definst_</value>`
5. Chmod the `uploadedFiles` folder to 777 (otherwise the upload function might not work)
6. Chmod the `tokens` folder to 777

<h3>Install the add-on</h3>

1. Login into your forum Control Panel and go to Plugins & Products > Manage Products as highlighted below:
<img src="{{site.github.url}}/assets/images/vbulletin/manage_products_link.gif" class="img-responsive" />
2. On the right frame click <kbd>[Add/Import Product]</kbd> as highlighted below:
<img src="{{site.github.url}}/assets/images/vbulletin/add_product_link.gif" class="img-responsive" />
3. On the right frame an **Import Product** form will appear. Modify the "import the XML file from your server" field to `./includes/xml/product-avchat3.xml` and click on <kbd>Import</kbd> button as shown below:
<img src="{{site.github.url}}/assets/images/vbulletin/import_product_form.gif" class="img-responsive" />
4. After the installation, AVChat 3 will appear in products list and it will also appear in the left menu, as shown in the image below:
<img src="{{site.github.url}}/assets/images/vbulletin/avchat3_product_in_vbulletin_4.0.x.gif" class="img-responsive" />

</section>

<section class="bs-docs-section" markdown="1">
<h1 id="avchat-vbulletin-application-features" class="page-header">Add-on Features</h1>
<h2 id="open-avchat-in-a-popup-window-vbulletin">Open AVChat in a pop up</h2>

This guide will show you how to create a link in the vBuletin 4.x menu that will open up AVChat in a pop up window.

This is the recommended way to open AVChat as it's easier for your web site users to visit the web site, user profiles, threads on the forum, without leaving the video chat.

1. From the admin area Go to **Styles & Templates > Style Manager** and choose **Edit Templates** from the dropdown and hit <kbd>Go</kbd> button
<img src="{{site.github.url}}/assets/images/vbulletin/edit_template_screen1.gif" class="img-responsive" />
2. Scroll the list until you get to **Navigation / Breadcrumb Templates** and select it. Next click <kbd>Expand Collapse</kbd> button.
<img src="{{site.github.url}}/assets/images/vbulletin/edit_template_screen2.gif" class="img-responsive" />
3. Scroll the list until you get to **Navigation / Breadcrumb Templates > navbar** and select it. Next click <kbd>Edit</kbd> button
<img src="{{site.github.url}}/assets/images/vbulletin/edit_template_screen3.gif" class="img-responsive" />
4. Add this HTML code to main navigation (placed the link after Calendar) and hit <kbd>Save</kbd>:

```html
<li><a href="#" onclick="window.open('videochat/index.php','FlashVideoChat','height=580','width=970');">Flash Video Chat</a></li>
```

<img src="{{site.github.url}}/assets/images/vbulletin/vBulletin_4.0.3_add_popup_link_in_menu.png" class="img-responsive" />

In your forum you should see this link:

<img src="{{site.github.url}}/assets/images/vbulletin/vBulletin_4.0.3_menu.png" class="img-responsive" />


<h2 id="embed-avchat-vbulletin">Embed AVChat</h2>

Altough we recommend opening AVChat in a pop-up, the following tutorial will show you how to open it embedded in a HTML page on your web site.

1. Open the `videochat_embedded_4.0.x`
2. Upload `videochat.php `to the root folder of your forum.
3. Login as admin, go to **Styles & Templates > Style Manager**, choose **Add New Template** from the dropdown and hit <kbd>Go</kbd> button
<img src="{{site.github.url}}/assets/images/vbulletin/vbulletin_add_new_template.png" class="img-responsive" />
4. Open `template.txt` from the `videochat_embedded_4.0.x`, copy its content and paste it into the **Template field**. **Make sure that the template's name is FlashVideoChat**. Click on the <kbd>Save</kbd> button.
<img src="{{site.github.url}}/assets/images/vbulletin/vbulletin_add_new_template_content.png" class="img-responsive" />
5. Now you need to add a link to the vBulletin menu that will take users to the new web page with the video chat embedded on it. To do this follow the [Open AVChat in a pop up](http://docs.avchat.net/vbulletin-3.8#open-avchat-in-a-popup-window-vbulletin) **Step 4** use the following HTML code:

```html
<li><a href="videochat.php">Flash Video Chat</a></li>
```

<h2 id="accessing-avchat-vbulletin">Accessing the AVChat admin interface in vBulletin</h2>

The admin interface will be automaticaly given to the designated users, based on the first lines from `integration.php` file from `[your website root]/videochat/integration.php` and also the first lines from the `index.php` file from the same directory.


<h2 id="usergroups-vbulletin">vBulletin's usergroups and limiting features for specific usergroups</h2>

1. Login as admin into your forum Control Panel and go to **Usergroups > Usergroup manager**
<img src="{{site.github.url}}/assets/images/vbulletin/usergroup_manager.gif" class="img-responsive" />
2. Select from the Usergroups list the usergroup you want to edit and click <kbd>Go</kbd>. Here we chose **Administrators**
<img src="{{site.github.url}}/assets/images/vbulletin/edit_usergroup_screen1.gif" class="img-responsive" />
3. Change permissions (for admins and moderators you have one more set of permissions: **AVChat Admin Permissions** that are not available for regular users)
<img src="{{site.github.url}}/assets/images/vbulletin/edit_usergroup_screen2.gif" class="img-responsive" />


<h2 id="allowing-visitors-vbulletin">Allowing visitors to join the video chat</h2>

If you want visitors to access the chat, then you need to specify so from the vBulletin admin area, like we specified on the above question.

1. Login as admin into your forum Control Panel and go to **Usergroups > Usergroup manager**.
<img src="{{site.github.url}}/assets/images/vbulletin/usergroup_manager.gif" class="img-responsive" />
2. Select from the Usergroups list the usergroup you want to edit and click <kbd>Go</kbd>. Here you must choose **Unregistered / Not Logged In**
3. Change permissions accordingly.
4. Click <kbd>Update</kbd>.

</section>
