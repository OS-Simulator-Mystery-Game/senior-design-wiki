### `Application.gd` reference
*extends [Control](https://docs.godotengine.org/en/stable/classes/class_control.html)*

`Application` is a general-purpose class that is inherited by software on the desktop. It handles a lot of directing user input on the desktop, as well as the focus mechanics of control nodes. By default, inheriting this class will handle a lot of that functionality for you, as well as other mechanics such as making system calls, and updating the window's theme.

#### Property reference
`application_name : String`
Contains the name of the application to be displayed in the filesystem and on the desktop.

`icon : Texture2D`
Contains the icon for this application in the filesystem, desktop, taskbar, and corner of the window.

`tooltip : String`
Contains the tooltip for this application on the desktop or in the filesystem.

`window : ApplicationWindow`
Reference to the window containing this `Application`.

`interacting : bool`
Tracks if we are interacting at all with this application. Signals in `_ready()` are connected in order to make sure this variable is updated correctly and is accurate. This is tracked because elements in the application may grab focus, but we don't want the window visual to think it has lost focus.

#### Function reference
##### `_ready()`
Sets up signals for when this window or any of the other children in the application gets focus. These objects are connected to `_on_focus_gained()` and `_on_focus_exited()`, which handle some visual display elements of the window to show the user if the current application is the selected one or not. A signal is also connected for the OS window theme changing that `Application` handles.
> **NOTE:** If inheriting `Application`, call `super()` in that script's `_ready()` function!

##### `_on_focus_gained()`
Updates `interacting` and calls `window.on_focus_exit()`.

##### `_on_focus_exited()`
Checks if any of the nodes in this application have focus. If not, sets `interacting` to `false` and calls `window.on_focus_exit()`.

##### `get_all_children()`
Helper method that returns an array of all the nodes that are children of this `Application`.

##### `update_theme()`
Updates the window's theme by instantiating a new one based on the global OS theme, copying over the current window's properties, copying over its focus state, and reparenting itself to the new window and freeing the old one. It also connects the new window to the connected `TaskbarApplication` object.