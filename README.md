## Adding This Module to Another Unity Project

### 1. Download the Module

Download or clone this repository from GitHub.

Copy these folders into the other Unity project:

- `Assets/Scripts/SolutionPreparation`
- `Assets/Prefabs/SolutionPreparation`

Keep all accompanying `.meta` files. Do not copy the `Library` folder.

### 2. Allow Unity to Compile

Open the receiving project in Unity and wait for script compilation to finish. Check the Console for errors.

### 3. Add the Prefab

Find:

`Assets/Prefabs/SolutionPreparation/SolutionPreparationModule.prefab`

Drag it into the required scene.

### 4. Configure the Solution

Select the prefab and configure these Inspector values:

- Chemical name
- Target molarity
- Target volume in cm³
- Molar mass
- Mass and volume tolerances

### 5. Connect Other Modules

Reference the component from another script:

```csharp
using UnityEngine;
using SolutionPreparationSystem;

public class LabIntegration : MonoBehaviour
{
    [SerializeField]
    private SolutionPreparationModule solutionModule;

    public void UpdateMeasuredMass(float mass)
    {
        solutionModule.SetMeasuredMass(mass);
    }

    public void UpdateLiquidLevel(float level)
    {
        solutionModule.SetLiquidLevel(level);
    }

    public void CompleteDissolving()
    {
        solutionModule.AddSolute();
        solutionModule.AddWater();
        solutionModule.Stir();
        solutionModule.MarkDissolved();
    }

    public bool IsSolutionReady()
    {
        return solutionModule.SolutionPrepared;
    }

    public double GetConfirmedMolarity()
    {
        return solutionModule.ConfirmedMolarity;
    }
}
