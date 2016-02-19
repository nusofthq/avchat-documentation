
<h2 id="changing-themes">Themes</h2>

Starting with [version  3.5](http://avchat.net/blog/avchat-3-5-now-available-with-major-redesign-and-themes/) AVChat ships with 2 themes: **light** and **dark**. Both themes are located in the new `themes` folder. The **light** theme is the default one.

You can make your own theme by simply creating a new folder inside the themes folder and putting a customized `style.xml` inside it.

### Switching between the default light and dark themes

To switch between themes, either the default ones or to your custom created theme, you need to take the following steps:

**Change theme**
1. Open `style.php` or `style.aspx.cs` depending on wether you run AVChat using PHP or ASPX
2. Edit the `$pathToTheme` var and change the theme folder in the path. By default it will look like this: `themes/light/style.xml`. If you want to switch to the dark theme it should look like this `themes/dark/style.xml`.
4. Save and exit.

**Change background color**
5. Next we need to change the background color and it can only be changed from the `index.html` and `admin.html` files.
6. Edit `index.html` and search for `bgcolor` JS parameter which by default will be `bgcolor : "#F1F1F1"`, and change the hex value to `#101622` which is the correct dark theme bacground color.
7. Save and exit. Do the same for `admin.html`.

See below for details.

<h2 id="changing-bg-color">Background color of AVChat</h2>

The background color of AVChat is defined in the HMTL web page that embeds the AVChat swf file. In case of the sandalone version of AVChat, it ships with 2 HTML pages:
* `index.html` for the user interface, embeds `index.swf`
* `admin.html` for the admin/moderator interface, embeds `admin.swf`

In order to change the color of the user interface you will need to open `index.html` in a text editor and find the following lines:

{% highlight js %}
var params = {
  quality : "high",
  bgcolor : "#272727",
  play : "true",
  loop : "false",
  allowFullScreen : "true"
};
{% endhighlight %}

Replace the default `bgcolor` value (`#272727`) with your desired color.

*Hint: Use a [color picker](http://www.colorpicker.com/) to find the perfect color.*

Save and upload the modified `index.html` to your web site. Do the same with `admin.html`.

<h2 id="changing-bg-image">Background image</h2>
<p class="lead">AVChat can display a .jpg/.png image or .swf animation as it's background.</p>

To add a background image open the `style.xml` file with a text editor (found inside your `themes` folder for AVChat 3.5 and up) and at the beginning, you'll see this xml code:

{% highlight xml %}
<backgroundArea>
  <backgroundImageUrl></backgroundImageUrl>
  <backgroundImageScale>stretch</backgroundImageScale>
  <backgroundImageAlpha>100</backgroundImageAlpha>
</backgroundArea>
{% endhighlight %}

Rename the `bg.jpg` with the name of your image uploaded on your AVChat installation folder.

<div class="bs-callout bs-callout-info" id="callout-tables-responsive-overflow"> <h4>Transparency</h4> <p markdown="1">You can also change the transparency of this background image by changing the value of the `backgroundImageAlpha` xml tag in the theme's `style.xml`. By default it's set to 100 (no transparency). If set to a lower value the background color will be visible through the transparent background image. 0 means fully transparent.
</p> </div>


The image will automatically tile to fit the size of the video chat software.

<h2 id="changing-sounds">Sounds used in AVChat</h2>

You can change the sounds used throughout AVChat with your own sounds. AVChat currently uses 6 `.mp3` sounds which you can find in the sounds folder:

* alert.mp3 (used when a text chat message kicks in)
* private.mp3 (used when receiving private messages)
* videorequest.mp3 (used whena request to view your private stream comes in)
* buzz.mp3 (used when someone gives you a buzz)
* online.mp3 (used when someone joins a room)
* offline.mp3 (used when someone leaves a room)

**How to change them**: Just replace the existing mp3's with your own mp3's. Try to keep their size as small as possible because these sounds are loaded at runtime.

To disable the sounds just delete the mp3's.

<h2 id="changing-size">Changing the size of AVChat</h2>

<p class="lead">You can change the size of the AVChat user and admin interfaces to better fit within your website pages.</p>

The size of the AVChat user and admin interfaces is defined in the HMTL pages that embed these `index.swf` and `admin.swf` files. By default AVChat ships with 2 HTML pages: `index.html` (that embeds the user interface `index.swf`) and `admin.html` ( that embeds the admin interface `admin.swf`).

In order to change the size of the AVChat user interface  you will need to edit `index.html` with a text editor and and find the following line:

{% highlight js %}
swfobject.embedSWF("index.swf", "myContent", "100%", "100%", "10.3.0", "", flashvars, params, attributes);
{% endhighlight %}

and replace `"100%", "100%"` with your desired dimensions (first width, second height). Save and upload the modified `index.html` to your web site, and refresh. Do the same to `admin.html`.

<h2 id="changing-window-looks">Customizing AVChat windows</h2>

The theme's `style.xml` file controls (among other things) the looks of the windows inside AVChat. By editing `style.xml` you can change the following:

* the color of the windows
* if the windows have rounded corners or not (set to 0 for straight corners)
* the space between the windows
* the space between the margin of the windows and its content
* if the windows cast shadows
* the border color

Here is the actual `windows` tag from `style.xml`:

{% highlight xml %}
<windows>
	<margin>4</margin>
	<padding>6</padding>
	<backgroundcolor>#FFFFFF</backgroundcolor>
	<cornerradius>4</cornerradius>
	<windowsCastShadows>false</windowsCastShadows>
	<borderColor>#E9E9E9</borderColor>
</windows>
{% endhighlight %}

<h2 id="changing-fonts">Fonts</h2>

The theme's `style.xml` file also controls the fonts used throughout the video chat. By editing the `style.xml` file you can change for every group of fonts (like titles, side menu links, etc...):

* the font face (fontfamily:\_sans)
* the size of the font (fontsize:16)
* the font weight (fontweight:bold)
* the color of the text (color:#ffffff)

<h2 id="changing-gender-icons">Gender icons</h2>

<p class="lead" markdown="1">Starting with [build 1880](http://nusofthq.com/blog/new-avchat-november-build-1880-has-arrived) AVChat supports any number of genders through the use of the new `genders.xml`.</p>

Customizing genders:

1. Upload your new gender icons to the `gender_icons` folder located in your AVChat installation.
2. Open the `genders.xml` file and edit the lines, for example:

{% highlight xml %}
<gender id="cat" label="Cheshire Cat" iconUrl="gender_icons/cheshire_cat_32.png" adminOnly="false" sortPriority="b" outlineColor ="0x577ce5" />
{% endhighlight %}

3. Rename the `id`, `label` and `iconUrl` corresponding to your new gender and it will become:

{% highlight xml %}
<gender id="polar_bear" label="Polar Bear" iconUrl="gender_icons/polar_bear.png" adminOnly="false" sortPriority="b" outlineColor ="0x577ce5" />
{% endhighlight %}


Starting with [AVChat 3.5](http://avchat.net/blog/avchat-3-5-now-available-with-major-redesign-and-themes/) you can also specify the color (through the new `outlineColor` parameter) to be used for the left line element that is drawn in the users list on mouse over the user item.

<div class="alert alert-warning" role="alert"><p markdown="1">Do not change the ID's of the already defined  *male*, *unknown*, *admin* and *hidden* genders.</p></div>
