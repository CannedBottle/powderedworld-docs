# PowderSimulation
**Inherits:** [Node2D](https://docs.godotengine.org/en/stable/classes/class_node2d.html) < 
[CanvasItem](https://docs.godotengine.org/en/stable/classes/class_canvasitem.html#class-canvasitem) < 
[Node](https://docs.godotengine.org/en/stable/classes/class_node.html#class-node) < 
[Object](https://docs.godotengine.org/en/stable/classes/class_object.html#class-object)

--------------------------------

This node is what you will use to handle individual simulations. It could be called an "orchestrator" class for the simulation, as it does not define the base
chunk or cell classes, but simply contains them and tells them what to do. It also contains useful methods for maniplulating the world, such as placing elements or clearing all cells.

<br><br>

***NOTE:** This node defines `_Ready()` and `_Draw()`, so if you are attaching a script to this node and using those functions, make sure to include `super()` in it so it still calls the parent class functions as well as whatever you put.*
<br>

-------------------------------

### Public Methods
| Return Type | Method |
| ------ | -------- |
| void | [FillWorld()](#void-fillworldallelements-with) |
| void | [ClearWorld()](#void-clearworld) |
| bool | [PlaceElement()](#bool-placeelementvector2i-pos-allelements-element-bool-override-false) |
| void | [PlaceGroupElements()](#void-placegroupelementsint-brushsize-vector2i-pos-allelements-element-bool-override-false) |
| Vector2I | [WorldToLocal()](#vector2i-worldtolocalvector2-from_world) |
| Vector2 | [LocalToWorld()](#vector2-localtoworldvector2i-fromlocal-bool-includeparentoffset-true) |
| void | [SetWorldStreamer()](#void-setworldstreamerworldstreamer-newstreamer) |
| [WorldStreamer](worldstreamer.md) | [GetWorldStreamer()](#worldstreamer-getworldstreamer) |
| [SandInfo.Chunk](sandinfo.md) | [GetChunk()](#sandinfochunk-getchunkvector2i-pos) |
| bool | [SimContainsCell()](#bool-simcontainscellvector2i-pos) |
| bool | [SimContainsChunk()](#bool-simcontainschunkvector2i-pos) |
| void | [SetFollowMode()](#void-setfollowmodebool-to) |
| void | [SetFollowNode()](#void-setfollownodenode2d-what) |
| void | [SetConstraints()](#void-setconstraintsvector2-to) |
| Vector2 | [ChunkLocalToWorld()](#vector2-chunklocaltoworldvector2i-fromlocal-bool-includeparentoffset-true) |
| Vector2I | [LocalToChunk()](#vector2i-localtochunkvector2i-localpos) |
| Vector2I | [WorldToChunk()](#vector2i-worldtochunkvector2-worldpos) |
| void | [QueueSwap()](#void-queueswapsandinfocell-cell1-sandinfocell-cell2) |
| void | [CommitSwapQueue()](#void-commitswapqueue) |
| bool | [AddChunk()](#bool-addchunkvector2i-at) |
| bool | [RemoveChunk()](#bool-removechunkvector2i-at) |
| void | [InitGrid()](#void-initgrid) |
| void | [UpdateChunks(int tick)](#void-updatechunksint-tick) |
| void | [DecideSleepingChunks()](#void-decidesleepingchunks) |
| void | [RenderChunkUpdates()](#void-renderchunkupdates) |
| void | [UpdateSimulationSize()](#void-updatesimulationsize) |
| void | [UpdateSimulation()](#void-updatesimulationbool-wait-true) |
| [SandInfo.Cell](sandinfo.md) | [GetCell()](#sandinfocell-getcellvector2i-pos) |
| void | [SetCell(Vector2I pos, AllElements element)](#void-setcellvector2i-pos-allelements-element) |



### Properties
| Type | Property |
| -------- | --------- |


---------------------------------

### Method Descriptions

### `void` FillWorld(`AllElements` with)

Replaces every cell in the current world with the element specified in `with`. 

<br>

--------------------------------------------

### `void` ClearWorld()

Replaces every cell in the current world with `AllElements.AIR`. Functionally equivalent to calling `FillWorld(AllElements.AIR)`.

<br>

--------------------------------------------

### `Vector2I` WorldToLocal(`Vector2` from_world)
> - `Vector2 from_world` - the world-space coordinates to find the closest element from. world-space is the same as global_position for Nodes.

Returns the given cell world position (Godot's regular `global_position` for nodes) translated into local simulation position.

<br>

---------------------------------------------

### `Vector2` LocalToWorld(`Vector2I` fromLocal, `bool` includeParentOffset `= true`)
> - `Vector2I fromLocal` - the local-space coordinates to translate to world-space.
> - `bool includeParentOffset` - Whether or not to include the offset of the `PowderSimulation` parent Node in the calculation.

Returns the given chunk local simulation position translated into world position. <br>

<br>

--------------------------------------------

### `bool` PlaceElement(`Vector2I` pos, `AllElements` element, `bool` overRide = false)

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

### `void` PlaceGroupElements(`int` brushSize, `Vector2I` pos, `AllElements` element, `bool` overRide `= false`)

> - `int brushSize` - the amount the square placement pattern expands in all four directions.

Calls [PlaceElement](#bool-placeelementvector2i-pos-allelements-element-bool-override-false) repeatedly in a square pattern which starts at `pos` and expands outward `brushSize` times.

> *Ex. `brushSize` = 0 will place a single element, and `brushsize` = 1 will place a group of nine elements, starting from `pos` and extending 1 cell in all four directions.*

<br>

--------------------------------------------

### `void` SetWorldStreamer(`WorldStreamer` NewStreamer)

> - `WorldStreamer NewStreamer` - The [WorldStreamer](worldstreamer.md) instance to assign.

Assigns a WorldStreamer object to the simulation. When assigned, using FollowMode will save/load chunks using the WorldStreamer object. Set to `null` to disable this behavior.

<br>

--------------------------------------------

### [`WorldStreamer`](worldstreamer.md) GetWorldStreamer()

Returns the current WorldStreamer instance attached to this node.

<br>

--------------------------------------------

### `void` GetChunk(`Vector2I` pos)

> - `Vector2I pos` - The position to search for a chunk.

Returns the chunk currently at `pos`. Throws an error if there is no chunk at `pos`.

<br>

--------------------------------------------

### `bool` SimContainsCell(`Vector2I` pos)

> - `Vector2I pos` - The position to search for a cell.

Returns Whether the given `pos` corresponds to a cell in the simulation.

<br>

--------------------------------------------

### `bool` SimContainsChunk(`Vector2I` pos)

> - `Vector2I pos` - The position to search for a chunk.

Returns Whether the given `pos` corresponds to a chunk in the simulation.

<br>

--------------------------------------------

### `void` SetFollowMode(`bool` to)

> `bool to` - The boolean to set `FollowEnabled` to.

Sets `FollowEnabled` to `to`.

<br>

--------------------------------------------

### `void` SetFollowNode(`Node2D` what)

> `Node2D what` - The node to set `FollowNode` to.

Sets the node for the simulation to follow. If `FollowEnabled` is set to `true`, the simulation uses the Node2D's position to determine where the constraints are centered.

<br>

--------------------------------------------

### `void` SetConstraints(`Vector2` to)

> `Vector2 to` - What to set the constraints to.

Sets the constraints for the simulation. If `FollowEnabled` is set to `true`, the simulation auto loads/unloads chunks to fill the range ± `to`.

<br>

--------------------------------------------

### `Vector2` ChunkLocalToWorld(`Vector2I` fromLocal, `bool` includeParentOffset `= true`)

> `Vector2I fromLocal` - The local chunk position in which to transform.
> `bool includeParentOffset` - Whether or not to include the offset of the the parent node in the calculation. For example, if the position of the chunk is (32, 32) and the
 local position of this node is (10, 10) the final position will be (42, 42).

Returns the given chunk local simulation position translated into world position.

<br>

--------------------------------------------

### `Vector2I` LocalToChunk(`Vector2I` localPos)

> `Vector2I localPos` - The local simulation position (position of a cell) to convert to chunk position.

Returns the local simulation position to chunk coordinates. Truncates decimals toward zero. Used for finding a cell's chunk from just the position.

<br>

--------------------------------------------

### `Vector2I` WorldToChunk(`Vector2` worldPos)

> `Vector2I worldPos` - The world position (same as global_position for Node2Ds) converted to local chunk position.

Returns the given global (world) position converted to local chunk position.

<br>

--------------------------------------------

### `void` QueueSwap(`SandInfo.Cell` Cell1, `SandInfo.Cell` Cell2)

> `SandInfo.Cell Cell1` - The first cell to swap.
> `SandInfo.Cell Cell2` - The second cell to swap.

Adds two cells to list of cells to be swapped at the end of the frame.

<br>

--------------------------------------------

### `void` CommitSwapQueue()

Writes all the buffered swaps onto the simulation.

<br>

--------------------------------------------

### `bool` AddChunk(`Vector2I` at)

> `Vector2I at` - The chunk position at which the new chunk will be created.

Adds an empty chunk at the specified coordinates.
<br><br>
Returns whether or not the chunk was successfully added.

<br>

--------------------------------------------

### `bool` RemoveChunk(`Vector2I` at)

> `Vector2I at` - The chunk position at which the chunk will be removed.

Removes the chunk at the specified coordinates.
<br><br>
Returns whether there was a chunk at the specified position or not.

<br>

--------------------------------------------

### `void` InitGrid()

Populates the grid with Chunk and Cell objects set to the correct default state. One of the functions called in this node's _Ready() function.

<br>

--------------------------------------------

### `void` UpdateChunks(`int` tick)

> `int tick` - The elapsed frame, mod by two (constrained to 0 and 1). Changes update direction based on the current tick, making the simulation less one-sided.

Updates the cells in all the chunks of the simulation, sending them to the swap buffer. Automatically called in [UpdateSimulation()](#void-updatesimulationbool-wait-true).

<br>

--------------------------------------------

### `void` DecideSleepingChunks()

Updates the sleep state of each chunk in the simulation decided by their insomnia count.
<br><br>
There are currently no functions that require this to be called as [UpdateChunks()](#void-updatechunksint-tick) does it itself.

<br>

--------------------------------------------

### `void` RenderChunkUpdates()

Loops through each chunk and sends its cell data to its respective ChunkRenderer.

<br>

--------------------------------------------

### `void` UpdateSimulationSize()

Updates the simulation_size variable if chunk grid size has been changed. This is automatically done, so no need to call this.

<br>

--------------------------------------------

### `void` UpdateSimulation(`bool` wait `= true`)

> `bool wait` - Whether or not to check if the correct amount of time has passed specified in `SimulationSpeed`, and if not, does not call the function.

Updates the simulation while being safe to put in `_Process`/`_PhysicsProcess` because if `wait` is set to `true`, it will not tick until the right amount of time has passed specified in `SimulationSpeed`. 
If `wait` is set to `false`, runs one tick of the simulation regardless.

<br>

--------------------------------------------

### [`SandInfo.Cell`](sandinfo.md) GetCell(`Vector2I` pos)

> `Vector2I pos` - The position to get the cell from.

Returns the cell at the specified `pos`. Throws an error if a cell does not exist at `pos`.

<br>

--------------------------------------------

### `void` SetCell(`Vector2I` pos, `AllElements` element)

> `Vector2I pos` - The position to get the cell for editing.
> `AllElements element` - The element to change the cell to.

Replaces the element at `pos` with `element`.

<br>

--------------------------------------------