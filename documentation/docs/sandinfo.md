### [Autoload Script](https://docs.godotengine.org/en/latest/tutorials/scripting/singletons_autoload.html)
# SandInfo
**Inherits:** [Object](https://docs.godotengine.org/en/stable/classes/class_object.html#class-object)

----------------------------------

This [Autoload script](https://docs.godotengine.org/en/latest/tutorials/scripting/singletons_autoload.html) is where the `Cell` and `Chunk` classes are defined and stored, as well as the plugin version and some static element information.

<br>

-----------------------------------

### Static Methods
| Return Type | Method |
| ------ | -------- |
| ElementStorage | [GetElementResource()](#elementstorage-getelementresource) |
| void | [SaveElementStorage()](#void-saveelementstorage) |
| Array[StringName] | [GetElementFlags()](#arraystringname-getelementflags) |
| Array[String] | [GetElementFlagsAsString()](#arraystring-getelementflagsasstring) |
| int | [CellPosToChunkPos()](#int-cellpostochunkposvector2i-cellpos-int-chunksize) |
| void | [UpdateCloseChunks()](#void-updateclosechunkscell-cell-powdersimulation-simref) |
| void | [SwapCells()](#void-swapcellscell-copycell-cell-pastecell) |
| void | [OnUpdate(Cell cell, PowderSimulation simRef)](#void-onupdatecell-cell-powdersimulation-simref) |


### Properties
| Type | Property |
| -------- | --------- |
| String | [PluginVersion](#string-pluginversion) |
| Enum | [ElementTypes](#enum-elementtypes) |
| Enum | [ElementFlags](#enum-elementflags) |



### Constants
| Type | Property |
| -------- | --------- |
| String | [ElementResourcePath](#string-elementresourcepath) |
| Vector2I | [TOPLEFT](#vector2i-topleft) |
| Vector2I | [TOPMIDDLE](#vector2i-topmiddle) |
| Vector2I | [TOPRIGHT](#vector2i-topright) |
| Vector2I | [LEFTMIDDLE](#vector2i-leftmiddle) |
| Vector2I | [RIGHTMIDDLE](#vector2i-rightmiddle) |
| Vector2I | [BOTTOMLEFT](#vector2i-bottomleft) |
| Vector2I | [BOTTOMMIDDLE](#vector2i-bottommiddle) |
| Vector2I | [BOTTOMRIGHT](#vector2i-bottomright) |

-------------------------------------------

### Static Method Descriptions

### `ElementStorage` GetElementResource()

Returns the current ElementStorage resource where all element information is stored.

<br>

--------------------------------------------

### `void` SaveElementStorage()

Saves the current ElementStorage resource to [ElementResourcePath](#string-elementresourcepath).

<br>

--------------------------------------------

### `Array[StringName]` GetElementFlags()

Returns [ElementFlags](#enum-elementflags) as a Godot Array of StringNames.

<br>

--------------------------------------------

### `Array[String]` GetElementFlagsAsString()

Returns [ElementFlags](#enum-elementflags) as a Godot Array of Strings.

<br>

--------------------------------------------

### `int` CellPosToChunkPos(`Vector2I` cellPos, `int` chunkSize)

> - `Vector2I cellPos` - The local simulation position of the cell to convert.
> - `int chunkSize` - The size of the axis of a single chunk, e.g. 64.

Returns `cellPos` translated into its local chunk index (aka the index of the cell inside the chunks's cell array).

<br>

--------------------------------------------

### `void` UpdateCloseChunks(`Cell` cell, `PowderSimulation` simRef)

> - `SandInfo.Cell cell` - The cell to use to find the correct chunk to update.
> - [`PowderSimulation`](powdersimnode.md) `simRef` - A reference to the [PowderSimulation](powdersimnode.md) Node for the current simulation.

If `Cell` is on the edge of its chunk, wakes the chunk nearest to the cell.

<br>

--------------------------------------------

### `void` SwapCells(`Cell` copyCell, `Cell` pasteCell)

> - `SandInfo.Cell copyCell` - The first cell to swap.
> - `SandInfo.Cell pasteCell` - The second cell to swap.

Swaps the variables necessary to carry ove when moving cells. Parameter order does not matter.

<br>

--------------------------------------------

### `void` OnUpdate(`Cell` cell, `PowderSimulation` simRef)

> - `SandInfo.Cell cell` - The cell to update.
> - [`PowderSimulation`](powdersimnode.md) `simRef` - A reference to the [PowderSimulation](powdersimnode.md) Node for the current simulation.

Runs the reactions, and then the movement of the specified cell in the simulation.

<br>

--------------------------------------------

--------------------------------------------

### Property Descriptions

### `String` PluginVersion

The current version of this plugin being used.

-------------------------------------------

### `Enum` ElementTypes

The possible types an element can be classified as.

| Values | Description |
| --------- | -------- |
| STATIC | An unmoving element. |
| SOLID | A moving element that can pass through LIQUID and GAS elements. |
| LIQUID | A moving element that can pass through GAS elements. |
| GAS | A moving element that cannot pass through any element types. |

-------------------------------------------

### `Enum` ElementFlags

The possible flags an element can have attached to it to give it special interactions and properties.

| Values | Description |
| --------- | -------- |
| FLAMMABLE | This element can be set on fire. |
| ACID_RESISTANT | This element cannot be destroyed by the ACID default element. |
| INDESTRUCTIBLE | This element cannot be destroyed by another element as part of its reaction. |

-------------------------------------------

-------------------------------------------

### Constant Descriptions

### `String` ElementResourcePath
 = `"res://addons/powder_engine/PowderedWorldEngine/ElementData.tres"`

The path to the saved ElementStorage resource in the FileSystem.

-------------------------------------------

### `Vector2I` TOPLEFT
 = `Vector2I(-1, -1)`

The vector to add to the position of a cell to find its top-left neighbor.

-------------------------------------------

### `Vector2I` TOPMIDDLE
 = `Vector2I(0, -1)`

The vector to add to the position of a cell to find its top-middle neighbor.

-------------------------------------------

### `Vector2I` TOPRIGHT
 = `Vector2I(1, -1)`

The vector to add to the position of a cell to find its top-right neighbor.

-------------------------------------------

### `Vector2I` LEFTMIDDLE
 = `Vector2I(-1, 0)`

The vector to add to the position of a cell to find its left-middle neighbor.

-------------------------------------------

### `Vector2I` RIGHTMIDDLE
 = `Vector2I(1, 0)`

The vector to add to the position of a cell to find its right-middle neighbor.

-------------------------------------------

### `Vector2I` BOTTOMLEFT
 = `Vector2I(-1, 1)`

The vector to add to the position of a cell to find its bottom-left neighbor.

-------------------------------------------

### `Vector2I` BOTTOMMIDDLE
 = `Vector2I(0, 1)`

The vector to add to the position of a cell to find its bottom-middle neighbor.

-------------------------------------------

### `Vector2I` BOTTOMRIGHT
 = `Vector2I(1, 1)`

The vector to add to the position of a cell to find its bottom-right neighbor.

-------------------------------------------
