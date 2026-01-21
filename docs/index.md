# SpineLite

**Drag-and-drop Spine character customization for Unity.**

---

## Features

- **Equipment System** - Helmet, armor, weapons, capes, and more
- **Color Tinting** - Skin, hair, eyes, armor with full color control
- **Animation Support** - Automatic weapon-compatible animation switching
- **Save/Load** - JSON and file-based character persistence
- **Editor Preview** - See changes in real-time without Play mode

---

## Quick Start

Add `SpineLiteController` to your Spine character, then:

```csharp
var controller = GetComponent<SpineLiteController>();

controller.Helmet   = "head/Warrior_Helmet_T1";
controller.Armor    = "body/Leather_Armor";
controller.MainHand = "weapons/Sword_1H";
controller.SkinTint = new Color(0.9f, 0.8f, 0.7f);
```

**No-code alternative:** Attach `SpineLiteButton` to any UI Button and set Property/Value in the Inspector.

---

## What's Included

The demo scene is optional - your model prefab stays clean with just `SpineLiteController`.

---

## Requirements

- **Unity 6** (6000.0.23f1 or later)
- **Spine Unity Runtime 4.2+**
- **TextMeshPro** (for UI components)

---

## Support

- [GitHub Issues](https://github.com/LandoGames/SpineLite-docs/issues)
- [Full Documentation](getting-started.md)
