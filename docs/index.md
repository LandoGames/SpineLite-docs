# SpineLite

**Drag-and-drop character customization for Spine models in Unity.**

SpineLite makes it easy to customize Spine characters with equipment, colors, and animations - no code required.

---

## Features

- **No-Code Setup** - Drag prefabs, configure in Inspector
- **Equipment System** - Helmet, armor, weapons, capes, and more
- **Color Tinting** - Skin, hair, eyes, armor with full color control
- **Animation Support** - Automatic weapon-compatible animation switching
- **Save/Load** - JSON and file-based character persistence
- **Editor Preview** - See changes in real-time without Play mode

---

## Quick Start

### 1. Add the Controller

Add `SpineLiteController` to your Spine character GameObject.

```csharp
var controller = GetComponent<SpineLiteController>();
```

### 2. Equip Items

```csharp
controller.Helmet   = "head/Warrior_Helmet_T1";
controller.Armor    = "body/Leather_Armor";
controller.MainHand = "weapons/Sword_1H";
```

### 3. Set Colors

```csharp
controller.SkinTint  = new Color(0.9f, 0.8f, 0.7f);
controller.HairTint  = Color.red;
controller.ArmorTint = new Color(0.3f, 0.5f, 0.7f);
```

### 4. No-Code Buttons (SpineLiteButton)

1. Add a UI Button to your Canvas
2. Attach `SpineLiteButton` component
3. Pick **Property Type** (Helmet, Armor, Animation, etc.)
4. Set **Value** (skin path or animation name)
5. Done!

---

## Demo vs Product

| Content | Description | Can Delete? |
|---------|-------------|-------------|
| **Model Prefab** | Clean character with `SpineLiteController` | Keep this |
| **Demo Scene** | Shows buttons + UI panel | Safe to delete |
| **SpineLiteDemoUI** | Demo script for showcase | Safe to delete |

---

## Requirements

- **Unity 6** (6000.0.23f1 or later)
- **Spine Unity Runtime 4.2+**
- **TextMeshPro** (for UI components)

---

## Support

- [GitHub Issues](https://github.com/LandoGames/SpineLite-docs/issues)
- [Documentation](getting-started.md)
