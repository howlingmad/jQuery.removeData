# jQuery.removeData
Extend jQuery [removeData()](https://api.jquery.com/removeData/) to add the following functionality:
- Optionally remove the corresponding data-attribute on the element (if added without using `.data()`)
- Only remove the attribute if the value matches one passed in the options
- Allow data attribute value to be passed containing `data-`

**Current Version:** 2.0.0

## Installation
Include [jQuery](http://jquery.com/download) and `jQuery.removeData.js` in your HTML document. Supports jQuery version 1.7+
```html
<script src="http://code.jquery.com/jquery-latest.min.js"></script>  
<script src="jQuery.removeData.js"></script>
```

## How to Use
Call the ```removeData()``` method on any element with a data attribute.

**HTML**
```html
<div data-foo="selector" data-bar="baz" data-boom="bloz">content</div>
```

**jQuery**  
remove just data cache (original behaviour)  
```javascript
$('div[data-foo=selector]').removeData('bar');  
```

**jQuery**  
removes data cache and attribute  
```javascript
$('div[data-foo=selector]').removeData('bar', {
  removeAttr: true
});
```

**jQuery**  
removes data cache (and optionally attribute) if value matches 
```javascript
$('div[data-foo=selector]').removeData('bar', {
  values: 'baz'
});  

$('div[data-foo=selector]').removeData('bar', {
  removeAttr: true,
  values: 'baz'
});
```

**Variations**  
The attribute value can cater for the following variations
```javascript
$('div[data-foo=selector]').removeData('bar');  
$('div[data-foo=selector]').removeData('data-bar');  
$('div[data-foo=selector]').removeData('[bar, boom]');  
$('div[data-foo=selector]').removeData('[data-bar, data-boom]');  
$('div[data-foo=selector]').removeData('bar boom');  
$('div[data-foo=selector]').removeData('data-bar data-boom');
```
The values option can cater for the following variations
```javascript
$('div[data-foo=selector]').removeData('bar', {values: 'baz'});  
$('div[data-foo=selector]').removeData('[bar, boom]', {values: ['baz','bloz']});  
$('div[data-foo=selector]').removeData('bar boom', {values: 'baz bloz'});  
```

### Edge cases
This will remove **both** the bar and boom attributes
```javascript
$('div[data-foo=selector]').removeData(['bar','boom'], {values:'baz'});
```
But this will remove **just** the bar attribute
```javascript
$('div[data-foo=selector]').removeData(['bar','boom'], {values:['baz','']});
```
These will also remove **both** the bar and boom attributes
```javascript
$('div[data-foo=selector]').removeData(['bar','boom'], {values:[undefined, 'baz']});
$('div[data-foo=selector]').removeData(['bar','boom'], {values:['baz', null]});
```
This will remove **just** the bar attribute  
*note the space after baz. this will translate to ['baz','']*
```javascript
$('div[data-foo=selector]').removeData(['bar','boom'], {values:'baz '});
```

**For more edge cases, see the test suite**

## Running the Unit Tests
Run the unit tests with a local server that supports PHP. Ensure that you run the tests from the **test** directory. No database is required. Pre-configured php local servers are available for Windows and Mac. Here are some options:

- Windows: [WAMP download](http://www.wampserver.com/en/)
- Mac: [MAMP download](http://www.mamp.info/en/index.html)
- Linux: [Setting up LAMP](https://www.linux.com/learn/tutorials/288158-easy-lamp-server-installation)
- [Mongoose (most platforms)](http://code.google.com/p/mongoose/)

Ensure you select the **Enable coverage** option to see test coverage provided by [Blanket.js](http://blanketjs.org/).

## Feedback
If you discover any issues or have questions regarding usage, please add an issue on GitHub.
