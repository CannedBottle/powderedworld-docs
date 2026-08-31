# PowderSimulation
**Inherits:** [Node2D](https://docs.godotengine.org/en/stable/classes/class_node2d.html) < 
[CanvasItem](https://docs.godotengine.org/en/stable/classes/class_canvasitem.html#class-canvasitem) < 
[Node](https://docs.godotengine.org/en/stable/classes/class_node.html#class-node) < 
[Object](https://docs.godotengine.org/en/stable/classes/class_object.html#class-object)

--------------------------------

This node is what you will use to handle individual simulations. It could be called an "orchestrator" class for the simulation, as it does not define the base
chunk or cell classes, but simply contains them and tells them what to do. It also contains useful methods for maniplulating the world, such as placing elements or clearing all cells.

<br>

-------------------------------

### Public Methods
| Return Type | Method |
| ------ | -------- |
| `void` | [FillWorld(AllElements with)](#void-fillworldallelements-with) |
| `void` | [ClearWorld()](#void-clearworld) |
| `void` | [PlaceElement(Vector2I pos, AllElements element, bool overRide = false)](#bool-placeelementvector2i-pos-allelements-element-bool-override-false) |
| `void` | [PlaceGroupElements(Vector2I pos, AllElements element, bool overRide = false)](#void-placegroupelementsint-brushsize-vector2i-pos-allelements-element-bool-override-false) |
| `Vector2I` | [WorldToLocal(Vector2 from_world)](#vector2i-worldtolocalvector2-from_world) |
| `Vector2` | [LocalToWorld(Vector2I fromLocal, bool includeParentOffset = true)](#vector2-localtoworldvector2i-fromlocal-bool-includeparentoffset-true) |


### Properties
| Type | Property |
| -------- | --------- |


---------------------------------

### Method Descriptions

### `void FillWorld(AllElements with)`

Replaces every cell in the current world with the element specified in `with`. 

<br>

--------------------------------------------

### `void ClearWorld()`

Replaces every cell in the current world with `AllElements.AIR`. Functionally equivalent to calling `FillWorld(AllElements.AIR)`.

<br>

--------------------------------------------

### `Vector2I WorldToLocal(Vector2 from_world)`
> - `Vector2 from_world` - the world-space coordinates to find the closest element from. world-space is the same as global_position for Nodes.

Returns the given cell world position (Godot's regular `global_position` for nodes) translated into local simulation position.

<br>

---------------------------------------------

### `Vector2 LocalToWorld(Vector2I fromLocal, bool includeParentOffset = true)`
> - `Vector2I fromLocal` - the local-space coordinates to translate to world-space.
> - `bool includeParentOffset` - Whether or not to include the offset of the `PowderSimulation` parent Node in the calculation.

Returns the given chunk local simulation position translated into world position. <br>

<br>

--------------------------------------------

### `bool PlaceElement(Vector2I pos, AllElements element, bool overRide = false)`

> - `Vector2I pos` - the local-space coordinates to the cell where the specified element will be placed.
- `AllElements element` - the element to replace the specified cell's element with.
- `bool overRide` - if `false`, only places the specified element if the cell's element is `AIR`.

Replaces the element of the cell at `pos` with `element`. If `overRide` is set to `true`, overrides the element of the cell at `pos` regardless of what it already is. 
If `overRide` is `true`, only changes the element if the element of the cell is already `AIR`.

> Returns `true` if the placement succeeded, otherwise returns `false`.

<br>

> *Ex. `PlaceElement(Vector2I(0, 0), AllElements.SAND, true)` will replace the cell at pos `(0, 0)`'s element with `element`, regardless of the element it was beforehand because `overRide` was set to `true`.*

<br>

--------------------------------------------

### `void PlaceGroupElements(int brushSize, Vector2I pos, AllElements element, bool overRide = false)`

> - `int brushSize` - the amount the square placement pattern expands in all four directions.

Calls [PlaceElement](#bool-placeelementvector2i-pos-allelements-element-bool-override-false) repeatedly in a square pattern which starts at `pos` and expands outward `brushSize` times.

> *Ex. `brushSize` = 0 will place a single element, and `brushsize` = 1 will place a group of nine elements, starting from `pos` and extending 1 cell in all four directions.*

<br>

--------------------------------------------