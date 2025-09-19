### `OSManager.gd` reference
*extends [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)*

`OSManager` is a global node that processes system calls, and contains functions that have various utilities such as opening files, closing windows, getting all the files in a directory, and more. Routing everything through here allows applications and other software to be more scalable and also manipulate the OS by making their own calls to the system, which can be leveraged for viruses or other tools.

#### Property reference
`WINDOW_THEMES : Enum`
Enum containing all of the window themes the user can change to.

`MOUSE_THEMES : Enum`
Enum containing all of the mouse themes the user can change to. *(not yet implemented)*

`commands : Dictionary[String, Dictionary]`
A list of commands used in the terminal. The string contains the primary command keyword, and the dictionary value contains mappings to the type of system call (as specified in the `SystemCommand.COMMAND_TYPES` enum), a description for the terminal display, and an array of strings serving as the "parameters" to the function (these strings are used when showing the arguments to each command in the terminal's `help` command).

`fileicon_pfb : PackedResource`
Prefab/Scene used for creating desktop icons.

`desktop_manager : DesktopManager`
Reference to a `DesktopManager` object.

`mouse : Mouse`
Reference to the `Mouse` object that replaces the player's system mouse.

`debug_terminals : Array[Terminal]`
A list of references to all `Terminal`s with debug mode on. System commands issued in another `Terminal` that provide output also have its output sent to these `Terminal`s, and these `Terminal`s also recieve notifications when the user opens a file or application (among other system events) outside of a terminal command.

`system_commands : Array[SystemCommand]`
An array of `SystemCommands` to be executed. This array of `SystemCommand` events is processed in a queue-like fashion.

> The following properties should likely be moved to a different class/global node later.

`window_theme : WINDOW_THEMES`
Specifies the current window theme in use.

`mouse_theme : MOUSE_THEMES`
Specifies the current mouse theme in use.

`mouse_trail_enabled : bool`
Tracks whether mouse trails are enabled or not on the system.

`num_trails_mouse : int`
Specifies the maximum amount of mouse trails to have active at once.

`trail_frame_delay_mouse : int`
Specifies how many "frames" behind each mouse trail is from each other.

`trail_lifetime_mouse : float = 0.2`
Specifies how long (in seconds) a mouse trail lasts.

`window_trail_enabled : bool`
Tracks if the trail effect for desktop windows is enabled.

`num_trails_win : int`
Specifies the maximum amount of window trails to have active at once.

`trail_frame_delay_win : int`
Specifies how many "frames" behind each window trail is from each other.

`trail_lifetime_win : float`
Specifies how long (in seconds) a window trail lasts.

`wobbly_windows_enabled : bool`
Tracks if the KDE "Wobbly Windows" effect is enabled.

`maximum_window_count : int`
Specifies the maximum amount of application instances we can have open at once.

`base_dir : String`
The base user directory referenced when searching for files. Should be updated later to be not a static string...

`mouse_theme_changed : Signal`
Signal used when the mouse theme has changed to let the `Mouse` know to update its visuals.

`window_theme_changed : Signal`
Signal used when the window theme has changed to let `Application`s know to update its window's visual.

#### Function reference
##### `_ready()`
Hides the system mouse cursor and creates a new `Mouse` object if one does not already exist.

##### `physics_process(_delta)`
If the queue of system events in `system_commands` isn't empty, calls `execute()` on the one at the start of the array and removes it.

##### `update_theme(new_window_theme : WINDOW_THEMES = window_theme, new_mouse_theme : MOUSE_THEMES = mouse_theme, sender = null)`
Updates the `mouse_theme` or `window_theme` variables, and emits the signal `mouse_theme_changed` or `window_theme_changed` to let listener objects know when the mouse or window theme has changed.

##### `open(file : File, sender = null)`
Opens a provided `File`, creating a new `ApplicationWindow`. If the `File` object references an application Scene, the scene is instantiated and placed in the new `ApplicationWindow`. Otherwise, based on the filetype/extension, a wrapper application to view the file is opened and placed in the new `ApplicationWindow`. The new `ApplicationWindow` is returned.

##### `toggle_minimize(application : ApplicationWindow, sender = null)`
Minimizes or maximizes the given `ApplicationWindow` by tweening its position and scale, caching those at the start of the function.

##### `close(application : ApplicationWindow, sender = null)`
Closes the given `ApplicationWindow` by dithering it out, removing it from any pinned window or system message lists, and calling `queue_free()` at the end.

##### `load_directory(path : String, is_absolute_path : bool = false)`
Loads a directory specified by `path`, which can be absolute or relative to `base_dir` depending on the value of `is_absolute_path`. Returns an array of `File` and `String` objects, where `File`s represent files and `String`s represent directories in the relative path `path` from the base directory `base_dir` or files and directories in the absolute path `path`.

##### `get_dir_files(path : String)`
Returns a list of `Strings` specifying the directories and files in the provided relative path `path` from base directory `base_dir`.

##### `get_file(rel_path : String)`
Returns a `File` object if there is a file at the relative path `rel_path` from the base directory `base_dir`.

##### `parse_command(command : String, sender)`
Splits the provided `command` from `sender` by spaces, and processes the array of strings as a command and its arguments. Based on the items in the array resulting from the split, a command is created and added to the queue or an error message is sent.

##### `get_terminal_help_strings()`
Returns an array of strings corresponding to the `help` terminal command based on the commands specified in the `commands` Dictionary.

##### `send_debug_message(msg : String, sender)`
Sends a provided message to all terminals in the `debug_terminals` array and the original sender.

##### `issue_command(command : SystemCommand)`
Adds a provided `SystemCommand` to the queue by appending it to the `system_commands` array. Wrapper to make code more readable when issuing system commands to `OSManager`.

##### `toggle_window_pin(window : ApplicationWindow, caller = null)`
Adds or removes the provided `ApplicationWindow` to or from the desktop's pinned window list (moving it to the top of all windows in the process), and updates the window's pin button (should later be changed to a `TextureButton` that toggles tbh). Returns instantly if it is a `SystemMessage` since `SystemMessage`s have their own window list.

##### `send_system_message(type : SystemMessage.MESSAGE_TYPES, msg : String, caller = null)`
Creates a system dialog of the specified type (types are unimplemented) displaying the provided message from some caller that renders on top of all other windows.

##### `rename_file()`
Unimplemented.

##### `copy_file()`
Unimplemented.

##### `move_file()`
Unimplemented.

##### `download_file()`
Unimplemented.
