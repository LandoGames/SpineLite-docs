# Save & Load

Save and restore character appearance using JSON or file-based persistence.

---

## Quick Reference

```csharp
// File-based
controller.SaveToFile();
controller.LoadFromFile();

// JSON-based
string json = controller.ToJson();
controller.FromJson(json);
```

---

## File-Based Saves

### SaveToFile()

Saves appearance to a JSON file in your project:

```csharp
// Uses default path (Assets/LandoGames/Data/)
controller.SaveToFile();

// Or specify custom path
controller.SaveToFile("Assets/MyGame/Saves/character.json");
```

### LoadFromFile()

Loads appearance from the assigned `TextAsset`:

```csharp
// Loads from the TextAsset assigned in Inspector
controller.LoadFromFile();
```

!!! tip "Assigning the Data File"
    In the Inspector, drag your saved JSON file to the **Appearance Data File** field on SpineLiteController.

---

## JSON-Based Saves

For runtime saves (PlayerPrefs, server, etc.):

### ToJson()

```csharp
string json = controller.ToJson();

// Save to PlayerPrefs
PlayerPrefs.SetString("CharacterSave", json);
PlayerPrefs.Save();

// Or send to server
StartCoroutine(SendToServer(json));
```

### FromJson()

```csharp
// Load from PlayerPrefs
string json = PlayerPrefs.GetString("CharacterSave");
controller.FromJson(json);
```

---

## JSON Format

```json
{
  "baseSkin": "skin/nude_T1",
  "hairStyle": "face/hair/Long_Hair_01",
  "beardStyle": "",
  "eyeStyle": "face/eyes/Blue_Eyes",
  "helmet": "head/Warrior_Helmet_T1",
  "armor": "body/Leather_Armor",
  "legs": "legs/Leather_Pants",
  "cape": "",
  "mainHand": "weapons/Sword_1H",
  "offHand": "shields/Wooden_Shield",
  "skinTint": [0.9, 0.8, 0.7, 1.0],
  "hairTint": [0.3, 0.2, 0.1, 1.0],
  "armorTint": [0.4, 0.4, 0.5, 1.0],
  "savedAt": "2026-01-21 12:00:00",
  "version": "1.1"
}
```

---

## AppearanceData Object

For more control, use the data object directly:

```csharp
// Get current appearance as data object
SpineLiteAppearanceData data = controller.GetAppearanceData();

// Modify it
data.helmet = "head/Wizard_Hat";
data.armorTint = new float[] { 0.2f, 0.3f, 0.8f, 1.0f };

// Apply it back
controller.ApplyAppearanceData(data);
```

---

## Save Manager Example

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

    public void Save(string characterName)
    {
        string json = controller.ToJson();
        string path = Path.Combine(savePath, characterName + ".json");
        File.WriteAllText(path, json);
        Debug.Log($"Saved to: {path}");
    }

    public void Load(string characterName)
    {
        string path = Path.Combine(savePath, characterName + ".json");
        if (File.Exists(path))
        {
            string json = File.ReadAllText(path);
            controller.FromJson(json);
            Debug.Log($"Loaded: {characterName}");
        }
    }

    public string[] GetSaveFiles()
    {
        return Directory.GetFiles(savePath, "*.json");
    }
}
```

---

## Demo Save/Load

The Demo scene includes working save/load buttons. Check `SpineLiteDemoUI.cs` for implementation details.

---

## Best Practices

1. **PlayerPrefs** - Good for single character saves
2. **File-based** - Good for multiple save slots
3. **Server** - Send JSON via HTTP for cloud saves
4. **ScriptableObject** - Use `SpineLiteAction` for preset appearances
