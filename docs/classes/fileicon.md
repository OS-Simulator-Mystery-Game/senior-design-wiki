### `FileIcon.gd` reference
*extends [DesktopElement](./desktopelement.md)*

`FileIcon` is a class used to represent the physical . It is tied to the scene `file_icon.tscn`.

#### Property reference
`icon : TextureRect`
References the `TextureRect` that displays the file's icon.

`text : Label`
References the `Label` that displays the filename.

`text_highlight : ColorRect`
References the background highlight `ColorRect` that displays when this `FileIcon` has focus.

`file : File`
Reference to the corresponding `File` for this `FileIcon`.

#### Function reference
##### `_ready()`
Calls `super()` and connects `open()` to the `double_clicked` signal inherited from `DesktopElement`.

##### `_input(event)`
Handles detecting if this `FileIcon` was double clicked or dragged across the desktop.

##### `setup(sys_file : File)`
Sets up all of the properties for this `FileIcon` by linking `sys_file` to `File`, and linking the `File`'s `icon` and `filename` to `icon` and `text`.

##### `open()`
Creates and issues a `SystemCommand` to open this `FileIcon`'s corresponding `File` object.

##### `grab_tooltip_text()`
Returns this `FileIcon`'s corresponding `tooltip` inherited from `DesktopElement`, using its filename (`text`) as a fallback if `tooltip_text` is empty.