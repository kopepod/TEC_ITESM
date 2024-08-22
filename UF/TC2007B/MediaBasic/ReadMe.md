# Play a sound and change the APP icon

1. Create a template project, mine is Test220824

2. Download an audio file, e.g.

```bash
yt-dlp URL
```

3. Create inside the _res_ folder a new folder called _raw_. You should see this tree.

```bash
tree -d -L 4
.
├── app
│   ├── build
│   │   ├── generated
│   │   │   └── res
│   │   ├── intermediates
│   │   │   ├── aar_metadata_check
│   │   │   ├── ..... (lot more)
│   │   ├── kotlin
│   │   │   └── compileDebugKotlin
│   │   ├── outputs
│   │   │   └── logs
│   │   └── tmp
│   │       └── kotlin-classes
│   └── src
│       ├── androidTest
│       │   └── java
│       ├── main
│       │   ├── java
│       │   └── res  (THIS ONE HERE!!!)
│       └── test
│           └── java
└── gradle
    └── wrapper
```

4. Place your audio file inside _raw_. You should see this tree

```bash
tree app/src/main/res/raw/
app/src/main/res/raw/
└── sound.mp3
```

5. Open the main layout and add a button, and assign and ID that button.

Then call it on the main activity file, i.e., _MainActivity.kt_. Also add the media player segment to the call.

```java
package com.example.test220824

import android.media.MediaPlayer
import android.os.Bundle
import android.widget.Button
import androidx.activity.enableEdgeToEdge
import androidx.appcompat.app.AppCompatActivity
import androidx.core.view.ViewCompat
import androidx.core.view.WindowInsetsCompat

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContentView(R.layout.activity_main)

        val bttnSnd : Button = findViewById(R.id.bttn)

        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main)) { v, insets ->
            val systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars())
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom)
            insets
        }

        bttnSnd.setOnClickListener {
            var MP = MediaPlayer.create(this, R.raw.sound) // media player segment
            MP.start() // media player segment


        }
    }
}
```
6. Modify the manifest adding these permissions.

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
```
The full manifest:
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.WAKE_LOCK" />

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Test220824"
        tools:targetApi="31">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

7. Create an svg icon. Or download mine from this repository (pig.svg).

8. Click on the *ResourceManager* i.e. View/ToolWindows/ResourceManager

9. Add an image asset on the *+* (upper left corner) and selecting the *ic_launcher_foreground* layout.

10. On the *sourceasset* select the path of the svg icon, scale it, and click Next/Finish.

11. Launch the application, when the button is pressed the audio file should pay, rise the volume on the emulator.





