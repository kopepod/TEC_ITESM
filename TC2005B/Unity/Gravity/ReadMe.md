# Unity basis - Falling Object

## 1. New Project

Create a new proyect Projects > NewProject > 3D

## 2. Create static objects - Plane, cubes and sphere

GameObject > 3D Object > Plane
GameObject > 3D Object > Sphere
GameObject > Empty

Move the empty object to X = 1 and Z = 1

## 3. Add script to Sphere

1. Click the object
2. See the inspector Add Component
3. Click on Add Component/Script
4. Name the script, mine is Control
5. Click on Component/Physics/RigidBody

4. Edit Control.cs

```c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Control : MonoBehaviour
{
    public List <Transform> Nodes = new List <Transform>();
    private Transform targetNodoPoint;
    // Start is called before the first frame update
    void Start()
    {
        targetNodoPoint = Nodes[0];
    }

    // Update is called once per frame
    void Update()
    {
        Vector3 direction2target = targetNodoPoint.position - transform.position;
        float currentDistance = Vector3.Distance(transform.position, targetNodoPoint.position);
        Debug.Log("Distance to Node: " + currentDistance);	
    }
}

```
Save it and drag the empty Node to Control Nodes elemnts list.

