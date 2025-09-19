### `TaskbarApplication.gd` reference
*extends [DesktopElement](./desktopelement.md)*

`TaskbarApplication` is an object that represents its `linked_window` as a task on the taskbar.

#### Property reference
`task_name : Label`
Reference to the `Label` containing the 'title' of `linked_window` in the taskbar.

`icon : TextureRect`
Reference to the `TextureRect` containing the icon of `linked_window` in the taskbar.

`linked_window : ApplicationWindow`
The window/application this `TaskbarApplication` is representing.

#### Function reference
##### `_ready()`
Calls `super()` and connects the signal focus_entered to `_on_gain_focus()`.

##### `_process(_delta)`
Does nothing currently.

##### `_input(event)`
Tracks if it is being clicked, darkening itself until left click is released, then toggling `linked_window`'s minimization and giving it focus.

##### `_on_mouse_entered()`
Sets `hovered` to `true`, as inherited from `DesktopElement`.

##### `_on_mouse_exited()`
Sets `hovered` to `false`, as inherited from `DesktopElement`.

##### `grab_tooltip_text()`
Returns `tooltip`, using the `text` of `task_name` as a fallback if `tooltip` is empty.

##### `_on_gain_focus()`
Gives its focus to `linked_window` if it is visible.