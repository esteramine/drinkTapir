# drinkTapir
drinkTapir is an app which I practiced simulating the functions in food delivery app like foodpanda or Uber eats. 

drinkTapir is basically an app which I simulated the menu options view and order placing function of four different tea shops in Taiwan which are The Alley, Truedan(珍煮丹), CoCo(都可), and Milkshop(迷客夏). 

In this small project, I have implemented and practiced the following skills in Android Studio:
1.	***RecyclerView***
2.	RecyclerView with ***CardView***
3.	CardView to another CardView
4.	***ActionBar***
5.	Placing buttons in each card of CardView and making the buttons able to change the data in different cards
6.	Storing the data of every card of CardView 
7.	Passing the useful data to another page using ***Intent***
8.	***Toast***

How I did the Recyclerview with CardView: 

In order to show the RecyclerView efficiently, we will implement a Model, MyHolder, and MyAdapter class to facilitate it. 

(reference: https://www.youtube.com/watch?v=oq_xGMN0mRE&t=474s)
1.	Add libraries in build.gradle file
2.	(***activity_main.xml***)

    i.	Change ConstraintLayout to LinearLayout + orientation = “vertical”
  
    ii.	Under LinearLayout, add android.support.v7.widget.RecyclerView (required elements: layout_width = “match_parent”, layout_height = “wrap_content”, and id = “recyclerView”)

3.	Create a layout file row.xml (Root element: android.support.v7.widget.CardView)
4.	(***row.xml***)

    i.	In <…CardView> part, add xmlns:app="http://schemas.android.com/apk/res-auto", cardCornerRadius, cardElevation, cardUseCompatPadding...
  
    ii.	Under <…CardView>, set a RelativeLayout (layout_width = “match_parent”, layout_height = “wrap_content”), and under this RelativeLayout, put all the content you want to put in the cards, for example:
    ```xml
    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <ImageView
            android:id="@+id/cardIV"
            android:layout_width="match_parent"
            android:layout_height="150dp"
            android:src="@drawable/tapir"/>
        <TextView
            android:id="@+id/cardStoreName"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Store Name"
            android:textColor="#000"
            android:textSize="22dp"
            android:layout_marginTop="5dp"
            android:layout_marginLeft="10dp"
            android:layout_below="@id/cardIV"/>
        <TextView
            android:id="@+id/cardAddress"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Address"
            android:textSize="15dp"
            android:layout_marginTop="5dp"
            android:layout_marginBottom="10dp"
            android:layout_marginLeft="10dp"
            android:layout_below="@id/cardStoreName"/>
    </RelativeLayout>
    ```
    
5. Create a java ***Model*** class 

        i. Set all the parameters which data needed to be stored in the cards (from the row.xml file example above, we could set private String storeName, address; private int img;)
    
        ii. Press alt+insert to insert all the getters and setters
        
6. Create a java ***MyHolder*** class (extends RecyclerView.ViewHolder)  

        i . A red light bulb will appear, click on it and add the constructor
        
        ii. Add the parameters needed to display in the cards (from the row.xml example above, we could set public TextView mStore, mAddress; public ImageView mImg;)
        
        iii. Add all the findViewById method of all the parameters in the constructor, for example:
        ```java
        public MyHolder(@NonNull View itemView) {
        super(itemView);
        this.mStore = itemView.findViewById(R.id.cardStoreName);
        this.mAddress = itemView.findViewById(R.id.cardAddress);
        this.mImg = itemView.findViewById(R.id.cardIV);
        }
        ```
     
7. Create a MyAdapter class (extends RecyclerView.Adapter<MyHolder>)
    
        i. A red light bulb will appear, click on it and choose "Implement methods", and three methods which are onCreateViewHolder, onBindViewHolder, getItemCount will be automatically created for you
    
        ii. Add 2 parameters
        ```java
        Context c;
        ArrayList<Model> models; //create a list of array whcih parameters defined in the Model class
        ```
        
        iii. Add parameterized contructor (press alt+insert and click on "Constructor"), and in the constuctor, add
        ```java
        public MyAdapter(Context c, ArrayList<Model> models) {
            this.c = c;
            this.models = models;
        }
        ```
        
        iv. In onCreateViewHolder function, add 
        ```java
        View view = LayoutInflater.from(viewGroup.getContext()).inflate(R.layout.row, null);
        return new MyHolder(view);
        ```
        
        v. In onBindViewHolder function, add setText or setImageResource functions as below to display all the elements set in row.xml 
        ```java
        public void onBindViewHolder(@NonNull MyHolder myHolder, int i) {
            myHolder.mStore.setText(models.get(i).getStoreName());
            myHolder.mAddress.setText(models.get(i).getAddress());
            myHolder.mImg.setImageResource(models.get(i).getImg());
        }
        ```
        
        vi. In getItemCount function, change return 0; to return models.size()
    
