
# Ex.No:4 Create Your Own Content Providers to get Contacts details.


## AIM:

To create your own content providers to get contacts details using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min. required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as “ex.no.3″ and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Get contacts details and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the text create your own content providers to get contacts details.
Developed by: GANESH PRABHU J
Registeration Number : 212223220023
*/
```

MainActivity.java
```
package com.example.exp4;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

import android.Manifest;
import android.annotation.SuppressLint;
import android.content.ContentResolver;
import android.content.pm.PackageManager;
import android.database.Cursor;
import android.net.Uri;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.util.Log;
import android.view.View;

public class MainActivity extends AppCompatActivity {

    private static final int REQUEST_CONTACTS = 100;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    public void btnGetContacts(View v) {
        getPhoneContacts();
    }

    public void getPhoneContacts() {

        if (ContextCompat.checkSelfPermission(this,
                Manifest.permission.READ_CONTACTS)
                != PackageManager.PERMISSION_GRANTED) {

            ActivityCompat.requestPermissions(this,
                    new String[]{Manifest.permission.READ_CONTACTS},
                    REQUEST_CONTACTS);
            return;
        }

        ContentResolver contentResolver = getContentResolver();
        Uri uri = ContactsContract.CommonDataKinds.Phone.CONTENT_URI;

        Cursor cursor = contentResolver.query(uri,
                null,
                null,
                null,
                null);

        if (cursor == null) {
            return;
        }

        Log.i("CONTACT_PROVIDER",
                "TOTAL # of CONTACTS ::: " + cursor.getCount());

        if (cursor.getCount() > 0) {

            while (cursor.moveToNext()) {

                @SuppressLint("Range")
                String contactName = cursor.getString(
                        cursor.getColumnIndex(
                                ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME));

                @SuppressLint("Range")
                String contactNumber = cursor.getString(
                        cursor.getColumnIndex(
                                ContactsContract.CommonDataKinds.Phone.NUMBER));

                Log.i("CONTACT_PROVIDER_DEMO",
                        "Contact Name ::: " + contactName +
                                " Phone Number ::: " + contactNumber);
            }
        }

        cursor.close();
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        if (requestCode == REQUEST_CONTACTS) {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                getPhoneContacts();
            } else {
                Log.e("CONTACT_PROVIDER", "Permission denied to read contacts");
            }
        }
    }


}
```

activity_main.xml

```
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Content Provider"
        android:textSize="30sp"
        android:textStyle="bold"
        android:gravity="center"
        android:padding="20dp"/>

    <Button
        android:id="@+id/button"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Get Contact Details"/>

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_marginTop="20dp">

        <TextView
            android:id="@+id/contactText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Contact details will appear here"
            android:textSize="18sp"
            android:padding="10dp"/>

    </ScrollView>

</LinearLayout>
```


android_manifest.xml
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android">

    <uses-permission android:name="android.permission.READ_CONTACTS"/>

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="ContentProvider"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Contentprovider">

        <activity
            android:name=".MainActivity"
            android:exported="true">

            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>

        </activity>

    </application>

</manifest>
```

## OUTPUT

<img width="1919" height="1024" alt="Screenshot 2026-08-21 092708" src="https://github.com/user-attachments/assets/93c9343e-5130-49f9-9b3f-64fd570732e1" />

<img width="1919" height="1024" alt="Screenshot 2026-08-21 092801" src="https://github.com/user-attachments/assets/57cd60d4-67bb-4831-8640-5983633da8f8" />


## RESULT
Thus a Simple Android Application create your own content providers to get contacts details using Android Studio is developed and executed successfully.




