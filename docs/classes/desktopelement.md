### `DesktopElement.gd` reference
*extends [Control](https://docs.godotengine.org/en/stable/classes/class_control.html)*

`DesktopElement` is a general-purpose class for creating an element with some properties on the desktop.

#### Property reference
`tooltip : String`
The text for the tooltip displayed when this object is hovered over for a set amount of time on the desktop.

`can_be_dragged : bool`
Determines if this object can be dragged while on the desktop or not.

`double_click_window : float`
The amount of time (in seconds) the player has to click again after an initial click for the second to count as a double-click.

`hovered : bool`
Tracks if this object is currently being hovered over.

`dragging : bool`
Tracks if this object is currently being dragged.

`clicked : bool`
Tracks if this object has been clicked once. Used to help detect double-clicking.

`timer : float`
Variable used to help make sure double-clicks only occur while in the window specified by `double_click_window`.

`double_clicked : Signal`
Signal emitted when this `DesktopElement` is double-clicked within `double_click_window`.

#### Function reference
##### `_ready()`
Connects its `mouse_entered` and `mouse_exited` signals to `_on_mouse_entered()` and `_on_mouse_exited()` respectively.

##### `_physics_process(delta)`
Counts down the `timer` or sets `clicked` to `false` depending on `timer`, also manages showing/hiding `tooltip` in `DesktopManager` and setting its text if it is being hovered.

##### `_on_mouse_entered()`
Callback function used when the mouse hovers over this element to track that it is now hovered over.

##### `_on_mouse_exited():`
Callback function used when the mouse stops hovering over/leaves this element to track that it is no longer hovered over.

##### `_input(event)`
Checks on a left click if we should emit the `double_clicked` signal.

##### `grab_tooltip_text()`
Wrapper that returns `tooltip`. Makes code in other classes more readable.