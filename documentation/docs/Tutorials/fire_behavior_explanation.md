# FireBehavior Explanation

This page will explain how the custom ElementBehavior system (see [Making Custom ElementBehaviors](making_custom_elementbehaviors.md)) was used to make the behavior for the FIRE element. <br>
Here is the code for FireBehavior:
```
[Tool]
[GlobalClass]
public partial class FireBehavior : ElementBehavior
{
    
    public override Dictionary<string, byte> _DefaultFields()
    {
        return new Dictionary<string, byte>
        {
            {"R#MovesBeforeExpire", 25},
            {"R#random", 1},
			{"R#direction", 0},
			{"bumps", 0},
        };
    }
    


    public override void _OnCellUpdate(SandInfo.Cell cell, PowderSimulation sim)
    {
        
        if(cell.GetField("R#MovesBeforeExpire") <= 0)
        {
            cell.SetElement(Elements.AllElements.AIR);   
        }
        else
        {
            cell.SetField("R#MovesBeforeExpire", (byte)(cell.GetField("R#MovesBeforeExpire") - 1));
            
            RunGas(cell, sim);
        }

    }


}
```

--------------------------------

### Let's look at the _DefaultFields function first:

```
public override Dictionary<string, byte> _DefaultFields()
{
    return new Dictionary<string, byte>
    {
        {"R#MovesBeforeExpire", 25},
        {"R#random", 1},
		{"direction", 0},
		{"bumps", 0},
     };
}
```
`_DefaultFields` returns a Dictionary with strings as the keys and bytes as the values. <br>

* `R#MovesBeforeExpire` is the number of update ticks passed before it deletes itself, with a starting value of 0-25.

* `R#random` is used for the GAS movement that is used in `_OnCellUpdate`, with a starting value of 0-1.

* `direction` is used for the GAS movement preset that is used in `_OnCellUpdate`, with a starting value of 0.

* `bumps` is used for the GAS movement preset that is used in `_OnCellUpdate`, with a starting value of 0.

> *Note: when using preset movement within a custom behavior, make sure to include the same fields the preset uses. The fields they use can be found by opening ElementAttributes.cs in the Scripts/CSharp folder of the plugin and looking at MoveTypeDefaultFields.*

-----------------------------

### Now let's look at _OnCellUpdate:

```
public override void _OnCellUpdate(SandInfo.Cell cell, PowderSimulation sim)
{
        
    if(cell.GetField("R#MovesBeforeExpire") <= 0)
    {
        cell.SetElement(Elements.AllElements.AIR);   
    }
    else
    {
        cell.SetField("R#MovesBeforeExpire", (byte)(cell.GetField("R#MovesBeforeExpire") - 1));
            
        RunGas(cell, sim);
    }

}
```

What this code does is replace the cell with AIR if MovesBeforeExpire is zero, and otherwise lower that number by one and run the GAS movement preset. <br><br>
To do this, it uses the cell.GetField and cell.SetField methods to change and access the specific values of that cell's fields.