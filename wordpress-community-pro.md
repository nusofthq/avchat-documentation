---
layout: default
title: AVChat - WordPress Community PRO
description: WordPress Community PRO documentation
isHome: false
hide: true
---
<section class="bs-docs-section" markdown="1">
  <h1 id="overview" class="page-header">Quick Overview</h1>
  The Community PRO Video Chat Plugin for WordPress handles the integration between your WordPress web site and the AVChat video chat platform.

  The plugin will handle the following:

  * User name integration
  * Profile url integration
  * Profile image integration
  * Placement of video chat within the web site (user and admin interface)
  * Enable/disable/limit more than 47 features for each user role
  * MultiSite support
  * BuddyPress support: BuddyPress avatars will be used and BuddyPress users profiles can be accessed directly from AVChat

  All the documentation regarding the Community PRO plugin is on this page so if you're looking for something specific use the menu on the right or search within this page by pressing <kbd>Ctrl+F</kbd> on your keyboard. The main AVChat documentation is [here](/standalone).
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="installation" class="page-header">Installation instructions</h1>

  First, you will need the two archives downloaded from your client area:

  * **AVChat 3.0 Build xxxx.zip** (contains media server files for Red5/FMIS/Wowza and AVChat Standalone)
  * **avchat3_wordpress_plugins_pro.zip** (contains 1 plugin for WordPress 4.x)

  <img src="/assets/images/wordpress_images/downloaded_archives.png" class="img-responsive"/>

  Save and extract the archives somewhere on your computer.

  <h2 id="media-server-app">Setting up the media server application</h2>
  {% include media-server-app.md %}
  <h2 id="plugin">Plugin installation</h2>
  To install the plugin, you will need to be logged in as admin on your website. Once logged in:



  1. Go to the **Plugins** page, section **Add New** in your WordPress backend:
  <img src="/assets/images/wordpress_images/plugins_section.png" class="img-responsive"/>


  2. Press the <kbd>Upload Plugin</kbd> button:
  <img src="/assets/images/wordpress_images/upload_plugin.png" class="img-responsive"/>


  3. Press <kbd>Choose File</kbd> and select the avchat3_wordpress_plugins_pro.zip file:
  <img src="/assets/images/wordpress_images/select_archive.png" class="img-responsive"/>


  4. Press <kbd>Install Now</kbd> and wait for the setup to finish:
  <img src="/assets/images/wordpress_images/install_now.png" class="img-responsive"/>


  Before activating the plugin, you will have to upload the AVChat client files on your server. To do so, you will need FTP (or SFTP) access to your server.

  <div class="alert alert-info">
    If you are not sure how to access your server using FTP, it's better to contact your Hosting Company.
  </div>

  Go ahead and open your favorite FTP Client.
  <img src="/assets/images/wordpress_images/ftp_client.png" class="img-responsive"/>
  Navigate to **/wp-content/plugins**:
  <img src="/assets/images/wordpress_images/avchat_folder.png" class="img-responsive"/>
  You should see a new folder called **avchat-3-pro**. Open it.

  Also open the folder on your computer containing the AVChat client files (the ones from the **AVChat 3.0 Build xxxx.zip** archive):
  <img src="/assets/images/avchat_archive_folder.png" class="img-responsive"/>
  Copy all the files in the **Files to upload to your website** folder inside the **avchat-3-pro** folder:
  <img src="/assets/images/wordpress_images/uploaded_files.png" class="img-responsive"/>

  Make sure you change the permissions on the **tokens** and **uploadedFiles** folders to `777`:
  <img src="/assets/images/chmod.png" class="img-responsive"/>

  <h2 id="plugin-configure">Plugin Configuration</h2>
  You can now activate the plugin. Once activated, a new page is added in your WordPress Dashboard: **Video Chat PRO**.
  <img src="/assets/images/wordpress_images/activate.png" class="img-responsive"/>

  You need to insert the connection string. The connection string has the following form:

  <pre>rtmp://your_media_server_ip/avchat30/_definst_</pre>

  Add your connection string in the **Connection string** field:
  <img src="/assets/images/wordpress_images/connection_string.png" class="img-responsive"/>

  Scroll down and press <kbd>Update Options</kbd>

  Now go to **Enter Chat** to access the chat interface:
  <img src="/assets/images/wordpress_images/chat_interface.png" class="img-responsive"/>

  You will be asked for the license key. You can get your license key from your client area:
  <img src="/assets/images/wordpress_images/license_key.png" class="img-responsive"/>

  The installation is complete and you should be able to see the chat interface:
  <img src="/assets/images/wordpress_images/install_complete.png" class="img-responsive"/>
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="accessing-admin">Plugin Features</h1>

  <h2 id="access-admin">Embed the chat</h2>
  In order for your users to access the chat, it must be accessible from a page on your website.
  The Community PRO plugin will allow you to embed the chat easily, using a shortcode in a post or page.

  To embed the chat in a page:

  1. Go to the **Pages** section in your Wordpress Dashboard:
  <img src="/assets/images/wordpress_images/pages.png" class="img-responsive"/>
  2. Press <kbd>Add New</kbd> and give your page a title.

  3. Add the `[chat]` shortcode in your page body and press <kbd>Publish</kbd>:
  <img src="/assets/images/wordpress_images/publish.png" class="img-responsive"/>

  Going to this page will allow you and your users to access AVChat:
  <img src="/assets/images/wordpress_images/embedded.png" class="img-responsive"/>

  <h2 id="permissions">User roles and permissions</h2>
  The Community PRO plugin for WordPress allows you to control permissions for each user role.
  By default, there are 5 user roles predefined on every WordPress installation:

  * Administrator
  * Editor
  * Author
  * Contributor
  * Subscriber

  You can also handle permissions for non-registered users (visitors).

  * In your WordPress Dashboard, go to **Video Chat PRO** > **Settings**.
  * Select the **User roles & Permissions** tab.
   <img src="/assets/images/wordpress_images/roles_permissions.png" class="img-responsive"/>
  * Here you can enable or disable any permission for each user role
  * Once you are done setting up the permissions, don't forget to press the <kbd>Update Options</kbd> button.

  For example, if you want to disable access for visitors, you will have to uncheck the **Can access chat** box under **Visitors**:
  <img src="/assets/images/wordpress_images/visitors.png" class="img-responsive"/>

  <h2 id="admin-access">Admin access</h2>
  The admin interface is visible to all the users that have the permission to access it (see [User Roles and Permissions](#permissions)).

  If you access the chat from a page in which AVChat is embedded, the integration plugin will automatically detect if the user has access to the admin interface, and will show it accordingly.

  If you access the chat from your WordPress Dashboard (**Video Chat PRO** > **Enter Chat**), you will get access to the admin interface.

  <h2 id="files">AVChat files location</h2>
  All the files are in the `/wp-content/plugins/avchat-3-pro/` folder.

  <h2 id="opening-method">Opening method</h2>
  By default, AVChat will be embedded where you place the `[chat]` shortcode. However, you have the possibility of opening AVChat in a popup window.

  To do so, go to **Video Chat PRO** > **Settings** and find **How AVChat opens**.

  Change the opening method to **Popup** and press <kbd>Update Options</kbd>.

  <h2 id="facebook-login">Facebook Login</h2>
  To enable Facebook Login you will need to create a Facebook Application from where you will receive an App ID. You can follow the next steps to accomplish this.

  1. Go and Register as a Developer at: [http://developers.facebook.com](http://developers.facebook.com)
  <img src="/assets/images/wordpress_images/fb_register_dev.png" class="img-responsive"/>
  2. Click <kbd>Create New App</kbd>
  <img src="/assets/images/wordpress_images/fb_create_new_app_btn.png" class="img-responsive"/>
  3. Insert your application name (App Name), select the category and press <kbd>Create App</kbd>
  <img src="/assets/images/wordpress_images/facebook_create_new_app.png" class="img-responsive"/>
  4. After pressing the <kbd>Create App</kbd> button you will be redirected to the application page where you will find the App ID. Don't forget to enter your website URL in Website with Facebook Login
  <img src="/assets/images/wordpress_images/fb_app_id_1.png" class="img-responsive"/>
  <img src="/assets/images/wordpress_images/fb_app_id_2.png" class="img-responsive"/>
  <img src="/assets/images/wordpress_images/fb_app_id_3.png" class="img-responsive"/>

  5. Now that you have your Facebook App ID, in your website, go to your **WordPress Admin** > **Video Chat PRO** > **Facebook & Twitter Login** tab
  <img src="/assets/images/wordpress_images/fb_conf.png" class="img-responsive"/>
  6. Insert your Facebook App ID
  <img src="/assets/images/wordpress_images/fb_insert_app_id.png" class="img-responsive"/>
  7. Press <kbd>Update Options</kbd>

  <h2 id="twitter-login">Twitter Login</h2>
  To enable Twitter Login for your video chat you will need to create a Twitter Application that will provide you with a Consumer Key and an Consumer Secret. You can follow the next steps to accomplish this.

  1. Go to [https://dev.twitter.com/apps](https://dev.twitter.com/apps) and click on the <kbd>Create a new application</kbd> button.
  <img src="/assets/images/wordpress_images/twitter_new_application.png" class="img-responsive"/>
  2. Complete the form:
  * **Name** - enter the name of your application
  * **Description** - insert the description
  * **Website** - enter your website URL
  * Press <kbd>Create your Twitter application!</kbd>

  <img src="/assets/images/wordpress_images/twitter_new_app_form.png" class="img-responsive"/>
  3. After you completed the form you will be redirected to the application page, where you will find your `Consumer key` and `Consumer secret`.
  <img src="/assets/images/wordpress_images/twitter_app_page.png" class="img-responsive"/>
  4. Now that you have your Consumer key and Consumer Secret, in your website, go to your **WordPress Admin** > **Video Chat PRO** > **Facebook & Twitter Login** tab
  <img src="/assets/images/wordpress_images/fb_conf.png" class="img-responsive"/>
  5. Insert your Consumer key in Twitter Consumer Key option and Consumer secret in Twitter Consumer Secret
  <img src="/assets/images/wordpress_images/wp_twitter_settingup.png" class="img-responsive"/>
  6. Press <kbd>Update Options</kbd>

  <h2 id="plugin-update">Updating the plugin</h2>
  First you should download the new archive from your client area on [nusofthq.com](http://nusofthq.com)

  Then we need to remove the old version. While logged in as and admin in the WP backend go to **Plugins** and click <kbd>Deactivate</kbd> followed by <kbd>Delete</kbd> for the AVChat Community PRO plugin. This will remove the **wp-content/plugins/avchat-3-pro** folder and all its contents.
  <div class="alert alert-danger"><strong>Warning!</strong> This will also delete the chat client so make sure you make a backup before updating</div>
  You will now have to re-[install](/wordpress-community-pro#installation) the plugin and upload the AVChat 3 client side files again to the **wp-content/plugins/avchat-3-pro** folder.

  Any existing settings or permissions will be kept. Any new settings or permissions added by the new version will most probably be empty, make sure you configure them as you wish for each user role from **Video Chat PRO** > **User Roles & Permissions** tab.

  <h2 id="plugin-remove">Removing the plugin</h2>
  While logged in as and admin in the WordPress backend go to **Plugins** and click <kbd>Deactivate</kbd> followed by <kbd>Delete</kbd> for the AVChat Community PRO plugin.

  This will remove the **wp-content/plugins/avchat-3-pro** folder and all it's contents.

  The plugin's database holding the permissions for each user role and general settings will still remain tough. To remove it, delete the `wp_avchat3_general_settings` and the `wp_avchat3_permissions` tables.

  You might also want to remove the page holding the `[chat]` tag that was replaced by the plugin with the AVChat 3 software

  <h2 id="multisite">Multisite support</h2>
  WordPress has a special mode called **Multisite**. This mode has been introduced in 2010 in WordPress 3.0.

  Starting with build 2359, the plugin adds support for installations of WordPress with multisite on.

  A new WP user role is present in multisite setups:

  Super Admin – somebody with access to the site network administration features and all other features.
  In such an installation the plugin can either be network activated for all sites or individually activated.

  After installation, the super admin can network activate it for all the websites or he can activate it individually for each of his websites.

  If **My Sites** > **Network Admin** > **Dashboard** > **Settings** > **Network Settings** > **Enable administration menus** > **[  ]Plugins** is checked then other network users can independently activate it for their websites too.

  <h3>Network Activation</h3>

  When the plugin is network activated, it can not be individually deactivated.

  When the plugin is network activated you must visit the **Settings** > **Video Chat PRO** page for each of the websites in the network for the permissions tables for AVChat3 to be created. Otherwise in the front end you will find the following error:

  `Warning: Invalid argument supplied for foreach() in /home/observer/public_html/wp-content/plugins/avchat-3-pro/avchat3.php on line 86`

  When using a standard WordPress installation (non multisite) or when individually activating the plugin for each sub site in the network the tables are created at activation.
  <h3>Network Users</h3>

  When used in a multisite setup, the plugin will show a new column (role) in the **Settings** > **Community PRO** area called **Network** users. These are users who belong to the network but they do not belong to any other website on the network other than their own. They have no role in other websites than their own.

  <h3>Permissions and Settings</h3>

  Each site on the network can control the permissions and settings individually. This also means that each site on the network has to have their own connection string. It is possible for 2 or more websites to use the same connection string, in this case they will share the rooms and users list,etc. .

  
  <h2 id="shortcode-opts">Extended short code functionality</h2>
  To display AVChat 3 in your WordPress page or posts, you will use the short code [chat].

  You can extend the functionality of short code by adding the following options:

  * dropInRoom:r0 - this option allows you to define the rooms ids (r0, r1, r2 etc) in which users will be droped when entering the chat
  * showOnlyRooms:r0 - this options allows you to define the rooms that users will be able to see
  * roomsListEnabled:1 - you can disable (0), enable (1) or hide (2) the rooms list button in the top bar

  <img src="/assets/images/wordpress_images/extended_shortcode.png" class="img-responsive"/>

  <h2 id="gpl">Community PRO for WordPress and GPL</h2>
  The AVChat Video Chat Plugin is licensed under the [GPL v2](http://www.gnu.org/licenses/gpl.txt) or later. Once you buy the plugin you can modify it and distribute it as long as you keep it under the GPL.
</section>
