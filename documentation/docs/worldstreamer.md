# WorldStreamer 
**Inherits:** [RefCounted](https://docs.godotengine.org/en/stable/classes/class_refcounted.html) < [Object](https://docs.godotengine.org/en/stable/classes/class_object.html)

-----------------

This class is what you will use for saving and loading 

<br><br>

***NOTE:** This class defines an override for `_Notification()`, so if you are extending this class and using those functions, make sure to include `super()` or the C# equivalent in it so it still calls the parent class functions as well as whatever you put.*
<br>

-----------------
### Static Methods
| Return Type | Method |
| ------ | -------- |
| [WorldStreamer](worldstreamer.md) | [Open()](#worldstreamer-openstring-worldpath-powdersimulation-simulation) |
| [WorldStreamer](worldstreamer.md) | [Create()](#worldstreamer-createstring-worlddirpath-string-filename-powdersimulation-simulation) |
| string | [SaveEmpty()](#string-saveemptystring-name-string-path) |
| bool | [IsFileUsable()](#bool-isfileusablestring-path) |



### Public Methods
| Return Type | Method |
| ------ | -------- |
|unwritten desc|
| void | [Close()](#void-close) |
| bool | [FlushDeadChunks()](#bool-flushdeadchunks) |
| void | [SaveWorld(bool Override)](#void-saveworldbool-override) |
| bool | [LoadWorld()](#bool-loadworld) |
| void | [SaveChunk(Sandinfo.Chunk chunk)](#void-savechunksandinfochunk-chunk) |
| void | [UnloadChunk(SandInfo.Chunk chunk)](#void-unloadchunksandinfochunk-chunk) |
| bool | [LoadChunk(Vector2I ChunkPosition)](#bool-loadchunkvector2i-chunkposition) |
| Array[Vector2I] | [GetAvailableChunks()](#arrayvector2i-getavailablechunks) |




### Properties
| Type | Property |
| -------- | --------- |


---------------------------------

### Static Method Descriptions

### [`WorldStreamer`](worldstreamer.md) Open(`string` WorldPath, [`PowderSimulation`](powdersimnode.md) Simulation)

> - `string WorldPath` - The path to the file to open. must point to a file with the `.pwdr` extension.
> - [`PowderSimulation`](powdersimnode.md) `Simulation` - The simulation node for this [WorldStreamer](worldstreamer.md) instance to save and load from.

Creates a new WorldStreamer object and assigns it the specified file. `WorldPath` must point to an existing file with the `.pwdr` extension.

> Returns a new `WorldStreamer` object if the file is usable; otherwise returns `null`.

<br>

--------------------------------------------

### [`WorldStreamer`](worldstreamer.md) Create(`string` WorldDirPath, `string` FileName, [`PowderSimulation`](powdersimnode.md) Simulation)

> - `string WorldDirPath` - The path to the folder for this file to be saved in. Usually starts with `user://`. **Must** end with `/`
> - `string FileName` - The name for the new file to be called. The extension is automatically attached, so no need to add `.pwdr` to the end of this parameter.
> - [`PowderSimulation`](powdersimnode.md) `Simulation` - The simulation node for this [WorldStreamer](worldstreamer.md) instance to save and load from.

Creates a new WorldStreamer object and a fresh `.pwdr` file with the given `FileName` assigned to it. `WorldDirPath` must point to a directory in which the file can be created.
<br>**FileName MUST be different than an already existing file. Otherwise it opens the existing file.**

> Returns a new `WorldStreamer` object if the filename and directory path are usable; otherwise returns `null`.

<br>

--------------------------------------------

### `string` SaveEmpty(`string` Name, `string` Path)

> - `string Name` - The name to be given to the newly created file. The file extension is automatically attached, so no need to add `.pwdr` to the end of this parameter.
> - `string Path` - The path to the folder for this file to be saved in. Usually starts with `user://`. **Must** end with `/`

Creates an empty save file. `Path` must point to a directory in which the new file can be added to. `Path` also must end with `/`.

> Returns the path to the newly created file.

<br>

--------------------------------------------

### `bool` IsFileUsable(`string` Path)

> - `string Path` - The path to the file to check.

Returns whether the given file correctly contains the key and the correct file extension. Basically whether or not the save is initially valid.

<br>

--------------------------------------------


### Method Descriptions

### `void` FillWorld(AllElements with)

Replaces every cell in the current world with the element specified in `with`. 

<br>

--------------------------------------------