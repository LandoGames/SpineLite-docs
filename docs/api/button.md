# SpineLiteButton

A no-code component for UI buttons that control character customization.

---

## Overview

`SpineLiteButton` lets you create character customization buttons without writing code. Just add it to any UI Button and configure in the Inspector.

---

## Properties

### Target

| Property | Type | Description |
|----------|------|-------------|
| `targetMode` | `TargetMode` | How to find the controller |
| `targetController` | `SpineLiteController` | Manual reference (if mode is Manual) |
| `targetName` | `string` | GameObject name (if mode is FindByName) |

### Configuration

| Property | Type | Description |
|----------|------|-------------|
| `configMode` | `ConfigMode` | Inline or ScriptableObject |
| `actionAsset` | `SpineLiteAction` | Reusable action asset |
| `propertyType` | `PropertyType` | What property to change |
| `stringValue` | `string` | Skin/animation path value |
| `colorValue` | `Color` | Color value (for tints) |
| `loopAnimation` | `bool` | Loop animation (for PlayAnimation) |

### Visual Feedback

| Property | Type | Description |
|----------|------|-------------|
| `autoUpdateText` | `bool` | Auto-update button text |
| `displayText` | `string` | Custom display text |
| `showSelectionHighlight` | `bool` | Highlight when selected |
| `selectedColor` | `Color` | Button color when selected |
| `normalColor` | `Color` | Button color when not selected |

### Events

| Property | Type | Description |
|----------|------|-------------|
| `onBeforeApply` | `UnityEvent` | Called before applying |
| `onAfterApply` | `UnityEvent` | Called after applying |

---

## Enums

### TargetMode

| Value | Description |
|-------|-------------|
| `Manual` | Use the assigned `targetController` |
| `FindInParent` | Search up the hierarchy |
| `FindInScene` | Find any controller in scene |
| `FindByName` | Find by GameObject name |

### PropertyType

#### Body
- `HairStyle` - Hair attachment
- `BeardStyle` - Beard attachment
- `EyeStyle` - Eye style
- `EyeGear` - Glasses, eyepatch, etc.

#### Equipment
- `Helmet` - Head armor
- `Armor` - Body armor
- `Legs` - Leg armor
- `Cape` - Cape/cloak
- `Overcoat` - Overcoat
- `Trinket` - Trinket accessory

#### Weapons
- `MainHand` - Main weapon
- `OffHand` - Shield/off-hand item

#### Colors
- `SkinTone` - Skin color
- `HairColor` - Hair color
- `BeardColor` - Beard color
- `EyeColor` - Eye color
- `ArmorTint` - Armor tint
- `BootsTint` - Boots tint
- `CapeTint` - Cape tint

#### Animation
- `PlayAnimation` - Play animation (uses `stringValue` and `loopAnimation`)

#### Actions
- `Randomize` - Randomize everything
- `RandomizeEquipment` - Randomize equipment only
- `RandomizeColors` - Randomize colors only
- `ResetToDefault` - Reset to defaults

---

## Methods

### `Apply()`
Manually trigger the button action.

```csharp
var button = GetComponent<SpineLiteButton>();
button.Apply();
```

### `SetTarget(SpineLiteController controller)`
Set the target controller at runtime.

```csharp
button.SetTarget(myController);
```

### `SetValue(string value)`
Set the string value at runtime.

```csharp
button.SetValue("head/Wizard_Hat");
```

### `SetColorValue(Color color)`
Set the color value at runtime.

```csharp
button.SetColorValue(Color.red);
```

### `UpdateVisualState()`
Update button highlight state.

```csharp
button.UpdateVisualState();
```

---

## Setup Examples

### Equipment Button

1. Add UI Button to Canvas
2. Add `SpineLiteButton` component
3. Set **Target Mode** = `FindInScene`
4. Set **Property Type** = `Helmet`
5. Set **String Value** = `"head/Warrior_Helmet_T1"`

### Color Button

1. Add UI Button to Canvas
2. Add `SpineLiteButton` component
3. Set **Target Mode** = `FindInScene`
4. Set **Property Type** = `SkinTone`
5. Set **Color Value** = Your desired color

### Randomize Button

1. Add UI Button to Canvas
2. Add `SpineLiteButton` component
3. Set **Target Mode** = `FindInScene`
4. Set **Property Type** = `Randomize`
5. No value needed!

### Animation Button

1. Add UI Button to Canvas
2. Add `SpineLiteButton` component
3. Set **Target Mode** = `FindInScene`
4. Set **Property Type** = `PlayAnimation`
5. Set **String Value** = `"idle"` (or any animation name)
6. Set **Loop Animation** = `true` or `false`

---

## Events Example

Listen to button events:

```csharp
public class ButtonListener : MonoBehaviour
{
    public SpineLiteButton equipmentButton;

    void Start()
    {
        equipmentButton.onBeforeApply.AddListener(OnBeforeEquip);
        equipmentButton.onAfterApply.AddListener(OnAfterEquip);
    }

    void OnBeforeEquip()
    {
        Debug.Log("About to change equipment...");
    }

    void OnAfterEquip()
    {
        Debug.Log("Equipment changed!");
        // Play sound, show particle effect, etc.
    }
}
```
