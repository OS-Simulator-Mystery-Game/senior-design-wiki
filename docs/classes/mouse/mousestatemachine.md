### `MouseStateMachine.gd` reference
*extends [StateMachine](../statemachine.md)*

`MouseStateMachine` is a `StateMachine` for `Mouse` that can determine the parent `Mouse`'s appearance, as well as add behavior based on its `state`.

#### Property reference
`CURSORS : Enum`
An enum containing the different possible mouse cursor sprites we can show.

`drag_angle : ApplicationWindow.RESIZE_CORNERS`
Stores which corner we are resizing, if we are doing so. Used to determine which mouse cursor sprite to show.

`applications_in_resize_bounds : int`
The amount of applications we could be resizing. Used to determine if resizing cursors should be shown or not, and when to stop showing them.

#### Function reference
##### `_ready()`
Adds states to `states` as inherited from `StateMachine` and sets the starting state.

##### `state_logic(delta)`
Calls the `parent`'s `update_frames()` and `_physics_process()` functions.

##### `get_transition(delta)`
Called every frame. Contains behavior about what to do in the current state, such as setting the parent `Mouse`'s `frame` or the `offset`. To leave the current state and enter a new one, it may return a state in `states`, as inherited from `StateMachine`.

##### `enter_state(new_state, old_state)`
Does nothing currently. Called after leaving a state and entering a new one.

##### `exit_state(new_state, old_state)`
Does nothing currently. Called when leaving a state, and before entering a new one.

##### `state_includes(state_array)`
Returns `true` if the current state matches any state in `state_array`, `false` if otherwise.