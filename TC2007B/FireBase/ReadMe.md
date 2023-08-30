# R/W Firebase Kotlin

This tutorial shows how to create an APP to read and write into a google Firebase database.

On android sutdio
1. Create an empty project in Android Studio
2. Name the project, mine is **UsingFireBase**
3. Open the MainActivity.kt and copy the package name of the project i.e. com.example.**usingfirebase**

Once the android studio project is created
1. Open firebase at https://firebase.google.com/
2. Go to console
3. Click on add project
4. Name the project, mine is **FireBaseTest**.
5. Locate android on the APP type "Add an app to get started". Select the android icon
6. Paste the package name of the project, in my case: com.example.**usingfirebase**
7. Click on register and download the _google-services.json_ file.
8. That file must be placed at: [Project] /UsingFireBase/app/
9. Copy paste the gradle dependencies at build.gradle(Project: )
    id("com.google.gms.google-services") version "4.3.15" apply false
10. Copy paste the gradle dependencies at build.gradle(Module: )
    _Plugins_
    id("com.google.gms.google-services")
    _dependencies_
    implementation(platform("com.google.firebase:firebase-bom:32.2.3"))
11. Clock on go to console
12. Click on the left side [Build/RealTime Database]
13. Click on create database
14. Click on start in **test mode**
15. 


16. Click on sync now on android studio

Android Studio
1. Click on [Tools/Firebase/RealTimeDatabase/Get started with realtime database]
2. Click on add the Realtime Database to your app
    
    
    

