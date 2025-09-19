### `MouseTrail.gd` reference
*extends [Sprite2D](https://docs.godotengine.org/en/stable/classes/class_sprite2d.html)*

`MouseTrail` is a `Sprite2D` that animates itself dithering out to provide a smooth mouse trailing effect.

#### Property reference
`frames : int`
The amount of frames that have elasped since this `MouseTrail` has been ready.

#### Function reference
##### `_init()`
Sets its position to the mouse's current position, and connects `OSManager`'s `mouse_theme_changed` signal to call `update_theme()`.

##### `_process(_delta)`
Increases `frames` by 1, and ensures its `Sprite2D`'s `frame` and `offset` match the mouse's `Sprite2D`'s current `frame` and `offset`.

##### `update_theme()`
Based on the current mouse theme in `OSManager`, loads the corresponding spritesheet for the mouse trail.