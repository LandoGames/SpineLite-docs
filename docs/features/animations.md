# Animations

Play animations and auto-switch based on equipped weapons.

---

## Basic Playback

```csharp
controller.PlayAnimation("idle", true);              // Loop
controller.PlayAnimation("melee/M1_short_weapon", false);  // Once
controller.StopAnimation();
```

---

## Weapon-Compatible Animations

When weapons are equipped, SpineLite auto-selects compatible animations:

```csharp
// This auto-selects the best idle for current weapon
controller.PlayCompatibleIdle();
```

The controller checks your equipped weapon and plays the matching idle animation automatically.

---

## Dominant Hand (Weapon Priority)

SpineLite chooses compatible animations based on the **dominant weapon**. If both hands have weapons, the **off-hand** (left/back hand) wins and its animation set is used.

**Example:**

- Off-hand = Torch
- Main-hand = Sword
- → Walk uses torch-style animations, not sword walk

This lets you swap weapons without manually picking the animation set.

---

## Animation Naming Conventions

Animations follow a naming pattern that indicates weapon compatibility:

### Idle Animations

| Animation | Weapon Type |
|-----------|-------------|
| `idle` | No weapon visible |
| `idle_combat/1H` | One-handed weapon |
| `idle_combat/2H` | Two-handed weapon |
| `idle_combat/bow` | Bow |
| `idle_hold/1H` | Holding 1H casually |
| `idle_hold/2H` | Holding 2H casually |

### Attack Animations

| Animation | Description |
|-----------|-------------|
| `melee/M1_short_weapon` | Quick attack with short weapon |
| `melee/M1_long_weapon` | Attack with long weapon |
| `melee/M1_2H` | Two-handed attack |
| `ranged/bow_shoot` | Bow shot |
| `ranged/throw` | Throwing attack |

### Other Categories

| Category | Prefix | Description |
|----------|--------|-------------|
| Walk | `walk/` | Walking animations |
| Run | `run/` | Running animations |
| Block | `block/` | Blocking with shield |
| Cast | `cast/` | Spell casting |
| Death | `death/` | Death animations |
| Hit | `hit/` | Taking damage |

---

## How Auto-Selection Works

When you call `PlayCompatibleIdle()`:

1. Controller checks `MainHand` weapon
2. Determines weapon type (1H, 2H, bow, etc.)
3. Finds matching `idle_combat/` or `idle_hold/` animation
4. Falls back to base `idle` if no match

```csharp
// Example: Sword equipped
controller.MainHand = "weapons/Sword_1H";
controller.PlayCompatibleIdle();  // Plays idle_combat/1H

// Example: Staff equipped
controller.MainHand = "weapons/Staff_2H";
controller.PlayCompatibleIdle();  // Plays idle_combat/2H

// Example: No weapon
controller.MainHand = "";
controller.PlayCompatibleIdle();  // Plays idle
```

---

## Animation Discovery

To see all available animations on your model:

```csharp
controller.DiscoverAnimations();

// Now you can iterate available animations
foreach (var anim in controller.availableAnimations)
{
    Debug.Log(anim);
}
```

Or use the Inspector - click **Discover Animations** to populate the list.

---

## Playing Specific Animations

```csharp
// Play idle animation (looping)
controller.PlayAnimation("idle", true);

// Play attack animation (once)
controller.PlayAnimation("melee/M1_short_weapon", false);

// Stop current animation
controller.StopAnimation();
```

---

## SpineLiteButton for Animations

Use the no-code approach:

1. Add `SpineLiteButton` to a UI Button
2. Set **Property Type** = `PlayAnimation`
3. Set **String Value** = animation name (e.g., `"idle"`)
4. Set **Loop Animation** = `true` or `false`
