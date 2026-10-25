# Cell Class Functions

**Defined In:** [SandInfo](sandinfo.md)

-----------------------

`SandInfo.Cell` is a class that is used to represent every active cell in the simulation. It contains helper functions that are very useful when making custom behaviors (see [Making Custom ElementBehaviors](Tutorials/making_custom_elementbehaviors.md)) or just interacting with cell objects.

### Getting/Setting Properties

| Return Type | Function |
| ---- | ------ |
| void | [SetElement()](#void-setelementallelements-to) |
| void | [SetField()](#void-setfieldstring-fieldname-byte-setto) |
| byte | [GetField()](#byte-getfieldstring-fieldname) |
| void | [ReplaceTypeAttributesWithDefault()](#void-replacetypeattributeswithdefault) |

### Finding Neighbors

| Return Type | Function |
| ---- | ------ |
| Cell? | [SearchNeighborElements()](#cell-searchneighborelementspowdersimulation-simref-allelements-targetelement-bool-opposite-false-int-targetamount-1-allelements-secondarytarget-null) |
| Cell? | [GetNeighbor()](#cell-getneighborvector2i-neighbor-powdersimulation-simref) |

### Movement

| Return Type | Function |
| ---- | ------ |
| bool | [CanMove()](#bool-canmovecell-neighborcell) |
| bool | [TryMove()](#bool-trymovevector2i-toneighbor-powdersimulation-simref) |

--------------------

## Method Descriptions

### `void` SetElement([`AllElements`](elements.md) to)

> - [`AllElements`](elements.md) to - The element to assign to the cell.

Sets this cell's Element while marking it updated on this cell's chunk. Marking a cell updated makes sure it sends the updated information to the renderer at the end of the current tick.

<br>

------------------------------

### `void` SetField(`string` FieldName, `byte` SetTo)

> - `string` FieldName - The name of the field to access. Include prefixes like `R#`.
> - `byte` SetTo - The number to set the field to.

Sets a specified field to a specified value. Also clamps the value to a range of (0, 255).

<br>

------------------------------

### `byte` GetField(`string` FieldName)

> - `string` FieldName - The field whose value to return. Include prefixes like `R#`.

Returns the specified field's value.

<br>

------------------------------

### `void` ReplaceTypeAttributesWithDefault()

Reverts all changes to this cell's fields and generates new starting fields.

<br>

------------------------------

### `Cell?` SearchNeighborElements(`PowderSimulation` simRef, `AllElements` targetElement, `bool` opposite `= false`, `int` targetAmount `= 1`, `AllElements?` SecondaryTarget `= null`)

> - [`PowderSimulation`](powdersimnode.md) simRef - A reference to the PowderSimulation node this cell is a part of.
> - `AllElements` targetElement - The element to look for.
> - `bool` opposite `= false` - whether to look for any element other than `targetElement` when true, or to look for `targetElement` when false.
> - `int` targetAmount `= 1` - The amount of neighbors needed to fulfill the condition. *Ex. if targetAmount is 2, it will look for 2 neighbors with the targetElement.*
> - `AllElements?` SecondaryTarget `= null` - A secondary target that will also fulfill the condition.

Iterates over this cell's neighbors and returns the cell it stops on when the condition defined by the parameters is true.

<br>

------------------------------

### `Cell?` GetNeighbor(`Vector2I` neighbor, `PowderSimulation` simRef)

> - `Vector2I` neighbor - The transformation applied to this cell's Position to get the neighbor cell from. Use [SandInfo](sandinfo.md)'s constants like TOPLEFT or TOPRIGHT for better readability.
> - [`PowderSimulation`](powdersimnode.md) simRef - A reference to the PowderSimulation node this cell is a part of.

Returns the neighbor cell specified in `neighbor`, and `null` if the neighbor doesn't exist (is past the edge of the simulation).

<br>

------------------------------

### `bool` CanMove(`Cell` NeighborCell)

> - `Cell` NeighborCell - The cell to check whether it can move to it or not.

This is called in TryMove() so if you are just moving the cell, you do not need to call this.
<br><br>
Returns whether the cell can move or not, **only** comparing the `Cell.Attributes.Type` of both cells.

<br>

------------------------------

### `bool` TryMove(`Vector2I` toNeighbor, `PowderSimulation` simRef)

> - `Vector2I` toNeighbor - The transform applied to this cell's Position to get the neighbor cell from. Use [SandInfo](sandinfo.md)'s constants like TOPLEFT or TOPRIGHT for better readability.
> - [`PowderSimulation`](powdersimnode.md) simRef - A reference to the PowderSimulation node this cell is a part of.

Attempts to move this cell to one of its neighbors.
<br><br>
Returns whether the move was successful or not.

<br>

------------------------------