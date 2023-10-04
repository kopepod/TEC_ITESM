# Web APP

This tutorial shows how to create a WEB APP on android studio. Create an empy project and edit 3 files.

1. MainActivity.kt
  ```javascript
package com.example.webappsol

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.webkit.WebView //add this
import android.webkit.WebViewClient //add this

class MainActivity : AppCompatActivity() {

    private lateinit var webREF: WebView //Define the view

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // add these lines
        webREF = findViewById(R.id.WEBCTRL) // Find the xml ID
        webREF.webViewClient = WebViewClient() // Method call
        webREF.loadUrl("https://sites.google.com/tec.mx/tc2007b") // APP URL
        webREF.settings.javaScriptEnabled = true // enable JS
        webREF.settings.setSupportZoom(true) // enable zoom

    }

    // back button
    override fun onBackPressed() {
        // go back if possible
        if (webREF.canGoBack())
            webREF.goBack()
        // exit otherwise
        else
            super.onBackPressed()

    }
}
```
2. activity_main.xml

 ```xml
 <?xml version="1.0" encoding="utf-8"?>
 <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <WebView
        android:id="@+id/WEBCTRL"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
 </androidx.constraintlayout.widget.ConstraintLayout>
 ```
3. AndroidManifest.xml

 ```xml
 <?xml version="1.0" encoding="utf-8"?>
 <manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

    <application
        android:usesCleartextTraffic="true"
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/Theme.WEBAPPsol"
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

