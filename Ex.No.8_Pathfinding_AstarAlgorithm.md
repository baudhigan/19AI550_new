# Ex.No: 8  Implementation of Path finding using A* algorithm
### DATE: 22/08/2026                                                                           
### REGISTER NUMBER : 212223230028
### AIM: 
To write a program to create graph using waypoints and use A* algorithm to find path between source and destination.
### Algorithm:
```
1. Create a New Unity Project by Open the  Unity Hub and create a new 3D Project,Name the project (e.g., Pathfinding).
2. Create Waypoints in Scene => Create empty or sphere GameObjects ( minimum 4)  and  name it as Waypoint1, Waypoint2, ..., Waypoint4
   Position them freely in the scene (not on a grid)
3. Write a waypoint script to draw the lines between neighbors.
4.Attach waypoint.cs script to each waypoint GameObject and Manually assign neighbors in the Inspector to form a graph.
5. Create a empty game object and name it as WaypointManager - to manage all waypoints
6. Attach Waypoint script to it
7.Write a Pathfinding algorithm using A*search
8. Create a Game Object for Player ( choose capsule or any others) and attach the script to move player from start to end waypoints
```  
### Program:
```
**#1.Waypoint.cs**
using UnityEngine;
using System.Collections.Generic;

public class Waypoint : MonoBehaviour {
    public List<Waypoint> neighbors = new List<Waypoint>();

    // Optional: Draw connections in the editor
    private void OnDrawGizmos() {
        Gizmos.color = Color.yellow;
        foreach (var neighbor in neighbors) {
            if (neighbor != null) {
                Gizmos.DrawLine(transform.position, neighbor.transform.position);
            }
        }
    }
}
**#2. WaypointGraph.cs**
using UnityEngine;

public class WaypointGraph : MonoBehaviour {
    public Waypoint[] allWaypoints;

    void Awake() {
        allWaypoints = FindObjectsOfType<Waypoint>();
    }
}
**#3.Pathfinding.cs**
using System.Collections.Generic;
