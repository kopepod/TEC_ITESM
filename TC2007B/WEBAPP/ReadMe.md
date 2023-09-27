# Web APP

This tutorial shows how to create a WEB APP on android studio. Create an empy project and edit 3 files.

1. MainAcitivity.kt
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
3. activity_main.xml
4. AndroidManifest.xml

