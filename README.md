OverScrollListView
==================

Simple ListView subclass that allows you to set the over scroll max and hook a listener to see how far you have over scrolled.

To use just grab the OverScrollListView.java file and add it to your project. Its not big enough to throw up on maven central.

You can add the OverScrollListView to your xml file or set it up in code like any other widget.

```xml
<com.yourpackage.widgets.OverScrollListView
    android:id="@+id/over_scroll_list"
    android:background="@color/default_light_grey"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />
```

Then grab a reference to it in your Activity/Fragment.

```java
@InjectView(R.id.over_scroll_list) // ButterKnife
OverScrollListView listView;
```

Initialize like any other list, the only extra step is to add the Offset listener (optional). 

```java
listView.setAdapter(myAwesomeAdapter);
listView.setOverScrollOffsetY(150); // default is also 150.
listView.setOverscrollHeader(myDrawable); // set a drawable to be shown in the scroll offset area.
listView.setOverScrollListener(new OverScrollListView.OverScrolledListener() {
@Override
public void overScrolled(int scrollY, int maxY, boolean exceededOffset, boolean didFinishOverScroll) {

    // You can check the scrollY value and use it however you need. (0 - yMax)
    if(scrollY < (maxY/2)) { // you are half way to full offset.
        // do something
    }else if(scrollY == maxY) { // you are at full offset.
        // do Something
    }else{  // anything below half offset.
        // do Something
    } 
    
    // You can check if they are exceeding the offset. Still pulling down after full offset.
    if(exceededOffset){
        // do something
    }
    
    // You can check if the view is back to 0 offset after its been pulled.
    // This will currently be true if you swipe it back or let it go and let
    // the view bounce.
    if(didFinishOverScroll){
       // do someting
    }
});
```


