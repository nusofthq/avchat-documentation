---
layout: default
title: AVChat Component for Joomla! 3.0 - 3.x
description: Documentation covering the AVChat component for Joomla! 3.0 - 3.x.
isHome: false
hide: true
---

<section class="bs-docs-section" markdown="1">
  <h1 id="overview" class="page-header">Quick Overview</h1>
  <p class="lead">The AVChat Integration Kit for Joomla! handles the integration between your Joomla! web site and the AVChat 3 video chat software.</p>

  <p class="lead">Joomla! is the first CMS with which AVChat was ever integrated, and, to this day, it's the one we devote the most time to.</p>

  If you like our AVChat Integration Kits for Joomla! don't forget to rate them and review them in the [Joomla! Extensions Directory](http://extensions.joomla.org/extensions/extension/communication/chat/avchat-video-chat-integration-kit).

  If you cannot find the answer you’re looking for here, we encourage you to try our [forums](http://discuss.avchat.net). There's also more documentation regarding AVChat in the documentation area for the main [standalone](standalone) version.

  All the specific documentation regarding Joomla! is on this page so if you're looking for something specific just hit <kbd>Ctrl+F</kbd> on your browser.
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="installation" class="page-header">Installation instructions</h1>
  <h2 id="download">Download & Extract archives</h2>
  First, you will need the two archives downloaded from your client area:

  * **AVChat 3.0 Build xxxx.zip** (contains media server files for Red5/FMIS/Wowza and AVChat Standalone)
  * **avchat3_joomla_integrationKits_UNZIPFIRST.zip** (contains 4 plugins for Joomla! 1.0-3.x)

  <img src="/assets/images/joomla_images/downloaded_archives.png" class="img-responsive"/>

  Save and extract the archives somewhere on your computer.

  <h2 id="media-server-app">Setting up the media server application</h2>
  Once we've downloaded &amp; unzipped everything the next thing we need to do is to setup the media server app to which AVChat will connect to.

  AVChat uses a media server to send all the audio video and text data between users. AVChat supports the 3 major media servers:

  * Red5
  * Adobe Media Server
  * Wowza

  Here's how to install the `avchat30` app on each one of them:
  {% include media-server-app.md %}

  <h2 id="plugin">Plugin installation</h2>
  To install the component, you will need to be logged in as admin on your website. Once logged in:

  Go to **Extensions** > **Manage**
  <img src="/assets/images/joomla_images/3-0/extensions_menu.png" class="img-responsive"/>

  Press <kbd>Choose File</kbd> and locate the **com_avchat3.zip** archive in the **joomla 3.0.x-3.1.x** > **joomla 3.0.x-3.1.x_component** folder.
  <img src="/assets/images/joomla_images/3-0/component_location.png" class="img-responsive"/>

  Press <kbd>Upload & Install</kbd> and wait for the installation to finish. You should see the success message:
  <img src="/assets/images/joomla_images/3-0/success.png" class="img-responsive"/>

  In the Joomla! administration area go to **Components** > **Avchat 3**. There is a warning about permissions and settings not being set. Click the <kbd>Options</kbd> button then click <kbd>Save & Close</kbd>:
  <img src="/assets/images/joomla_images/3-0/options.png" class="img-responsive"/>

  We'll get back to that a little later.

  You should now see a message informing you that the AVChat files are missing, because we installed the component but not the chat client files.

  You will need to connect to your server using FTP (or SFTP) in order to upload the files.
  Go ahead and open up your favorite FTP Client:

  Upload the files from the **Files to upload to your website** folder to **components** > **com_avchat3** > **chat**
  <img src="/assets/images/joomla_images/3-0/uploaded_files.png" class="img-responsive"/>

  Make sure you change the permissions on the **tokens** and **uploadedFiles** folders to `755`:
  <img src="/assets/images/chmod755.png" class="img-responsive"/>

  <h2 id="configuration">Complete installation</h2>
  <h3>Connect AVChat to the media server app</h3>
  Go to **Components** > **Avchat 3** and press the <kbd>Options</kbd> button.

  In the **RTMP Connection String** field insert the connection string for your media server. The connection string has the following form:
  <pre>rtmp://your_media_server_ip/avchat30/_definst_</pre>

  Press <kbd>Save & Close</kbd>.

  <h3>Enter the chat, connect and insert the license key</h3>
  Press <kbd>Enter Chat</kbd> and AVChat will ask you for the license key. You can get your license key from your client area:
  <img src="/assets/images/joomla_images/3-0/license_key.png" class="img-responsive"/>

  The installation is complete and you should be able to see the admin chat interface in Joomla!'s backend
  <img src="/assets/images/joomla_images/3-0/complete.png" class="img-responsive"/>

  <h3>Embedding the chat in a page</h3>
  In order for your users to access the chat, it must be accessible from a page on your website.
  To add AVChat to the main menu:

  1. Go to **Menus** > **Main Menu** > **Add New Menu Item**
  2. In the **Menu Item Type** field, click <kbd>Select</kbd>
  3. Find **AVChat 3** in the list and select it:
  <img src="/assets/images/joomla_images/3-0/main_menu_select.png" class="img-responsive"/>
  4. Add a **Title** to your menu item by filling the **Menu Title** field.
  5. From the **Access** list select the desired access level.
  6. Press <kbd>Save and close</kbd>.

  AVChat can now be accessed from the page you just created:
  <img src="/assets/images/joomla_images/3-0/page_created.png" class="img-responsive"/>

</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="plugin_features">Component Features</h1>

  <h2 id="permissions">User groups and permissions</h2>

  Joomla! comes with 9 default user groups and the possibility to add more.

  * Public
  * Guest
  * Manager
  * Administrator
  * Registered
  * Author
  * Editor
  * Publisher
  * Super Users

  To limit powers for a certain user group you need to edit the permissions for the user group in the **Components** > **AVChat 3** > **Options** > **Permissions** tab:
  <img src="/assets/images/joomla_images/3-0/permissions.png" class="img-responsive"/>

  If you change a setting, it will apply to the active group and all child groups. If you're editing a child group the permissions set in the parent group might affect the permissions in the child group. The calculated final permission is in the "Calculated Setting" column. Here are the possible values for each setting and how they pass on to child groups:

  * **Inherited** means that the permissions from the parent group will be used.
  * **Denied** means that no matter what the parent group's setting is, the group being edited cannot take this action.
  * **Allowed** means that the group being edited will be able to take this action (but if this is in conflict with the parent group it will have no impact; a conflict will be indicated by **Not Allowed (Locked)** under Calculated Settings).

  For example, if we want web site users part of the **Registered** user group (and all its child groups) to not be able to create rooms:

  1. Login as administrator
  2. Go to **Components** > **AVChat 3** -> **Options** -> **Permissions**
  3. Select the **Registered** user group
  4. For the **Allow users to create rooms** permission, select **Denied**
  5. Click <kbd>Save</kbd>

  Or if we want to allow visitors into the chat in Joomla! you have to:

  1. Login as a administrator
  2. Go to **Components** > **AVChat 3** -> **Options** -> **Permissions**
  3. Select the **Public** user group
  4. Set **Allow Access to the Chat's User Interface** to **Allowed**
  5. Set **Allow Users to Join Other Rooms** to **Allowed**
  6. Set **Allow Users to Send Messages in Text Chat Area** to **Allowed**
  7. Click <kbd>Save</kbd>




  <h2 id="admin-access">Admin access</h2>
  The AVChat admin area can be accessed in both the Joomla! backend (**Components 3** > **AVChat**) and in the front-end (**Main Menu** > **Video Chat**) by users belonging to groups that have permission to access it.

  To grant access to other groups follow these steps:

  1. Login the Joomla! backend as a Super User
  2. Go to **Components** > **AVChat 3** > **Options** > **Permissions**
  3. Click on the user group you want to grant access to
  4. Set to Allow the following permission **Allow access to the Chat's Admin Interface**
  5. Press <kbd>Save</kbd>
  6. Now the Calculated Setting on the right should be set to Allowed

  <div class="alert alert-info" markdown="1">
  <strong>Notes:</strong>


  * Only users part of the **Super Users** can edit the AVChat permissions as instructed above.

  * Even if the Super User gives permission for a user group to enter the Joomla! backend, that user group will not gain access to the AVChat admin interface. Such access can be given to him from the AVChat Component's Options menu by Super Users.

  * If you give a certain user group permission to access the admin area of AVChat, then he can access that through front-end and backend as well (if he has permissions to backend, of course)

  * By default Managers and Administrators do not have access to the Components part of the backend so if given permission to access the AVChat admin area they need to access it trough the front-end OR they must be given permissions to access the Components area in the backend.
  </div>

  Here is a tutorial on how to allow **Managers** and **Administrators** access to the Components area in the Joomla! backend and thus have access to the AVChat Component:

  1. Login as a Super User in the Joomla! backend area
  2. Go to **System** > **Global Configuration** > **Permissions**
  3. Click the **Manager** user group and set the **Access Administration Interface** permission to **Allowed**.
  4. The **Administrators** user group will automatically inherit the permission.
  5. Click <kbd>Save</kbd>

  Now **Managers** and **Administrators** will have access to the AVChat Component in the Joomla! backend.

  <h2 id="files">AVChat files</h2>
  All the files are in the `/components/com_avchat3/` folder.

  <h2 id="opening-method">Opening method</h2>
  You can also open the chat in a pop-up window instead of embedding it in a page.

  1. Log in the administrator area of Joomla!.
  2. Go to **Components** > **AVChat 3** > **Options**
  3. Go to the **AVChat 3 Open Method** tab.
  4. Select **Popup** in the **Open Method** list.
  5. You can change the size of the pop-up window by changing the values from the **Popup Height** and **Popup Width** fields.
  6. Click <kbd>Save</kbd>.

  AVChat will now open in a pop-up window.

  <h2 id="placing-ads">Placing ads around the video chat</h2>
  Placing ads around the video chat is simple. The video chat itself is actually a Flash .swf file embedded in a HTML file. In that HTML file you can place anything: links, images, AdWords ads, banners, etc. .

  In order to place ads around the chat, you will have to edit the file that embeds it in page. The file is `components/com_avchat3/views/avchat3/tmpl/default.php`.

  The chat is embedded in the `div` element with id `myContent`.

  <img src="/assets/images/joomla_images/3-0/around_chat.png" class="img-responsive"/>

  Add the code to the page and save the file on your server.

  <h2 id="facebook-login">Facebook Login</h2>
  You have the possibility of allowing guests and visitors to access the chat using their Facebook account.
  To do this, make sure that:

  1. Visitors have access to the chat.
  2. The Facebook application is configured.

  Here's how to configure Facebook Login for visitors on your Joomla! website:

  1. [Setup the Facebook application](standalone#setup-facebook-authentication)
  2. Log in the administrator area of Joomla!.
  3. Go to **Components** > **AVChat 3** > **Options**
  4. Insert your application ID in the **Facebook Application ID** field.
  5. Click <kbd>Save & Close</kbd>.

  <h2 id="design">Customizing the looks</h2>
  <h3>Changing the size</h3>
  If you're using the Popup opening method, the size of the popup window can be changed from **Components** > **AVChat 3** > **Options** > **AVChat 3 Open Method**.

  If you're embedding the chat in a page, to change the size of the chat interface:

  1. Open `components/com_avchat3/views/avchat3/tmpl/default.php` in a text editor
  2. Search for the line that starts with `swfobject.embedSWF`:


        `swfobject.embedSWF("%3C%3Fphp echo $chat_path."/".$swf; %3F%3E", "myContent", "100%", "600", "11.1.0", "", flashvars, params, attributes);</script>`

  3. `100%` represents the width (in percentage) of the chat interface
  4. `600` represents the height (in pixels) of the chat interface
  5. Change these values as you need and save the file.

  <h3>Changing the background color</h3>
  1. Open `components/com_avchat3/views/avchat3/tmpl/default.php` in a text editor
  2. Search for `bgcolor` and enter the color code you want
  3. Save the file.

  <h2 id="whos-chatting">Who's Chatting Module</h2>

  In the **avchat3_joomla_integrationKits_UNZIPFIRST.zip** archive, under **joomla 3.0.x-3.1.x** you will also find a folder named **joomla3.0.x_mod_avchat3online**. It contains an archive named **mod_avchat3online.zip**.

  It's a module for your Joomla! web site that shows in the side bar a list of the users online in the video chat at that time.

  To install it:

  1. Log in the administrator area of Joomla!.
  2. Go to **Extensions** > **Extension Manager**.
  3. Press <kbd>Choose File</kbd> and locate the **mod_avchat3online.zip** archive in the **joomla 3.0.x-3.1.x** folder.
  4. Click <kbd>Upload & Install</kbd>.
  5. Now go to **Extensions** > **Module Manager**, you should see the **Who's online in chat** module in the list. Click on it:
  <img src="/assets/images/joomla_images/3-0/whos_online.png" class="img-responsive"/>
  6. Enable it by selecting **Published** from the **Status** field
  7. Now you have to select the position on page. Click on the **Type or Select a Position** and choose from the list where you want the module to be displayed. We recommend position-7 since it represents the right column in the default Joomla! template (protostar).
  8. Choose who you want to have access to it
  9. Now move to the Menu Assignment tab and choose the pages you want to be displayed in.
  10. Click <kbd>Save & Close</kbd>

  Done, now it will show up on your web site:
  <img src="/assets/images/joomla_images/3-0/whos_online_site.png" class="img-responsive"/>

  <h2 id="update">Updating the component</h2>
  We make new versions of the AVChat Component independently from the actual AVChat software, that's why it's necessary to update the component and not the AVChat software itself. Here's how to do it:

  1. Log in the administrator area of Joomla!.
  2. Go to **Extensions** > **Extension Manager**.
  3. Press <kbd>Choose File</kbd> and locate the **com_avchat3.zip** archive in the **joomla 3.0.x-3.1.x** > **joomla 3.0.x-3.1.x_component** folder.
  4. Click on <kbd>Upload & Install</kbd>
  5. Go to **Components** > **AVChat 3** > **Options**
  6. Make sure all your permissions and settings are correct!
  7. Click on <kbd>Save & Close</kbd>

  <h2 id="community_scripts">Community Scripts</h2>
  The AVChat Integration Kit for Joomla! integrates with the 3 big Joomla! community scripts.
  It will detect if you're using **EasySocial**, **JomSocial** or **Community Builder** and will seamlessly integrate the features offered by them such as:
  * Same Profile Photo - By default, Joomla! does not offer the possiblity of adding profile pictures.
  * Linked Profile Pages
  * Same gender


  <h2 id="gpl">AVChat Components for Joomla! and GPL</h2>
  The AVChat Video Chat Components are licensed under the [GPL v2](http://www.gnu.org/licenses/gpl.txt) in accordance with the [JED requirements](http://community.joomla.org/blogs/leadership/636-jed-to-be-gpl-only-by-july-2009.html). Once you buy the integration kits you can modify them and distribute them as long as you keep it under the GPL.
</section>
