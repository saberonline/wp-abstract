# WordPress Abstract

Creating custom post types and other things in WordPress can sometimes be a bit annoying. WordPress Abstract, from [Records On Ribs](http://recordsonribs.com) hopes to make it a little easier. We are using it to re-write our [Ribcage](http://github.com/recordsonrib/ribcage) plugin faster.

The hope of WordPress Abstract is that it provides a simple way in which to do things in WordPress that may be a little obscure, so plugins and themes aren't rammed with boilerplate code and you can get down to making functionality.

## Adding WordPress Abstract To Your Code

Either install WordPress Abstract as a plugin and begin using the below, or simply include this one file in your code for your theme or plugin using `require_once`. Done!

## Creating a Custom Post Type

Simply do the following:
    
    $records = new WPAbstractPostType('records');

And that is it! A custom post type called records will be created with quite a few bells and whistles.

Okay, so you want the custom post type to be called internally 'something' and in the interface 'thing'?

    $something = new WPAbstractPostType('something', 'thing');

Done! And say the plural of 'thing' is 'stuffs'?

    $something = new WPAbstractPostType('something', 'thing', 'stuffs');

And we are away!

## Using Named Arguments

Sadly for whatever reason the PHP developers don't like named arguments. But lets fake it anyway by running an array into WPAbstractPostType.

    $records = new WPAbstractPostType(array('name' => 'records'));

And we are away! The rest of the examples assume this syntax.

## Using WordPress Normal Custom Post Type Settings

Say you want to create records, but want to make `has_archive` when the custom post type is setup, which defaults to true, instead be false? We can do this by using the ovewrite parameter.

	$params = array('name' => 'records');
	$params['overwrite'] = array('has_archive' => false);

	$records = new WPAbstractPostType($params);

And we have no archive!

## Overwriting Titles Of Default Metaboxes

When you create a custom post type you are left with a load of WordPress boilerplate text inherited from posts and pages hanging about. But we don't 'Featured Image', we want something like 'Record Sleeve'! No problem at all, you don't even need to know the name of the metabox internally, just the text it normally displays, in this case, 'Featured Image'.

Then just issue the following, passing our changes into an array in overwrite with the name 'meta_box_titles'.

    $meta_box_titles = array('Featured Image' => 'Record Sleeve');
    $overwrite = array('meta_box_titles' => $meta_box_titles);

    $records = new WPAbstractPostType(array('name' => 'records', 'overwrite' => $overwrite);

Done! The when you run `the_post_thumbnail();` on the front end then it'll show what the user submitted in the 'Record Sleeve' metabox.

## Overwriting Everything In Default Metaboxes

Right now, the only thing you can over-write is the instructions for the Featured Image.

	$params['name'] = 'records';
	$params['overwrite'] = array('featured_image_instruction' => 'The cover image of the record.');

	$records = new WPAbstractPostType($params);

Soon we shall use the translation matrix to overwrite anything you see on screen!

## Overwriting The Title Prompt

We've all seen the boring 'Enter title here' in WordPress thousands of times. Lets change it for our record post type.

	$records = new WPAbstractPostType(array('name' => 'records', 'overwrite' => array('enter_post_here' => 'The title of the record'));

And we are away!

## Soon

A quick list of other things this will implement soon enough.

* Customised columns for a custom post type, the easy way.
* A better way of doing the things attached to `init` to allow on the fly changes.
* Less nested arrays for parameters, use them if you like, or don't!
* Taxonomies with just as much customisation.
* Change the default text of any default metabox, easily.
* Hierachical custom post types, handled.
* Integration with [Meta-Box](https://github.com/rilwis/meta-box) - this sort of works if you create your custom post type by extending the class and overload the `metaboxes` function to add your functions.
* CLI to create scaffold WordPress code, probably using [wp-cli](https://github.com/wp-cli/wp-cli).

