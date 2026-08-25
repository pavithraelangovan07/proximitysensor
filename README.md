# Ex.No:5 Develop a simple application for proximity sensor using Sensor Manager in android studio.


## AIM:

To develop a sensor application for proximity sensor using sensor manager in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Giraffe)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as proximitysensor and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display process of proximitysensor in android mobile devices.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the process of proximitysensor in android mobile devices”.
Developed by:E.pavithra
Registeration Number :212224220072
*/
```
## PROGRAM
## MainActivity.java
```
package com.example.proximitysensorapp;

import android.hardware.Sensor;
import android.hardware.SensorEvent;
import android.hardware.SensorEventListener;
import android.hardware.SensorManager;
import android.os.Bundle;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity implements SensorEventListener {

    private SensorManager sensorManager;
    private Sensor proximitySensor;
    private TextView tvStatus;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        tvStatus = findViewById(R.id.tvStatus);

        // Get the SensorManager service
        sensorManager = (SensorManager) getSystemService(SENSOR_SERVICE);

        // Get the proximity sensor (default)
        if (sensorManager != null) {
            proximitySensor =
                    sensorManager.getDefaultSensor(Sensor.TYPE_PROXIMITY);
        }

        // Check if the device has a proximity sensor
        if (proximitySensor == null) {
            tvStatus.setText("This device has NO proximity sensor.");
            Toast.makeText(
                    this,
                    "No proximity sensor found",
                    Toast.LENGTH_LONG
            ).show();
        } else {
            tvStatus.setText(
                    "Proximity sensor ready.\nMove your hand near the top of the phone."
            );
        }
    }

    @Override
    protected void onResume() {
        super.onResume();

        // Register the listener when app is in foreground
        if (proximitySensor != null) {
            sensorManager.registerListener(
                    this,
                    proximitySensor,
                    SensorManager.SENSOR_DELAY_NORMAL
            );
        }
    }

    @Override
    protected void onPause() {
        super.onPause();

        // Unregister to save battery when app is in background
        if (sensorManager != null) {
            sensorManager.unregisterListener(this);
        }
    }

    @Override
    public void onSensorChanged(SensorEvent event) {

        // When proximity sensor value changes
        if (event.sensor.getType() == Sensor.TYPE_PROXIMITY) {

            float distance = event.values[0];

            // Maximum range value means "far" (no object near)
            float maxRange = proximitySensor.getMaximumRange();

            if (distance < maxRange) {

                // Near
                tvStatus.setText(
                        "Object is NEAR\nDistance: " + distance + " cm"
                );

                getWindow().getDecorView().setBackgroundColor(
                        getResources().getColor(
                                android.R.color.holo_red_dark
                        )
                );

            } else {

                // Far
                tvStatus.setText(
                        "Object is FAR\nDistance: " + distance + " cm"
                );

                getWindow().getDecorView().setBackgroundColor(
                        getResources().getColor(
                                android.R.color.holo_green_dark
                        )
                );
            }
        }
    }

    @Override
    public void onAccuracyChanged(Sensor sensor, int accuracy) {
        // Not needed for this app, but required by the interface
    }
}
```
## activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="16dp">

    <TextView
        android:id="@+id/tvTitle"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Proximity Sensor"
        android:textSize="28sp"
        android:textStyle="bold"
        android:layout_marginBottom="40dp"/>

    <TextView
        android:id="@+id/tvStatus"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Waiting for sensor data..."
        android:textSize="22sp"
        android:gravity="center"/>

</LinearLayout>
```
## OUTPUT
## proximitysensor far
<img width="738" height="1600" alt="WhatsApp Image 2026-08-25 at 8 31 25 AM" src="https://github.com/user-attachments/assets/845c4e4f-5e65-4812-9096-5740c32d3e48" />

## proximitysensor near
<img width="738" height="1600" alt="WhatsApp Image 2026-08-25 at 8 31 21 AM" src="https://github.com/user-attachments/assets/c0654c03-e770-4f01-91f0-369e8d55b857" />





## RESULT
Thus a Simple Android Application to display the details of proximity sensor using sensor manager in Android Studio is developed and executed successfully.
