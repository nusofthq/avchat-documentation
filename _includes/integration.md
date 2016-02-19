
<h2 id="passing-username-and-gender">Passing the user name and gender from your web site to AVChat (auto login)</h2>


The login screen in AVChat 3 shows up to ask the user for its username and gender. However if you provide these info’s via `integration.php` (or `integration.aspx.cs`) and block the user from modifying them the login screen is not needed anymore so it will be skipped.

So this is what you need to do in order to auto login users:

1. Set `$avconfig['username']` to the username of the person logged in the website (you can collect this info from cookies, sessions or from the database).
2. Set `$avconfig['gender']` to male or female ( the gender of the person logged in the website, you can collect this info from cookies, sessions or from the database). Starting with [build 1880](http://nusofthq.com/blog/new-avchat-november-build-1880-has-arrived) make sure the genders are the same with the id attribute from the `genders.xml` file.
3. Set `$avconfig['changegender']=0` which means the user will not be given the chance to change its gender
4. Set `$avconfig['changeuser']=0` which means the user will not be given the chance to change its username

If all the 4 steps above are completed, the login screen will be skipped and users will be logged in directly in the video chat without them being asked for a user name or gender (confrmation).

You can also use `$avconfig['disableGenderSelection']` to disable the gender selection altogether (everyone will get the unknown gender and will have no icon displayed).


<h2 id="drop-in-room">Automatically dropping users in a certain room with AVChat</h2>

By default, when a user joins AVChat 3 he is presented with a list of existing rooms. He can choose one and join it. You can however skip that and drop users directly into the room of your choice.

What you need to do is edit `avc_settings.xml` and change the value of the `dropInRoom` variable with the `id` of the room you want users to automatically be dropped in.

Below you see the setting configured (`<value>` tag) to drop in the room with id `r1`

{% highlight xml %}
<dropInRoom>
	<title>dropInRoom</title>
	<name>Drop in room</name>
	<type>string</type>
	<desc>Use the interface administration window to see what ids each room has, then come back here and paste that id here. If left empty the rooms list window will be shown automatically after login. Example value for single id: r0. Example value for multiple room ids: [r0,r1,r2]</desc>
	<examples>any room id shown in the roms panel in the admin area of AVChat (admin.swf) </examples>
	<default></default>
	<value>r1</value>
</dropInRoom>
{% endhighlight %}

Starting with [build 1880](http://nusofthq.com/blog/new-avchat-november-build-1880-has-arrived) the `dropInRoom` variable also supports an array of id's so that the users will automatically join multiple rooms.

Example notice the `<value>`;

{% highlight xml %}
<dropInRoom>
	<title>dropInRoom</title>
	<name>Drop in room</name>
	<type>string</type>
	<desc>Use the interface administration window to see what ids each room has, then come back here and paste that id here. If left empty the rooms list window will be shown automatically after login. Example value for single id: r0. Example value for multiple room ids: [r0,r1,r2]</desc>
	<examples>any room id shown in the roms panel in the admin area of AVChat (admin.swf) </examples>
	<default></default>
	<value>[r1,r2,r3]</value>
</dropInRoom>
{% endhighlight %}

Every room in AVChat 3 has a unique `id`. When you log in the AVChat through the admin interface (`admin.swf`) the leftmost column in the rooms list shows the id of each room:

<img src="http://docs.avchat.net/assets/images/rooms_list.jpg" class="img-responsive"/>


<h2 id="integration-guide">General integration guide</h2>


This is not a step by step guide because user management systems are different from a web site to another and from a CMS to another.

By integrating AVChat with your users database we understand that the users of your web site will have to login only once (through he normal login process on your web site) and have the same user name on the web site and in the video chat. Furthermore if your web site allows for several user levels (like guests, free members & premium members) you can impose restrictions one some user levels in order to incentivise them to purchase a paid plan.

**How AVChat loads username/gender/enabled features information**

When a user visits your web site and reaches the HMTL page with AVChat embedded in it, the HTML file and the the AVChat Flash .swf file are downloaded to the users computer and displayed in their browser.

Then `avc_settings.xxx` (PHP or .NET depending on your webserver) is executed on the web server and returns a string containing many variable/value pairs that are used by the `.swf` file. There's one variable for the username, one for the background image, etc. .

You can see an example of what is returned by executing our `avc_settings.php` file (from our online demo) in the browser: [http://avchat.net/demos/avchat30/avc_settings.php](http://avchat.net/demos/avchat30/avc_settings.php).

All the variables accepted and used by the `.swf` file are listed and explained in the `avc_settings.xml` file.

If we were to talk about it in a timely manner, the integration will take place when the `avc_settings.xxx` file executes on the web server.

**Deep in the problem**

Once a person is logged in on your web site, the user management system will remember (using a cookie, or a session variable) the persons id, username, real name, email, gender and other details. Once the user logs out, the user management system "forgets" him (the cookie saved in the users browser is deleted, session variables are also deleted from the web server).

You need to look through the existing code and analize how the existing management system remembers the person logged in. Either COOKIES or SESSIONS are used. If you have never learned about these before, this is a good time to do it! :)

Cookies are little bits of information that are stored by your browser and sent with every call to the web site. Session variables are little bits of information that are stored by the web server individually for each visitor of your website.

**Username and gender are automatically recognized**

When the `avc_settings.xxx` file is executed, it should check for existing cookies (sent by the users browser) or session variables (saved on the web server for that specific user), and should populate the `username` and `gender` variables with the correct values for that user.

The variable for the `username` inside the PHP configuration file is `$avconfig['username']`. The variable for the gender inside the PHP configuration file is `$avconfig[gender]`.

**Different settings for different user groups**

If your web site allows for different levels of membership you can impose restrictions on some of them.

AVChat obeys to whatever values the `avc_settings.xxx` file returns so you can configure it to return a special set of variables/values when a guest user is executing it (detection based on COOKIES or SESSIONS) and another set of variables/values when a paying user executes it.

Every variable in the `avc_settings.xxx` file can be configured according to the level of the user.

**Here are a few ideas of what you can do**

* Allow "gold" users to send higher quality video and audio by pointing the value of `miccamsettingsurl` to a XML file with better quality settings
* Integrate will all the [Pay Per View](http://docs.avchat.net/standalone#pay-per-view-api) settings
* Allow "gold" users to see more web cams at a time by modifying the value of `maxcams` when the logged in user is detected as "gold"
* Drop "gold" users in selected rooms, while "free" users gather only in the lobby by modifying the value of `dropInRoom` according to the level of the user
* Prevent "free" users from creating rooms or initializing private chat or making their video streams private

**Further notes**

* You might want to block the user from changing the username and gender detected by `the avc_settings.xxx` file in the login screen of the AVChat user interface: to do this set the value of `changeuser` and `changegender` to `0`.
* When both `changeuser` and `changegender` are set to `0` in the .NET/PHP intergration file, AVChat will skip the login screen of the user/admin interfaces and jump directly to the chat area.
* You can test the integration by logging in, loading the `avc_settings.xxx` file directly in the browser, and checking the variable/value pairs it returns. This way you can also check for any syntax errors that might have slipped in while editing the file.
* We also provide integration services for a certain fee: [http://avchat.net/buy-now#services](http://avchat.net/buy-now#services)
* If you are in need of a good text editor we recommend [Atom]https://atom.io/
* A good introduction on PHP (including Sessions and Cookie variables) can be found here: [http://www.w3schools.com/php/default.asp](http://www.w3schools.com/php/default.asp)
* A good introduction on .NET (including Sessions and Cookie variables) can be found here:[http://www.w3schools.com/aspnet/aspnet_pages.asp](http://www.w3schools.com/aspnet/aspnet_pages.asp)


<h2 id="placing-ads-around-the-videochat">Placing ads around the video chat</h2>


Placing ads around the video chat is simple. The video chat itself is actually a Flash .swf file embedded in a HTML file. In that HTML file you can place anything: links, images, AdWords ads, banners, etc. .

The default HTML file embedding the `index.swf` file (main video chat file) is: `index.html` so to add ads around your video chat:

1. Connect to your web site using FTP
2. Edit `index.html` with a text editor
3. Place your ad code in it
4. Save and upload back to web server

A little bit of HTML knowledge might be required tough to properly place the ads above, below or to the sides of the video chat.
