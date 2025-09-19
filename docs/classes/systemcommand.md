### `SystemCommand.gd` reference
*extends [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)*

`SystemCommand` represents one of several possible events in the operating system, and operates its own logic upon calling `execute()`.

#### Property reference
`COMMAND_TYPES : Enum`
An enum of all the possible system command types for the OS.

`caller : Variant`
Tracks what `Node` called this command.

`type : COMMAND_TYPES`
Tracks which type of command this `SystemCommand` corresponds to.

`parameters : Array`
An array of parameters for this `SystemCommand`.

#### Function reference
##### `_init(_type : COMMAND_TYPES, _params : Array, _caller)`
Sets up the corresponding properties for this `SystemCommand`.

##### `execute()`
Based on the `type` of this `SystemCommand`, it further processes the parameters passed to it, and grabs corresponding files or information to use when executing its logic for its given `type`. Eventually, makes a call to a corresponding function in `OSManager` or changes something within the OS, and sends a message exclusively back to `caller` if it is a `Terminal`.