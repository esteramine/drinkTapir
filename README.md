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
  ii.	Under <…CardView>, set a RelativeLayout (layout_width = “match_parent”, layout_height = “wrap_content”), and under this RelativeLayout, put all the content you want to put in the cards
