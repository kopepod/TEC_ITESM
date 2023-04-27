# FPS

This tutorial creates a FPS unity project.

1. PlayerMovement.cs
```c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
	public CharacterController controller;
	public Transform playerRoot;
	public float speed;
	Vector3 velocity;
	public float gravity;
	public bool grounded;
	public LayerMask whatIsGround;
	public Transform groundCheck;
	public float groundCheckDistance;	
	
	public float jumpHeight;
	
	// Start is called before the first frame update
	public void Start()
	{
	
         Mesh mesh = GetComponent<MeshFilter>().sharedMesh;
         float volume = VolumeOfMesh(mesh);
         string msg = "The volume of the mesh is " + volume + " cube units.";
         Debug.Log(msg);
	
	}

	// Update is called once per frame
	private void Update()
	{
		float x = Input.GetAxis("Horizontal") * speed;
		float y = Input.GetAxis("Vertical") * speed;
		
		Vector3 move = playerRoot.forward * y + playerRoot.right * x;
		
		controller.Move(move * Time.deltaTime);		
		
		RaycastHit groundHit;
		
		grounded = Physics.Raycast(groundCheck.position, groundCheck.TransformDirection(Vector3.down), out groundHit, groundCheckDistance, whatIsGround);

		if(grounded == true){
			velocity.y = -2f;
		}
		else{
			velocity.y += gravity * Time.deltaTime;
		}
		
		if(Input.GetKeyDown(KeyCode.Space) && grounded == true){
			velocity.y += Mathf.Sqrt(jumpHeight * -2f * gravity);
		}
		
		controller.Move(velocity * Time.deltaTime);

	}
	
float SignedVolumeOfTriangle(Vector3 p1, Vector3 p2, Vector3 p3)
{
    float v321 = p3.x * p2.y * p1.z;
    float v231 = p2.x * p3.y * p1.z;
    float v312 = p3.x * p1.y * p2.z;
    float v132 = p1.x * p3.y * p2.z;
    float v213 = p2.x * p1.y * p3.z;
    float v123 = p1.x * p2.y * p3.z;
    return (1.0f / 6.0f) * (-v321 + v231 + v312 - v132 - v213 + v123);
}

float VolumeOfMesh(Mesh mesh)
{
    float volume = 0;
    Vector3[] vertices = mesh.vertices;
    int[] triangles = mesh.triangles;
    for (int i = 0; i < mesh.triangles.Length; i += 3)
    {
        Vector3 p1 = vertices[triangles[i + 0]];
        Vector3 p2 = vertices[triangles[i + 1]];
        Vector3 p3 = vertices[triangles[i + 2]];
        volume += SignedVolumeOfTriangle(p1, p2, p3);
    }
    return Mathf.Abs(volume);
}
}
```
MouseLook.cs
```c++
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class MouseLook : MonoBehaviour
{

	public Transform cam;
	public Transform playerRoot;
	public float sensitivity;
	public AudioSource Shot;
	
	float rotX;
	float rotY;	

	// Start is called before the first frame update
	private void Start(){
		Cursor.lockState = CursorLockMode.Locked;
        
	}

	// Update is called once per frame
	void Update(){
		float x = Input.GetAxis("Mouse X") * sensitivity;
		float y = Input.GetAxis("Mouse Y") * sensitivity;
		
		rotX -= y;
		rotY += x;
		
		playerRoot.rotation = Quaternion.Euler(0f, rotY,0f);
		cam.rotation = Quaternion.Euler(rotX, rotY, 0f);
		
		if(Input.GetMouseButtonDown(0)){
			Shot.Play();
		}
		
	}
}
```

