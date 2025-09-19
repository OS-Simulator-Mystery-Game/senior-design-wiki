### `File.gd` reference
*extends [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)*

`File` is a general-purpose object that stores details about a given file in the filesystem. 

#### Property reference
`filename : String`
The name of the file displayed to the player.

`file : Variant`
The actual, physical file being referenced.

`icon : Texture2D`
The icon to use when representing this file in the filesystem.

`path : String`
The path to this file from the base directory `res://computer_files/`.

#### Function reference
##### `_init(sys_file)`
Sets up all of the properties for this `File`, linking the file to `sys_file` and determining what `icon` and `filename` it should have based on the type of `sys_file`. Also sets up the `path` to this file.