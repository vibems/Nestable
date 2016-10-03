Nestable
========


### Drag & drop hierarchical list with mouse and touch compatibility (jQuery / Zepto plugin)

[**Try Nestable Demo**](http://dbushell.github.com/Nestable/)

Nestable is an experimental example and not under active development. If it suits your requirements feel free to expand upon it!

## Usage

Write your nested HTML lists like so:

    <div class="dd">
        <ol class="dd-list">
            <li class="dd-item" data-id="1">
                <div class="dd-handle">Item 1</div>
            </li>
            <li class="dd-item" data-id="2">
                <div class="dd-handle">Item 2</div>
            </li>
            <li class="dd-item" data-id="3">
                <div class="dd-handle">Item 3</div>
                <ol class="dd-list">
                    <li class="dd-item" data-id="4">
                        <div class="dd-handle">Item 4</div>
                    </li>
                    <li class="dd-item" data-id="5">
                        <div class="dd-handle">Item 5</div>
                    </li>
                </ol>
            </li>
        </ol>
    </div>

Then activate with jQuery like so:

    $('.dd').nestable({ /* config options */ });

### Events

The `change` event is fired when items are reordered.

    $('.dd').on('change', function() {
        /* on change event */
    });

### Methods

You can get a serialised object with all `data-*` attributes for each item.

    $('.dd').nestable('serialize');

The serialised JSON for the example above would be:

    [{"id":1},{"id":2},{"id":3,"children":[{"id":4},{"id":5}]}]

### Configuration

You can change the follow options:

* `maxDepth` number of levels an item can be nested (default `5`)
* `group` group ID to allow dragging between lists (default `0`)

These advanced config options are also available:

* `listNodeName` The HTML element to create for lists (default `'ol'`)
* `itemNodeName` The HTML element to create for list items (default `'li'`)
* `rootClass` The class of the root element `.nestable()` was used on (default `'dd'`)
* `listClass` The class of all list elements (default `'dd-list'`)
* `itemClass` The class of all list item elements (default `'dd-item'`)
* `dragClass` The class applied to the list element that is being dragged (default `'dd-dragel'`)
* `handleClass` The class of the content element inside each list item (default `'dd-handle'`)
* `collapsedClass` The class applied to lists that have been collapsed (default `'dd-collapsed'`)
* `placeClass` The class of the placeholder element (default `'dd-placeholder'`)
* `emptyClass` The class used for empty list placeholder elements (default `'dd-empty'`)
* `expandBtnHTML` The HTML text used to generate a list item expand button (default `'<button data-action="expand">Expand></button>'`)
* `collapseBtnHTML` The HTML text used to generate a list item collapse button (default `'<button data-action="collapse">Collapse</button>'`)

**Inspect the [Nestable Demo](http://dbushell.github.com/Nestable/) for guidance.**

Nestable with 5 little callbacks
========

## This is a modified version of Nestable

Original can be found here: https://github.com/dbushell/Nestable

## Example
```
$('#example-list-element').nestable({
    afterInit: function ( event ) { 
        console.log( event ); 
    }
})
.on('beforeDragStart', function(handle) {
    console.log('dragStart', handle);
})
.on('dragStart', function(event, item, source) {
    console.log('dragStart', event, item, source);
})
.on('dragMove', function(event, item, source, destination) {
    console.log('dragMove', event, item, source);
})
.on('dragEnd', function(event, item, source, destination) {
    console.log('dragEnd', event, item, source, destination);
})
.on('beforeDragEnd', function(event, item, source, destination, position, feedback) {
    // If you need to persist list items order if changes, you need to comment the next line
    if (source[0] === destination[0]) { feedback.abort = true; return; }

    feedback.abort = !window.confirm('Continue?');
})
.on('dragEnd', function(event, item, source, destination, position) {
    // Make an ajax request to persist move on database
    // here you can pass item-id, source-id, destination-id and position index to the server
    // ....

    console.log('dragEnd', event, item, source, destination, position);
});
```
* * *

Original Author: David Bushell [http://dbushell.com](http://dbushell.com/) [@dbushell](http://twitter.com/dbushell/)

Event handler addition done by BeFiveINFO 

Big thanks to @bigfoot90 !

Copyright © 2012 David Bushell | BSD & MIT license
