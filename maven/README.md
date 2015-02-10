# AspectRatioImageView

An ImageView with a height or width dimension set to WRAP_CONTENT will experience jank when loading an image from the network or after a long-running background task.

Common solutions to this include setting the height and width to explicit values or setting a minimum height or width on the ImageView. Unfortunately, sometimes the images that are loaded from the network may be much larger than the size of the target view. In this case, the image must be resized to the bounds of the ImageView. This is simple when either the height or width of the ImageView is known.

If the constraint is MATCH_PARENT, however, the only way we can know the missing value of the image is to attach an OnGlobalLayoutListener or OnLayoutChangeListener and update the height after the first layout. Since the values are only known after the layout occurs, jank can still occur because of updating cthe layout.

The AspectRatioImageView eliminates the jank. It requires that the desired aspect ratio or the height and width of the original image to be set before measurement occurs. It will calculate an aspect ratio and update the measured dimension of the view to match what it will be when the image load is complete.

That's a lot to take in. Here's an image of what it does. The top cell is the AspectRatioImageView. The bottom cell is a standard ImageView:

![alt text](loading.gif?raw=true  "Demonstration Image")

##Usage
I'm hoping to eventually get this added to a Maven repo so that it is compatible with Gradle. Until then, you'll have to include it as a module in your project the old fashioned way. The module that contains the widget is the library module. There is a test module that contains a unit test covering the functionality in this widget. There's also a sample module that contains an Android application that will demonstrate the same thing shown in the GIF above.