# slugIt - just another jQuery slugs generator plugin

I've created this one because I wanted a jQuery slug plugin capable of convert
european utf8 chars plus some symbols and easily extensible for custom extra mappings.
None of the ones listed on http://plugins.jquery.com/plugin-tags/slug does what I needed.

I got the idea of this plugin after using the excelent perl module Text::Unidecode
(http://search.cpan.org/dist/Text-Unidecode/) for this same task server side.

I've taken some chars tables from Django admin urlify.js
(http://code.djangoproject.com/browser/django/trunk/django/contrib/admin/media/js/urlify.js)
as this one was the most similar aproach to what I was looking to implement over jQuery.

This fork of the plugin adds the ability to have multiple source text fields. See below for examples.

## Requirements

Requires JQuery (It should work with all version)::

```html
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js"></script>
```

## Usage

Load this plugin like any other::

```html
<script type="text/javascript" src="jquery.slugit.js"></script>
```

Then, you select the source field to be converted::
```html
<form>
  <input type="text" id="slugme"/>
  <input type="text" id="slug"/>
</form>

<script>
  $(function(){
    $('#slugme').slugIt();
  });
</script>
```

"I love my umbrella'" will be converted to "i-love-my-umbrella"

When there are two fields, the syntax follow jQuery norms.

```html
<form>
  <input type="text" id="first_name"/>
  <input type="text" id="last_name"/>
  <input type="text" id="slug"/>
</form>

<script>
  $(function(){
    $('#first_name, #last_name').slugIt();
  });
</script>
```

"John" and "Smith" will be converted to "john-smith"


## Options

While the slugIt() method has some defaults that make the previous example to work, you'll be probably
inerested in customize for your convenience. These are the available options and their defaults::

```javascript
{
  events:    'keypress keyup',  // Any sensible jquery event (http://api.jquery.com/category/events/)
  output:    '#slug',           // A selector or function to send the generated slug
  separator: '-',               // A separator which will be use to separate words

  map:       false,             // A hash with extra replacemets.
                                // You can overwrite default replacements just passing the
                                // ones you like to replace.

  before:    false              // Callback that will be fired before processing slug (you can modify the input)
  after :    false              // Callback that will be fired after processing slug (You can modify the slug)
}
```

## Examples

You can add some extra mappings::

```html
<script>
  $(function(){
    $('#slugme').slugIt({ map: { '☂': 'umbrella' } });
  });
</script>
```

...So, "I ♥ my ☂'" will be converted to "i-love-my-umbrella"

Or customize word separator::
```html
<script>
  $(function(){
    $('#slugme').slugIt({ separator: '_' });
  });
</script>
```

Now, "I love my umbrella'" will be converted to "i_love_my_umbrella"

Working examples can be found at http://github.com/radionewzealand/slugit-jquery/tree/master/examples/

## Pull Requests

I will consider pull requests to fix bugs, or add new character sets. Also tests, if anyone feels inspired.

## Licensing

BSD License can be found at http://www.opensource.org/licenses/bsd-license.php
