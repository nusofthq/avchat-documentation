---
layout: default
title: AVChat - WordPress Community PRO
description: Simple documentation template for Github pages
isHome: false
hide: true
---
<section class="bs-docs-section" markdown="1">
  <h1 id="overview" class="page-header">Quick Overview</h1>
  The Community PRO Video Chat Plugin for WordPress handles the integration between your WordPress web site and the AVChat video chat platform.

  The plugin will handle the following:

  * user name integration
  * profile url integration
  * profile image integration
  * placement of video chat within the web site (user and admin interface)
  enable/disable/limit more than 47 features for each user role
  * MultiSite support
  * BuddyPress support: BuddyPress avatars will be used and BuddyPress users profiles can be accessed directly from AVChat

  All the documentation regarding the Community PRO plugin is on this page so if you're looking for something specific just hit Ctrl+F on your keyboard. The main AVChat documentation is here.
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="installation" class="page-header">Installation instructions</h1>

  First, you will need the two archives downloaded from your client area:

  * AVChat 3.0 Build xxxx.zip (contains media server files for Red5/FMIS/Wowza and AVChat Standalone)
  * avchat3_wordpress_plugins_pro.zip (contains 1 plugin for WordPress 4.x)

  <img src="/assets/images/wordpress_images/downloaded_archives.png" class="img-responsive"/>

  Extract the 2 archives somewhere on your computer and follow Steps 1.1 and 1.2 mentioned below.

  <h2 id="media-server-app">Setting up the media server application</h2>
  foo
  <h2 id="plugin">Plugin installation</h2>
  To install the plugin, you will need to be logged in as admin on your website. Once logged in:

  1. Go to the plugins page, section <kbd>Add New</kbd> in your WordPress backend:
  <img src="/assets/images/wordpress_images/plugins_section.png" class="img-responsive"/>
  2. Press the <kbd>Upload Plugin</kbd> button:
  <img src="/assets/images/wordpress_images/upload_plugin.png" class="img-responsive"/>
  3. Press <kbd>Choose File</kbd> and select the avchat3_wordpress_plugins_pro.zip file:
  <img src="/assets/images/wordpress_images/select_archive.png" class="img-responsive"/>
  4. Press <kbd>Install Now</kbd> and wait for the setup to finish:
  <img src="/assets/images/wordpress_images/install_now.png" class="img-responsive"/>

  Before activating the plugin, you will have to upload the AVChat files on your server. To do so, you will need FTP (or SFTP) access to your server.

  <div class="alert alert-info">
    If you are not sure how to access your server using FTP, it's better to contact your Hosting Company.
  </div>

  Go ahead and open your favorite FTP Client.
  <img src="/assets/images/wordpress_images/ftp_client.png" class="img-responsive"/>
  Navigate to **/wp-content/plugins**:
  <img src="/assets/images/wordpress_images/avchat_folder.png" class="img-responsive"/>
  You should see a new folder called **avchat-3-pro**. Open it.

  Also open the folder on your computer containing the AVChat client files (the ones from the **AVChat 3.0 Build xxxx.zip** archive):
  <img src="/assets/images/wordpress_images/avchat_archive_folder.png" class="img-responsive"/>
  Copy all the files in the **Files to upload to your website** folder inside the **avchat-3-pro** folder:
  <img src="/assets/images/wordpress_images/uploaded_files.png" class="img-responsive"/>

  Make sure you change the permissions on the **tokens** and **uploadedFiles** folders to `777`:
  <img src="/assets/images/wordpress_images/chmod.png" class="img-responsive"/>

  <h2 id="plugin-configure">Plugin Configuration</h2>
  You can now activate the plugin. Once activated, a new page has been added in your WordPress Dashboard.
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
  <h1 id="accessing-admin">Accessing the AVChat admin interface in WordPress</h1>
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="who-has-access">Who has access to the video chat admin interface</h1>
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="location">Location of AVChat and plugin files</h1>
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="in-popup">Opening up the video chat in a pop up</h1>
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="ads">Placing ads around the video chat</h1>
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="roles">WordPress's user roles and limiting features for specific user roles</h1>
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="visitors">Allowing visitors to join the video chat</h1>
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="facebook">Allow users to login with their Facebook account</h1>
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="design">Changing the looks of AVChat to better fit your WordPress web site</h1>
  <h2 id="design-color">Changing the background color</h2>
  <h2 id="design-image">Changing the background image</h2>
</section>

<section class="bs-docs-section" markdown="1">
  <h1>Community PRO for WordPress and GPL</h1>
</section>

<section class="bs-docs-section" markdown="1">
  <h1>Removing the plugin</h1>
</section>

<section class="bs-docs-section" markdown="1">
  <h1>Updating the plugin when a new version is available</h1>
</section>

<section class="bs-docs-section" markdown="1">
  <h1>Multisite support</h1>
</section>

<section class="bs-docs-section" markdown="1">
  <h1>Allow users to login with their Twitter account</h1>
</section>

<section class="bs-docs-section" markdown="1">
  <h1>Extended short code functionality</h1>
</section>
