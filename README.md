# Map Scale View
[![](https://jitpack.io/v/pengrad/MapScaleView.svg)](https://jitpack.io/#pengrad/MapScaleView)

Scale view for Google Maps Android API  

![Image](images/image.png)

Include in layout file over map
```xml
<FrameLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <fragment
        android:id="@+id/mapFragment"
        class="com.google.android.gms.maps.SupportMapFragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

    <com.github.pengrad.mapscaleview.MapScaleView
        android:id="@+id/scaleView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="bottom|end"
        android:layout_margin="4dp"/>
</FrameLayout>
```

Or with custom style
```xml
<com.github.pengrad.mapscaleview.MapScaleView
        android:id="@+id/scaleView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="bottom|end"
        android:layout_margin="4dp"
        app:scale_color="#009"
        app:scale_strokeWidth="3dp"
        app:scale_textSize="20sp"/>
```

Update on map changed
```java
MapScaleView scaleView = (MapScaleView) findViewById(R.id.scaleView);
scaleView.update(map.getProjection(), map.getCameraPosition());
```

Full example with subscribing to map events and updating scale view
```java
@Override
public void onMapReady(GoogleMap googleMap) {
    map = googleMap;
    googleMap.setOnCameraMoveListener(this);
    googleMap.setOnCameraIdleListener(this);
    googleMap.setOnCameraChangeListener(this);
}

@Override
public void onCameraMove() {
    scaleView.update(map.getProjection(), map.getCameraPosition());
}

@Override
public void onCameraIdle() {
    scaleView.update(map.getProjection(), map.getCameraPosition());
}

@Override
public void onCameraChange(CameraPosition cameraPosition) {
    scaleView.update(map.getProjection(), cameraPosition);
}
```

# Download

**Step 1.** Add the JitPack repository to your build file
```groovy
allprojects {
    repositories {
        ...
        maven { url "https://jitpack.io" }
    }
}
```

**Step 2.** Add the dependency
```groovy
dependencies {
    compile 'com.github.pengrad:MapScaleView:1.0.0'
}
```

