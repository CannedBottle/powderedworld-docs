# `PowderSimulation` Node
--------------------------------

This node is what you will use to handle individual simulations. It could be called an "orchestrator" class for the simulation, as it does not define the base
chunk or cell classes, but simply contains them and tells them what to do. It also contains useful methods for maniplulating the world, such as placing elements or clearing all cells.

<br>

-------------------------------

### Methods
| Return Type | Method |
| ------ | -------- |
| `void` | [FillWorld(AllElements with)](#void-fillworldallelements-with) |
| `void` | [ClearWorld()](#void-clearworld) |
| `Elements.AllElements` | [FindClosestElementW(from_pos: Vector2)](#findclosestelementwfrom_pos-vector2) |
| `Elements.AllElements` | [FindClosestElementL(from_pos: Vector2I)](#findclosestelementlfrom_pos-vector2i) |
| `void` | [PlaceElement(Vector2I pos, AllElements element, bool overRide = false)](#bool-placeelementvector2i-pos-allelements-element-bool-override-false) |
| `void` | [PlaceGroupElements(Vector2I pos, AllElements element, bool overRide = false)](#void-placegroupelementsint-brushsize-vector2i-pos-allelements-element-bool-override-false) |


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

### `FindClosestElementW(from_pos: Vector2)`
> - `Vector2 from_pos` - the world-space coordinates to find the closest element from.

Finds the closest element to the specified `from_pos`, in world space. Useful for things like dynamic footsteps.

<br>

---------------------------------------------

### `FindClosestElementL(from_pos: Vector2I)`
> - `Vector2 from_pos` - the local-space coordinates to find the closest element from.

The local-space equivalent of [`FindClosestElementW()`](#findclosestelementwfrom_pos-vector2). Local space contains the coordinates inside the simulation itself. <br>
> *Ex. `(0, 0)` corresponds to the topmost and leftmost element.*

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

Calls [PlaceElement(Vector2I pos, AllElements element, bool overRide = false)](#bool-placeelementvector2i-pos-allelements-element-bool-override-false) repeatedly in a square pattern which starts at `pos` and expands outward `brushSize` times.

> *Ex. `brushSize` = 0 will place a single element, and `brushsize` = 1 will place a group of nine elements, starting from `pos` and extending 1 cell in all four directions.*

<br>

--------------------------------------------