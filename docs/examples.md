# Examples

## Character Creator

```csharp
using UnityEngine;

public class CharacterCreator : MonoBehaviour
{
    public SpineLiteController controller;

    public void SetWarrior()
    {
        controller.Helmet   = "head/Warrior_Helmet_T1";
        controller.Armor    = "body/Plate_Armor";
        controller.MainHand = "weapons/Sword_1H";
        controller.OffHand  = "shields/Metal_Shield";
        controller.ArmorTint = new Color(0.5f, 0.5f, 0.6f);
    }

    public void SetMage()
    {
        controller.Helmet   = "";
        controller.Armor    = "body/Mage_Robe";
        controller.MainHand = "weapons/Staff_2H";
        controller.OffHand  = "";
        controller.ArmorTint = new Color(0.3f, 0.2f, 0.5f);
    }

    public void SetArcher()
    {
        controller.Helmet   = "head/Hood";
        controller.Armor    = "body/Leather_Armor";
        controller.MainHand = "weapons/Bow";
        controller.OffHand  = "";
        controller.ArmorTint = new Color(0.4f, 0.3f, 0.2f);
    }
}
```

---

## Save System

```csharp
using UnityEngine;
using System.IO;

public class SaveManager : MonoBehaviour
{
    public SpineLiteController controller;
    private string savePath;

    void Start()
    {
        savePath = Path.Combine(Application.persistentDataPath, "saves");
        Directory.CreateDirectory(savePath);
    }

    public void Save(string name)
    {
        string json = controller.ToJson();
        File.WriteAllText(Path.Combine(savePath, name + ".json"), json);
    }

    public void Load(string name)
    {
        string path = Path.Combine(savePath, name + ".json");
        if (File.Exists(path))
            controller.FromJson(File.ReadAllText(path));
    }
}
```

---

## Runtime Randomizer

```csharp
using UnityEngine;

public class RandomizerButton : MonoBehaviour
{
    public SpineLiteController controller;

    public void RandomizeAll()
    {
        controller.Randomize();
    }

    public void RandomizeEquipmentOnly()
    {
        controller.RandomizeEquipment();
    }

    public void RandomizeColorsOnly()
    {
        controller.RandomizeColors();
    }

    public void ResetCharacter()
    {
        controller.ResetToDefaults();
    }
}
```

---

## Animation Controller

```csharp
using UnityEngine;

public class AnimationController : MonoBehaviour
{
    public SpineLiteController controller;

    void Update()
    {
        // Auto-play compatible idle when idle
        if (Input.GetKeyDown(KeyCode.I))
            controller.PlayCompatibleIdle();

        // Attack animation
        if (Input.GetKeyDown(KeyCode.Space))
            controller.PlayAnimation("melee/M1_short_weapon", false);

        // Stop animation
        if (Input.GetKeyDown(KeyCode.S))
            controller.StopAnimation();
    }
}
```

---

## Demo Scenes

| Scene | Description |
|-------|-------------|
| `Demo.unity` | Complete working example with buttons |
| `ModelGallery.unity` | Browse and spawn different models |

Open `Assets/LandoGames/Scenes/Demo.unity` for a complete working example.
