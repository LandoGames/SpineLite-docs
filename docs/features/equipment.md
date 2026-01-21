# Equipment System

SpineLite uses Spine's skin system to manage equipment.

## Equipment Slots

| Slot | Prefix | Example |
|------|--------|---------|
| Base Skin | `skin/` | `skin/nude_T1` |
| Hair | `face/hair/` | `face/hair/Long_Hair_01` |
| Beard | `face/beard/` | `face/beard/Full_Beard` |
| Eyes | `face/eyes/` | `face/eyes/Blue_Eyes` |
| Helmet | `head/` | `head/Warrior_Helmet_T1` |
| Armor | `body/` | `body/Leather_Armor` |
| Legs | `legs/` | `legs/Leather_Pants` |
| Cape | `accessories/cape/` | `accessories/cape/Red_Cape` |
| Main Weapon | `weapons/` | `weapons/Sword_1H` |
| Off-Hand | `shields/` or `offhand/` | `shields/Wooden_Shield` |

## Usage

```csharp
controller.Helmet = "head/Warrior_Helmet_T1";
controller.Armor = "body/Leather_Armor";
controller.MainHand = "weapons/Sword_1H";
```

To unequip, set to empty string:
```csharp
controller.Helmet = "";
```
