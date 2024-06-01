# JellySkin

### over engineered css theme for Jellyfin
  
![npm (tag)](https://img.shields.io/npm/v/jellyskin/latest?style=for-the-badge) ![jsDelivr hits (npm)](https://img.shields.io/jsdelivr/npm/hm/jellyskin?label=Downloads&style=for-the-badge) ![GitHub](https://img.shields.io/github/license/prayag17/JellySkin?style=for-the-badge)\
![GitHub Repo stars](https://img.shields.io/github/stars/prayag17/JellySkin?style=social)

# ℹ️ Usage

> [!IMPORTANT]
> JellySkin requires Chrome (105 and above), Edge (105 and above), Safari (15.4 and above), Firefox (121 and above), Opera (91 and above) and any other Browser supporting Baseline 23 css features to work properly

- To use the JellySkin theme copy the line below into "Dashboard -> General -> Custom CSS" and click save, it will apply immediately server-wide to all users on top of any theme they may be using. To remove the theme, clear the "Custom CSS" field and then click save. <b>NOTE: Theme may not work when using Nginx Reverse Proxy. Scroll down below to learn how to fix this.

  ```css
  @import url("https://cdn.jsdelivr.net/npm/jellyskin@latest/dist/main.css");
  ```

- To enable Logos add this to custom css:

  ```css
  @import url("https://cdn.jsdelivr.net/npm/jellyskin@latest/dist/logo.css");
  ```
  
- You can also use Jellyfin-Skin-Manager-Plugin : <https://github.com/danieladov/jellyfin-plugin-skin-manager>
  > [!CAUTION]
  > Jellyfin Skin Manager is not being actively maintained and might not load latest css themes

# 🧩 Addons

- ## Improve Performance

- ### Remove BackdropFilter

  This removes the frosted glass like effect from every place and improves performance

      ```css
      @import url("https://cdn.jsdelivr.net/npm/jellyskin@latest/dist/addons/improvePerformance/removeBackdropFilter.css");
      ```

- ### Remove scroll fade

  This removes the gradient faded bar at top of a scrollable container

      ```css
      @import url("https://cdn.jsdelivr.net/npm/jellyskin@latest/dist/addons/improvePerformance/removeFadingScroll.css");
      ```

- ## Horizontal My Media

    Brings back the horizontal section for My Media

    ```css
    @import url("https://cdn.jsdelivr.net/npm/jellyskin@latest/dist/addons/horizontalMyMedia.css");
    ```

- ## Using/Changing default gradient accent

    If you want want to change the default jellyfin gradient accent to some other preset gradient use:
    > **Note** : Remember to put gradient css files below the main.css file import. Also this won't affect the login mesh background's colors.
    >
    - ### Mauve

      ```css
      @import url("https://cdn.jsdelivr.net/npm/jellyskin@latest/dist/addons/gradients/mauve.css");
      ```

      Example:\
      ![image](https://user-images.githubusercontent.com/55829513/200132732-d188392a-5642-47f7-bb62-f204a85d992e.png)

  - ### NightSky

      ```css
      @import url("https://cdn.jsdelivr.net/npm/jellyskin@latest/dist/addons/gradients/nightSky.css");
      ```

      Example:\
      ![image](https://user-images.githubusercontent.com/55829513/200132808-5b02c8e9-29c1-4a6b-ad3c-514588cf717a.png)

  - ### Sea

      ```css
      @import url("https://cdn.jsdelivr.net/npm/jellyskin@latest/dist/addons/gradients/sea.css");
      ```

      Example:\
      ![image](https://user-images.githubusercontent.com/55829513/200132840-984deaf3-c228-4092-be8f-44c325d57782.png)

  - ### Custom

      If you need to add your own gradient use:

      ```css
      :root {
        --accent1-light: YOUR ACCENT COLOR 1(LIGHTER SHADE);
        --accent1-dark: YOUR ACCENT COLOR 1(DARKER SHADE);
        --accent1-light-opacity1: YOUR ACCENT COLOR 1(WITH OPACITY 0.4);
        --accent2-light: YOUR ACCENT COLOR 2(LIGHTER SHADE);
        --accent2-dark: YOUR ACCENT COLOR 2(DARKER SHADE);
      }
      ```

# 💻 Screenshots

- ### Login Page
    ![Login_Page](https://github.com/prayag17/JellySkin/assets/55829513/9ca0d0c2-9ada-4e41-93b9-e4281be20d1d)
  
- ### Home Screen
    ![Home page](https://github.com/prayag17/JellySkin/assets/55829513/075d844b-ca43-4f61-b54a-cb75110e77ed)

- ### Library
    ![Library](https://github.com/prayag17/JellySkin/assets/55829513/c3ef8e48-df17-44f0-9708-e10dfa448237)
  
- ### Title Screen
    ![Title page](https://github.com/prayag17/JellySkin/assets/55829513/270bb0bb-a755-449d-a57d-9da4e31d6082)

- ### Episodes List
    ![Episodes](https://github.com/prayag17/JellySkin/assets/55829513/eaded068-5930-47fd-b5d0-03cf89e1da44)

# ❓ Common Problem Fixes

- ### Unable to see blured background in Firefox

  Deaktiviert From version 70: this feature is behind the `layout.css.backdrop-filter.enabled` preference (needs to be set to true) and the `gfx.webrender.all`  preference (needs to be set to true).
  To change preferences in Firefox, visit about:config
  
- ### Logos are not visible even with `logo.css`

  - Get Fanart Plugin, Dashboard -> Plugin -> Catalog
  - Enable Fanart as a metadata provider for your libraries in the library settings, Dashboard -> Library -> Click on 3 dots on your Library -> Manage Library -> Scroll to find Metadata provider and enable Fanart in all of them.
  - Rescan your drive and also enable `Replace Metadata` and scan

- ### Background not visible

  - Go to Settings -> Display -> and enable `Backdrops` option

- ### Fix for Nginx Reverse Proxy

  When using the Nginx Reverse proxy config from the <a href="https://jellyfin.org/docs/general/networking/nginx.html">Jellyfin docs</a> the theme will probably not work by default. (If you are using the subpath config, you can ignore all this.)

  This config includes an CSP (Content Security Policy) with headers that don't allow for loading in external content that are not defined there.

  In the nginx config you should add the URLs of all the CSS files you've imported through the "Custom CSS" box.
  this:

  ```shell
  add_header Content-Security-Policy "default-src https: data: blob: http://image.tmdb.org; style-src 'self' 'unsafe-inline'; script-src 'self' 'unsafe-inline' https://www.gstatic.com/cv/js/sender/v1/cast_sender.js https://www.youtube.com blob:; worker-src 'self' blob:; connect-src 'self'; object-src 'none'; frame-ancestors 'self'";
  ```

  becomes (with only adding the default style):

  ```shell
  add_header Content-Security-Policy "default-src https: data: blob: http://image.tmdb.org; style-src 'self' 'unsafe-inline' https://cdn.jsdelivr.net/npm/jellyskin@latest/dist/main.css; script-src 'self' 'unsafe-inline' https://www.gstatic.com/cv/js/sender/v1/cast_sender.js https://www.youtube.com blob:; worker-src 'self' blob:; connect-src 'self'; object-src 'none'; frame-ancestors 'self'";
  ```

  If you don't do this the theme will simply not load (reverts back to default theme) and the browser console will spit out an error. Even if you paste in all the CSS, the font will still not load since it is loaded from a disallowed external source.

- ### How to report a Bug or request a Feature?

  - Go to <https://github.com/prayag17/JellySkin/issues>
  - Click on `New Issue` button
  - Select the appropriate template

- ### How to contribute

  - Fork this repository.
  - Add your patch/feature
  - Create a pull request and thats it
