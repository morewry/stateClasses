# stateClasses

Plugin to toggle custom CSS classes to indicate user interface state.

On applications which use JavaScript styling using both classes and pseudo-classes can be inconvenient.  Some states for a single interface element might be styled using pseudo-classes, while some (which depend on JavaScript) might not.  This can sometimes result in writing redundant and conflicting styles.  Also, the states handled by JavaScript often have classes hard-coded into scripts which are inconvenient for designers to access.

It can be useful to let JavaScript handle all of the states, and this plugin is a simple utility for that purpose.


## Example Use

When the plugin initiates it will create (an) event listener(s).  By default, the mouseenter, mouseleave, focus, and blur events will map to a hover state.  Custom events named "active" and "normal" will also be created which provide access points for other scripts to utilize state indication via stateClasses.

In addition, it is possible to create any number of states and map them to either default JavaScript events or custom events.

	// Example Init
	$('[data-states]').stateClasses();

	// Example HTML
	<button class="tabs--tab" data-states="active: tabs--tab__active, hover: tabs--tab__hover">Button</button>

The above will ensure that the class "tabs--tab__hover" is added to the button element on mouseenter, focus, or focusin and that it will be removed on mouseleave, blur, or focusout.

In addition, the following code can be used to trigger the active state on the button element (which will add the class "tabs--tab__active").

	// Example Trigger Active
	$('tabs--tab').trigger('active');

To return the button to its normal state:

	// Example Trigger Normal
	$('tabs--tab').trigger('normal');

It is also possible to set configuration on one element while control of the state happens on another.  Useful to reduce repetative configurations or to set a class on a parent when a child is clicked.

	// Example delegation
	<button data-states="delegate: #parentid">Button</button>
	<div id="parentid"></div>



## Options

**states**<br>
optional, configuration object

To create new states or alter defaults, pass in an object using this format:

	{
		states: {
			stateName: "class names"
		},
		stateName: {
			events: ["defaultEventName"]
		}
	}

Defaults are:

	{
		selector: "[data-states]",
		normal: {
			events: ["normal"]
		},
		active: {
			events: ["active"]
		},
		hover: {
			events: ["mouseenter", "mouseleave", "focus", "blur"],
			on: ["mouseenter", "focus", "focusin"],
			off: ["mouseleave", "blur", "focusout"]
		},
		states: {
			normal: "",
			active: "active",
			hover: "hover"
		}
	}


## Methods

There are no methods designed to be public, but any method could be accessed directly using the standard syntax for jQuery plugins.

	$(selector).stateClasses(medthodName);
