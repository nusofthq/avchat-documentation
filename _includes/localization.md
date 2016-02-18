
<h2 id="changing-welcome-message">Changing the welcome message</h2>

**Edit the welcome message for the desktop version in 5 steps:**

Quick painless way to change the welcome message that shows up in the first room you enter in AVChat:

1. Edit this XML file on your web server AVChat installation folder: `translations/en.xml`
2. Go to line 416, you will see the welcome message on that line
3. Change it to whatever you want
4. Save and upload the `en.xml` file back to your web server/site
5. Reload AVChat in the browser (if the old message still shows up refresh a few times or clear your browser cache)

<img src="http://docs.avchat.net/assets/images/welcome_message.png" class="img-responsive"/>

<h2 id="translating-avchat">Translating AVChat</h2>


AVChat loads the words and phrases used in the admin and user interface from external XML files. You will find these XML files in the translations folder. AVChat by default ships only with the English translation: `translations/en.xml`.

`en.xml` is a plain XML file that can be edited with any text editor.

In order to change a word, to translate the entire interface in another language or to change the initial welcome message you just need to edit these files and change whatever you need.

The `languagefile` variable in `avc_settings.xml` controls which language file will be loaded. You can have several language files (en.xml, es.xml, fr.xml, etc.) and load one or another based on the user's location, ip or language settings in the browser (this is not a feature built in AVChat but it's something that's possible).

<div class="alert alert-info" role="alert" markdown="1">After editing the `en.xml` file and uploading it back to your web server, make sure you clear your cache so that the browser picks up the new version.</div>

Where to find and share translations?

There's a special area in our AVChat forum dedicated to exchanging language files: [http://discuss.avchat.net/c/translation-files](http://discuss.avchat.net/c/translation-files). You need to sign up as a user to access the existing uploaded language files.


<h2 id="switching-to-rtl">Switching to RTL</h2>

Switching to RTL is very simple.

Just edit `avc_settings.xml` and change the value of the `rightToLeft` variable to `1`. This will cause all text fields, including the text chat area to become right aligned and part of the UI to be arranged from right to left.
