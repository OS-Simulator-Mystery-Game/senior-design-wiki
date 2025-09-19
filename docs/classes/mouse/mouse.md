### `Mouse.gd` reference
*extends [Sprite2D](https://docs.godotengine.org/en/stable/classes/class_sprite2d.html)*

`Mouse` is a `Sprite2D` that follows the player's mouse input and replaces the system mouse.

#### Property reference
`trail_count : int`
The amount of `MouseTrail`s currently active.

`frames : int`
The amount of frames that have elasped since the `Mouse` has been ready.

`state : Variant`
A reference to the current state of the `Mouse` used by its `MouseStateMachine`.

`state_machine : StateMachine`
Reference to the `Mouse`'s `MouseStateMachine` node.

`mouse_trail_pfb : PackedScene`
Prefab/Scene reference to the `MouseTrail`'s corresponding object that animates the actual mouse trail.

#### Function reference
##### `_ready()`
Sets the theme using `update_theme()` and connects `OSManager`'s `mouse_theme_changed` signal to call `update_theme()`.

##### `_process(delta)`
Sets its position to the current mouse position by the user, and updates `trail_frame_delay_mouse` in `OSManager` based on the lifetime and amount of mouse trails. If conditions are met and a new mouse trail can be made, calls `create_trail()`.

##### `_physics_process(_delta)`
Does nothing. Required since it is called by the `state_machine`.

##### `update_frames(_delta)`
Increases `frames` by 1. Called by the `state_machine`.

##### `update_theme()`
Based on the current mouse theme in `OSManager`, loads the corresponding spritesheet for the mouse.

##### `update_trails()`
Callback for once a `MouseTrail` is fully dithered out to decrease `trail_count` by 1 so a new trail can be made.

##### `create_trail()`
Creates a new `MouseTrail` object by instantiating `mouse_trail_pfb`, sets up its properties, and tweens its dithering shader to animate it out and free it once it is done.

