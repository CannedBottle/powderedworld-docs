# The Element Creator Tab

In this tutorial, you will learn how to use the Element Creator Tab in the editor to create and edit elements and their basic properties.

-----------------------------

## Sections

* [Menu Overview](#menu-overview)

-----------------------------

## Menu Overview

![The element creator editor tab.](img\element editor tab.png)

This menu contains all the tools needed to edit the basic properties and reactions of elements, as well as add your own.
Here are brief descriptions of each button/field and what they do:
<br>

| **Field Name** | **Description** |
| --------- | ---------- |
| Element To Edit | The element currently being edited. Select "+ Add Element" to create a new element. |
| Element Name | The name of the element. This is the name reflected in the `AllElements` enum and everywhere else the element is referenced. |
| Element Type | [Element Types](#element-types) |
| Movement Preset | [Movement Presets](#movement-presets) |
| Reactions | [Reactions](#reactions) |
| Flags | [Flags](#flags) |
| Base Color | The base color of the element when displayed in game. |
| Noise Strength | The strength of the random brightness effect applied to the element's Base Color. Ranges from 0-1, with 1 equal to fully random brightness, and 0 is a flat, unchanging color. |
| Apply Changes | This is the button that, when pressed, saves all your changes in the `ElementData` file included in the plugin and generates the `AllElements` Enum. Your changes will not be in effect unless you press this button. |
| Delete Current Element | Deletes the selected element. You cannot delete default elements. Make sure there are no references of the element in your code before this, since the enum entry will be deleted as well. |
| Reset Defaults | Deletes all elements and replaces them with the original set. The original set is all the elements included when you initially download the plugin. |

--------------------------


<br>
# Extra Field Descriptions

## Element Types

**An element's Type defines which elements can pass through each other when moving.** Here is the list of types and what they define:

| Type | Can Pass Through |
| ----------- | ------------ |
| STATIC | Does not move |
| SOLID | LIQUID, GAS |
| LIQUID | GAS |
| GAS | None |

--------------------------

## Movement Presets

**An element's Movement Preset defines its behavior and how it moves in the simulation.** Here is the list of movement presets and what movement they use:

| Movement Preset | Movement Description |
| ----------- | ------------ |
| NONE | No movement |
| SAND | Moves down if nothing is blocking it, otherwise moves diagonally down either left or right |
| LIQUID | Same as SAND if nothing is blocking, otherwise moves left or right. Changes directions when hitting another element. |
| STONE | Moves down if nothing is blocking it, **and** only if there are less than two elements directly to the left or right of it. |
| GAS | The same as LIQUID, but upside-down. |
| CUSTOM | Uses the movement defined in the `ElementBehavior` assigned to it. See [Making Custom ElementBehaviors](making_custom_elementbehaviors.md) for more information. |

--------------------------

## Reactions

The reaction editor lets you create simple reactions with other elements without having to use custom ElementBehaviors. 
> *The order of reactions in the Reactions menu is the order they will be executed in. This can sometimes affect the element's intended interaction.*

![the reaction editor.](img\reaction editor tab.png)

It contains a 3 sections:

* [Marked Neighbors](#marked-neighbors)
* [Condition](#condition)
* [Effect](#effect)


### Marked Neighbors

The Marked Neighbors are the cells adjacent to the updating cell that get checked against the condition. Click on the buttons around the center cell to mark that corresponding neighbor.

### Condition

The condition section includes all UI under the `(Condition)` parentheses, and before the `(Effect)` parentheses. <br>
The reaction loops around all Marked Neighbors and checks them against a condition defined here. <br>
**The condition has three parts as well:** The comparison, the amount, and the element to look for. <br>
The comparison can either `==`, `>=`, or `<`. The element to look for can either be a single element, or Any (any non-AIR element) with exclusions. The comparison basically is you making an if-statement;
for example, if the comparison is `>=`, the amount is `2`, and the element is `SAND`, it would work like this: <br>
```
var sand_neighbors: int

if sand_neighbors >= 2:
    do_effect()
```
Where `sand_neighbors` is the number of Marked Neighbors that are currently SAND.

### Effect
> [Element] refers to the `Replace With` option under Effect Options.

The effect section has four options for effect types:

| Effect Type | Description |
| ----------- | ------------ |
| Replace element with [Element]                | Replaces the currently updating cell with [Element] |
| Replace All Neighbors with [Element]          | Replaces every adjacent cell with [Element] |
| Replace Marked Neighbors with [Element]       | Replaces all adjacent cells that are marked in the Marked Neighbors section with [Element] |
| Replace Last Iterated Neighbor with [Element] | When running a reaction, all the marked cells get iterated over. This option replaces the cell the iterator stopped on when the condition became `true` with [Element]. *If no MarkedNeighbors are assigned, this will return the updating cell.* |

--------------------------

## Flags

Adding flags to an element is a quick way to add unique features to said element.

![The element flag menu.](img\flag_reaction_tab.png)

There are currently two flags available to use on any element:

| Flag Name | Description |
| --------- | ------------ |
| INDESTRUCTIBLE | Makes the element unchangable by anything other than itself. <br> <br> *If a reaction from a different element adjacent to it would change it, it does not get changed. On the other hand, if it gets changed by its own reaction, it still gets changed.* |
| FLAMMABLE | Allows the element to be set on fire when adjacent to a cell with the FIRE element. [It has some configurable properties.](#flammable-properties) |


### FLAMMABLE Properties

![The flammable options.](img\flammable_options.png)

> These properties appear only when the element has the FLAMMABLE flag.

| Propery Name | Description |
| ------ | ------- |
| Burn Speed | How long, in seconds, it takes for the element to burn completely. *(if it is already on fire)* |
| Spread Resistance | The percent chance, from 0.0-1.0, for the element to resist being caught on fire every time a FIRE cell reacts with it. <br><br> *This should be on the higher end if you want visible changes, since it usually attempts to be set on fire very frequently.* |
