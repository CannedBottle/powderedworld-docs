# Elements
**Inherits:** [Resource](https://docs.godotengine.org/en/stable/classes/class_resource.html) < [RefCounted](https://docs.godotengine.org/en/stable/classes/class_refcounted.html) < [Object](https://docs.godotengine.org/en/stable/classes/class_object.html)

-----------------

This class is made from autogenerating a script from strings so an element enum can be dynamically changed when interacting with the element creation editor tab.
<br>
It contains the AllElements Enum and a few helper functions.


### Static Methods
| Return Type | Method |
| -------- | ---------- |
| Array[StringName] | [GetElementNames()](#arraystringname-getelementnames) |
| [AllElements](#enum-allelements) | [GetFromName(StringName name)](#allelements-getfromnamestringname-name) |



### Properties
| Type | Property |
| -------- | --------- |
| Enum | [AllElements](#enum-allelements) |

------------------------------------

### Static Method Descriptions

### `Array[StringName]` GetElementNames()

Returns a Godot Array of all of the existing elements in [AllElements](#enum-allelements) as StringNames.

-----------------------------------

### [`AllElements`](#enum-allelements) GetFromName(`StringName` name)

> - `StrigName name` - The name of the element to get the enum equivalent of.

Returns the [AllElements](#enum-allelements) equivalent of `name`.

> *Ex. GetFromName(&"SAND") would return AllElements.SAND.*

-----------------------------------

-----------------------------------

### Property Descriptions

### `Enum` AllElements

An Enum containing every element created in the Element Editor tab. Dynamically changed when the Apply Changes button in the element tab is pressed.

It has some default values:

| Value |
| --------- |
| AIR |
| SAND |
| WATER |
| ACID |
| STONE |
| WALL |
