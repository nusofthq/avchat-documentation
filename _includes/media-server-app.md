<ul class="nav nav-tabs" id="serversTab">
  <li class="active"><a data-target="#red5" data-toggle="tab">Red5</a></li>
  <li><a data-target="#ams" data-toggle="tab">Adobe Media Server</a></li>
  <li><a data-target="#wowza" data-toggle="tab">Wowza</a></li>
</ul>

<div class="tab-content">

  <div class="tab-pane active" id="red5">

<p>Upload the <code class="highlighter-rouge">avchat30</code> folder from the <b>Files to upload to your media server (Red5)</b> folder to your Red5's <b>webapps</b> folder (C:\Program Files\Red5\webapps on Win, /opt/red5/webapps/ on Linux).</p>

<p>On Linux, chmod the new <code class="highlighter-rouge">avchat30</code> folder to 777.</p>

<p>Restart the Red5 server.</p>

  </div>

  <div class="tab-pane" id="ams">

Upload the <code class="highlighter-rouge">avchat30</code> folder (you will find it in your AVChat archive in the <b>Files to upload to your media server (FMS) folder)</b> to the <b>applications</b> folder of your AMS installation.

Chmod the new <code class="highlighter-rouge">avchat30</code> folder to 777.

  </div>

  <div class="tab-pane" id="wowza">

Upload the <code class="highlighter-rouge">applications</code>, <code class="highlighter-rouge">lib</code> and <code class="highlighter-rouge">conf</code> folders from the <b>Files to upload to your media server (Wowza)</b> folder to the root folder of your Wowza Media Server installation.

Restart the Wowza server.

Starting with Wowza Streaming Engine 4, a new GUI has been added that allows you to control the server and individual applications. This can be accessed using a browser by going to <b>http://WOWZA_SERVER_ADDRESS:8088/enginemanager</b>

Wowza Streaming Engine 4 comes with the default stream prefix <b>mp4</b>. This needs to be changed to <b>flv</b>. Here's how:
<ol>
<li>Go to <b>http://WOWZA_SERVER_ADDRESS:8088/enginemanager/</b></li>
<li>From the top menu click the [Server] page</li>
<li>In Server Setup click Edit</li>
<li>Change Default Stream Prefix from mp4 to flv</li>
<li>Save</li>
</ol>
  </div>

</div>

<script>
jQuery(function () {
    jQuery('#serversTab a:last').tab('show')
})
</script>
