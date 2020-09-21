# MyNote_AndroidStudio

### Index:

[Change landscpe and no action bar when Activity `extends AppCompatActivity`](#0001)

[Button click event template/sample](#0002) 

[Draw pixel art on background full screen](#0003)

[Use normal layout and custom View at same time](#0004)

[Use immersive sticky mode (no navigation bar, state bar)](#0005)

[Get width, height when using immersive sticky mode](#0006)

[Open another activity](#0007)

[Navigation back button click](#0008)

[Navigation Home Press](#0009)

[Activity flow with surfaceview and navigation button press.](#0010)

[You can't restart thread, you should new a instance to use.](#0011)

[Set Color relate to `/res/value/color.xml`](#0012)

[Change Bitmap Color](#0013)

[Play Sound](#0014)

[Change project name on Android Studio](#0015)

[Play Video](#0016)

[Sensor Orientation](#0017)

___

### 0001

Change landscpe and no action bar when Activity `extends AppCompatActivity` 

add following code to `AndroidManifest.xml`  in `activity` tag

```java
//<activity ..
android:screenOrientation="landscape"
android:theme="@style/Theme.AppCompat.Light.NoActionBar"
tools:ignore="LockedOrientationActivity"
// ... >
```

https://stackoverflow.com/questions/21814825/you-need-to-use-a-theme-appcompat-theme-or-descendant-with-this-activity

___

### 0002

Button click event template/sample

```java
public class MainActivity extends AppCompatActivity implements View.OnClickListener{

    Button btnStart;
    Button btnExit;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btnStart = findViewById(R.id.btnStart);
        btnExit = findViewById(R.id.btnExit);

        btnStart.setOnClickListener(this);
        btnExit.setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        if(v == btnStart){
            Log.i("", "btnStart click");
        }else if(v == btnExit){
            Log.i("", "btnExit click");
        }
        /*
        switch(v.getId()){
        	case R.id.btnStart:
        		break;
        	case R.id.btnExit:
        		break;
        }
        */
    }
}
```

https://spicyboyd.blogspot.com/2018/04/apponclick5.html

___

Button should not assign before `setContentView(R.layout.activity_main)` 

___

### 0003

Draw pixel art on background full screen

remember `background.png`  put on `drawable-nodpi` folder

```java
public class MenuBackground extends View {

    Bitmap bitmap;
    Paint paint = new Paint();
    int width;
    int height;

    public MenuBackground(Context context) {
        super(context);
        bitmap = BitmapFactory.decodeResource(this.getResources(), R.drawable.background);
        paint.setAntiAlias(false);
        paint.setDither(true);
        paint.setFilterBitmap(false);
        width = bitmap.getWidth();
        height = bitmap.getHeight();
    }

    @Override
    protected void onDraw(Canvas canvas) {
        canvas.scale(getWidth() / (float)width , getHeight() / (float)height);
        canvas.drawBitmap(bitmap,0,0, paint);
        super.onDraw(canvas);
    }
}
```

https://stackoverflow.com/questions/46028774/disable-anti-aliasing-on-android-imageview

http://www.41post.com/4241/programming/android-disabling-anti-aliasing-for-pixel-art

___

### 0004

Use normal layout and custom View at same time

get layout class and use `addView()`

```java
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    root = findViewById(R.id.root);
    root.addView(new MenuBackground(this));
}
```

___

### 0005

Use immersive sticky mode (no navigation bar, state bar)

```java
@RequiresApi(api = Build.VERSION_CODES.KITKAT)
static void setImmersiveSticky(Activity activity){
    int option = View.SYSTEM_UI_FLAG_LOW_PROFILE
        | View.SYSTEM_UI_FLAG_FULLSCREEN
        | View.SYSTEM_UI_FLAG_LAYOUT_STABLE
        | View.SYSTEM_UI_FLAG_IMMERSIVE_STICKY
        | View.SYSTEM_UI_FLAG_LAYOUT_HIDE_NAVIGATION
        | View.SYSTEM_UI_FLAG_HIDE_NAVIGATION;
    activity.getWindow().getDecorView().setSystemUiVisibility(option);
}
```

https://developer.android.google.cn/training/system-ui/immersive?hl=zh-cn

https://www.jianshu.com/p/11a2b780fd9b

___

### 0006

Get width, height when using immersive sticky mode

```java
DisplayMetrics displaymetrics = new DisplayMetrics();
activity.getWindowManager().getDefaultDisplay().getRealMetrics(displaymetrics);
screenWidth = displaymetrics.widthPixels;
screenHeight = displaymetrics.heightPixels;
```

___

### 0007

Open another activity

```java
Intent intent = new Intent(this, GameActivity.class);
startActivity(intent);
```

___

### 0008

Navigation back button click

override this:

```java
@Override
public void onBackPressed() {
    super.onBackPressed();
}
```

if you delete `super.onBackPressed();`, 

You can't exit or back to upper activity by click navigation back button.

it is good and we can control the behavior of navigation back button.

Also, there are tutorial for press Back button two times and back : 

https://www.youtube.com/watch?v=1Nmy88n7CZ8

___

### 0009

Navigation Home Press

No, you can't.

You can't override Home button.

https://stackoverflow.com/questions/4783960/call-method-when-home-button-pressed

https://stackoverflow.com/questions/8881951/detect-home-button-press-in-android/8883447#8883447

___

### 0010

Activity flow with surfaceview and navigation button press.

there show three flow line:

[1] : `onStart -> onResume -> sufaceCreated -> surfaceChanged` 

[2] : `onPause -> surfaceDestroyed` 

[3] : `onBackPressed -> [2]` 

___

and flow event:

Start app -> [1]

[1] -> Press Home or Overview(the third/right one) -> [2]

[2] -> Back to app -> [1]

[1] -> press Back(the left one) -> [3]

You can control press back behaviour by override onBackPressed : [0008](#0008)

https://source.android.com/devices/graphics/arch-sv-glsv

https://blog.csdn.net/ttmxh/article/details/7530531

___

### 0011

You can't restart thread, you should new a instance to use.

https://stackoverflow.com/questions/3826402/how-can-i-restart-a-thread-in-java-android-from-a-button/3826980

___

### 0012

Set Color relate to `/res/value/color.xml`

```java
int color = ContextCompat.getColor(context, R.color.white);
paint.setColor(color);
```

https://stackoverflow.com/questions/12899428/how-to-set-paint-setcolorr-color-white

https://stackoverflow.com/questions/31590714/getcolorint-id-deprecated-on-android-6-0-marshmallow-api-23/31590927#31590927

___

### 0013

Change Bitmap Color

```java
Paint p = new Paint();
ColorFilter filter = new LightingColorFilter(Color.RED, 0);
p.setColorFilter(filter);
```

https://gamedev.stackexchange.com/questions/5393/how-do-i-blend-a-bitmap-with-a-color

https://stackoverflow.com/questions/5699810/how-to-change-bitmap-image-color-in-android

On the other hand, you can change pixel by pixel

https://stackoverflow.com/questions/11449687/android-change-the-color-of-a-bitmap

https://stackoverflow.com/a/55204374/11693034 

___

### 0014

Play Sound

```java
MediaPlayer mediaPlayer;
mediaPlayer = MediaPlayer.create(<Context>, R.raw.xxx);

// Start
mediaPlayer.start();

// Stop (can not restart)
mediaPlayer.stop();

// Releases resources 
mediaPlayer.release();

// Reset (can restart) //
mediaPlayer.pause();
mediaPlayer.seekTo(0);

// Looping
mediaPlayer.setLooping(true);
```

https://developer.android.com/guide/topics/media/mediaplayer

___

### 0015

Change project name on Android Studio

- Close Android Studio
- **Change project root directory name**
- Open Android Studio
- Open the project (not from local history but by browsing to it)
- Clean project

If your `settings.gradle` contains the below line, either delete it or update it to the new name.

```
rootProject.name = 'Your project name'
```

Rebuild Project

Click File -> Sync Project with Gradle Files

https://stackoverflow.com/questions/18276872/change-project-name-on-android-studio 

___

### 0016

Play Video

```java
videoView = findViewById(R.id.videoView);
String path = "android.resource://" + getPackageName() + "/" + R.raw.samplevideo;
Uri uri = Uri.parse(path);
videoView.setVideoURI(uri);

// Start 
videoView.start();

// Pause
videoView.pause();

// Reset (can restart) //
videoView.pause();
videoView.seekTo(0);

// I don't know how to use resume(), stop()
```

https://developer.android.com/reference/android/widget/VideoView.html

___

### 0017

Sensor Orientation

```java
package com.example.motionsensorstest;

import android.content.Context;
import android.hardware.Sensor;
import android.hardware.SensorEvent;
import android.hardware.SensorEventListener;
import android.hardware.SensorManager;
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity implements SensorEventListener{

    SensorManager sensorManager;

    private Sensor accelerometer;
    private Sensor magnetometer;

    float[] accelerometerValues = new float[3];
    float[] magneticFieldValues = new float[3];

    float[] values = new float[3];

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        sensorManager = (SensorManager) getSystemService(Context.SENSOR_SERVICE);
        assert sensorManager != null;
        accelerometer = sensorManager.getDefaultSensor(Sensor.TYPE_ACCELEROMETER);
        magnetometer = sensorManager.getDefaultSensor(Sensor.TYPE_MAGNETIC_FIELD);
    }

    protected void onResume() {
        super.onResume();
        sensorManager.registerListener(this, accelerometer, SensorManager.SENSOR_DELAY_UI);
        sensorManager.registerListener(this, magnetometer, SensorManager.SENSOR_DELAY_UI);
    }

    @Override
    protected void onPause() {
        super.onPause();
        sensorManager.unregisterListener(this);
    }

    public void onSensorChanged(SensorEvent sensorEvent) {
        switch (sensorEvent.sensor.getType()) {
            case Sensor.TYPE_MAGNETIC_FIELD:
                magneticFieldValues = sensorEvent.values;
                break;
            case Sensor.TYPE_ACCELEROMETER:
                accelerometerValues = sensorEvent.values;
                break;
        }
        updateOrientation();
        Log.i("","z: " + values[0] + "\tx: " + values[1] + "\ty: " + values[2]);
    }

    private  void updateOrientation() {
        float[] R = new float[9];
        SensorManager.getRotationMatrix(R, null, accelerometerValues, magneticFieldValues);
        SensorManager.getOrientation(R, values);

        values[0] = (float) Math.toDegrees(values[0]);
        values[1] = (float) Math.toDegrees(values[1]);
        values[2] = (float) Math.toDegrees(values[2]);
    }

    @Override
    public void onAccuracyChanged(Sensor sensor, int accuracy) {
        Log.i("", "onAccuracyChanged()");
    }
}
```

Package to be a class `MyOrientationSensorManager` :

```java
package com.example.motionsensorstest;

import android.content.Context;
import android.hardware.Sensor;
import android.hardware.SensorEvent;
import android.hardware.SensorEventListener;
import android.hardware.SensorManager;
import android.util.Log;

public class MyOrientationSensorManager implements SensorEventListener {

    public Context context;
    public SensorManager sensorManager;

    public Sensor accelerometer;
    public Sensor magnetometer;

    public float[] accelerometerValues = new float[3];
    public float[] magneticFieldValues = new float[3];

    public float[] values = new float[3];

    MyOrientationSensorManager(Context context){
        this.context = context;
        sensorManager = (SensorManager) context.getSystemService(Context.SENSOR_SERVICE);
        assert sensorManager != null;
        accelerometer = sensorManager.getDefaultSensor(Sensor.TYPE_ACCELEROMETER);
        magnetometer = sensorManager.getDefaultSensor(Sensor.TYPE_MAGNETIC_FIELD);
    }

    public void reset(){
        sensorManager.registerListener(this, accelerometer, SensorManager.SENSOR_DELAY_UI);
        sensorManager.registerListener(this, magnetometer, SensorManager.SENSOR_DELAY_UI);
    }

    public void cancel(){
        sensorManager.unregisterListener(this);
    }

    public void onSensorChanged(SensorEvent sensorEvent) {
        switch (sensorEvent.sensor.getType()) {
            case Sensor.TYPE_MAGNETIC_FIELD:
                magneticFieldValues = sensorEvent.values;
                break;
            case Sensor.TYPE_ACCELEROMETER:
                accelerometerValues = sensorEvent.values;
                break;
        }
        updateOrientation();
        Log.i("","z: " + values[0] + "\tx: " + values[1] + "\ty: " + values[2]);
    }

    private  void updateOrientation() {
        float[] R = new float[9];
        SensorManager.getRotationMatrix(R, null, accelerometerValues, magneticFieldValues);
        SensorManager.getOrientation(R, values);

        values[0] = (float) Math.toDegrees(values[0]);
        values[1] = (float) Math.toDegrees(values[1]);
        values[2] = (float) Math.toDegrees(values[2]);
    }

    @Override
    public void onAccuracyChanged(Sensor sensor, int accuracy) {
        Log.i("", "onAccuracyChanged()");
    }

}
```

___



