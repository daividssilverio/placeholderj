# PlaceholderJ
PlaceholderJ is a simple Android library created to assist you handling placeholders for screens with empty lists, no itens found, loading and errors.

##Observations
Before you start, it is important to keep in mind that PlaceholderJ views were projected to handle errors generated from Retrofit requests. So, make sure you're passsing only RetrofitErros to PlaceholderJ.

Feel free to implement your own error handling for another cases, and please send me a pull to request. :)

### How to include this library:

``` groovy
allprojects {
    repositories {
        ...
        maven { url "https://jitpack.io" }
    }
}
```

``` groovy
dependencies {
  compile 'com.github.jackmiras:placeholderj:1.0.2'
}
```
###Quick Start
-----------
####Step 1 - You will need some views for PlaceHolderJ in your layout.
``` xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <include layout="@layout/item_toolbar" />

    <android.support.v7.widget.RecyclerView
        android:id="@+id/recyclerview_cupon"
        android:scrollbars="vertical"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_marginTop="?attr/actionBarSize"
        android:padding="8dp" />

    <include layout="@layout/view_empty" />

    <include layout="@layout/view_loading" />

    <include layout="@layout/view_error" />

</FrameLayout>
```
As you see, you can include a loading, empty and error views to your layout, but is good practice to include only the views that you will use.

####Step 2 - You will need create a instance of PlaceHolderJ in your Activity or Fragment.
##### Activity
``` java
public class MainActivity extends AppCompatActivity {

    PlaceHolderJ placeHolderJ;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        placeHolderJ = new PlaceHolderJ(SampleApplication.getPlaceHolderManager());
        placeHolderJ.init(this, R.id.recyclerview_cupon, R.id.view_loading, R.id.view_empty, R.id.view_error);
    }
}
```
##### Fragment
``` java
public class MainFragment extends Fragment {

    private PlaceHolderJ placeHolderJ;

    @Nullable
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        container = (ViewGroup) inflater.inflate(R.layout.fragment_main, null);
        placeHolderJ = new PlaceHolderJ(SampleApplication.getPlaceHolderManager());
        placeHolderJ.init(container, R.id.recyclerview_cupon, R.id.view_loading, R.id.view_empty, R.id.view_error);
        return container;
    }
}
```
Note that in placeHolderJ.init() you can pass five parameters but only the Activity or View, the id of the view that will be manipulated to show the placeholders and at least the id of 1 placeholder are mandatory.

Contributor: Daivid Silverio (https://github.com/daividssilverio) - Docs
