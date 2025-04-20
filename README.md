# DynamicMenuWindow
Dynamic Menu Window for Unity
Opens also a Scene and ReadSceneNames Example

```
using UnityEditor;
using System.Collections.Generic;
using UnityEditor.SceneManagement;

public class DynamicMenuWindow : EditorWindow
{
    public static string[] scenes;

    private static string[] ReadSceneNames()
    {
        List<string> temp = new List<string>();
        foreach (UnityEditor.EditorBuildSettingsScene S in UnityEditor.EditorBuildSettings.scenes)
        {
            if (S.enabled)
            {
                //Debug.Log("Scene Name: " + S.path);

                string name = S.path.Substring(S.path.LastIndexOf('/') + 1);
                name = name.Substring(0, name.Length - 6);
                temp.Add(name);
                //Debug.Log("Scene Name: " + name);
            }
        }
        return temp.ToArray();
    }
    
    private string[] menuOptions = new[] { "Item 1", "Item 2", "Item 3" };

    [MenuItem("Tools/Dynamic Menu Window")]
    public static void OpenDynamicWindow()
    {
        EditorWindow.GetWindow<DynamicMenuWindow>("Dynamic Menu");
    }

    void OnGUI()
    {
        GUILayout.Label("Choose an Option", EditorStyles.boldLabel);
        foreach (var option in menuOptions)
        {
            if (GUILayout.Button(option))
            {
                Debug.Log($"Clicked: {option}");

                string scenePath = $"Assets/Scenes/{option}.unity";
                EditorSceneManager.OpenScene(scenePath);
            }
        }
    }
}
```
