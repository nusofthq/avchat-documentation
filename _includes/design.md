
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

Rename the bg.jpg with the name of your image uploaded on your AVChat installation folder.

You can also change the transparency of this background image by changing the value of the backgroundImageAlpha variable. The background color will be seen trough a partially transparent background image!

The image will automatically tile to fit the size of the video chat software.

<h2 id="changing-sounds">Sounds used in AVChat</h2>

<h2 id="changing-size">Changing the size of AVChat</h2>

<h2 id="changing-window-looks">Customizing AVChat windows</h2>

<h2 id="changing-fonts">Fonts</h2>

<h2 id="changing-gender-icons">Gender icons</h2>

<h2 id="changing-themes">Switching between themes</h2>
