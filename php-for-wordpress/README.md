# PHP for WordPress

- [What is PHP](#what-is-php)
- [Basic Concepts](#basic-concepts)
- [Variables](#variables)
- [WordPress PHP Coding Standards](#wordpress-php-coding-standards)
- [The Loop](#the-loop)
- [Template Tags](#template-tags)
- [Conditional Tags](#conditional-tags)
- [WordPress Hooks](#wordpress-hooks)

## What is PHP

**PHP (PHP HyperText Preprocessor)** is a server side programming language. This means that our PHP is processed on the server running our website, whether that is locally or with a hosting service. Once PHP is executed, it generates HTML files and served them to the browser.

- PHP is a programming language.
- WordPress itself is built largely with PHP.
- PHP runs on the server before HTML is sent to browser.
- PHP can be used outside of WordPress as well.

<br/>
<div align="right">
  <b><a href="#php-for-wordpress">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Basic Concepts

- PHP files end with the extension `.php`. This means they can include PHP code. However, they can also include HTML code as well.
- Although PHP files can include PHP, all PHP must be wrapped inside a PHP block `<?php ... ?>`
- **Variables** is the way to temporarily store values in memory. The variables names start with a dollar sign `$` and should use an `_` (underscore) rather than spaces or camelCase style.
- **Echo** is a function for us to display something on the page with PHP. When we have an arry or object saved as variables, we may have to use `var_export` to display the values.
- **Arrays** are variables that store multiple values. To create an array, we use `[]` and separate each value with a comma `,`.
- **Foreach Loop** will let us repeat a set of actions on each item in an array.
- **Functions** let us write and reuse blocks of code. A function contains two parts: (1) function declaration and (2) function body.

<br/>
<div align="right">
  <b><a href="#php-for-wordpress">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Variables

```php
<?php
  $first_name = "Da-Ming";
  $last_name = "Wang";
?>

<h2>Welcome!</h2>
<p>My name is "<?php echo $first_name . " " . $last_name; ?>."</p>
```

- A **variable** starts with a dollar sign `$`, followed by the name of the variable.
- Don't forget the semi-colon `;` at the end of every line.
- We can use period character `.` to concatenate strings.

<br/>
<div align="right">
  <b><a href="#php-for-wordpress">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## WordPress PHP Coding Standards

- Use **single and double quotes when appropriate**.
- Use **real tabs and not spaces** for indentation.
- **Braces should always be used**, even when they are not required.
- Use `elseif` instead of `else if`.
- Use **long array syntax `array( 1, 2, 3 )`** for declaring arrays more readable.
- Not shorthand PHP tags `<? ...?>`.
- Always **put spaces after commas, and on both sides of logical, comparison, string and assignment operations**.
- Use **lowercase letters** in variable, action and function names. Separate words via **underscores**.
- Class names should use **capitalized words separated by underscores**. Any acronyms should be all **upper case**.
- Constants should be in **all upper-case with underscores separating words**.
- Files should be named descriptively using **lowercase letters**. **Hyphens** should separate words.
- Class file names should be based on the class name with `class-` prepended and the underscores in the class name replaced with hyphens.
- Always have **Tenary operators** if the statement is `true`.
- Use **Yoda Conditions** (always put the variable on the right side and put constants, literals or function calls on the left side).

Visit [PHP Coding Standards | WordPress Developer](https://developer.wordpress.org/coding-standards/wordpress-coding-standards/php/) for more information.

<br/>
<div align="right">
  <b><a href="#php-for-wordpress">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## The Loop

```php
<?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
  <h1><?php the_title(); ?></h1>
  <?php the_content(); ?>
<?php endwhile; else: ?>
  <p><?php _e( "Sorry, no content available!", "textdomain" ); ?></p>
<?php endif; ?>
```

<br/>
<div align="right">
  <b><a href="#php-for-wordpress">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Template Tags

The **Template Tags** are special functions that allow us to easily get information and content from WordPress. Here are a few examples of the many different template tags that are available.

- `get_header()`
- `get_footer()`
- `get_sidebar()`
- `get_template_part()`
- `get_the_title()`
- `the_title()`
- `the_content()`
- `the_author`()`
- `the_category()`
- `the_tags`
- `the_post_thumbnail()`
- `the_permalink()`()
- `edit_post_link()`
- `site_url()`
- `wp_nav_menu()`
- `wp_login_form()`
- `bloginfo()`
- `comment_author()`
 

<br/>
<div align="right">
  <b><a href="#php-for-wordpress">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Conditional Tags

The **Conditional Tags** are WordPress functions that return `true` when certain conditions are met. ere are a few examples of the many different conditional tags that are available.

- `is_front_page()`
- `is_home()`
- `is_admin()`
- `is_single()`
- `is_single('slug')`
- `is_single(['slug-1'], ['slug-2'])`
- `is_singular()`
- `get_post_type()`
- `has_excerpt()`
- `is_page()`
- `is_page('slug')`
- `is_page(['slug-1', 'slug-2'])`
- `is_page_template('custom.php')`
- `comments_open()`
- `is_category()`
- `is_tag()`
- `is_archive()`
- `in_the_loop()`

<br/>
<div align="right">
  <b><a href="#php-for-wordpress">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## WordPress Hooks

The **Hooks** allow us to add custom code into existing software (e.g. WordPress). There're two different types of hooks in WordPress:

- **Action Hooks** let us run our own code when certain events take place in the WordPress run cycle.

    ```php
    function phpforwp_theme_styles() {
      // Enqueue google fonts https://fonts.googleapis.com/css?family=Open+Sans|Varela+Round
      wp_enqueue_style( 'font-css', 'https://fonts.googleapis.com/css?family=Open+Sans|Varela+Round' );
      
      // Enque main style sheet (make dependent on google fonts)
      wp_enqueue_style( 'main-css', get_stylesheet_uri(), [ 'font-css' ], get_the_time() );
    }

    // Add phpforwp_theme_styles function to wp_enqueue_scripts action hook with a priority of 10
    add_action( 'wp_enqueue_scripts', 'phpforwp_theme_styles', 10 );
    ```

- **Filter Hooks** let us modify how content is displayed on a page or saved to the database.

    ```php
    function phpforwp_read_more_link( $excerpt ) {

      // Create a variable called $extended_excerpt and assign it the value of $excerpt
      $extended_excerpt = $excerpt;

      // Append a read more link using get_permalink() as the url
      $extended_excerpt .= ' <a href="' . get_permalink() . '">';
      $extended_excerpt .= 'Read more &raquo;';
      $extended_excerpt .= '</a>';

      // Return $extended_excerpt
      return $extended_excerpt;

    }
    // Add phpforwp_read_more_link function to the get_the_excerpt with a priority of 10
    add_filter( 'get_the_excerpt', 'phpforwp_read_more_link', 100 );
    ```

So the hooks are generally used in plugin files or the `functions.php` file in themes, not in the template files.

<br/>
<div align="right">
  <b><a href="#php-for-wordpress">[ ↥ Back To Top ]</a></b>
</div>
<br/>