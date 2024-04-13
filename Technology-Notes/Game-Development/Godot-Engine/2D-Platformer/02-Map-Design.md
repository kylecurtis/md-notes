
<br>

---

<br>

## Getting The Map Assets

For the map, I am going to use a free pack called `Pixel Art Platformer Village Props` by Cainos.

<br>

The size of the the tiles in this pack is 32x32.

<br>

#### Tile Set Example

![[Map-Tileset-Example.png]]

The asset pack can be found [Here](https://cainos.itch.io/pixel-art-platformer-village-props).

<br>

---

<br>

## Map Setup

<br>

#### Import Assets

Before using the map, you have to add the assets to the Godot File System in the `main-map/` folder from the Project Setup.

Convert the file names to lowercase (for compatability), and then copy all the contents from the `Texture/` folder into the `main-map/` directory. The File System should now look like this:

![[Main-Map-Import.png]]

<br>

---

<br>

#### Add TileMap Node

Add a TileMap node to the `Main` 2D Scene Node by right clicking and selecting `Add Child Node...` or by pressing `Ctrl + A` while the Main node is selected:

![[Add-TileMap-Node.png]]

<br>

This will add the child node under `Main` called `TileMap`.

<br>

---

<br>

#### Create A Tile Set

With the `TileMap` node selected, click on the `Tile Set` dropdown for the `TileMap` properties in the `Inspector`, and select `New TileSet`.

![[Create-New-TileSet.png]]

<br>

Now set the size of the Tile Set `x` and `y` values to the size from the asset pack (32x32):

![[Set-32-32-Size.png]]

<br>

In the bottom toolbar, select the `TileSet` tab:

![[TileSet-Tab.png]]

<br>

Now drag the `tx-tileset-ground` asset into the `Tiles` box indicated by the darker color. If you recieve a popup asking if you want to automatically create tiles in the atlas, choose `Yes`.

You should now see something that looks like this (NOTE: The `Texture Region Size` values in the `Atlas` should also be `32` and `32` for the `x` and `y` respectively).

![[TileSet-Import.png]]

<br>

---

<br>

#### Add Tile Collision

In the `Inspector` tab, expand the `Physics Layers` and click the `Add Element` button to add a new physics layer:

![[Add-TileSet-Physics-Layer.png]]

This should now display a `Collision Layer` and a `Collision Mask` section with layer `1` selected for both.

<br>

In the `TileSet` tab in the bottom toolbar, Press the `Select` button between `Setup` and `Paint`, and select the tile(s) that you want to have collision for. Expand the `Physics > Physics Layer 0` dropdown to affect the collision for the selected tile:

![[Add-Tile-Collision.png]]

<br>

You can now select the menu button (three vertical dots) to `Reset To Default Tile Shape` or press `F` to add a collision across the whole tile (This should place a red square across the tile). 

> Note: You can also modify the collision in more detail using the various options to fit your needs.

Repeat this step for each tile by selecting them manually and adding the desired collision.

<br>

---

<br>

#### Add TileMap Layers

To add more depth to the game, we need to add layers, which dictate which elements are in front or behind other elements.

To add layers, expand the `Layers` dropdown in the `Inspector` window, which will expose the default layer for the TileMap.

Give the default layer the name `BG` to indicate it is the background layer and keep the `Z Index` set to `0`.

Click the `Add Element` button to add a new Layer, and name it `Collision` for all elements that have collision and set the `Z Index` to `1`.

Next repeat the process for a `FG` (foreground) layer and give it a `Z Index` of `2`.

The layers should now look like this:

![[Add-TileMap-Layers.png]]

> NOTE: The layers should now be visible in the `TileMap` tab in the bottom toolbar.

<br>

---

<br>

#### Design The Map

This part is personal preference, but make sure to assign the correct tiles to the correct layers. 

For example, I am using the solid color tile for the `BG` layer to cover the whole background, and will be placing the tiles with collision on the `Collision` layer.

The finished design looks something like this:

![[Map-Design-Layout.png]]