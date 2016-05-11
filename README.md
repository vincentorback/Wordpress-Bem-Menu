# Wordpress BEM Menu - Forked and adjusted for [SUIT CSS](https://github.com/suitcss/suit) syntax

Say goodbye to badly named menus in Wordpress and say hello to Wordpress BEM Menus!

To use simply drop the contents of wp_bem_menu.php into your functions.php file.


## Usage

First you need to register a nav menu in your themes `functions.php` file.

`register_nav_menu('my_menu', 'primary site menu');`

You also need to create a menu in wp-admin and make sure it is assigned a theme location that matches your registered nav menu above.

Then insert the following function into your theme. The first argument is the theme location (as defined in wp-admin) and the second argument is the class prefix you would like to use for this particular menu. The class prefix will be applied to the menu `<ul>` and every child `<li>` as the 'block'. The third optional argument accepts either an `array()` or a `string`.

```php
<?php bem_menu('menu_location', 'Nav', 'Nav--myModifier'); ?>
```
If you want to add multiple modifiers to the `<ul>` use an array e.g:
```php
<?php bem_menu('menu_location', 'Nav', array('Nav--myModifier','Nav--myOtherModifier')) ?>
```
Please note that these modifier classes are not inherited by descendants. this is by design to avoid bloated navigation markup. You can still target children of a specific modifier like so: `.Nav--myModifier .Nav-item{}`

## html output
```html
<ul class="my-menu my-menu--my-modifier">
    <li class="Nav-item is-active"><a href="#">Home</a></li>
    <li class="Nav-item"><a href="#">Page 2</a></li>
    <li class="Nav-item"><a href="#">Page 3</a></li>
</ul>
```

## Css classes

The syntax is very simple, all menu items are logically grouped by depth to avoid some of the nesting issues of the standard output.

```css
/* Top level items */
.Nav-item{}

/* Parent item */
.Nav-item--parent{}

/* Active page item */
.Nav-item.is-active{}

/* sub menu class */
.Nav-Sublist{}

```

## Modification

BEM syntax is very subjective and different developers use different conventions. If you wish to change or adapt the syntax to go with your own implemntation all the menu suffixes are contained within the `$this->item_css_classes` array:

```php
$this->item_css_classes = array(
    'list'                      => $this->css_class_prefix . 'List',
    'item'                      => $this->css_class_prefix . 'Item',
    'link'                      => $this->css_class_prefix . 'Link',
    'parent_item'               => $this->css_class_prefix . 'Item--parent',
    'sub_menu'                  => $this->css_class_prefix . 'Sublist',
    'sub_menu_item'             => $this->css_class_prefix . 'Item',
    'active_item'               => 'is-active',
    'parent_of_active_item'     => '',
    'ancestor_of_active_item'   => ''
);

```
