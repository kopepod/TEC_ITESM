# Navigation Drawers

This tutorials shows how to create an APP koltin with navigations containers

1. Create a new project
2. Locate *mobile_navigation.xml* and activate the Design tool
3. Clock on add new destination and select Create New Destination.
4. Add any fragment, mine is Settings Fragment. Next/Finish
5. Add a new Icon the container. File/New/Vector Asset. Click on *Clip Art * and type settings. It would suggest an icon. CLick OK
6. Copy the name, mine is: *baseline_settings_24*. Click on Next/Finish
7. Locate *activity_main_drawer.xml*, i.e., ./app/res/menu/
8. Within the group tag add a new one as:

```xml
        <item
            android:id="@+id/settingsFragment"
            android:icon="@drawable/baseline_settings_24"
            android:title="Settings" />
```

9. The full xml is as:

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    tools:showIn="navigation_view">

    <group android:checkableBehavior="single">
        <item
            android:id="@+id/nav_home"
            android:icon="@drawable/ic_menu_camera"
            android:title="@string/menu_home" />
        <item
            android:id="@+id/nav_gallery"
            android:icon="@drawable/ic_menu_gallery"
            android:title="@string/menu_gallery" />
        <item
            android:id="@+id/nav_slideshow"
            android:icon="@drawable/ic_menu_slideshow"
            android:title="@string/menu_slideshow" />
        <item
            android:id="@+id/settingsFragment"
            android:icon="@drawable/baseline_settings_24"
            android:title="Settings" />
    </group>
</menu>
```

10. Optional, remove the hardcore from the title.
