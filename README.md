# drinkTapir
drinkTapir is an app which I practiced simulating the functions in food delivery app like foodpanda or Uber eats. 

drinkTapir is basically an app which I simulated the menu options view and order placing function of four different tea shops in Taiwan which are The Alley, Truedan(珍煮丹), CoCo(都可), and Milkshop(迷客夏). 

In this drinkTapir app, you could see a main page with four different tea shops, the menu list of a specific shop after clicking on one of those shops, and eventually the "Confirm Order and Pay" page after ordering all the drinks.

Illustrations:
1. Main Page
<img src = "https://github.com/esteramine/drinkTapir/blob/master/drinkTapirProject_Main%20Page.png?raw=true" width="150"  />
<img src = "https://github.com/esteramine/drinkTapir/blob/master/drinkTapirProject_Main%20Page2.png?raw=true" width="150" />
2. Menu (ex. The Alley's Menu list)
<img src = "https://github.com/esteramine/drinkTapir/blob/master/drinkTapirProject_The%20Alley's%20Menu.png?raw=true" width="150" />
3. Confirm and Pay page
<img src = "https://github.com/esteramine/drinkTapir/blob/master/drinkTapirProject_Confirm%20and%20Pay.png?raw=true" width="150" />
4. Pay
<img src = "https://github.com/esteramine/drinkTapir/blob/master/drinkTapirProject_Pay.png?raw=true" width="150" />

In this small project, I have implemented and practiced the following skills in Android Studio:
1.	***RecyclerView***
2.	RecyclerView with ***CardView***
3.	CardView to another CardView
4.	***ActionBar***
5.	Placing buttons in each card of CardView and making the buttons able to change the data in different cards
6.	Storing the data of every card of CardView 
7.	Passing the useful data to another page using ***Intent***
8.	***Toast***



## How I did the Recyclerview with CardView: 

In order to show the RecyclerView efficiently, we will implement a Model, MyHolder, and MyAdapter class to facilitate it. 

(reference: https://www.youtube.com/watch?v=oq_xGMN0mRE&t=474s)
1.	Add libraries in build.gradle file (in dependencies)
```
implementation 'com.android.support:recyclerview-v7:28.0.0'

implementation 'com.android.support:cardview-v7:28.0.0'
```
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
    and it will show something like the below:
    
    <img src = "https://user-images.githubusercontent.com/55351011/86438362-f71e5580-bd38-11ea-9ff8-ee6ce3d2d9d8.PNG" width="113" height="201" />
    
5. Create a java ***Model*** class 

    i. Set all the parameters which data needed to be stored in the cards (from the row.xml file example above, we could set private String storeName, address; private int img;)
    
    ii. Press alt+insert to insert all the getters and setters
        
6. Create a java ***MyHolder*** class (extends RecyclerView.ViewHolder)  

    i . A red light bulb will appear, click on it and add the constructor
        
    ii. Add the parameters needed to display in the cards (from the row.xml example above, we could set public TextView mStore, mAddress; public ImageView mImg;)
        
    iii. Add all the *findViewById* method of all the parameters in the constructor, for example:
    ```java
    public MyHolder(@NonNull View itemView) {
        super(itemView);
        this.mStore = itemView.findViewById(R.id.cardStoreName);
        this.mAddress = itemView.findViewById(R.id.cardAddress);
        this.mImg = itemView.findViewById(R.id.cardIV);
    }
    ```
     
7. Create a MyAdapter class (extends RecyclerView.Adapter<MyHolder>)
    
    i. A red light bulb will appear, click on it and choose "Implement methods", and three methods which are *onCreateViewHolder*, *onBindViewHolder*, and *getItemCount* will be automatically created for you
    
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
        
    iv. In *onCreateViewHolder* function, add 
    ```java
    View view = LayoutInflater.from(viewGroup.getContext()).inflate(R.layout.row, null);
    return new MyHolder(view);
    ```
        
    v. In *onBindViewHolder* function, add setText or setImageResource functions as below to display all the elements set in row.xml 
    ```java
    public void onBindViewHolder(@NonNull MyHolder myHolder, int i) { //i is the position
        myHolder.mStore.setText(models.get(i).getStoreName());
        myHolder.mAddress.setText(models.get(i).getAddress());
        myHolder.mImg.setImageResource(models.get(i).getImg());
    }
    ```
        
    vi. In *getItemCount* function, change return 0; to return models.size()
    
8. (***MainActivity.java***)

    i. Add 2 variables
    ```java
    RecyclerView recyclerView;
    MyAdapter myAdapter;
    ```
    
    ii. In *onCreate* function, add
    ```java
    recyclerView = findViewById(R.id.recyclerView);
    recyclerView.setLayoutManager(new LinearLayoutManager(this));
    myAdapter = new MyAdapter(this, getMyList());
    recyclerView.setAdapter(myAdapter);
    ```
    
    iii. Below the *onCreate* function, implement the *getMyList* function as below to display the four tea shops on the app:
    ```java
    private ArrayList<Model> getMyList(){
        ArrayList<Model> models = new ArrayList<>();
        Model m;

        m = new Model();
        m.setStoreName("THE ALLEY");
        m.setAddress("台北市大安區復興南路二段206號");
        m.setImg(R.drawable.the_alley);
        models.add(m);

        m = new Model();
        m.setStoreName("TRUEDAN");
        m.setAddress("台北市中正區羅斯福路一段12號");
        m.setImg(R.drawable.truedan);
        models.add(m);

        m = new Model();
        m.setStoreName("CoCo");
        m.setAddress("台北市中正區南昌路一段77號");
        m.setImg(R.drawable.coco);
        models.add(m);

        m = new Model();
        m.setStoreName("Milkshop");
        m.setAddress("台北市中正區寧波西街50號");
        m.setImg(R.drawable.milkshop);
        models.add(m);

        return models;
    }
    ```

## How I did the CardView with Item Click to an Intent

1. Create an Interface class (Class name: ItemClickListener), and add a *onItemClickListener* function in it as shown as below:
```java
public interface ItemClickListener {
    void onItemClickListener(View v, int position);
}
```

2. (***MyHolder*** class)
    
    i. Add "implements View.OnClickListener" beside the extends, and implement the method *onClick*
    
    ii. Delete the public keyword which is in front of the MyHolder constructor
    
    iii. Add a variable **ItemClickListener itemClickListener;** in the class
    
    iv. In the constructor, add **itemView.setOnClickListener(this);**
    
    v. In the *onCLick* function, add **this.itemClickListener.onItemClickListener(v, getLayoutPosition());**
    
    vi. Add a **setItemClickListener** function as shown as below:
    ```java
    public void setItemClickListener(ItemClickListener ic){
        this.itemClickListener = ic;
    }
    ```
    
    So, eventually, your MyHolder class will be like this:
    ```java
    public class MyHolder extends RecyclerView.ViewHolder implements View.OnClickListener{
        public TextView mStore, mAddress;
        public ImageView mImg;
        ItemClickListener itemClickListener;

        MyHolder(@NonNull View itemView) {
            super(itemView);
            this.mStore = itemView.findViewById(R.id.cardStoreName);
            this.mAddress = itemView.findViewById(R.id.cardAddress);
            this.mImg = itemView.findViewById(R.id.cardIV);

            itemView.setOnClickListener(this);
        }

        @Override
        public void onClick(View v) {
            this.itemClickListener.onItemClickListener(v, getLayoutPosition());
        }

        public void setItemClickListener(ItemClickListener ic){
            this.itemClickListener = ic;
        }
    }
    ```
    
3. Create a new empty Activity (for example, the activity name is "The Alley"), and in the xml file ***activity_the_alley.xml***, design your own interface

4. (***TheAlley.java***)
    
    i. Add the needed variables 
    
    ii. Hook the variables with their view (ex. mStoreName = findViewById(R.id.storeName2);)
    
    iii. Add a back button by adding **ActionBar actionBar = getSupportActionBar();**, and in ***AndroidManifest.xml***, add **android:parent_ActivityName = "MainActivity"** under activity The Alley
    
5. (***My Adapter.java***)
    
    i. In *onBindViewHolder* function, add
    ```java
    myHolder.setItemClickListener(new ItemClickListener() {
        @Override
        public void onItemClickListener(View v, int position) {
            String gStore = models.get(position).getStoreName();

            Intent intent = new Intent(c, TheAlley.class);
            intent.putExtra("iStore", gStore);
            c.startActivity(intent);
        }
    });
    ```
    
6. (***TheAlley.java***)
    
    i. In *onCreate* function, add
    ```java
    Intent intent = getIntent();
    mStore = intent.getStringExtra("iStore");
    mStoreName.setText(mStore); //set the store name
    actionBar.setTitle(mStore+"'s Products List");
    ```
    
## Conclusion
My project was basically repeatedly using all the steps above to create many RecyclerView with CardView and Intents.
    
     
