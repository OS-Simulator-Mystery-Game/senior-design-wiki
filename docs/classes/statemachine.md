### `StateMachine.gd` reference
*extends [Node](https://docs.godotengine.org/en/stable/classes/class_node.html)*

`StateMachine` is a general-purpose state manager for some `parent`, which can make implementing specific functionality or conditions easier. Often inherited in order to make specific functionality or changes for a given `parent`.

#### Property reference
`parent : Node`
Reference to the parent Node manipulated by this `StateMachine`.

`state : Variant`
Reference to the `parent`'s current state, tracked here.

`prevState : Variant`
Reference to the previous state we were in.

`states : Dictionary`
A `Dictionary` of possible states the `parent` can be in, and their values. Functions similarly to an `Enum`, but a `Dictionary` is used to make this extendable to an arbitrary amount of states and different states altogether.

#### Function reference
##### `_init(sys_file)`
Sets up all of the properties for this `File`, linking the file to `sys_file` and determining what `icon` and `filename` it should have based on the type of `sys_file`. Also sets up the `path` to this file.

##### `_physics_process(delta)`
Updates the `parent`'s `state`, to `state`, and updates our current `state` if we need to change it based on the return value of `get_transition()`.

##### `state_logic(delta)`
Method that can be overridden to specify behavior in our current `state`.

##### `get_transition(delta)`
Method that can be overridden to specify behavior or how we should change to a different state while in our current `state`.

##### `enter_state(new_state, old_state)`
Method that can be overridden to specify behavior when entering from `old_state` to `new_state`.

##### `exit_state(new_state, old_state)`
Method that can be overridden to specify behavior when exiting from `old_state` to `new_state`.

##### `set_state(new_state):`
Handles setting our `state` to `new_state`, and if we are even entering or exiting based on `prevState`.
		
##### `add_state(state_name)`
Adds a provided key `state_name` to `states` and assigns it a value.