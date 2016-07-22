# 'Nerdeando'
## Framer Studio LVL Workshop | 25-26 July 2016

### Overview

In day one of this workshop, we're going to cover the basics of Framer studio. On day two, we'll convert a static Sketch mockup into an interactive prototype. We will publish our prototypes both to the web and to our phones.

> _Note: this workshop is written for Mac OS X users. Our prototype app will be an iOS prototype._

### Setup:

1. [OS X] Install the free trial of [Sketch](https://www.sketchapp.com/static/download/sketch.zip)
2. [OS X] Install the free trial of [Framer Studio](http://framerjs.com/download/)
3. [OS X] Download Apple's free [San Francisco Fonts](https://github.com/misterburton/framer-lvl-workshop/raw/master/_assets/SFUI.zip), unzip the file and install them in `/Library/Fonts`
4. [iOS] Install the new [Framer Preview app](https://itunes.apple.com/app/id1124920547)
5. Download project assets **NEED LINK for all assets, not just fonts**

***
 
## Day 1: Framer Basics

### Getting Started

* Open Framer studio, and choose `File > New` From the top menu to create a new prototype. If you do not immediately see an iPhone 6s on the righthand side of the app, choose `Device > Apple iPhone 6s > iPhone 6s Silver`.
* Choose `File > Save` and save the project as `tutorial.framer` on your desktop. _(Note: saving your project creates a folder called `tutorial.framer`, rather than an individual file)_

Building with Framer is as easy as understanding its three main components:

1. Layers
2. States
3. Events

Today, we're going to walk through each of these to create a simple interaction.

### Layers

* To create a new layer, click the `Insert` button in the top left of Framer's UI and choose `Layer`
* You should now see 2 things:
	1. Code that reads `layerA = new Layer` has been written for you on the left
	2. A corresponding square, grey layer has been created on the iPhone screen on the right
* Click and drag the layer to move it around the phone's screen. As you do, you'll notice smart guides appearing to help you align your layer on the screen, while code is being written for the layer's x & y position on the left:

```
layerA = new Layer
	x: 275
	y: 567
```

To the left of the `layerA…` in your code, you'll notice a small square handle:

![handle](images/handle.png)

Click the handle and pay attention to Framer's center column. You should see the following:

![handle](images/properties.png)

These are the properties of the selected layer. You can change any of these values and, as you do, Framer will write the corresponding code for you in the lefthand column.

Using this property inspector, change the border radius to `10`, the scale to `0.50` and change the background color to whatever you like (I've chosen red at `100%` opacity). Your code should look something like this:

![handle](images/new-properties.png)

On the iPhone's screen, your layer should look like this:

![handle](images/red-square.png)

This first set of properties you've now created for `layerA` is the layer's default state. Keep this idea in mind as we move on.

### States

States are variations of a layer that we can transition between. To add a state to `layerA`, choose `Insert > State > layerA`, like so:

![handle](images/add-state.png)

You are immediately taken back into edit mode, where you can again change the properties of `layerA` to whatever your desired values. I've made the background white, the scale `2.00` and the rotation `45`.

My code for this new state looks like this:

![handle](images/add-state-code.png)

And my layer now looks like this:

![handle](images/white-square.png)

It's now time to add some interactivity to transition between this new state, and our original 

### Events

To add a `Click` event to our layer, choose `Insert > Event > layerA > Click > Click`, like this:

![handle](images/add-event.png)

You'll see that Framer has written the following code for you:

`layerA.onClick (event, layer) ->`

The cursor is already indented for you to write the code for your event. This is the only line of code we'll write for our entire demo:

`layerA.states.next()`

The full code for your event should now read:

```
layerA.onClick (event, layer) ->
	layerA.states.next()
```

How this reads is as follows:

1. `layerA.onClick …` when `layerA` is clicked, perform the actions listed below this line
2. `layerA.states.next()` Whatever the current state of `layerA`, transition to the next one. For example:
	* If our square is in its default state that we first created (the small, red square), transition to `stateA` (the larger, rotated white square)
	* However, if `layerA` is already in `stateA`, transition back to its default state

### Viewing The Prototype On Your iPhone

1. Keep Framer Studio open on your Mac
2. Make sure both your iPhone and Mac are on the same Wi-Fi network
3. Open the `Framer` app on your iPhone
4. You should see a thumbnail of your project w/ the name `tutorial` listed beneath; click to open it
5. You will be prompted to enter an access code from Framer Studio on your Mac. Click the `Mirror` button just above the center column and enter the code shown into the Framer app on your phone:

![access code](images/access-code.png)

You should now be able to interact w/ the prototype on your iPhone.

### Bonus: Extra State

Getting Back to Framer Studio on your Mac, let's insert another State to see what happens.

Just as before, use the `Insert` button to add another state:

![handle](images/add-state.png)

You should now see `stateB` highlighted in your code editor, and you're already in edit mode in the center panel.

For our `stateB` values, I've chosen a blue background color, `8.00` for the scale and a rotation of `180`:

![state b](images/state-b.png)

Now, when you interact with your layer, you'll see it cycle through its 3 states — default, `stateA` and `stateB` — each time you click. To see this on your phone, swipe up from the bottom of the Framer Preview app and press the circular `refresh` button.

***

### References:

* Quick Tour of Framer's New [Auto-Code](https://www.youtube.com/watch?v=XoV1iWH1naE)
* 