
<h2 id="troubleshooting-connection-issues">Connection issues</h2>

You may experience one of the following connection issues.

Here we will explain what they mean and what can be done to solve them.

> If when trying to connect using AVChat 3, you are getting this error message:

    Connection failed, media server might be down or firewall might be blocking the connection!

You need to check:     

* Your RTMP connection string and make sure it is correct
* The media server might not be running (you can check if Red5 is running by going to http://yourred5server.com:5080/ or on Wowza http://yourwowzaserver.com:1935)
* The media server might have not started properly (thus is not running, you can check the logs for any error messages during startup)
* There is a firewall on the media server blocking TCP traffic over the specific ports: 1935 and 5080
* The user trying to connect is behind a firewall that blocks the connection (either a personal one installed on his computer or a corporate one installed on his network, to test his connection capabilities he should run these connection tests: [http://www.flashcomguru.com/apps/port_test/index.cfm](http://www.flashcomguru.com/apps/port_test/index.cfm) )

> If when trying to connect using AVChat 3, you are getting this error message:

    Connection Rejected:No scope ”avchat30/_definst_” on this server OR The connection with the video chat server could not be made

It means you are using Red5 and your Red5  is running but:

* make sure you installed the AVChat 3 Red5 server files properly (Red5/webapps/avchat30)
* make sure you restart Red5 after you installed the Red5 server side files (Red5/webapps/avchat30)

> If when trying to connect using AVChat 3, you are getting this error message:

    Connection Rejected: [Server.Reject]: (_defaultRoot_,_defaultVHost_): Application (avchat30) is not defined

There are 2 causes/solutions for this error:

* You are using AMS/FMS and you have not created the AMS/FMS server side avchat30 app `AMS/applications/avchat30`, follow the [installation instructions](http://docs.avchat.net/standalone#standalone-installation-instructions) and try again.
* If the avchat30 app folder is installed properly restart the AMS/FMS server (or just the vHost through the FMS Management Console)

> If when trying to connect using AVChat 3, you are getting this error message:

    Connection success, waiting for server…

There is 1 possible cause/solution for this issue:

The `avchat30` application folder was not installed properly on the media server (it does not contain the proper files). Make sure you follow the [installation instructions](http://docs.avchat.net/standalone#standalone-installation-instructions) for the `avchat30` app folder exactly.


<h2 id="troubleshooting-video-quality-issues">Video quality issues</h2>

**On the publisher side**

**Problem: Low framerate**

Solutions:

1. Increase the light in the room, natural light works best.
2. Get a better web cam, good web cams capture a lot of frames with little light in the room.
3. [Lower the picture resolution](http://docs.avchat.net/standalone#editing-existing-quality-profiles) requested by AVChat 3, some web cams just can’t capture 30fps at higher resolutions.
4. Increase the movement in the shot, if there’s no movement Flash Player will not capture many frames/second because there’s no movement.

**Problem: Video stream does not use entire allocated bandwidth**

Solutions:

1. Increase the light in the room, natural light works best. More light helps the web cam capture more details!
2. Get a better web cam, good web cams capture a lot of detail with little light in the room. DV cams for example capture huge amounts of data compared to normal web cams.
Check your connection to the media server. When you’re publishing video you’re  uploading data to the media server. Even tough you might have a 20Mbits/s or higher Internet connection, that’s most probably your download rate, your actual upload rate could be much less. If you’ve [configured the video chat to use as much as 768kbits/s per stream](http://docs.avchat.net/standalone#audio-video-quality), this ammount of video data will not fit in real time through your 350kbits/s upload pipe.

**Problem: dark image or noisy image**

Solutions:

1. Increase the light in the room, natural light works best.
2. Get a better webcam.

**Problem: no image at all or blank image**

Solutions:

1. Make sure your web cam is not already used by another app.
2. Make sure the proper web cam is used by Flash Player (Right click -> Settings -> Web Cam tab -> Select the web cam you want to use from the drop down list)
3. Make sure the browser was allowed to have access to your webcam. A pop up dialog shows up on most modern browsers asking you if you wish to allow access to your camera and microphone.


<h2 id="ensuring-high-connection-success-rate">Ensuring high connection success rate</h2>

**Why a connection attempt to a working media server might fail**

Red5, AMS/FMS and Wowza by default only accept RTMP connections over port 1935. This will work fine for most home Internet connections however when your user is behind a corporate firewall/network he might hit 2 major restrictions:

1. NO traffic/connections to non standard ports like `1935` (default port for RTMP). Traffic is only allowed to standard ports like `80` (HTTP) and `443` (HTTPS) . The solution for this is to configure the media server to accept  RTMP connections over ports `443` and `80` .
2. NO non-http traffic allowed (or a proxy server is used). The solution for this is to configure the media server to accept  RTMPT connections. RTMPT is RTMP wrapped as HTTP and its slower. It also adds some overhead/consumes more bandwidth because each RTMP packet needs to be wrapped as HTTP. According to a 2004 Adobe article, only 4% of Internet users are behind such a network.

**The automatic connection sequence in Flash Player:**

By default, when a Flash Player app (AVChat 3 for example) tries to connect to a media server (Red5, AMS/FMS or Wowza), it automatically tries to establish a connection by using the following sequence of ports and protocols:

1. `rtmp://myserver:1935/avchat30/_definst_`
2. `rtmp://myserver:443/avchat30/_definst_`
3. `rtmp://myserver:80/avchat30/_definst_`
4. `rtmpt://myserver:80/avchat30/_definst_`

This connection sequence can enable connections to succeed that otherwise would not. This automatic retry sequence occurs only if the initial connection specifies the RTMP protocol and does not specify a port – for example `rtmp://myserver/avchat30/_definst_`. During this connection sequence, users may wait several seconds for multiple connection attempts to time out.

<div class="alert alert-info" role="alert">However for the above connection sequence to actually produce more successful connection attempts, the media server must also be properly configured to listen for RTMP connections over ports 1935, 443 and 80 and for RTMPT connections over port 80.</div>

**Configuring your media server for best connection success rate**

<div class="alert alert-warning" role="alert">Before making the below changes make sure there is no other program listening on port 80 or 443 on your media server. These ports are surely already used by Apache. Use the netstat -ant command on linux to see which ports are already used.  AMS/FMS, Red5 and Wowza use port 1935 by default for a reason.</div>

> If you’re using AMS/FMS:

* Solution for restriction 1: configure it to listen for RTMp connections over ports `1935`, `443` and `80`. You need to edit `conf/fms.ini`, set `ADAPTOR.HOSTPORT = :1935,443,80` and restart `AMS/FMS`. Make sure you don’t have other apps (like the Apache web server) started and listening on `80` or `443`.
* Solution for restriction 2:  same as above, AMS/FMS can listen for both RTMP and RTMPT connections over the same ports at the same time

Most AMS/FMS hosting services (like [influxis.com](http://influxis.com/)) are already configured like this  out of the box.

> If you’re using  Wowza:

* solution for restriction 1: make it listen for RTMP connections over ports `1935`, `443` and `80`. You need to edit `conf/VHost.xml` , set `<Port>1935,443,80</Port>` and restart Wowza. Make sure you don’t have other apps (like the Apache web server) started and listening on `80` or `443`.
* Solution for restriction 2: same as above, Wowza can listen for both RTMP and RTMPT connections over the same ports at the same time

> If you’re using Red5:

* Solution for restriction 1: bind RTMP connections to port `443` instead of `1935` (Red5 can listen for RTMP connections over several simultaneous ports like Wowza and AMS/FMS can). You need to edit `conf/red5.properties`, set `rtmp.port=443` and restart Red5. Make sure you don’t have other apps (like the Apache web server) started and listening on `443` . You can also use port `80` but we will use that for listening for RTMPT connections as explained below.
* Solution for restriction 2: bind RTMPT connections to port `80`. You need to edit `conf/red5.properties`, set `rtmpt.port=80` and restart Red5. Make sure you don’t have other apps (like the Apache web server) started and listening on `80`.

**How you can check your connection**

[Here](http://www.flashcomguru.com/apps/port_test/index.cfm) you will find 2 port testers which will attempt to establish RTMP and RTMPT connections (using all ports) to a properly configured media server. Red5 ships with a similar tool.
