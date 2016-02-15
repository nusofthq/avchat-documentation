<ul class="nav nav-tabs" id="serversTab">
  <li class="active"><a data-target="#red5" data-toggle="tab">Red5</a></li>
  <li><a data-target="#ams" data-toggle="tab">Adobe Media Server</a></li>
  <li><a data-target="#wowza" data-toggle="tab">Wowza</a></li>
</ul>

<div class="tab-content">
  <div class="tab-pane active" id="red5">Red5</div>
  <div class="tab-pane" id="ams">AMS</div>
  <div class="tab-pane" id="wowza">Wowza</div>
</div>

<script>
jQuery(function () {
    jQuery('#serversTab a:last').tab('show')
})
</script>
