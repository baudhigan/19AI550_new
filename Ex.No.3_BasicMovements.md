# Ex.No: 3  Basic movements in Unity 
### DATE: 29.07.2026                                                                         
### REGISTER NUMBER : 212223230028
### AIM: 
 To learn the basic movements translation,scaling and rotation of game objects through code.
### Procedure:
1. Setup the Scene
2. Open Unity and create a 3D Scene.
3. Add three objects:Cube → Rename to Object1 (for movement),Sphere → Rename to Object2 (for rotation).Capsule → Rename to Object3 (for scaling).
4. Add the Script,Create a C# Script → Name it TransformOperations.cs.
5. Write the code for translation,scaling and rotation,save and close the script
6. Save the script
7. Select any empty GameObject (or create one: GameObject → Create Empty).
8. Attach the TransformOperations script to it.
9. In the Inspector, assign Object1 → Drag the Cube,Object2 → Drag the Sphere.Object3 → Drag the Capsule.
10. Run the Scene Press Play ▶️ in Unity
11. Stop the program.
### Program 
```
using UnityEngine;

public class welcom : MonoBehaviour
{
    // Start is called once before the first execution of Update after the MonoBehaviour is created
    public Transform o1;
    public Transform o2;
    public Transform o3;
    void Start()
    {
        print("Welcome");
    }

    // Update is called once per frame
    void Update()
    {
        // print("Welcome to Unity");
        o1.Translate(2f, 0, 0);
        o2.Rotate(0, 10f, 0);
        o3.localScale+=new Vector3(0.2f, 0.2f, 0.2f);

    }
}

```
### Output:

<img width="1920" height="1080" alt="Screenshot (37)" src="https://github.com/user-attachments/assets/c8d93691-36f9-482f-8e71-253e190a57ef" />

<img width="1920" height="1080" alt="Screenshot (38)" src="https://github.com/user-attachments/assets/6ff5eec0-0da3-46a8-8db7-2d695712cd18" />

<img width="1920" height="1080" alt="Screenshot (39)" src="https://github.com/user-attachments/assets/c724ee9a-038b-4405-ae81-3806eef95be0" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1986698a-54fe-471b-b524-72bc71490aa5" />


### Result:
Thus the basic movement is learned through scripting


