backbone-dragandrop-delegation
==============================

A consistent drag and drop across browsers using native like events. Read more about it on:
http://christianalfoni.com/2013/09/09/delegated-drag-and-drop-for-backbone/

*Note* : Does not work on IE8 er below

```javascript
  Backbone.View.extend({
        tagName: 'div',
        className: 'dragdrop',
        events: {
            //Handle drag
            'mousedown .draggable': 'detectDrag',
            'dragstart .draggable': 'dragstart',
            'dragend .draggable': 'dragend',
            // Handle drop
            'dragenter .dropable': 'dragenter',
            'dragleave .dropable': 'dragleave',
            'drop .dropable': 'drop'
        },
        detectDrag: function (event) {
            // Trigger detectDrag on the mousedowned element
            $(event.currentTarget).detectDrag();
        },
        dragstart: function (event, data, clone, element) {
            // Add any properties to the data object
            // to pass it to the drop. You can also 
            // manipulate the clone created that follows the 
            // mouse pointer and the element that started 
            // the drag
            data.someProperty = 'someValue';
            // Or set the value of data
            data.set('someValue');
        },
        dragenter: function (event, clone, element) {
          // When you drag something and hover the drop container.
          // Do something to the dropcontainer, the element where the
          // drag started or the clone following the cursor
          var dropContainer = $(event.currentTarget);
          dropContainer.animate({opacity: 1}, 'fast');
        },
        dragleave: function (event, clone, element) {
          // Typically revert changes on dragenter
          var dropContainer = $(event.currentTarget);
          dropContainer.animate({opacity: 0.5}, 'fast');
        },
        drop: function (event, data, clone, element) {
          // Trigger code on drop
          console.log(data.someProperty); // => someValue
          // Or if data was set()
          console.log(data); // => someValue
        },
        dragend: function (event, clone, element) {
           // Triggered when NOT dropping into a drop container.
           // Either the drop or the dragend event is triggered
        },
    });
```
