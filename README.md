# jQuery.sdFilterMe
This plugin allows you to display an `<ul>` list with the shape of a set of boxes that would move according to your filtering needs. 

## Releases
* **v0.2** - 06/08/2015
* **v0.1** - 05/08/2015

## Changelog
### v0.2
* links on boxes with `data-link` attribute
* message when nothing to show in category
* sorting option available with `data-order` attribute
* callback handler for the click event

## Requirements
`jQuery.sdFilterMe` requires the latest version of [`jQuery`](https://jquery.com/download/).

## Demo
See this [JSFiddle link](http://jsfiddle.net/D4V1D/8obf6vye/) to see the plugin.

## Features
* filtering and sorting options available
* supports unlimited number of elements
* animation and CSS customizable
* boxes are `href`-able

## Usage
* **HTML**

First of all, you would need to make a `<ul>` list populated with `<li>` items containing a `img` tag (the plugin can handle different image sizes). `<li>` *must* have a `class` attribute to set the categories which filter applies on and *can* have a `data-title` attribute to set a title overlaying the box.

```html
<ul id="sort-me">
    <li class="food" data-title="2" data-order="2" data-link="http://www.steve-david.com/">
        <img src="http://lorempixel.com/300/200/food/1"/>
    </li>
    <li class="sports" data-title="5" data-order="5">
        <img src="http://lorempixel.com/300/200/sports/1"/>
    </li>
    <li class="sports" data-title="6" data-order="6">
        <img src="http://lorempixel.com/300/200/sports/3"/>
    </li>
    <li class="business" data-title="1" data-order="1">
        <img src="http://lorempixel.com/300/200/business/4"/>
    </li>
    <!-- and so on -->
</ul>
```

You then need to add the filter trigerring elements. You define them in the options you pass to the plugin and they can be whatever DOMElement you need. They *must* have the `data-filter` attribute matching the `class` of the `<li>` elements. For exemple:

```html
<button class="sorter" data-filter="food">Food</button>
<button class="sorter" data-filter="sports">Sports</button>
<button class="sorter" data-filter="business">Business</button>
|
<button class="sorter" data-filter="*">All</button>
```

You can also add the ordering option. It works the same way and they **must** have the `data-order` set to either `asc` or `desc`.

```html
<button class="orderer" data-order="asc">ASC</button>
<button class="orderer" data-order="desc">DESC</button>
```


* **jQuery**

The syntax of `jQuery.sdFilterMe`'s initialization is the following:
```javascript
jQuery(function($) {

  $('#sort-me').sdFilterMe({
      filterSelector: '.sorter', // string: selector
      orderSelector: '.orderer', // string: selector
      duration: 1000, // integer: in ms
      animation: 'ease', // string: ease | ease-in | ease-out | linear | ease-in-out
      hoverEffect: true, // boolean
      sortedOut: 'disappear', // string: disappear | opacity
      css: { // object
          overlay: { // object
              background: { // object
                  r: 0, // integer: as in CSS
                  v: 0, // integer: as in CSS
                  b: 0 // integer: as in CSS
              },
              duration: 250, // integer: in ms
              border: '1px solid white', // string: as in CSS
              color: 'white', // string: color
              opacity: 0.5 // float: as in CSS
          },
          border: { // object
              width: 10, // integer: in px
              color: '#2A4153' // string: color
          },
          margin: 10, // integer: in px
          pointer: true // boolean
      },
      nothingToShow: {
          text: 'Nothing to show', // string: text
          color: '#ccc' // string: color
    }
  }).on('fm.boxClicked', function(e, position, order) {
        console.log('Box position is ' + position);
        console.log('Box sort order is ' + order);
    });

});
```

## Options
Name | Type | Default | Description
------------ | ------------- | ------------- | -------------
filterSelector | string | `'.sorter'` | The jQuery element that is targetting the filter elements
orderSelector | string | `'.orderer'` | The jQuery element that is targetting the sorting elements
duration | integer | `1000` | The duration in `ms` of the moving animation
animation | string | `'ease'` | The CSS animation to apply
hoverEffect | boolean | `true` | If title provided, applies a `scale(0, 0)` to overlay element when hovering
sortedOut | string | `'disappear'` | Set to `'opacity'` to reduce the opacity of the non-matching elements to `0.25` instead of disappearing
css | object | `// ...` | The CSS properties to apply to each element


## Events
Name | Parameters | Description
------------ | ------------- | -------------
fm.boxClicked | `e, position, order` | This event is triggered when the user clicks on a box (whether `data-link` is provided or not). Three parameters are given: `e` is the event; `position` is the initial position of the clicked box and `order` is the value of `data-order`. 

## Licence
Copyright (c) 2015 Steve David

Licensed under the MIT license.
