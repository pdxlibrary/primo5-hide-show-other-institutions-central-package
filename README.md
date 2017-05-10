# Primo NUI Hide/Show Other Institutions Toggle Button - Designed for use in a Central Package Setup

Adds a toggle button to hide/show other institutions that own the item when viewing a record's details in Ex Libris Primo NUI (Primo 5). Setup designed to use central package and local config


# Central Package Setup 

Inside Closure:

```js

// hide/show other institutions toggle button placeholder
app.component('prmAlmaMoreInstAfter', {
  bindings: {parentCtrl: '<'},
  controller: function () {
  this.$onInit = function () {
    if(enable_hide_show_other_institutions) {
      hide_show_other_institutions_add_button();
    }
  };
  },
  template: '<div class="hide_show_other_institutions_container hide"></div>'
});

```

Outside Closure:

```js

//////////////////////////////////
// hide/show other institutions //
//////////////////////////////////

// hide/show other institutions default settings
var enable_hide_show_other_institutions = false;
var hide_show_other_institutions_default_state = "hidden";
var hide_show_other_institutions_hide_libraries_button_label = "Hide Summit Libraries";
var hide_show_other_institutions_show_libraries_button_label = "Show Summit Libraries";

// hide/show other institutions set options from local config
function hide_show_other_institutions(options) {
  if(typeof options === 'undefined')
    options = new Array();
  enable_hide_show_other_institutions = true;
  if(typeof options.default_state !== 'undefined')
    hide_show_other_institutions_default_state = options.default_state;
  if(typeof options.hide_libraries_button_label !== 'undefined')
    hide_show_other_institutions_hide_libraries_button_label = options.hide_libraries_button_label;
  if(typeof options.show_libraries_button_label !== 'undefined')
    hide_show_other_institutions_show_libraries_button_label = options.show_libraries_button_label;

  hide_show_other_institutions_add_button();
}

// hide/show other institutions add toggle button
function hide_show_other_institutions_add_button() {
  if(hide_show_other_institutions_default_state == "visible") {
    angular.element(document.querySelector('md-tabs')).removeClass("hide");
    angular.element(document.getElementsByClassName('hide_show_other_institutions_container')).html('<button class="hide_show_other_institutions_button" onclick="hide_show_other_institutions_toggle()">'+hide_show_other_institutions_hide_libraries_button_label+'</button>');
  } else {
    angular.element(document.querySelector('md-tabs')).addClass("hide");
    angular.element(document.getElementsByClassName('hide_show_other_institutions_container')).html('<button class="hide_show_other_institutions_button" onclick="hide_show_other_institutions_toggle()">'+hide_show_other_institutions_show_libraries_button_label+'</button>');
  }
  // place button above list of libraries 
  angular.element(document.querySelector('prm-alma-more-inst-after')).after(angular.element(document.querySelector('prm-alma-more-inst md-tabs')));
  // show the button
  angular.element(document.getElementsByClassName('hide_show_other_institutions_container')).removeClass("hide");
}

// hide/show other institutions toggle visibility of other institutions list
function hide_show_other_institutions_toggle() {
  if(angular.element(document.querySelector('md-tabs')).hasClass("hide")) {
    angular.element(document.querySelector('md-tabs')).removeClass("hide");
    angular.element(document.getElementsByClassName('hide_show_other_institutions_button')).text(hide_show_other_institutions_hide_libraries_button_label);
  } else {
    angular.element(document.querySelector('md-tabs')).addClass("hide");
    angular.element(document.getElementsByClassName('hide_show_other_institutions_button')).text(hide_show_other_institutions_show_libraries_button_label);
  }
}

```

*************************	

# Local custom.js Setup


Basic Usage (uses centrally managed default settings):

```js

hide_show_other_institutions();

```

Advanced Usage:

There are currently 3 configuration settings:
* default_state - Sets the default state of the other instiutions list when the screen first loads. Possible values: "hidden" or "visible". Defaults to "hidden".
* show_libraries_button_label - Sets the button label for the toggle button to show the other instituions list. Defaults to "Show Summit Libraries".
* hide_libraries_button_label - Sets the button label for the toggle button to hide the other instituions list. Defaults to "Hide Summit Libraries".

Example using all three optional parameters:

```js

hide_show_other_institutions({
  'default_state': 'visible',
  'show_libraries_button_label': 'SHOW',
  'hide_libraries_button_label': 'HIDE'
});

```

These code snippets can be added anywhere in the local custom.js file as long as they are outside the closure.

***************

# CSS Styling

The hide/show other institutions button can be styled using CSS in the custom1.css file.

For example:

```css

/* hide/show other institutions button */
.hide_show_other_institutions_button {
    color: #FFF;
    background-color: #A33F1F;
    background-image: none;
    border-radius: 3px;
    font-size: 16px;
    border: none;
    padding: 7px 24px;
}

/* hide/show other institutions button - on hover */
.hide_show_other_institutions_button:hover {
    background-color: #b5654c;
}

```
