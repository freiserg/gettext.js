# gettext.js

gettext.js is a lightweight (3k minified!) yet complete and accurate GNU
gettext port for node and the browser. Manage your i18n translations the right
way in your javascript projects.


## Why another i18n javascript library?

gettext.js aim is to port the famous GNU gettext and ngettext functions to
javascript node and browser applications.
It should be standards respectful and lightweight (no dictionary loading
management, no extra features).

The result is a < 200 lines javascript tiny lib yet implementing fully
`gettext()` and `ngettext()` and having the lighter json translation files
possible (embeding only translated forms, and not much headers).

There are plenty good i18n libraries out there, notably
[Jed](https://github.com/SlexAxton/Jed) and [i18n-next](http://i18next.com/),
but either there are too complex and too heavy, or they do not embrace fully
the gettext API and philosophy.

There is also [gettext.js](https://github.com/Orange-OpenSource/gettext.js)
which is pretty good and heavily inspired this one, but not active since 2012
and without any tests.


## Installation

### Node

Install the lib with the following command: `npm install gettext.js --save`

Require it in your project:

```javascript
var i18n = require('gettext.js');
i18n.gettext('foo');
```

### Browser

Download the latest
[archive](https://github.com/guillaumepotier/gettext.js/archive/master.zip) or
get it through bower: `bower install gettext.js --save`

```html
<script src="/path/to/gettext.js" type="text/javascript"></script>
<script>
  var i18n = window.i18n(options);
  i18n.gettext('foo');
</script>
```

## Usage

### Load your messages

You can load your messages these ways:

```javascript
// i18n.setMessages(domain, locale, messages, plural_form);
i18n.setMessages('messages', 'fr', {
  "Welcome": "Bienvenue",
  "There is %1 apple": [
    "Il y a %1 pomme",
    "Il y a %1 pommes"
  ]
}, 'nplurals=2; plural=n>1;');
```

```javascript
// i18n.loadJSON(jsonData /*, domain */);
var json = {
  "": {
    "locale": "fr",
    "plural-forms": "nplurals=2; plural=n>1;"
  }
  "Welcome": "Bienvenue",
  "There is %1 apple": [
    "Il y a %1 pomme",
    "Il y a %1 pommes"
  ]
};
i18n.loadJSON(jsonData, 'messages');
```

See Required JSON format section below for more info.


### Set the locale

You could do it from your dom

```html
<html lang="fr">
```

or from javascript

```javascript
i18n.setLocale('fr');
```


### `gettext(msgid)`

Translate a string.


### `ngettext(msgid, msgid_plural, n)`

Translate a pluralizable string


### Variabilized strings

`gettext('There are %1 in the %2`, 'apples', 'bowl'); -> "There are apples in the bowl`
`ngettext('One %2', '%1 %2', 10, 'bananas'); -> "10 bananas"`

It uses the public method `i18n.strfmt("string", var1, var2, ...)` you could
reuse elsewhere in your project.


## Required JSON format

You'll find in `/bin` a `po2json.js` converter, based on the excellent
[po2json](https://github.com/mikeedwards/po2json) project that will dump your
`.po` files into the proper json format below:

```json
{
    "": {
        "lang": "en",
        "plural_forms": "nplurals=2; plural=(n!=1);"
    },
    "simple key": "It's tranlation",
    "another with %1 parameter": "It's %1 tranlsation",
    "a key with plural": [
        "a plural form",
        "another plural form",
        "could have up to 6 forms with some languages"
    ],
    "a context\u0004a contextualized key": "translation here"
}
```

Use `bin/po2json.js input.po output.json` or
`bin/po2json.js input.po output.json -p` for pretty format.


## Parsers

You could use [xgettext-php](https://github.com/Wisembly/xgettext-php) parser
to parse your files. It provides helpful javascript and handlebars parsers.


## License

MIT
