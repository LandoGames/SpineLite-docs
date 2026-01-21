# SpineLiteController

The main component for controlling Spine character appearance.

---

## Properties

### Equipment

| Property | Type | Description |
|----------|------|-------------|
| `BaseSkin` | `string` | Base nude skin (e.g., `"skin/nude_T1"`) |
| `HairStyle` | `string` | Hair attachment path |
| `BeardStyle` | `string` | Beard attachment path |
| `EyeStyle` | `string` | Eye style path |
| `EyeGear` | `string` | Eye gear (glasses, eyepatch) |
| `Helmet` | `string` | Head armor path |
| `Armor` | `string` | Body armor path |
| `Legs` | `string` | Leg armor path |
| `Cape` | `string` | Cape/cloak path |
| `Overcoat` | `string` | Overcoat path |
| `Trinket` | `string` | Trinket accessory path |
| `MainHand` | `string` | Main hand weapon path |
| `OffHand` | `string` | Off-hand item/shield path |

### Colors

| Property | Type | Description |
|----------|------|-------------|
| `SkinTint` | `Color` | Skin tone color |
| `HairTint` | `Color` | Hair color |
| `BeardTint` | `Color` | Beard color |
| `EyeTint` | `Color` | Eye color |
| `ArmorTint` | `Color` | Armor color overlay |
| `WeaponTint` | `Color` | Weapon color overlay |
| `BootsTint` | `Color` | Boots/footwear color |
| `CapeTint` | `Color` | Cape color |

### Animation

| Property | Type | Description |
|----------|------|-------------|
| `CurrentAnimation` | `string` | Current animation name |
| `LoopAnimation` | `bool` | Whether animation loops |
| `IsPlaying` | `bool` | Is animation playing (read-only) |

---

## Methods

### Appearance

#### `RebuildAppearance()`
Rebuilds the combined skin with all current equipment. Called automatically when properties change.

```csharp
controller.RebuildAppearance();
```

#### `ApplyColors()`
Reapplies all color tints. Called automatically when color properties change.

```csharp
controller.ApplyColors();
```

### Randomization

#### `Randomize()`
Randomizes all equipment, hair, and colors.

```csharp
controller.Randomize();
```

!!! note
    Armor and eyes are always set to valid items (never "none").

#### `RandomizeEquipment()`
Randomizes only equipment (armor, weapons, helmet, etc.). Colors remain unchanged.

```csharp
controller.RandomizeEquipment();
```

#### `RandomizeColors()`
Randomizes only colors (skin, hair, armor tints). Equipment remains unchanged.

```csharp
controller.RandomizeColors();
```

#### `ResetToDefaults()`
Resets character to default appearance (nude, no equipment, white colors).

```csharp
controller.ResetToDefaults();
```

### Animation

#### `PlayAnimation(string name, bool loop)`
Plays the specified animation.

```csharp
controller.PlayAnimation("idle", true);
controller.PlayAnimation("melee/M1_short_weapon", false);
```

#### `StopAnimation()`
Stops the current animation and returns to setup pose.

```csharp
controller.StopAnimation();
```

#### `PlayCompatibleIdle()`
Plays the best idle animation for the current weapon.

```csharp
// Auto-selects idle_hold or idle_combat based on weapon
controller.PlayCompatibleIdle();
```

### Save/Load

#### `ToJson(bool prettyPrint = true)`
Exports current appearance to JSON string.

```csharp
string json = controller.ToJson();
// Save to PlayerPrefs, file, server, etc.
```

#### `FromJson(string json)`
Loads appearance from JSON string.

```csharp
string json = PlayerPrefs.GetString("CharacterSave");
controller.FromJson(json);
```

#### `SaveToFile(string path = null)`
Saves appearance to a JSON file. Uses default path if not specified.

```csharp
// Default path (Assets/LandoGames/Data/)
controller.SaveToFile();

// Custom path
controller.SaveToFile("Assets/MyGame/Saves/character.json");
```

#### `LoadFromFile()`
Loads appearance from the assigned TextAsset.

```csharp
// Requires Appearance Data File to be assigned in Inspector
controller.LoadFromFile();
```

#### `GetAppearanceData()`
Returns a `SpineLiteAppearanceData` object with all current settings.

```csharp
var data = controller.GetAppearanceData();
```

#### `ApplyAppearanceData(SpineLiteAppearanceData data)`
Applies settings from a data object.

```csharp
controller.ApplyAppearanceData(data);
```

### Discovery

#### `DiscoverSkins()`
Scans the skeleton for available skins and categorizes them.

```csharp
controller.DiscoverSkins();
// Now controller.helmets, controller.armors, etc. are populated
```

#### `DiscoverAnimations()`
Scans the skeleton for available animations.

```csharp
controller.DiscoverAnimations();
// Now controller.availableAnimations is populated
```

---

## Example: Full Setup

```csharp
using UnityEngine;
using SpineLite;

public class CharacterSetup : MonoBehaviour
{
    private SpineLiteController controller;

    void Start()
    {
        controller = GetComponent<SpineLiteController>();

        // Set appearance
        controller.HairStyle = "face/hair/Long_Hair_01";
        controller.Armor = "body/Leather_Armor";
        controller.MainHand = "weapons/Sword_1H";

        // Set colors
        controller.SkinTint = new Color(0.9f, 0.8f, 0.7f);
        controller.HairTint = new Color(0.4f, 0.2f, 0.1f);

        // Play animation
        controller.PlayAnimation("idle", true);
    }

    public void SaveCharacter()
    {
        string json = controller.ToJson();
        PlayerPrefs.SetString("MyCharacter", json);
        PlayerPrefs.Save();
    }

    public void LoadCharacter()
    {
        if (PlayerPrefs.HasKey("MyCharacter"))
        {
            controller.FromJson(PlayerPrefs.GetString("MyCharacter"));
        }
    }
}
```
