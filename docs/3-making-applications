# Making custom applications
###### [Application.gd reference](./classes/application.md)

Applications in the game are aimed to be developed as standalone scenes, and then later put into an OS window.

To make a custom application, create a new scene (`.tscn`) file, and ensure the root of that scene has a script attached that inherits/extends the `Application` class, with a class name. Applications can be developed in separate scenes, usually with their sizings set to Full Rect/what is needed to automatically resize properly. In your application's custom script, feel free to add new functions and create your own functionality! Inheriting `Application` should handle a lot of how your application will function on the desktop.

Currently, we do not have a linking system for files in our filesystem (eg. Windows'/UNIX's link/shortcut system). For now, put your `.tscn` file of your application in the user's filesystem.

> **NOTE:** If you extend the `Application` class, make sure to call `super()` in `_ready()`!