
<h2 id="changing-bg-color">Background color of AVChat</h2>

The background color of AVChat is defined in the HMTL web page that embeds the AVChat swf file. By default AVChat ships with 2 HTML pages: `index.html` (for the user interface, embeds `index.swf`) and admin.html (for the admin/moderator interface, embeds `admin.swf`).

1. In order to change the color of the user interface you will need to open `index.html` in a text editor and find the following lines:
```javascript
var params = {
quality : "high",
bgcolor : "#272727",
play : "true",
loop : "false",
allowFullScreen : "true"
};
```
2. Replace the default value `#272727` of `bgcolor` with your desired color.

*Hint: you can use a [color picker like this](http://www.colorpicker.com/)*

Save and upload the modified `index.html` to your web site.

The same procedure applies to `admin.html`.

<h2 id="changing-bg-image">Background image of AVChat</h2>

<h2 id="changing-sounds">Sounds used in AVChat</h2>

<h2 id="changing-size">Changing the size of AVChat</h2>

<h2 id="changing-window-looks">Customizing AVChat windows</h2>

<h2 id="changing-fonts">Fonts</h2>

<h2 id="changing-gender-icons">Gender icons</h2>

<h2 id="changing-themes">Switching between themes</h2>
