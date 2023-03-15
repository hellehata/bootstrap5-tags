# Tags for Bootstrap 4/5

[![NPM](https://nodei.co/npm/bootstrap5-tags.png?mini=true)](https://nodei.co/npm/bootstrap5-tags/)
[![Downloads](https://img.shields.io/npm/dt/bootstrap5-tags.svg)](https://www.npmjs.com/package/bootstrap5-tags)

## How to use

An ES6 native replacement for `select` using standards Bootstrap 5 (and 4) styles.

(almost) No additional CSS needed! Supports creation of new tags.

```js
import Tags from "./tags.js";
Tags.init();
// Tags.init(selector, opts);
// You can pass global settings in opts that will apply
// to all Tags instances
```

By default, only provided options are available. Validation error
will be displayed in case of invalid tag.

```html
<label for="tags-input" class="form-label">Tags</label>
<select class="form-select" id="tags-input" name="tags[]" multiple>
  <option disabled hidden value="">Choose a tag...</option>
  <option value="1" selected="selected">Apple</option>
  <option value="2">Banana</option>
  <option value="3">Orange</option>
</select>
<div class="invalid-feedback">Please select a valid tag.</div>
```

## Creation of new tags

Use attribute `data-allow-new` to allow creation of new tags. Their
default value will be equal to the text. Since you can enter
arbitrary text, no validation will occur.

```html
<select class="form-select" id="tags-input" name="tags[]" multiple data-allow-new="true"></select>
```

You can force these new tags to respect a given regex.

_NOTE: don't forget the [] if you need multiple values!_

## Server side support

You can also use options provided by the server. This script expects a json response that is an array or an object with the data key containing an array.

Simply set `data-server` where your endpoint is located. It should provide an array of value/label objects. The suggestions will be populated upon init
except if `data-live-server` is set, in which case, it will be populated on type. A ?query= parameter is passed along with the current value of the searchInput.

You can preselect values either by using `data-selected` or by marking the suggestion as `selected` in the json result.

```html
<label for="validationTagsJson" class="form-label">Tags (server side)</label>
<select
  class="form-select"
  id="validationTagsJson"
  name="tags_json[]"
  multiple
  data-allow-new="true"
  data-server="demo.json"
  data-live-server="1"
>
  <option disabled hidden value="">Choose a tag...</option>
</select>
```

You can pass additionnal parameters with `data-server-params` and choose the method with `data-server-method` (GET or POST).

## Options

Options can be either passed to the constructor (eg: optionName) or in data-option-name format.

| Name                 | Type                                       | Description                                                                                     |
| -------------------- | ------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| allowNew             | <code>Boolean</code>                       | Allows creation of new tags                                                                     |
| showAllSuggestions   | <code>Boolean</code>                       | Show all suggestions even if they don't match. Disables validation.                             |
| badgeStyle           | <code>String</code>                        | Color of the badge (color can be configured per option as well)                                 |
| allowClear           | <code>Boolean</code>                       | Show a clear icon                                                                               |
| clearEnd             | <code>Boolean</code>                       | Place clear icon at the end                                                                     |
| selected             | <code>Array</code> \| <code>String</code>  | A comma separated list of selected values                                                       |
| regex                | <code>String</code>                        | Regex for new tags                                                                              |
| separator            | <code>Array</code> \| <code>String</code>  | A list (pipe separated) of characters that should act as separator (default is using enter key) |
| max                  | <code>Number</code>                        | Limit to a maximum of tags (0 = no limit)                                                       |
| placeholder          | <code>String</code>                        | Provides a placeholder if none are provided as the first empty option                           |
| clearLabel           | <code>String</code>                        | Text as clear tooltip                                                                           |
| searchLabel          | <code>String</code>                        | Default placeholder                                                                             |
| keepOpen             | <code>Boolean</code>                       | Keep suggestions open after selection, clear on focus out                                       |
| allowSame            | <code>Boolean</code>                       | Allow same tags used multiple times                                                             |
| baseClass            | <code>String</code>                        | Customize the class applied to badges                                                           |
| addOnBlur            | <code>Boolean</code>                       | Add new tags on blur (only if allowNew is enabled)                                              |
| showDisabled         | <code>Boolean</code>                       | Show disabled tags                                                                              |
| hideNativeValidation | <code>Boolean</code>                       | Hide native validation tooltips                                                                 |
| suggestionsThreshold | <code>Number</code>                        | Number of chars required to show suggestions                                                    |
| maximumItems         | <code>Number</code>                        | Maximum number of items to display                                                              |
| autoselectFirst      | <code>Boolean</code>                       | Always select the first item                                                                    |
| updateOnSelect       | <code>Boolean</code>                       | Update input value on selection (doesn't play nice with autoselectFirst)                        |
| highlightTyped       | <code>Boolean</code>                       | Highlight matched part of the suggestion                                                        |
| fullWidth            | <code>Boolean</code>                       | Match the width on the input field                                                              |
| fixed                | <code>Boolean</code>                       | Use fixed positioning (solve overflow issues)                                                   |
| activeClasses        | <code>Array</code>                         | By default: ["bg-primary", "text-white"]                                                        |
| labelField           | <code>String</code>                        | Key for the label                                                                               |
| valueField           | <code>String</code>                        | Key for the value                                                                               |
| queryParam           | <code>String</code>                        | Name of the param passed to endpoint (query by default)                                         |
| server               | <code>String</code>                        | Endpoint for data provider                                                                      |
| serverMethod         | <code>String</code>                        | HTTP request method for data provider, default is GET                                           |
| serverParams         | <code>String</code> \| <code>Object</code> | Parameters to pass along to the server                                                          |
| fetchOptions         | <code>Object</code>                        | Any other fetch options (https://developer.mozilla.org/en-US/docs/Web/API/fetch#syntax)         |
| liveServer           | <code>Boolean</code>                       | Should the endpoint be called each time on input                                                |
| noCache              | <code>Boolean</code>                       | Prevent caching by appending a timestamp                                                        |
| debounceTime         | <code>Number</code>                        | Debounce time for live server                                                                   |
| notFoundMessage      | <code>String</code>                        | Display a no suggestions found message. Leave empty to disable                                  |
| onRenderItem         | <code>function</code>                      | Callback function that returns the suggestion                                                   |
| onSelectItem         | <code>function</code>                      | Callback function to call on selection                                                          |
| onClearItem          | <code>function</code>                      | Callback function to call on clear                                                              |
| onCanAdd             | <code>function</code>                      | Callback function to validate item. Return false to show validation message.                    |
| onServerResponse     | <code>function</code>                      | Callback function to process server response. Must return a Promise                             |

To know more about these features, check the demo!

## Tips

- You can also use it on single selects! :-)
- Use arrow down to show dropdown when using showAllSuggestions
- If you have a really long list of options, a scrollbar will be used
- Access Tags instance on a given element with Tags.getInstance(mySelect)

## Style

While styling is not mandatory, some pseudo styles may help align your styles with a regular bootstrap form-control
We basically replicate input state as pseudo classes on the form-control container

- Support focus styles by implementing a pseudo class `form-control-focus`
- Support improved floating labels by implementing a pseudo class `form-placeholder-shown`
- Support disabled styles by implementing a pseudo class `form-control-disabled`

These styles can be found in `_tags.scss`

## Without Bootstrap 5

### Bootstrap 4 support

Even if it was not the initial idea to support Bootstrap 4, this component is now compatible with Bootstrap 4 because it only
requires minimal changes.

Check out demo-bs4.html

### Standalone usage

Obviously, this package works great with the full bootstrap library, but you can also use it without Bootstrap or with a trimmed down version of it

Actually, this library doesn't even use the js library to position the dropdown menu, so its only dependencies is on css classes.
You can check out the .scss file to see how to reduce bootstrap 5 css to a smaller size.

Check out demo-standalone.html

## Demo

https://codepen.io/lekoalabe/pen/ExWYEqx

## How does it look ?

![screenshot](screenshot.png "screenshot")

## Do you need to init this automagically ?

You can use [Modular Behaviour](https://github.com/lekoala/modular-behaviour.js)

https://codepen.io/lekoalabe/pen/wvmBLoB

## Browser supports

Modern browsers (edge, chrome, firefox, safari... not IE11). [Add a warning if necessary](https://github.com/lekoala/nomodule-browser-warning.js/).

## Also check out

- [Bootstrap5 autocomplete](https://github.com/lekoala/bootstrap5-autocomplete): the autocomplete input for bootstrap 5 (and more!)
- [BS Companion](https://github.com/lekoala/bs-companion): the perfect bootstrap companion
- [Admini](https://github.com/lekoala/admini): the minimalistic bootstrap 5 admin panel
