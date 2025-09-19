### `ApplicationWindow.gd` reference
*extends [Control](https://docs.godotengine.org/en/stable/classes/class_control.html)*

`ApplicationWindow` 

#### Property reference
`RESIZE_CORNERS : Enum`
Enum that helps us keep track of what corner of the application we are currently resizing.

`toolbar : Control`
Contains the name of the appli

`window_title : RichTextLabel`
Reference to the RichTextLabel displaying the name of the application in the window.

`icon : TextureRect`
Reference to the TextureRect displaying the icon of this application in the window.

`drag_area : Control`
Reference to the Control object who, when dragged within its area, will drag around the entire window. Usually is the background of the title or the window title object itself.

`minimize_button : Button`
Reference to the button used for minimizing the window.

`close_button : Button`
Reference to the button used for closing the window.

`application_container : Control`
Reference to the main container `Application`s are added as children under in the window.

`pin_button : Button`
Reference to the button used for pinning the window.

`linked_task : TaskbarApplication`
Reference to the visual taskbar application on the bottom of the screen corresponding to this window.

`trails : Array`
Stores references to the currently active window trails this application has created.

`hovering : bool`
Tracks whether the window itself is being hovered over. Used in 

`title_hovering : bool`
Tracks whether the draggable area specified by `drag_area` is being hovered over. Used to check if we should be dragging the window.

`dragging : bool`
Tracks whether we are actively dragging the application around.

`can_be_resized : bool`
Allows or disallows the window from being resized.

`resizing : bool`
Tracks whether we are actively resizing the application window.

`resize_margin : Vector2`
The amount of pixels "deep" on each edge of the window we have to drag the window on. Mainly set in `check_mouse_in_resize_bounds()`, probably should be changed.

`resize_edge : RESIZE_CORNERS`
Keeps track of what edge of the window we are resizing.

`mouse_in_resize_bounds : bool`
Tracks if the mouse is currently within the margin specified by `resize_margin` to resize the window.

`scaling_tween : Tween`
Reference to the tween applying the scaling effect on window minimization.

`scaling_length : float`
Determines how long the window spends scaling in/out when minimized.

`fade_length : float`
Determines how long the window spends fading in/out when closed or opened.

`dither_overlay : ColorRect`
Reference to the ColorRect containing the shader that creates the "dither fade" effect when dragging a window on the desktop.

`frames : int`
Tracks the amount of frames elasped since the window has been ready. Used to determine when to create a new window trail if all conditions are met.

`trail_count : int`
Tracks the amount of trails still active when dragging or resizing the window, in order to help limit the amount of trails spawned.

`wobbly_window_overlay : ColorRect`
Reference to the ColorRect containing the shader that creates the "wobbly window" effect when dragging a window on the desktop.

`decay : Vector2`
A helper variable for `wobbly_window_overlay` that sets the decay/strength of the effect left.

`speed : Vector2`
A helper variable for `wobbly_window_overlay` that helps reduce the decay every frame to ease out the wobbly window effect.

`relative_movement : Vector2`
The relative distance moved by the window, mainly used to calculate the strength of the decay to add for the wobbly window effect.

`cached_size : Vector2`
Variable used to save the window's size before minimizing it, and when replacing it when swapping the window theme.

`cached_pos : Vector2`
Variable used to save the window's position before minimizing it, and when replacing it when swapping the window theme.

#### Function reference
##### `_ready()`
Sets up a lot of signals so buttons in the window have functionality, also adding a little bit of initial window wobble and fading the window in for a brief moment based on `fade_length`.

##### `_process()`
Sizes the shader overlays, determines when we should make a trail and updates `trail_frame_delay_win` in  `OSManager` based on the `trail_lifetime_win` and `num_trails_win`. Also decays the window wobble effect if there is any distortion.

##### `close_application()`
Issues a command to `OSManager` to close this window. Also lets the mouse's `MouseStateMachine` that we are no longer resizing this window if we were before.

##### `toggle_minimize()`
Issues a command to `OSManager` to toggle this window's minimized state.

##### `_mouse_entered_title()`
Sets `title_hovering` to `true`. Used to track if we are able to drag the window around by the title bar.

##### `_mouse_exited_title()`
Sets `title_hovering` to `false`. Used to track if we are able to drag the window around by the title bar.

##### `save_size()`
Sets `cached_size` and `cached_pos` to the window's current size and position.

##### `_input()`
Determines if we are resizing or dragging based on the values of `resizing`/`dragging` and the current mouse input/position. Resizes itself if we are resizing, or moves itself if we are dragging.

##### `_on_focus_enter()`
Moves this window to the top and modifies its appearance slightly to show it has focus.

##### `_on_focus_exit()`
Modifies this window's appearance slightly to show it no longer has focus.

##### `_mouse_entered()`
Sets `hovering` to `true`.

##### `_mouse_exited()`
Sets `hovering` to `false`.

##### `check_mouse_in_resize_bounds()`
Determines if the mouse is within the resize margin to resize the bounds of the window, and if so, updates the mouse's `MouseStateMachine` so the correct cursor is displayed. Otherwise, it updates `MouseStateMachine` to let it know the mouse is no longer in the resize bounds for this window.

##### `update_trails()`
Callback for when a trail is freed to decrement `trail_count` by 1.

##### `create_trail()`
Duplicates itself, disabling the duplicate from processing anything and tweening the value of `dither_overlay`'s `progress` in order to fade it out before freeing it.

##### `size_overlays()`
Sizes, sets the layering of, and positions `dither_overlay` and `wobbly_window_overlay` so the window appears as it normally would without these shaders (the setup for it to work is complicted don't worry about it).

##### `move_to_top()`
Moves itself to the top of the windows based on the group it is in (if it is pinned, a system window, or neither). Pinned windows always appear on top of regular windows, and system windows always appear on top of everything.

##### `toggle_pin_window()`
Issues a `SystemCommand` to `OSManager` to toggle this window's pinned state.

##### `disable_pinning()`
Hides `pin_button` so it cannot be pressed.

##### `disable_minimizing()`
Hides `minimize_button` so it cannot be pressed.