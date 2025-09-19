### `DesktopManager.gd` reference
*extends [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)*

`DesktopManager` is a script that manages the windows and icons on the desktop, as well as the taskbar.

#### Property reference
`taskbar : MarginContainer`
Reference to the main taskbar.

`taskbar_container : HBoxContainer`
Reference to the container that aligns `TaskbarApplication`s.

`desktop : Control`
Reference to a control node representing the bounds/space on the desktop.

`window_control : Control`
Reference to a node that stores `ApplicationWindows` so they display on top of `DesktopElement`s at all times.

`tooltip : MarginContainer`
Reference to the object that displays tooltips on the desktop.

`boot_overlay : Panel`
Reference to a panel that creates the slow fade in effect upon starting the game. *This will later be reworked!*

`mouse_cursor : Mouse`
Reference to the current `Mouse`.

`desktop_file_icons : Array[FileIcon]`
Reference to all FileIcons on the desktop.

`time_elasped : float`
Tracks time between blinks of the colon in the current time.

`blink_interval : float`
The amount of time (in seconds) needed to wait before toggling the visibility of the colon in the current time.

`tooltip_wait : float`
The amount of time (in seconds) needed to wait until the tooltip appears.

`total_windows : int`
Keeps track of how many windows we have open so we don't open too many.

`pinned_windows : Array[ApplicationWindow]`
Keeps track of all references to pinned `ApplicationWindow`s.

`sys_messages : Array[ApplicationWindow]`
Keeps track of all references to important system `ApplicationWindow`s.

`taskbar_pfb : PackedScene`
Reference to a `TaskbarApplication` prefab/Scene used to represent a corresponding `ApplicationWindow`.

`classic_window_pfb : PackedScene`
Reference to a `ApplicationWindow` prefab/Scene with the "classic" theme applied.

`glass_window_pfb : PackedScene`
Reference to a `ApplicationWindow` prefab/Scene with the "glass" theme applied.

`aero_window_pfb : PackedScene`
Reference to a `ApplicationWindow` prefab/Scene with the "aero" theme applied.

#### Function reference
##### `_ready()`
Gives `OSManager` and `GameGlobals` a reference to itself, also loads the desktop and tweens out the `boot_overlay` using the dither effect.

##### `_process(delta)`
Makes sure the `window_control` is always at the top of the desktop, and controls the current time and the blinking colon.

##### `_input(event)`
Does nothing.

##### `load_desktop()`
Clears the desktop, and loads all of the files in the `/Desktop` directory, creating `FileIcons` for each. Also calls `organize()` (will be changed later).

##### `create_application(sys_file)`
Creates and returns an `ApplicationWindow` with a reference to the corresponding `TaskbarApplication`, also checking and incrementing the value of `total_windows`.

##### `organize()`
Organizes all `FileIcons` on the desktop into a grid based on their size.