---
layout: default
title: AVChat - WordPress Pay Per Session
description: Simple documentation template for Github pages
isHome: false
hide: true
---
<section class="bs-docs-section" markdown="1">
  <h1 id="overview" class="page-header">Quick Overview</h1>

  The Pay Per Session plugin for WordPress transforms your website into a modern tool for delivering online services with the help of audio/video calls. It does this by seamlessly integrating WordPress with AVChat - our video chat platform - and PayPal.
</section>

<section class="bs-docs-section" markdown="1">
  <h1 id="installation" class="page-header">Installation instructions</h1>
  First, you will need the two archives downloaded from your client area:

  * **AVChat 3.0 Build xxxx.zip** (contains media server files for Red5/FMIS/Wowza and AVChat Standalone)
  * **avchat-3-pps.zip** (contains 1 plugin for WordPress 4.x)

  <img src="/assets/images/wordpress-pps_images/downloaded_archives.png" class="img-responsive"/>

  <h2 id="media-server-app">Setting up the media server application</h2>
  {% include media-server-app.md %}
  <h2 id="plugin">Plugin installation</h2>
  To install the plugin, you will need to be logged in as admin on your website. Once logged in:



  1. Go to the **Plugins** page, section **Add New** in your WordPress backend:
  <img src="/assets/images/wordpress_images/plugins_section.png" class="img-responsive"/>


  2. Press the <kbd>Upload Plugin</kbd> button:
  <img src="/assets/images/wordpress_images/upload_plugin.png" class="img-responsive"/>


  3. Press <kbd>Choose File</kbd> and select the avchat3_wordpress_plugins_pro.zip file:
  <img src="/assets/images/wordpress-pps_images/select_archive.png" class="img-responsive"/>


  4. Press <kbd>Install Now</kbd> and wait for the setup to finish:
  <img src="/assets/images/wordpress-pps_images/install_now.png" class="img-responsive"/>


  Before activating the plugin, you will have to upload the AVChat client files on your server. To do so, you will need FTP (or SFTP) access to your server.

  <div class="alert alert-info">
    If you are not sure how to access your server using FTP, it's better to contact your Hosting Company.
  </div>

  Go ahead and open your favorite FTP Client.
  <img src="/assets/images/wordpress_images/ftp_client.png" class="img-responsive"/>
  Navigate to **/wp-content/plugins**:
  <img src="/assets/images/wordpress-pps_images/avchat_folder.png" class="img-responsive"/>
  You should see a new folder called **avchat-3-pps**. Open it.

  Also open the folder on your computer containing the AVChat client files (the ones from the **AVChat 3.0 Build xxxx.zip** archive):
  <img src="/assets/images/avchat_archive_folder.png" class="img-responsive"/>
  Copy all the files in the **Files to upload to your website** folder inside the **avchat-3-pps** folder:
  <img src="/assets/images/wordpress-pps_images/uploaded_files.png" class="img-responsive"/>

  Make sure you change the permissions on the **tokens** and **uploadedFiles** folders to `777`:
  <img src="/assets/images/chmod.png" class="img-responsive"/>

  <h2 id="plugin-configure">Plugin Configuration</h2>
  You can now activate the plugin. Once activated, a new page is added in your WordPress Dashboard: **Pay Per Session**.
  <img src="/assets/images/wordpress-pps_images/activate.png" class="img-responsive"/>

  You need to insert the IP Address of your media server, license key and PayPal e-mail.

  The connection string has the following form:
  <pre>rtmp://your_media_server_ip/avchat30/_definst_</pre>

  Go to **Pay Per Session** > **Settings** > **AVChat settings**.

  Paste the license key in the **AVChat license key** field.

  Insert the IP Address of your media server in the **Media Server IP** field.

  Insert your PayPal e-mail address in the **PayPal e-mail** field.

  <img src="/assets/images/wordpress-pps_images/info.png" class="img-responsive"/>

  Press <kbd>Update Options</kbd>

  Now create a new page on your website, and place the [hosts] shortcode.
  Our recommandation is to exclude any left or right side menus and leave the page as simple as you can.

</section>


<section class="bs-docs-section" markdown="1">
  <h1 id="accessing-admin">Plugin Features</h1>

  <h2 id="setup-hosts">Setting up your first host</h2>
  1. Navigate to your **WordPress backend** > **Pay Per Session** > **Members & hosts**
  2. From here you can assign any user as host. He/She will receive an e-mail, confirming the change. Only registered users will show up in this list, therefore make sure the user is registered with your site. To add a new user, go to your **WordPress backend** > **Users** > **Add new**
  3. The new host will be able to change his/hers profile by going to your **WordPress backend** > **Pay Per Session** > **My Profile**. All fields are mandatory.

  All payments made are visible for all hosts in Pay Per Session -> View Payments
  Hosts will be able to consult their personal earnings by going to Pay Per Session -> My sessions

  <h2 id="create-profile">Creating your host profile & services</h2>
  A complete host profile will increase your users' confidence in acquiring new services and it will build loyalty for returning clients.

  <h4>Creating your profile</h4>

  Complete your public host profile by going to **Pay Per Session** > **My Profile** and fill up all details about yourself. We strongly recommend you to upload an avatar (profile picture) and a cover image, just like on Facebook.

  <h4>Adding your services</h4>
  Add new services by going to **Pay Per Session** > **My services**. Each service represents what you are selling (name), how much it costs (price), for how long the session will last (duration) and a full description of what you will be doing in that timespan. Choose an insightful title and a detailed description. You can add as many services as needed.

  You cannot delete services, but you can always disable and re-enable them at anytime. If mistakes occur, simply disable the service and create a new one with the same characteristics.

  <h2 id="session">Your first video chat session</h2>
  Your sessions are available in the **WordPress backend menu** > **Pay Per Session** > **My sessions**. From there you can directly access the video chat.

  Once you have completed your host profile and defined at least one service, you are now visible to both visitors and registered users of the WordPress site.

  <img src="/assets/images/wordpress-pps_images/service.png" class="img-responsive"/>

  After a client has paid for one of your services, both of you will receive a confirmation e-mail containing all the details regarding the session (name, cost, duration), including a unique session access link.

  * Do not share this link with anyone.
  * You must contact the client and establish a common date and time when the session will take place.

  The newly created session is also available in the host's backend control panel, where you have a clear overview of all your available and past sessions:

  <img src="/assets/images/wordpress-pps_images/my_sessions.png" class="img-responsive"/>

  After you get in touch with you client and establish a common day and hour, you can access the unique session link from your control panel or directly from the confirmation e-mail:

  <img src="/assets/images/wordpress-pps_images/session.png" class="img-responsive"/>

  The audio/video popup will contain a timer, which is strictly informative. No one will get kicked at the end of the countdown. The host must close the audio/video chat popup and Mark the session as delivered.

  <h2 id="updating">Updating the plugin</h2>
  The WordPress plugin can be updated by overwriting the plugin files located at `your-site.com/wp-content/plugins/avchat-3-pps`. No data or settings will be lost during the update unless specified in the change-log.

  The AVChat software can be updated by uploading the the contents of Files to upload to your web site to the `/wp-content/plugins/avchat-3-pps` folder.

  <h2 id="deactivating">Deactivating</h2>
  Deactivating the plugin will disable the hosts' access to the Pay Per Session backend menu. Also, all hosts and their profiles & services will not be visible anymore in the page where the **[hosts]** shortcode resides.

  The process is simple and standard, as with any other WordPress Plugin. In your **WordPress Backend** > **Plugins** and click <kbd>Deactivate</kbd>.

  **All settings will be preserved and you can re-activate the plugin anytime later.**

  <h2 id="uninstalling">Uninstalling the plugin</h2>
  Uninstalling will delete all settings, uploaded images and hosts profile (your WordPress users will remain intact). Go to **WordPress backend** -> **Plugins** and click <kbd>Uninstall</kbd>. All settings, files and customization will be lost.
</section>
