<div align="center">
<h1>JellySkin</h1><h3>Use 67% or 70% zoom in web browser for better experience</h3>
<h4>Note: To take full experience of this CSS on FireFox scroll down below to find the necessary settings.</h4>
</div>
<br>
<h3>How to use</h3>
To use the JellySkin theme copy the line below into "Dashboard -> General -> Custom CSS" and click save, it will apply immediately server-wide to all users on top of any theme they may be using. To remove the theme, clear the "Custom CSS" field and then click save. <b>NOTE: Theme may not work when using Nginx Reverse Proxy. Scroll down below to learn how to fix this.

```css
@import url("https://prayag17.github.io/JellySkin/default.css");
```
To use Logos like the images given below use:

```css
@import url("https://prayag17.github.io/JellySkin/addons/Logo.css");
```
  
<h3> You can also use Jellyfin-Skin-Manager-Plugin : https://github.com/danieladov/jellyfin-plugin-skin-manager
<br>

<h3>Fix Performance</h3>
In JellySkin 11 I have added a transparency gradient like CTalvio's Themes and just like his skin's have a performance issue on some older devices because of this I have created that remove all the transparency gradient in the skin.
  
```css
@import url("https://prayag17.github.io/JellySkin/addons/imp-per.css");
```

<br>

<h3>Background Fix:</h3>
Many of you are facing issues that backdrop is not visible by default....this is not a JellySkin issue but rather Jellfin issue, in Jellyfin Version 10.7.X backgrounds are disabled by defualt but you can enable them individually on you devices/client by going to: 
SETTINGS --> DISPLAY --> ENABLE BACKDROPS/BACKGROUND.

<br>
<h3>If you want to display your posters to be compact use the following line with default css</h3>

```css
@import url("https://prayag17.github.io/JellySkin/addons/compact-poster.css");
```

To use different gradient for your buttons I have added few different gradients you can choose or you can create your own (check the steps given bellow), the default gradient used is jellyfin's default logo gradient,using this alone will only skin the button colors and I know the names for this are very funny:
```css
@import url("https://prayag17.github.io/JellySkin/addons/Gradients/seaGradient.css");
@import url("https://prayag17.github.io/JellySkin/addons/Gradients/sunsetGradient.css");
@import url("https://prayag17.github.io/JellySkin/addons/Gradients/mauveGradient.css");
@import url("https://prayag17.github.io/JellySkin/addons/Gradients/nightSkyGradient.css");
```
<br>
Using custom own Gradient or color
Create your gradient or solid color and past it in <code>--accent</code> and gradient in opposite angle in <code>--accent-selected</code> :
  
```css
:root {
  --accent: your gradient;
  --accent-selected: your gradient in opposite angle;
}
```
  
Now, to use your own Gradient (to get great button or any gradient go to https://cssgradient.io/gradient-backgrounds or https://cssgradient.io) or solid color:
  
```css
:root {
  --accent: your gradient;
  --accent-selected: your gradient in opposite angle;
}
```
  
<br>
<h3>Don't like the progress bar</h3>
Add the follwing line to custom CSS with the default css file-

```css
@import url("https://prayag17.github.io/JellySkin/addons/progress-bar.css");
```

<h3>Here are some images:</h3>

<h5>Login Page</h5>
<img src="https://prayag17.github.io/JellySkin/img/login.jpg">

<h5>Home screen:</h5>
<img src="https://prayag17.github.io/JellySkin/img/Home.jpg">

<h5>Library View</h5>
<img src="https://prayag17.github.io/JellySkin/img/Movies.jpg">
<img src="https://prayag17.github.io/JellySkin/img/TV%20Shows.jpg">
<img src="https://prayag17.github.io/JellySkin/img/Collections.jpg">

<h5>Title screen:</h5>
<img src="https://prayag17.github.io/JellySkin/img/Title%20Page-Movie.jpg">
<img src="https://prayag17.github.io/JellySkin/img/Title%20Page-TV.jpg">

<h5>TV Shows Season Episode list:</h5>
<img src="https://prayag17.github.io/JellySkin/img/Ep-list.jpg">

<h5>Settings</h5>
<img src="https://prayag17.github.io/JellySkin/img/Settings.jpg">

<h5>Dashboard</h5>
<img src="https://prayag17.github.io/JellySkin/img/Dashboard.jpg">

<h5>Plugins</h5>
<img src="https://prayag17.github.io/JellySkin/img/Plugins.jpg">


<h5>Dialogs</h5>
<img src="https://prayag17.github.io/JellySkin/img/Menu.jpg">
<img src="https://prayag17.github.io/JellySkin/img/Dialog-1.jpg">
<img src="https://prayag17.github.io/JellySkin/img/Dialog-2.jpg">
<img src="https://prayag17.github.io/JellySkin/img/Dialog-3.jpg">
<br>
<br>

<div class="firefox">
<h3>Enabling backdrop-filter in FireFox</h3>

<code style="display: block !important;">
Deaktiviert From version 70: this feature is behind the
layout.css.backdrop-filter.enabled
preference (needs to be set to
  true
  ) and the
  gfx.webrender.all
  preference (needs to be set to
    true
    ).
 To change preferences in Firefox, visit about:config.
</code>

</div>


<div class="nginx-reverseproxy">
<h3>Using Nginx Reverse Proxy</h3>
  When using the Nginx Reverse proxy config from the <a href="https://jellyfin.org/docs/general/networking/nginx.html">Jellyfin docs</a> the theme will probably not work by default. (If you are using the subpath config, you can ignore all this.)

This config includes an CSP (Content Security Policy) with headers that don't allow for loading in external content that are not defined there.

In the nginx config you should add the URLs of all the CSS files you've imported through the "Custom CSS" box.
this:

```
add_header Content-Security-Policy "default-src https: data: blob: http://image.tmdb.org; style-src 'self' 'unsafe-inline'; script-src 'self' 'unsafe-inline' https://www.gstatic.com/cv/js/sender/v1/cast_sender.js https://www.youtube.com blob:; worker-src 'self' blob:; connect-src 'self'; object-src 'none'; frame-ancestors 'self'";
```
becomes (with only adding the default style):

```
add_header Content-Security-Policy "default-src https: data: blob: http://image.tmdb.org; style-src 'self' 'unsafe-inline' https://prayag17.github.io/JellySkin/default.css; script-src 'self' 'unsafe-inline' https://www.gstatic.com/cv/js/sender/v1/cast_sender.js https://www.youtube.com blob:; worker-src 'self' blob:; connect-src 'self'; object-src 'none'; frame-ancestors 'self'";
```

If you don't do this the theme will simply not load (reverts back to default theme) and the browser console will spit out an error. Even if you paste in all the CSS, the font will still not load since it is loaded from a disallowed external source.
  </div>

  <div class="logopull">
    <h2> How to get Logo </h2>
    <ul>
      <li>Get Fanart Plugin, Dashboard -> Plugin -> Catalog</li>
      <li>Enable Faart as a metadata provider for your libraries in the library settings, Dashboard -> Library -> Click on 3 dots on your Library -> Manage Library -> Scroll to find Metadata provider and enable Fanart in all of them.</li>
      <li>Rescan your drive by selecting <code>Replace Metadata</code> and scan</li>
      <li>Done!</li>
    </ul>
  </div>  

<div class="conribute" style="text-align: center;">
<h2> Wanna Contribute? </h2>
<ul>
<li>Fork this Repo</li>
<li>Add your features</li>
<li>Create a Pull Request</li>
<li>Wait for it to be merged.</li>
</ul>
</div>
<br>
<br>
