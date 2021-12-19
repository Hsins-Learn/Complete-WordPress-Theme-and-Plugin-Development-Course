# Hooks

- [Overview](#overview)
- [Important Action Hooks Functions](#important-action-hooks-functions)
- [WordPress Actions Runtime Lifecycle](#wordpress-actions-runtime-lifecycle)
- [Explore Action Hooks](#explore-action-hooks)

## Overview

**Hooks** are a way for us to add our own code to customize default WordPress behavior. There're two types of hooks in WordPress:

- **Action Hooks** let us run our own code when a certain event takes place in the WordPress lifecycle.
- **Filter Hooks** let us get data from WordPress, modify it, and then return it back customized.

<br/>
<div align="right">
  <b><a href="#hooks">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Important Action Hooks Functions

There are three fundamental functions to know about when working with action hooks:

```php
<?php // index.php
  do_action( 'before_footer' ); // create an action hook
?>

<?php // functions.php
  add_action( 'before_footer', 'my_function' ); // hook in code
  remove_action( 'before_footer', 'my_function' ); // unhook code
?>
```

- Wherever `do_action()` occurs, we have an action hook. The function doesn't do anything by itself, but it's the hook that we can use to run.
- The `add_action()` function lets us add a function to an action hook.
- To remove an action, we have to call `remove_action()`.

<br/>
<div align="right">
  <b><a href="#hooks">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## WordPress Actions Runtime Lifecycle

**The Action Lifecycle** refers to the order and relationship od `do_action()` calls. Check [Plugin API/Action Reference | WordPress Codex](https://codex.wordpress.org/Plugin_API/Action_Reference) for more information.

<br/>
<div align="right">
  <b><a href="#hooks">[ ↥ Back To Top ]</a></b>
</div>
<br/>

## Explore Action Hooks

There're several ways to explore action hooks:

1. Use the global variables `$wp_actions` and `$wp_filter` to get a list of all the action hooks and filters.
   - `$wp_actions` is an array of all the action hooks that have been registered.
   - `$wp_filter` is an array of all the filters that have been registered.
2. Use the `r-debug.php` plugin to get a list of all the action hooks and filters.
   - Add `require( dirname( __FILE__ ) . '/lib/r-debug.php' );` to the `functions.php` file.
3. Use the [Debug Bar](https://wordpress.org/plugins/debug-bar/) and [Debug Bar Actions and Filters](https://wordpress.org/plugins/debug-bar-actions-and-filters/) plugins to get a list of all the action hooks and filters.
4. Use the [Simply Show Hooks](https://wordpress.org/plugins/simply-show-hooks/) plugin to get a list of all the action hooks and filters.

<br/>
<div align="right">
  <b><a href="#hooks">[ ↥ Back To Top ]</a></b>
</div>
<br/>