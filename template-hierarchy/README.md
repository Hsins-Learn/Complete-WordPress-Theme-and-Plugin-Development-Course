# Template Hierarchy

- [Overview](#overview)
- [Setup the Theme Content and Files](#setup-the-theme-content-and-files)
- [Work with `style.css` File](#work-with-stylecss-file)
- [Work with `functions.php` File](#work-with-functionsphp-file)
- [Work with `index.php` File](#work-with-indexphp-file)
- [Work with Header and Footer](#work-with-header-and-footer)
- [Adding Menus and Body Class](#adding-menus-and-body-class)
- [Work with Sidebar](#work-with-sidebar)
- [Add Widget Area](#add-widget-area)
- [Work with the Loops](#work-with-the-loops)
- [Content Includes](#content-includes)

## Overview

A **Template** in WordPress is a PHP theme file that determines how content is displayed. The **Template Hierarchy** is a list of possible files that can be used in a theme and their relationship to each other. e.g.

- `page.php` controls how single pages are displayed.
- `single.php` controls how single blog posts are displayed.
- `category.php` controls category archive pages.
- `tag.php` controls tag archive pages.
- ...

The template hierarchy follow the **Fallback Architecture**. It means that if a certain template is not found, WordPress will look for through a series of backup templates to load instead. Check [VISUALIZE THE WORDPRESS TEMPLATE HIERARCHY](https://wphierarchy.com/) for more information.

> All templates eventually fall back to `index.php`, which is why an `index.php` file is required in all themes. The `style.css` and `functions.php` are not technically template files but are also required in themes.

<br/>
<div align="right">
  <b><a href="#template-hierarchy">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Setup the Theme Content and Files

1. Add in dummy content from [WP Test](http://wptest.io/). ([Tools] > [Import] > [WordPress] > [Run Importer])
2. Create Portfolio custom post type. (with plugin [Custom Post Type UI](https://wordpress.org/plugins/custom-post-type-ui/))
3. Create a `wphierarchy` theme folder.
4. Create a `style.css`, `functions.php` and `index.php` file.
5. Add screenshot.

<br/>
<div align="right">
  <b><a href="#template-hierarchy">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Work with `style.css` File

In the `style.css` file, there should be a very special comment that goes in the top that contains meta information about our theme.

```css
/*
  Theme Name: WP Hierarchy
  Author: Zac Gordon
  Author URI: https://zacgordon.com/
  Description: Demo theme for learning the WordPress Template Hierarchy
  Version: 1.0
  License: GNU General Public License v2 or later
  License URI: http://www.gnu.org/licenses/gpl-2.0.html
  Text Domain: wphierarchy
  Tags: one-column, two-columns, right-sidebar, flexible-header, accessibility-ready, custom-colors, custom-header, custom-menu, custom-logo, editor-style, featured-images, footer-widgets, post-formats, rtl-language-support, sticky-post, theme-options, threaded-comments, translation-ready
  Lorem to the longer descriptionum.
 */
```

WordPress uses the header comment section of the `style.css` file to display information about the theme in the Appearance dashboard panel.

<br/>
<div align="right">
  <b><a href="#template-hierarchy">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Work with `functions.php` File

The `functions.php` file is a generic file that is going to contain some custom code that wouldn't belong in one of the template files.

```php
<?php
  // Add Theme Support
  add_theme_support( 'title-tag' );
  add_theme_support( 'post-thumbnails' );
  add_theme_support( 'post_format', ['aside', 'gallery', 'link', 'image', 'quote', 'status', 'video', 'audio', 'chat'] );
  add_theme_support( 'html5' );
  add_theme_support( 'automatic-feed-links' );
  add_theme_support( 'custom-background' );
  add_theme_support( 'custom-header' );
  add_theme_support( 'custom-logo' );
  add_theme_support( 'customize-selective-refresh-widgets' );
  add_theme_support( 'starter-content' );

  // Load in our CSS
  function wphierarchy_enqueue_styles() {
    wp_enqueue_style( 'main-css', get_stylesheet_directory_uri() . '/style.css', [], time(), 'all' );
  }
  add_action( 'wp_enqueue_scripts', 'wphierarchy_enqueue_styles' );
?>
```

The function `add_theme_support()` resister the theme support for given features and **MUST** be called in the `functions.php` file to work.

<br/>
<div align="right">
  <b><a href="#template-hierarchy">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Work with `index.php` File

```php
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>WP Hierarchy</title>
  </head>
  <body>
    <h1>index.php</h1>
  </body>
</html>
```

<br/>
<div align="right">
  <b><a href="#template-hierarchy">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Work with Header and Footer

Add the `header.php` file:

```php
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <?php wp_head(); ?>
  </head>
  <body>
```

Don't forget to add the `get_header()` function in `index.php` file:

```php
<?php get_header();?>

    <h1>index.php</h1>
  </body>
</html>
```

- We can also use `get_header( 'custom' );` to load the header php named as `header-custom.php`.
- If the `header-custom.php` file is not found, WordPress will fallback to load the `header.php` file.

<br/>
<div align="right">
  <b><a href="#template-hierarchy">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Adding Menus and Body Class

Edit the `functions.php` files to add the `register_nav_menus()` function:

```php
// Register Menu Locations
register_nav_menus( [
  'main-menu' => esc_html__( 'Main Menu', 'wpheirarchy' ),
]);
```

Then add the navigation element in `header.php`:

```php
<nav id="site-navigation" class="main-navigation" role="navigation">
  <?php
    $args = [ 'theme_location' => 'main-menu' ];
    wp_nav_menu( $args );
  ?>
</nav>
```

- The function `register_nav_menus()` registers navigation menu locations for a theme.
- The function `wp_nav_menu()` displays a navigation menu.
- The function `body_class()` displays the classes for the body element.

<br/>
<div align="right">
  <b><a href="#template-hierarchy">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Work with Sidebar

The sidebars work the same way as the header and footer. There's a custom function at WordPress that will get the sidebar and by default it will look for the file sidebar to each piece of content.

First, create the `sidebar.php` file:

```php
<aside id="secondary" class="widget-area" role="complementary">
  <p>Place widgets here!</p>
</aside>
```

Then add `get_sidebar()` function in the `index.php` file.

<br/>
<div align="right">
  <b><a href="#template-hierarchy">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Add Widget Area

Edit the `functions.php` files to add the `register_sidebar()` function:

```php
// Setup Widget Areas
  function wphierarchy_widgets_init() {
    register_sidebar([
      'name'          => esc_html__( 'Main Sidebar', 'wphierarchy' ),
      'id'            => 'main-sidebar',
      'description'   => esc_html__( 'Add widgets for main sidebar here', 'wphierarchy' ),
      'before_widget' => '<section class="widget">',
      'after_widget'  => '</section>',
      'before_title'  => '<h2 class="widget-title">',
      'after_title'   => '</h2>',
    ]);  
  }
  add_action( 'widgets_init', 'wphierarchy_widgets_init' );
```

Now, add `dynamic_sidebar()` to `sidebar.php` to display the sidebar content:

```php
<?php
  if( ! is_active_sidebar( 'main-sidebar' ) ) {
    return;
  }
?>

<aside id="secondary" class="widget-area" role="complementary">
  <?php dynamic_sidebar( 'main-sidebar' ); ?>
</aside>
```

- `register_sidebar()` builds the definition for a single sidebar and returns the IDs.
- `is_active_sidebar()` check whether the sidebar is active or not.
- `dynamic_sidebar()` display dynamic sidebar.

<br/>
<div align="right">
  <b><a href="#template-hierarchy">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Work with the Loops

```php
<?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
  <article id="post-<?php the_ID(); ?>" <?php post_class(); ?>>
    <header class="entry-header">
      <?php the_title( '<h1>', '</h1>' ); ?>
    </header>
    <div class="entry-content">
      <?php the_content(); ?>
    </div>
  </article>
<?php endwhile; else : ?>
  <article id="post-<?php the_ID(); ?>" <?php post_class(); ?>>
    <header class="entry-header">
      <h1><?php esc_html_e( '404', 'wphierarchy' ); ?></h1>
    </header>
    <div class="entry-content">
      <p><?php esc_html_e( 'Sorry! No content found.', 'wphierarchy' ); ?></p>
    </div>
  </article>
<?php endif; ?>
```

<br/>
<div align="right">
  <b><a href="#template-hierarchy">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Content Includes

We can also break up chunks of files into smaller ones for modular meaning. Just split files into smaller files and place it inside the `template-parts` folder.

```php
<?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
  <?php get_template_part( 'template-parts/content' ); ?>
<?php endwhile; else : ?>
  <?php get_template_part( 'template-parts/content', 'none' ); ?>
<?php endif; ?>
```

Above code use `get_template_part()` function to get the content from `template-parts/content.php` file and `template-parts/content-none.php` file.

<br/>
<div align="right">
  <b><a href="#template-hierarchy">[ ↥ Back To Top ]</a></b>
</div>
<br/>