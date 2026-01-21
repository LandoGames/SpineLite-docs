# Getting Started

This guide will help you set up SpineLite in your Unity project.

---

## Installation

1. Import the SpineLite package from the Unity Asset Store
2. The package will be installed at `Assets/LandoGames/`

### Package Contents

```
LandoGames/
├── Scripts/
│   ├── ControllerLite/       # Core components (keep these)
│   │   ├── SpineLiteController.cs
│   │   ├── SpineLiteButton.cs
│   │   └── SpineLiteAction.cs
│   ├── Gallery/              # Model Gallery (optional)
│   └── Examples/             # Demo scripts (safe to delete)
├── Prefabs/
│   └── Characters/           # Model prefabs
├── Scenes/
│   ├── Demo.unity            # Button showcase
│   └── ModelGallery.unity    # Model browser
├── Data/                     # Saved appearances
└── Documentation/
```

---

## Prefab Structure

Each character prefab contains:

```
HumanFemaleMage (Prefab)
├── SkeletonAnimation         # Spine component
├── SpineLiteController       # Customization controller
└── SpineLiteInfo (optional)  # Metadata component
```

**What you can delete:**

- `SpineLiteDemoUI.cs` - Demo scene script only
- `Demo.unity` - Example scene
- `Examples/` folder - Demo scripts

**What to keep:**

- `ControllerLite/` folder - Core functionality
- Model prefabs
- `Gallery/` folder (if using Model Gallery)

---

## Basic Setup

### Step 1: Add the Controller

1. Select your Spine character GameObject (with `SkeletonAnimation`)
2. Add Component → **SpineLite Controller**
3. The controller auto-detects the `SkeletonAnimation` component

### Step 2: Discover Skins

Click **Discover Skins** in the Inspector to populate the available equipment lists.

The controller automatically categorizes skins by prefix:

| Prefix | Category |
|--------|----------|
| `skin/` | Base Skins |
| `face/hair/` | Hair Styles |
| `face/beard/` | Beard Styles |
| `face/eyes/` | Eye Styles |
| `head/` | Helmets |
| `body/` | Armor |
| `legs/` | Leg Armor |
| `accessories/cape/` | Capes |
| `weapons/` | Weapons |
| `shields/` | Shields |

### Step 3: Configure Appearance

Use the Inspector dropdowns to select:

- **Base Skin** - The nude/base skin
- **Hair Style** - Hair attachment
- **Equipment** - Helmet, armor, legs, cape
- **Weapons** - Main hand and off-hand

---

## Using SpineLiteButton (No-Code)

For UI-driven customization without writing code:

### 1. Create a Button

1. Right-click in Hierarchy → UI → Button
2. Add Component → **SpineLite Button**

### 2. Configure Find Mode

**Find Mode** determines how the button locates the controller:

| Mode | Use Case |
|------|----------|
| **Find In Scene** | Single character - finds first controller in scene |
| **Find In Parent** | Multiple characters - searches up the hierarchy |
| **Manual** | Drag the controller reference directly |
| **Find By Name** | Find controller by GameObject name |

!!! tip "Multiple Characters"
    If you have multiple characters in your scene, use **Manual** or **Find In Parent** to target the correct one.

### 3. Configure the Button

| Property | Description |
|----------|-------------|
| **Property Type** | What to change (Helmet, Armor, MainHand, etc.) |
| **String Value** | The skin path to apply |
| **Color Value** | For color properties |

### 4. Property Types

**Equipment:**

- `Helmet`, `Armor`, `Legs`, `Cape`, `Overcoat`, `Trinket`
- `MainHand`, `OffHand`

**Body:**

- `HairStyle`, `BeardStyle`, `EyeStyle`, `EyeGear`

**Colors:**

- `SkinTone`, `HairColor`, `BeardColor`, `EyeColor`
- `ArmorTint`, `BootsTint`, `CapeTint`

**Actions:**

- `Randomize` - Randomize everything
- `RandomizeEquipment` - Randomize equipment only
- `RandomizeColors` - Randomize colors only
- `ResetToDefault` - Reset to defaults
- `PlayAnimation` - Play a specific animation

---

## Code Examples

### Basic Equipment

```csharp
var controller = GetComponent<SpineLiteController>();

// Set equipment
controller.Helmet   = "head/Warrior_Helmet_T1";
controller.Armor    = "body/Leather_Armor";
controller.MainHand = "weapons/Sword_1H";
controller.OffHand  = "shields/Wooden_Shield";
```

### Color Tinting

```csharp
// Set skin tone
controller.SkinTint = new Color(0.9f, 0.75f, 0.6f);

// Set hair color
controller.HairTint = new Color(0.3f, 0.2f, 0.1f);

// Set armor tint
controller.ArmorTint = new Color(0.4f, 0.4f, 0.5f);
```

### Randomize

```csharp
// Randomize everything
controller.Randomize();

// Or separately:
controller.RandomizeEquipment();
controller.RandomizeColors();
```

### Save/Load

```csharp
// File-based (uses assigned TextAsset or default path)
controller.SaveToFile();
controller.LoadFromFile();

// JSON-based (for PlayerPrefs, server, etc.)
string json = controller.ToJson();
controller.FromJson(json);
```

---

## Demo Scenes

### Demo.unity

The main demo scene showing:

- All button types working
- Save/Load functionality
- Color and equipment randomization
- Animation playback

### ModelGallery.unity

A model browser for viewing all available characters:

- Grid layout of all model prefabs
- Click to spawn and customize
- Great for testing different characters

---

## Next Steps

- [SpineLiteController API](api/controller.md)
- [SpineLiteButton API](api/button.md)
- [Equipment System](features/equipment.md)
- [Save & Load](features/save-load.md)
- [Animations](features/animations.md)
