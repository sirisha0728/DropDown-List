## NAME OF THE PROJECT
# Drop Down List
### WHAT IT DOES ?

A drop-down list, similar to a list box, that allows the user to choose one value from a list
When a drop-down list is inactive, it displays a single value. When activated, it displays (drops down) a list of values, from which the user may select one. 


![screeen](https://user-images.githubusercontent.com/36668690/48099471-7c540e80-e1d4-11e8-91f1-43f96730dc0a.JPG)

 #### diagram represent the dropdownlist menu 

## Steps to make it work
 
#### step 1
  open Android studio >file > new > new project 
#### Step 2: 
Open res -> layout -> xml (or) activity_main.xml and add following code. Here we are creating Spinner inside Relative Layout.

<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context=".MainActivity">

    <Spinner
        android:id="@+id/simpleSpinner"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="50dp" />

</RelativeLayout>

## step 3: 

Create a new layout activity in res-> layout and name it custom_spinner_items.xml. Add the following code. Here we are defining basic layout for custom items that will  display inside Spinner.

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="horizontal">

    <ImageView
        android:id="@+id/imageView"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:padding="5dp"
        android:src="@drawable/ic_launcher" /><!--Make sure image is present in Drawable folder-->

    <TextView
        android:id="@+id/textView"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:padding="@dimen/activity_horizontal_margin"
        android:text="Demo"
        android:textColor="#000" />
</LinearLayout>

## step 4:

Open app -> java -> package -> MainActivity.java and add the following code

package com.example.mahi.myapplication;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.Spinner;
import android.widget.Toast;


import com.example.mahi.myapplication.CustomAdapter;

import com.example.mahi.myapplication.R;

public class MainActivity extends AppCompatActivity implements AdapterView.OnItemSelectedListener{


    String[] countryNames={"India","China","Australia","Portugle","America"};
    int flags[] = {R.drawable.india, R.drawable.china, R.drawable.australia, R.drawable.portugle, R.drawable.america};

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //Getting the instance of Spinner and applying OnItemSelectedListener on it
        Spinner spin = (Spinner) findViewById(R.id.simpleSpinner);
        spin.setOnItemSelectedListener(this);

        CustomAdapter customAdapter=new CustomAdapter(getApplicationContext(),flags,countryNames);
        spin.setAdapter(customAdapter);
    }


    //Performing action onItemSelected and onNothing selected
    @Override
    public void onItemSelected(AdapterView<?> arg0, View arg1, int position,long id) {
        Toast.makeText(getApplicationContext(), countryNames[position], Toast.LENGTH_LONG).show();
    }

    @Override
    public void onNothingSelected(AdapterView<?> arg0) {
        // TODO Auto-generated method stub
    }
}

### step 5:

 Create a new Class app -> java-> package and new class name CustomAdapter.java and add the following code. Here we will override the methods of BaseAdapter to fill data in Spinner


package com.example.mahi.myapplication;


import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.ImageView;
import android.widget.TextView;

public class CustomAdapter extends BaseAdapter {
    Context context;
    int flags[];
    String[] countryNames;
    LayoutInflater inflter;

    public CustomAdapter(Context applicationContext, int[] flags, String[] countryNames) {
        this.context = applicationContext;
        this.flags = flags;
        this.countryNames = countryNames;
        inflter = (LayoutInflater.from(applicationContext));
    }

    @Override
    public int getCount() {
        return flags.length;
    }

    @Override
    public Object getItem(int i) {
        return null;
    }

    @Override
    public long getItemId(int i) {
        return 0;
    }

    @Override
    public View getView(int i, View view, ViewGroup viewGroup) {
        view = inflter.inflate(R.layout.custom_spinner_items, null);
        ImageView icon = (ImageView) view.findViewById(R.id.imageView);
        TextView names = (TextView) view.findViewById(R.id.textView);
        icon.setImageResource(flags[i]);
        names.setText(countryNames[i]);
        return view;
    }
}

# documentation regarding steps 


[procedure of project.docx](https://github.com/KavyaReddy95/DropDown-List/files/2555687/procedure.of.project.docx)

## Limitation 

spinner shows the number of items which ever the user given but it collapses the app .So if I want to  show only three items remaining are scrollabe but it doesnt show all the items at atime because of space occupation. So that why by using ArrayAdapter we can display the list.

### Output:

Now run the app (press play button on right top corner)in Emulator/AVD and you will see the custom spinner displaying flags and country names together. Change country names inside spinner and you will see Toast displaying message which country is selected.

https://media.giphy.com/media/4JVQ69mhL0iss5ox2Y/giphy.gif

# Team Members 

1. K.Bala Kavya      (1794948)
2. M.Sirisha         (1794858)
3 .M.Mahender Reddy  (1794805)
