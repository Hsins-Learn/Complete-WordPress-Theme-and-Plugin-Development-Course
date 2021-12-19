# Child Themes and Starter Themes

- [Overview](#overview)
- [Child Themes](#child-themes)
  - [Child Theme Architecture](#child-theme-architecture)
  - [Create the Child Theme Using Code](#create-the-child-theme-using-code)
- [Starter Themes](#starter-themes)
  - [Starter Theme Basic](#starter-theme-basic)
  - [Specific Start Themes](#specific-start-themes)

## Overview

- A **Child Theme** allows us to override another theme (parent theme) without making direct changes that are lost during updates.
- A **Starter Theme** includes helpful files and functions for building themes from scratch. We usually edit starter themes directly, not using child themes.

<br/>
<div align="right">
  <b><a href="#child-themes-and-starter-themes">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Child Themes

### Child Theme Architecture

WordPress looks to see if files exist in child themes before it looks in the parent theme. A **Child Theme** contains a few important things:

1. Reference to parent theme in `style.css` file.
2. Include parent style in `functions.php` file.
3. Copies of any templates from parent theme we want to modified.

So the **Parent Theme** keeps all the original files unedited. We can updated without affecting code in Child Theme.

### Create the Child Theme Using Code

1. Open `/wp-content/themes/` in the WordPress installation folder.
2. Create a new folder for the child theme. (We can named this folder anything we want.)
3. Create `style.css` file.

    ```css
    /*
      Theme Name:   Custom Child
      Theme URI:    https://www.example.com/
      Description:  Custom Child Theme
      Author:       Hsins
      Author URI:   https://www.github.com/Hsins
      Template:     twentytwentyone
      Version:      1.0.0
      License:      GNU General Public License v2 or later
      License URI:  http://www.gnu.org/licenses/gpl-2.0.html
      Text Domain:  customchild
    */
    ```

4. Create `functions.php`.

    ```php
    /* enqueue scripts and style from parent theme */
    function template_child_theme_enqueue_styles() {
      wp_enqueue_style( 'parent-style', get_template_directory_uri() . '/style.css');
      wp_enqueue_style( 'child-style', get_stylesheet_directory_uri() . '/style.css', array( 'parent-style' ) );
    }
    add_action( 'wp_enqueue_scripts', 'template_child_theme_enqueue_styles');
    ```

<br/>
<div align="right">
  <b><a href="#child-themes-and-starter-themes">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Starter Themes

### Starter Theme Basic

A **Starter Theme** is a theme that is used to build other theme from scratch.

- Inlcude common theme templates files.
- No CSS styles (but some include Bootstrap / Foundation).
- Extra functionality in `functions.php`.
- Extra hooks in template files.
- Follow modular file architecture.
- Some include workflow tools.
- Usually edited directly, not via child themes.

### Specific Start Themes

There're a few specific WordPress start themes:

1. [Underscore](http://underscores.me/) (WP Core Team)
2. [JointsWP](http://jointswp.com/) (Foundation)
3. [Understrap](https://understrap.com/) (Bootstrap)
4. [Sage](https://roots.io/sage/) (Roots Framework)

<br/>
<div align="right">
  <b><a href="#child-themes-and-starter-themes">[ ↥ Back To Top ]</a></b>
</div>
<br/>