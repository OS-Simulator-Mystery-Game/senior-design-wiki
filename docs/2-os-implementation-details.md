# OS Implementation Details

## Making calls
In the OS, you can make calls to change the theme, minimize/expand a certain window, or close other applications (and more!). To do this, create a new instance of the `SystemCommand` class, passing it:
- The type of system call (present in the enum `COMMAND_TYPES` in `SystemCommand.gd`)
- An array of parameters/values to be used with the command (can be empty)
- What object is creating the call (usually just `self`)
After doing this, call `os_manager.issue_command(<your SystemCommand>)` to add it to the event queue.
*NOTE:* If you want to make a custom call, add it in the enum and define its behavior in the match statement within `SystemCommand`'s `execute()` function!
*NOTE:* If you want to make a custom terminal command, add it in the dictionary `commands` in `OSManager.gd`, defining:
- The name of the command (what to type as the first word/token of the command)
- A dictionary of parameters with the following key/value pairs:
   - `"type"`: The type of command being issued, from the enum `COMMAND_TYPES` in `SystemCommand.gd` (leave this key/value pair out if you don't want to make it a system call; the `help` command currently functions this way since it doesn't really modify anything and just prints!)
   - `description`: The help text that appears in the `help` command in the terminal
   - `args`: An array of strings defining the arguments to be passed. The strings will be displayed in the `help` command to show users what to pass.

## Custom applications
To make a custom application, create a new scene (`.tscn`) file, and ensure the root of that scene has a script attached that inherits/extends the `Application` class, with a class name. Applications can be developed in separate scenes, usually with their sizings set to Full Rect/what is needed to automatically resize. Put it in the user files to have it show in the filesystem.
*NOTE:* If you extend the `Application` class, make sure to call `super()` in `_ready()`!