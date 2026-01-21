# Color Tinting

Apply color tints to different parts of the character.

## Available Tints

| Tint | Affects |
|------|---------|
| `SkinTint` | All body parts with nude attachments |
| `HairTint` | Hair slots |
| `BeardTint` | Beard slots |
| `EyeTint` | Eye slots |
| `ArmorTint` | Non-nude armor (torso, arms, legs) |
| `BootsTint` | Feet/boot slots |
| `CapeTint` | Cape slots |
| `WeaponTint` | Equipped weapons |

## Usage

```csharp
controller.SkinTint = new Color(0.9f, 0.8f, 0.7f);
controller.HairTint = new Color(0.3f, 0.2f, 0.1f);
controller.ArmorTint = new Color(0.4f, 0.4f, 0.5f);
```

To remove tint, use white or clear:
```csharp
controller.ArmorTint = Color.white; // No tint
```
