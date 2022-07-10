<?xml version="1.0" encoding="utf-8"?>

<LinearLayout

 xmlns:android="http://schemas.android.com/apk/res/android"
 xmlns:tools="http://schemas.android.com/tools"
 android:layout_width="match_parent"
 android:layout_height="match_parent"
 android:orientation="vertical"
 android:background="#C0E7EC"
 android:padding="16dp"
 tools:context="com.ProjectGurukul.stopwatch.MainActivity">
 <TextView
 android:id="@+id/time_view"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:layout_gravity="center_horizontal"
 android:layout_marginTop="100dp"
 android:background="@drawable/border"
 android:textAppearance="@android:style/TextAppearance.Large"
 android:textSize="50dp" />
 <Button
 android:id="@+id/start_button"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:layout_gravity="center_horizontal"
 android:layout_marginTop="50dp"
 android:onClick="onClickStart"
 android:text="@string/start" />
 <Button
 android:id="@+id/stop_button"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"
 android:layout_gravity="center_horizontal"
 android:layout_marginTop="50dp"
 android:onClick="onClickStop"
 android:text="@string/stop" />
 <Button
 android:id="@+id/reset_button"
 android:layout_width="wrap_content"
 android:layout_height="wrap_content"

 android:layout_marginTop="50dp"

 android:layout_gravity="center_horizontal"
 android:onClick="onClickReset"
 android:text="@string/reset" />
</LinearLayout>
MainActivity.java
package com.example.stopwatch;
import android.os.Bundle;
import android.app.Activity;
import android.os.Handler;
import android.view.View;
import java.util.Locale;
import android.widget.TextView;
public class MainActivity extends Activity {
 private int sec = 0;
 private boolean is_running;
 private boolean was_running;
 @Override
 protected void onCreate(Bundle savedInstanceState)
 {
 super.onCreate(savedInstanceState);
 setContentView(R.layout.activity_main);
 if (savedInstanceState != null) {
 sec = savedInstanceState.getInt("seconds");
 is_running = savedInstanceState.getBoolean("running");
 was_running = savedInstanceState .getBoolean("wasRunning");
 }
 running_Timer();
 }
 @Override
 public void onSaveInstanceState(
 Bundle savedInstanceState)
 {
 savedInstanceState.putInt("seconds", sec);
 savedInstanceState.putBoolean("running", is_running);
 savedInstanceState.putBoolean("wasRunning", was_running);
 }
 @Override
 protected void onPause()
 {
 super.onPause();
 was_running = is_running;
 is_running = false;
 }

 @Override

 protected void onResume()
 {
 super.onResume();
 if (was_running) {
 is_running = true;
 }
 }
 public void onClickStart(View view)
 {
 is_running = true;
 }
 public void onClickStop(View view)
 {
 is_running = false;
 }
 public void onClickReset(View view)
 {
 is_running = false;
 sec = 0;
 }
 private void running_Timer()
 {
 final TextView t_View = (TextView)findViewById(R.id.time_view);
 final Handler handle = new Handler();
 handle.post(new Runnable() {
 @Override
 public void run()
 {
 int hrs = sec / 3600;
 int mins = (sec % 3600) / 60;
 int secs = sec % 60;
 String time_t = String .format(Locale.getDefault(), " %d:%02d:%02d ", hrs,mins, secs);
 t_View.setText(time_t);
 if (is_running) {
 sec++;
 }
 handle.postDelayed(this, 1000);
 }
 });
 }
}
String.xml

<resources>

 <string name="app_name">ProjectGurukul Stopwatch</string>
 <string name="start"> Start </string>
 <string name="reset"> Reset </string>
 <string name="stop"> Stop </string>
</resources>
Border.xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
 android:layout_width="match_parent"
 android:layout_height="match_parent"
 android:shape="rectangle">
 <stroke
 android:width="2dp"
 android:color="#932424"
 />
</shape>
