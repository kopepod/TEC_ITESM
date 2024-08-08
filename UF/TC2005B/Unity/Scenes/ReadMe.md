# Loading Scenes in Unity

1. Create New Project

2. Change scene name

Assets/Scenes/Untitled

second click and *Rename*

3. Create New Scene

File > New Scene

4. Generate new scene (add objects with game object)

5. Add scenes build

File > Build Settings

Click *Add Open Scenes*
CLick *Build*

Save Build *Save*

6. Add script to object

```c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class Controller : MonoBehaviour
{
    public List <Transform> Nodos = new List <Transform>();
    private Transform targetNodoPoint;
    private int targetNodoPointIndex = 0; // Hacia que nodo se va dirigir
	private int lastNodoIndex; // El ultimo nodo que se visito
	private float minDistance = 0.3f; // Esta es la distancia al Nodo
	private float speed = 3.0f; // Rapidez con la que se mueve el robot
    // Start is called before the first frame update
    
    void Start()
    {
        lastNodoIndex = Nodos.Count -1; // Numero total de nodos
        targetNodoPoint = Nodos[targetNodoPointIndex]; // Posicion en vector del nodo
    }

    // Update is called once per frame
    void Update()
    {
        float movementStep = speed * Time.deltaTime; // el incremento en el tiempo
        Vector3 direction2target = targetNodoPoint.position - transform.position; // vector de desplazamiento
        float currentDistance = Vector3.Distance(transform.position, targetNodoPoint.position);
        checkDistance(currentDistance); // revizar si ya llegue al nodo de evento

        transform.position = Vector3.MoveTowards(transform.position, targetNodoPoint.position, movementStep);
    }

    void checkDistance(float currentDistance)
	{
		if( currentDistance <= minDistance)
		{
			targetNodoPointIndex ++;
			UpdatetargetNodoPoint();
		}
	}        

	void UpdatetargetNodoPoint()
	{
		Debug.Log("Current Node: " + targetNodoPointIndex);	
		
		if( targetNodoPointIndex >  lastNodoIndex ){
			targetNodoPointIndex = 0;
			SceneManager.LoadScene("Two", LoadSceneMode.Single);
		}
		targetNodoPoint = Nodos[targetNodoPointIndex];
	}
    
}
```

7. Add Nodes List

Inspector > Script
