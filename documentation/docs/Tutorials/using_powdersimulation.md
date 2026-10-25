# Using PowderSimulation

When working with this plugin, most of the work will be done by interacting with one node: [PowderSimulation](../powdersimnode.md). With this node, you can do many things, such as edit the cells in the simulation, dynamically add/remove chunks, and more.

---------------------------

## Sections

* [Inspector Properties](../powdersimnode.md/#properties)
* [Coordinate Systems](#coordinate-systems)
* [Editing Cells](#editing-cells)
* [Chunk Addition/Removal](#chunk-additionremoval)
* [Making the Simulation Dynamically Follow any Node2D](#making-the-simulation-dynamically-follow-any-node2d)

--------------------------

## Coordinate Systems

There are 3 coordinate systems relevent to this plugin:

* World,
* Local,
* and Chunk.

The **World Coordinate system** is the regular coordinate system you're used to. It is used in regular Godot for the positioning of Node2Ds, Controls and such.
<br><br>

The **Local Coordinate system** is the coordinate system used inside the simulation of a [PowderSimulation](../powdersimnode.md) node for the positioning of **cells**. <br>
> *Ex. (0, 2) in local coords would be 2 cells down from the center of the simulation.*  

> You can use the built-in functions `WorldToLocal()`, `LocalToWorld()` and `LocalToChunk()` in the [PowderSimulation](../powdersimnode.md) node to convert between their respective coordinate systems.

<br>

The **Chunk Coordinate system** is the coordinate system used in the simulation of a [PowderSimulation](../powdersimnode.md) node for the positioning of **chunks**. <br>

> *Ex. (1, 3) in chunk coords would be 1 chunk to the right and 3 chunks down from the center chunk.*

> You can use the built-in functions `WorldToChunk()` and `LocalToChunk()` in the [PowderSimulation](../powdersimnode.md) node to convert between their respective coordinate systems. When converting, it rounds the resulting values to the nearest chunk.

------------------------------

## Editing Cells

The [PowderSimulation](../powdersimnode.md) node contains functions that let you directly add elements to the simulation as the game is running. Uses of this feature include procedural generation or letting the player place elements.
<br><br>
These are the functions that allow you to edit and get cells:

* [GetCell()](../powdersimnode.md/#sandinfocell-getcellvector2i-pos)
* [SetCell()](../powdersimnode.md/#void-setcellvector2i-pos-allelements-element)
* [PlaceElement()](../powdersimnode.md/#bool-placeelementvector2i-pos-allelements-element-bool-override-false)
* [PlaceGroupElements()](../powdersimnode.md/#void-placegroupelementsint-brushsize-vector2i-pos-allelements-element-bool-override-false)

> Note: when using `PlaceElement()` and `PlaceGroupElements()`, you can use the functions mentioned in the [Coordinate Systems](#coordinate-systems) section if you need to convert world coordinates to local coordinates.

As an example of how they can be used, this is how the placing in the Test_Playground scene works:

```

public override void _Process(double delta)
	{
		Vector2I MousePos = (Vector2I)GetGlobalMousePosition();

		// spawn elements using keys
		if(KeysPressed.Count > 0)
		{
			Sim.PlaceGroupElements(brushSize, Sim.WorldToLocal(MousePos), ElementKeys[KeysPressed[0]], ElementKeys[KeysPressed[0]] == AllElements.AIR);
		}
    }

```
`ElementKeys[KeysPressed[0]]` in this case is just the element it is trying to place.

This uses the position of the mouse, converted to local coordinates to find where to place the elements. It also only overrides other elements if the element being placed is AIR, so it functions as an eraser.

----------------------------------------

## Chunk Addition/Removal

When `FollowMode` is `false`, you can freely add or remove chunks from a simulation at any given time. Uses of this include things like expanding/shrinking the simulation, or making it follow a camera/player for optimization purposes (the latter can be done with a built-in feature, as outlined in the section [Making the Simulation Dynamically Follow any Node2D](#making-the-simulation-dynamically-follow-any-node2d)).

Adding/removing chunks can be accomplished with these functions in the [PowderSimulation](../powdersimnode.md) class:

* [AddChunk()](../powdersimnode.md/#bool-addchunkvector2i-at)
* [RemoveChunk()](../powdersimnode.md/#bool-removechunkvector2i-at)

These functions take a position in Chunk coordinates (see [Coordinate Systems](#coordinate-systems)) and either add a chunk if it does not exist, or remove a chunk if it does exist respectively.

-------------------------------------

## Making the Simulation Dynamically Follow any Node2D

This section goes over the properties in the `Follow` dropdown in the Inspector.

Setting a PowderSimulation to follow a Node2D will dynamically add/remove chunks in the simulation to fill a rectangle with a given size that wraps around a given node. 

This sacrifices your ability to manually add/remove chunks, but is useful for things like an expansive world that cannot all be loaded at the same time for performance reasons.

![The follow section of the PowderSimulation Inspector.](img\follow_section.png)

> The `Follow` section in the PowderSimulation Inspector. Notice how the `Position` of the AreaConstraint isn't used, as it will be overridden anyway.

These are the properties that can be changed in the Inspector when `FollowMode` is `true`:

* **Node:** This is the Node2D that the simulation will be constrained around.
> In this example, it is set to `Player`, which is a node that is controlled by the player. With this setup, the simulation will always be centered around this `Player` node.

* **Area Constraint:** The size of this Rect2 is used to determine the size the simulation is constrained to.
> The `Position` of this value is always overridden, so there is no point in setting it to anything.

* **Center Constraints on Followed Node:** If this is `false`, then the position of the Rect2 will be equal to the position of the followed node. Otherwise it will be equal to `Rect2.size / 2 + Node.position`.

These values can also be changed at runtime via code. The functions [`SetFollowMode()`](../powdersimnode.md/#void-setfollowmodebool-to), [`SetFollowNode()`](../powdersimnode.md/#void-setfollownodenode2d-what), and [`SetConstraints()`](../powdersimnode.md/#void-setconstraintsvector2-to) can be used to change their own respective values.
