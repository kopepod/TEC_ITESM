# R/W Firebase Kotlin

This tutorial shows how to create an APP to read and write into a google Firebase database.

## Android Studio
1. Create an empty project in Android Studio
2. Name the project, mine is **UsingFireBase**


## Google Console / Android Studio
1. Open firebase at https://firebase.google.com/
2. Go to console
3. Click on add project
4. Name the project, mine is **FireBaseTest**.
5. Locate android on the APP type "Add an app to get started". Select the android icon
6. Set the package name of the project, in my case: com.example.**usingfirebase**
7. Click on register and download the _google-services.json_ file.
8. That file must be placed at: [Project] /UsingFireBase/app/
9. Copy paste the gradle dependencies at build.gradle(Project: )
    ```javascript
    id("com.google.gms.google-services") version "4.3.15" apply false
    ```
11. Copy paste the gradle dependencies at build.gradle(Module: )
    
    _Plugins_
    ```javascript
    id("com.google.gms.google-services")
    ```
    _dependencies_
    ```javascript
    implementation(platform("com.google.firebase:firebase-bom:32.2.3"))
    ```
13. Click on go to console
14. Click on the left side [Build/RealTime Database]
15. Click on create database
16. Click on start in **test mode**
17. Click on sync now on android studio
    
## Android Studio
1. Click on [Tools/Firebase/RealTimeDatabase/Get started with realtime database]
2. Click on add the Realtime Database to your app

### Check the Database / Android Studio
Test the R/W database access in _MainActivity.kt_ (this is not the final file see below)
```javascript
package com.example.usingfirebase

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
// add this import
import com.google.firebase.database.FirebaseDatabase

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // set this value to firebase
        var database = FirebaseDatabase.getInstance().reference
        database.setValue("TEC")
    }
}

```
Check the following value is set:

https://{projet_ID}.firebaseio.com/:"TEC"

### Add form / Android Studio
1. Go to [Android] /res/layout/activity_main.xml and create three _Plain Text_ items and two _Button_ from the Palette:
   Rename android:text=" ... " -> android:hint=" ... " for all _Plain Text_ elements as: </br>
   android:hint="ID" \
   android:hint="Name"\
   android:hint="Salary" \
   with the respective id:</br>
   android:id="@+id/reg_id" \
   android:id="@+id/reg_name" \
   android:id="@+id/reg_sal" \
   and for the _Button_ as:</br>
   android:text="Insert" \
   android:id="@+id/insert_button" \
   android:text="Fetch" \
   android:id="@+id/fetch_button" \
   See the full file at the end \
3. Add buttons functionality in _MainActivity.kt_
   ```javascript
   package com.example.usingfirebase
   import androidx.appcompat.app.AppCompatActivity
   import android.os.Bundle
   import com.google.firebase.database.FirebaseDatabase
   // add these resources
   import android.widget.Button
   import android.widget.EditText
   import android.widget.TextView
   import com.google.firebase.database.DataSnapshot
   import com.google.firebase.database.DatabaseError
   import com.google.firebase.database.ValueEventListener

   class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val database = FirebaseDatabase.getInstance().reference
        //database.setValue("TEC")

        // get the elements values by their id
        val insertbutton: Button = findViewById(R.id.insert_button)
        val fetchtbutton: Button = findViewById(R.id.fetch_button)
        val textID: EditText = findViewById(R.id.reg_id)
        val textNA: EditText = findViewById(R.id.reg_name)
        val textSA: EditText = findViewById(R.id.reg_sal)
        val textMessage: TextView = findViewById(R.id.messageAPP)

        // call the button functionality
        insertbutton.setOnClickListener {
            val id = textID.text.toString().toInt()
            val na = textNA.text.toString()
            val sa = textSA.text.toString().toInt()

            // Overwrite every single register on request
            //database.setValue( Users(id,na,sa) )
            // Create a new entry on every request
            database.child(id.toString()).setValue(Users(id,na,sa))
        }

        // call the button functionality
        fetchtbutton.setOnClickListener {
            // Retrive registers
            // Hover *object* to implement members (alt+enter)
            val fetchData = object : ValueEventListener{
                override fun onDataChange(snapshot: DataSnapshot) {
                    //TODO("Not yet implemented")
                    val mssg = StringBuilder()
                    for(children in snapshot.children){
                        val userID = children.child("userID").value
                        val userNA = children.child("userNA").value
                        val userSA = children.child("userSA").value
                        mssg.append("key: ${children.key} ID: $userID Name:  $userNA Salary: $userSA \n")
                    }
                    textMessage.setText(mssg)
                }

                override fun onCancelled(error: DatabaseError) {
                    TODO("Not yet implemented")
                }
            }
            // call the fetch data method
            database.addValueEventListener(fetchData)
            database.addListenerForSingleValueEvent(fetchData)
         }



     }
   }
   ```
4. Create the file _Users.kt_
   ```javascript
   package com.example.usingfirebase
   class Users {
    var userID = 0
    var userNA = ""
    var userSA = 0
    constructor(userID: Int, userNA: String, userSA: Int){
        this.userID = userID
        this.userNA = userNA
        this.userSA = userSA

    }
   }
   ```
5. Full file _activity_main.xml_
   ```xml
	<?xml version="1.0" encoding="utf-8"?>
	<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    xmlns:app="http://schemas.android.com/apk/res-auto"
	    xmlns:tools="http://schemas.android.com/tools"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent"
	    tools:context=".MainActivity">
	
	    <TextView
	        android:id="@+id/messageAPP"
	        android:layout_width="wrap_content"
	        android:layout_height="wrap_content"
	        android:text="Hello World!"
	        app:layout_constraintBottom_toBottomOf="parent"
	        app:layout_constraintEnd_toEndOf="parent"
	        app:layout_constraintStart_toStartOf="parent"
	        app:layout_constraintTop_toBottomOf="@+id/reg_sal" />
	
	    <EditText
	        android:id="@+id/reg_id"
	        android:layout_width="wrap_content"
	        android:layout_height="wrap_content"
	        android:layout_marginTop="26dp"
	        android:ems="10"
	        android:hint="@string/id"
	        android:inputType="textPersonName"
	        android:minHeight="48dp"
	        app:layout_constraintEnd_toEndOf="parent"
	        app:layout_constraintStart_toStartOf="parent"
	        app:layout_constraintTop_toTopOf="parent" />
	
	    <EditText
	        android:id="@+id/reg_name"
	        android:layout_width="wrap_content"
	        android:layout_height="wrap_content"
	        android:layout_marginTop="44dp"
	        android:ems="10"
	        android:hint="@string/name"
	        android:inputType="textPersonName"
	        android:minHeight="48dp"
	        app:layout_constraintEnd_toEndOf="parent"
	        app:layout_constraintHorizontal_bias="0.497"
	        app:layout_constraintStart_toStartOf="parent"
	        app:layout_constraintTop_toBottomOf="@+id/reg_id" />
	
	    <EditText
	        android:id="@+id/reg_sal"
	        android:layout_width="wrap_content"
	        android:layout_height="wrap_content"
	        android:layout_marginTop="54dp"
	        android:ems="10"
	        android:hint="@string/salary"
	        android:inputType="textPersonName"
	        android:minHeight="48dp"
	        app:layout_constraintEnd_toEndOf="parent"
	        app:layout_constraintStart_toStartOf="parent"
	        app:layout_constraintTop_toBottomOf="@+id/reg_name" />
	
	    <Button
	        android:id="@+id/insert_button"
	        android:layout_width="wrap_content"
	        android:layout_height="wrap_content"
	        android:layout_marginTop="67dp"
	        android:layout_marginEnd="115dp"
	        android:text="@string/insert"
	        app:layout_constraintBottom_toTopOf="@+id/messageAPP"
	        app:layout_constraintEnd_toStartOf="@+id/fetch_button"
	        app:layout_constraintStart_toStartOf="parent"
	        app:layout_constraintTop_toBottomOf="@+id/reg_sal" />
	
	    <Button
	        android:id="@+id/fetch_button"
	        android:layout_width="wrap_content"
	        android:layout_height="wrap_content"
	        android:layout_marginTop="66dp"
	        android:text="@string/fetch"
	        app:layout_constraintBottom_toTopOf="@+id/messageAPP"
	        app:layout_constraintEnd_toEndOf="parent"
	        app:layout_constraintStart_toEndOf="@+id/insert_button"
	        app:layout_constraintTop_toBottomOf="@+id/reg_sal" />
	
	</androidx.constraintlayout.widget.ConstraintLayout>
   ``` 
    
    

