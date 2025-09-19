### `GameGlobals.gd` reference
*extends [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)*

`GameGlobals` is a global node that processes system calls, and contains functions that have various utilities such as opening files, closing windows, getting all the files in a directory, and more. Routing everything through here allows applications and other software to be more scalable and also manipulate the OS by making their own calls to the system, which can be leveraged for viruses or other tools.

#### Property reference
`sound_manager : SoundManager`
Reference to the game's `SoundManager`.

`desktop_manager : DesktopManager`
Reference to the game's `DesktopManager`.

`idle_timer : float`
Tracks how long the player has not done anything on the desktop for. Used for displaying tooltips.

`cursors : Dictionary[OSManager.MOUSE_THEMES, Texture2D]`
Stores a mapping of mouse themes and their spritesheets. Should eventually be moved somewhere else.

#### Function reference
##### `_ready()`
Limits the game's FPS to 60 (we should find a way to make animations correspond with 60 FPS despite the player's FPS), and instantiates a `SoundManager` object if there is none.

##### `physics_process(delta)`
Adds `delta` to `idle_timer`.

##### `_input(event)`
Resets the idle timer, and hides the tooltip. Also plays the mouse and keyboard press sound effects.
