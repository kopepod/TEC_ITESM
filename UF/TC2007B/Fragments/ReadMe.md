# Fragments

This tutorial shows how to create an APP with two fragments.

## Android Studio
1. Create an empty project in Android Studio with predetermined template
2. Name the project, mine is **Test120824**
3. Add three buttons and one TextView with their respectives IDs
4. See the script Below _MainActivity.kt_


```javascript
package com.example.test120824

import android.os.Bundle
import androidx.activity.enableEdgeToEdge

import androidx.core.view.ViewCompat
import androidx.core.view.WindowInsetsCompat
// Automatically created the moment you call the artifacts
import android.widget.Button
import android.widget.TextView

// Manually added
import android.widget.Toast

// Automatically created the moment you call the intent
import android.content.Intent
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContentView(R.layout.activity_main)
        val toastbutton: Button = findViewById(R.id.button)
        val countbutton: Button = findViewById(R.id.button2)
        val randombutton : Button = findViewById(R.id.button3)
        val mytext: TextView = findViewById(R.id.textView)

        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main)) { v, insets ->
            val systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars())
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom)
            insets
        }

        toastbutton.setOnClickListener {
            val myToast = Toast.makeText(this, "Hello Toast!", Toast.LENGTH_SHORT)
            myToast.show()
        }

        countbutton.setOnClickListener{
            //Get the value of the text view
            val countString = mytext.text.toString()
            //Convert value to a number and increment it
            var count: Int = Integer.parseInt(countString)
            count++
            //Display the new value in the text view
            mytext.text = count.toString()
        }

        randombutton.setOnClickListener{
            // The moment you create the next line creates SecondActivity.kt 
            val intent = Intent(this, SecondActivity::class.java)
            // Create the xml fragment on ALT+ENTER i.e. SecondActivity.kt
            val countValue = mytext.text.toString().toInt()
            intent.putExtra(SecondActivity.TOTAL_COUNT, countValue)
            startActivity(intent)

        }
    }
}

```

5. See the script Below _SecondActivity.kt_

```javascript
package com.example.test120824

import android.os.Bundle
import android.widget.Button
import android.widget.TextView
//Manually added
import java.util.Random

// Automatically created after intent call
import android.content.Intent
import androidx.appcompat.app.AppCompatActivity

class SecondActivity : AppCompatActivity() {

    companion object {
        const val TOTAL_COUNT = "total_count"
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        // The moment you add this line the xml will be generated
        setContentView(R.layout.activity_second)
        val backbttn : Button = findViewById(R.id.buttonback)
        showRandomNumber()

        backbttn.setOnClickListener{
            val intent = Intent(this, MainActivity::class.java)
            startActivity(intent)
        }

    }

    private fun showRandomNumber(){
        //get the count from the intent extras
        val textviewrandom: TextView = findViewById(R.id.textView2)
        val count = intent.getIntExtra(TOTAL_COUNT, 0)
        //Generate a random number
        val random = Random()
        var randomInt = 0
        if(count > 0){
            randomInt = random.nextInt(count+1)
        }
        textviewrandom.text = randomInt.toString()
    }
}
```

6. Modify the _AdroidManifest.xml_ to include the Second Activity adding these lines

```xml
<activity android:name=".SecondActivity"></activity>
```

The file should look like this

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Test120824"
        tools:targetApi="31">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <activity android:name=".SecondActivity"></activity>
    </application>

</manifest>
``` 
    
    

