<br>

This step covers setting up a basic 2D project, with a main scene and a simple directory structure for assets.

<br>

---

<br>

## New Project

Start a new project by setting the `Renderer` to `Mobile` and `Version Control Metadata` to `None` (or `Git` if you need VC).

Name the Project whatever you like and place make sure to select an empty folder for the project location.

![[New-Project.png]]

<br>

#### Empty Project Example

After creating a new project, you should see a window similar to this:

![[New-Project-Layout.png]]

<br>

---

<br>

## Project Setup

<br>

#### 2D View Setup

Set the viewport to 2D by clicking the `2D` button in the center of the top toolbar.

Your view should now look something like this:

![[Set-2D-View.png]]

<br>

---

<br>

#### Create A Root 2D Scene Node

To create a new 2D scene, press the `2D Scene` button in the `Scene` tab under `Create Root Node:`

![[2D-Scene-Button.png]]

<br>

You should now have a node called `Node2D`. You can change this to any name you like by right-clicking and selecting `rename` (for example: `Main` for the main scene) or by pressing `F2` while it is selected.

<br>

![[Rename-Main-Scene.png]]

<br>

---

<br>

#### Directory Structure (FileSystem)

In the bottom left of the window, you will see the Godot [FileSystem](https://docs.godotengine.org/en/stable/tutorials/scripting/filesystem.html). 

This will be used for managing all assets for the game, ranging from characters sprites, tilesets, scripts, audio, fonts, and more. Basically, this is where all content for your game lives.

<br>

A few things to keep in mind regarding the Godot FileSystem:

- Moving assets around (renaming them or moving them from one path to another inside the project) will break existing references to these assets. These references will have to be re-defined to point at the new asset location.

<br>

- To avoid this, do all your move, delete and rename operations from within Godot, on the FileSystem dock. Never move assets from outside Godot, or dependencies will have to be fixed manually (Godot detects this and helps you fix them anyway, but why go the hard route?).

<br>

- The second is that, under Windows and macOS, file and path names are case insensitive. If a developer working in a case insensitive host file system saves an asset as `myfile.PNG`, but then references it as `myfile.png`, it will work fine on their platform, but not on other platforms, such as Linux, Android, etc. This may also apply to exported binaries, which use a compressed package to store all files.

<br>

> One fool-proof convention is to only allow lowercase file and path names.

<br>

---

<br>

#### Basic Template Structure

The directory structure used in this guide is going to look something like this:

- res://
	- assets/
		- characters/
			- main-character/
		- maps/
			- main-map/
	- scenes/

<br>

![[File-System-Setup.png]]

<br>

If you see an `icon.svg`, you can safely delete it from the FileSystem.

<br>

---

<br>

#### Save the Scene

The tab under the toolbar at the top should say `[unsaved](*)`. This means that the scene needs to named and saved.

In the top toolbar, you can save the scene by pressing `Scene > Save Scene` or by pressing `Ctrl + S`. Name the scene `main.tscn` and set the location to the `scenes/` folder created in the previous step.

![[Save-Main-Scene.png]]

<br>

The basics for the project should now be setup, and should look something like this:

![[Project-Setup-Finish.png]]