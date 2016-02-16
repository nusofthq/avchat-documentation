
<h2 id="changing-bg-color">Background color of AVChat</h2>

The background color of AVChat is defined in the HMTL web page that embeds the AVChat swf file. By default AVChat ships with 2 HTML pages: `index.html` (for the user interface, embeds `index.swf`) and admin.html (for the admin/moderator interface, embeds `admin.swf`).

In order to change the color of the user interface you will need to open `index.html` in a text editor and find the following lines:

```javascript
var params = {
quality : "high",
bgcolor : "#272727",
play : "true",
loop : "false",
allowFullScreen : "true"
};
```

Replace the default value `#272727` of `bgcolor` with your desired color.

*Hint: you can use a [color picker like this](http://www.colorpicker.com/)*

Save and upload the modified `index.html` to your web site.

The same procedure applies to `admin.html`.

<h2 id="changing-bg-image">Background image of AVChat</h2>

AVChat can display a image as it's background.

This image can be specified in the style.css file. The last build's default image is bg.jpg

**How to do it**

Open the `style.xml` file with a text editor (found inside your `themes` folder for AVChat 3.5 and up) and at the beginning, you'll see this paragraph:

```xml
<backgroundArea>
  <backgroundImageUrl>bg.jpg</backgroundImageUrl>
  <backgroundImageScale>stretch</backgroundImageScale>
  <backgroundImageAlpha>100</backgroundImageAlpha>
</backgroundArea>
```

Rename the `bg.jpg` with the name of your image uploaded on your AVChat installation folder.

You can also change the transparency of this background image by changing the value of the `backgroundImageAlpha` tag. The background color will be seen through a partially transparent background image.

The image will automatically tile to fit the size of the video chat software.

<h2 id="changing-sounds">Sounds used in AVChat</h2>

You can change the sounds used throughout AVChat with your own sounds.

AVChat right now uses six mp3 sounds which you can find in the sounds folder:

* alert.mp3 (used when a text chat message kicks in)
* private.mp3 (used when receiving private messages)
* videorequest.mp3 (used whena request to view your private stream comes in)
* buzz.mp3 (used when someone gives you a buzz)
* online.mp3 (used when someone joins a room)
* offline.mp3 (used when someone leaves a room)

**How to change them**: Just replace the existing mp3's with your own mp3's. Try to keep their size as small as possible because these sounds are loaded at runtime.

To disable the sounds just delete the mp3's.

<h2 id="changing-size">Changing the size of AVChat</h2>

You can change the size of the AVChat user/admin Interface to better fit with the design and size of your website.

The size of the AVChat user and admin interfaces is defined in the HMTL pages that embed these swf files. By default AVChat ships with 2 HTML pages: `index.html` (that embeds the user interface: `index.swf`) and `admin.html` ( that embeds the admin interface: `admin.swf`).

In order to change the size of the AVChat user interface for example, you will need to edit `index.html` with a text editor and and find the following line:

```javascript
swfobject.embedSWF("index.swf", "myContent", "100%", "100%", "10.3.0", "", flashvars, params, attributes);
```

and replace `"100%", "100%"` with your desired dimensions (first width, second height).

Save and upload the modified `index.html` to your web site, and refresh.

The same procedure applies to `admin.html`.

<h2 id="changing-window-looks">Customizing AVChat windows</h2>

The `style.xml` file controls (among other things) the looks of the windows inside AVChat. By editing `style.xml` you can change the following:

* the color of the windows
* if the windows have rounded corners or not (set to 0 for straight corners)
* the space between the windows
* the space between the margin of the windows and its content
* if the windows cast shadows
* the border color

Here is the actual tag for the controls with the default values:

```xml
<windows>
	<margin>4</margin>
	<padding>6</padding>
	<backgroundcolor>#FFFFFF</backgroundcolor>
	<cornerradius>4</cornerradius>
	<windowsCastShadows>false</windowsCastShadows>
	<borderColor>#E9E9E9</borderColor>
</windows>
```

<h2 id="changing-fonts">Fonts</h2>

The `style.xml` file controls (among other things) the fonts used throughout the video chat. By editing the `style.xml` file you can change for every group of fonts (like titles, side menu links, etc...):

* the font face (fontfamily:\_sans)
* the size of the font (fontsize:16)
* the font weight (fontweight:bold)
* the color of the text (color:#ffffff)

<h2 id="changing-gender-icons">Gender icons</h2>

Starting with [build 1880](http://nusofthq.com/blog/new-avchat-november-build-1880-has-arrived) the genders are imported from `genders.xml` along with attributes like icon image URL's.

Customizing genders:

1. Upload your new gender icons in the `gender_icons` folder located in your AVChat installation.
2. Open the `genders.xml` file and edit the lines, for example:

        <gender id="cat" label="Cheshire Cat" iconUrl="gender_icons/cheshire_cat_32.png" adminOnly="false" sortPriority="b" outlineColor ="0x577ce5" />

3. Rename the `id`, `label` and `iconUrl` corresponding to your new gender and it will become:

        <gender id="new_icon" label="New Icon" iconUrl="gender_icons/new_icon.png" adminOnly="false" sortPriority="b" outlineColor ="0x577ce5" />



Starting with [AVChat 3.5](http://avchat.net/blog/avchat-3-5-now-available-with-major-redesign-and-themes/) you can also specify the color to be used for the left line element that is drawn in the users list on mouse over the user item through the new `outlineColor` parameter.

<div class="alert alert-warning" role="alert">Do not change the ID's of the already defined  male, unknown, admin and hidden genders.</div>


<h2 id="changing-themes">Switching between themes</h2>

Starting with [version  3.5](http://avchat.net/blog/avchat-3-5-now-available-with-major-redesign-and-themes/) AVChat ships with 2 themes: `light` and `dark`. Both themes are located in the new `themes` folder located in your AVChat installation directory. The `light` theme is default. You can also make your own theme by simply creating a new folder inside the themes folder and putting a customized `style.xml` inside it.

To switch between themes, either the default ones or your custom created theme you need to take the following steps:

1. Open `style.php` or `style.aspx.cs` depending on the webserver you are running.
2. Edit the path to theme. By default it will look like this: `themes/light/style.xml`.
3. Change the name of the folder, in this case light to dark or your custom made folder name resulting in this: `themes/dark/style.xml`.
4. Save and exit.
5. Next we need to change the background color of the SWF file and this can only be done where it is embeded in the webpage, by default in `index.html` and `admin.html`.
6. Search for `bgcolor` parameter which by default will be `bgcolor : "#F1F1F1"`, and change to `#101622`color which is the corespondent dark theme color.
7. Save and exit.
