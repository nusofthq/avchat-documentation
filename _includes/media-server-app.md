<ul class="nav nav-tabs" id="serversTab">
  <li class="active"><a data-target="#red5" data-toggle="tab">Red5</a></li>
  <li><a data-target="#ams" data-toggle="tab">Adobe Media Server</a></li>
  <li><a data-target="#wowza" data-toggle="tab">Wowza</a></li>
</ul>

<div class="tab-content" markdown ="1">

  <div class="tab-pane active" id="red5">

Upload the `avchat30` folder from the **Files to upload to your media server (Red5)** folder to your Red5's **webapps** folder (C:\Program Files\Red5\webapps on Win, /opt/red5/webapps/ on Linux).

On Linux, chmod the new `avchat30` folder to 777.

Restart the Red5 server.

  </div>

  <div class="tab-pane" id="ams">

Upload the `avchat30` folder (you will find it in your AVChat archive in the **Files to upload to your media server (FMS) folder)** to the **applications** folder of your AMS installation.

Chmod the new `avchat30` folder to 777.

  </div>

  <div class="tab-pane" id="wowza">

Upload the `applications`, `lib` and `conf` folders from the **Files to upload to your media server (Wowza)** folder to the root folder of your Wowza Media Server installation.

Restart the Wowza server.

Starting with Wowza Streaming Engine 4, a new GUI has been added that allows you to control the server and individual applications. This can be accessed using a browserby going to http://WOWZA_SERVER_ADDRESS:8088/enginemanager/.

Wowza Streaming Engine 4 comes with the default stream prefix **mp4**. This needs to be changed to **flv**. Here's how:

1. Go to http://WOWZA_SERVER_ADDRESS:8088/enginemanager/
2. From the top menu click the [Server] page
3. In Server Setup click Edit
4. Change Default Stream Prefix from mp4 to flv
5. Save

  </div>

</div>

<script>
jQuery(function () {
    jQuery('#serversTab a:last').tab('show')
})
</script>
