# Reference

PWEngine has a variety of useful methods and properties to make your development easier. 
This page will be organized into each of the specific nodes added in this plugin, where each section contains a list with entries that describe what each function/property of the node does and how it can be used.

## `PowderSimulation` Node
--------------------------------

-------------------------------

### Methods
| Return Type | Method |
| ------ | -------- |
| `void` | [ClearWorld()](#clearworld) |
| `Elements.AllElements` | [FindClosestElementW(from_pos: Vector2)](#findclosestelementwfrom_pos-vector2) |
| `Elements.AllElements` | [FindClosestElementL(from_pos: Vector2I)](#findclosestelementlfrom_pos-vector2i) |
| `void` | [PlaceElement(Vector2I pos, AllElements element, bool overRide = false)](#placeelementvector2i-pos-allelements-element-bool-override-false) |


### Properties
| Type | Property |
| -------- | --------- |


---------------------------------

### Method Descriptions


### `void ClearWorld()`

--------------------------------------------

### `FindClosestElementW(from_pos: Vector2)`
> - `Vector2 from_pos` - the world-space coordinates to find the closest element from.

finds the closest element to the specified `from_pos`, in world space. Useful for things like dynamic footsteps.

---------------------------------------------

### `FindClosestElementL(from_pos: Vector2I)`
> - `Vector2 from_pos` - the local-space coordinates to find the closest element from.

the local-space equivalent of [`FindClosestElementW()`](#findclosestelementwfrom_pos-vector2). Local space contains the coordinates inside the simulation itself. <br>
> *Ex. `(0, 0)` corresponds to the topmost and leftmost element.*

--------------------------------------------

### `bool PlaceElement(Vector2I pos, AllElements element, bool overRide = false)`

> - `Vector2I pos` - the local-space coordinates to the cell where the specified element will be placed.
- `AllElements element` - the element to replace the specified cell's element with.
- `bool overRide` - if `false`, only places the specified element if the cell's element is `AIR`.

replaces the element of the cell at `pos` with `element`. If `overRide` is set to `true`, overrides the element of the cell at `pos` regardless of what it already is. 
If `overRide` is `true`, only changes the element if the element of the cell is already `AIR`.

--------------------------------------------

### `void PlaceGroupElements(int brushSize, Vector2I pos, AllElements element, bool overRide = false)`

> - `int brushSize` - the 

calls [PlaceElement(Vector2I pos, AllElements element, bool overRide = false)](#placeelementvector2i-pos-allelements-element-bool-override-false) repeatedly in a square pattern which starts at `pos` and expands outward `brushSize` times.

> *Ex. `brushSize` = 0 will place a single element,*