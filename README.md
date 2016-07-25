# 'Nerdeando'
## Framer Studio LVL Workshop | 25-26 July 2016

### Overview

In day one of this workshop, we're going to cover the basics of Framer studio. On day two, we'll convert a static Sketch mockup into an interactive prototype. We will publish our prototypes both to the web and to our phones.

> _Note: this workshop is written for Mac OS X users. Our prototype app will be an iOS prototype._

### Setup:

1. Install the free trial of [Sketch](https://www.sketchapp.com/static/download/sketch.zip) on your Mac
2. Install the free trial of [Framer Studio](http://framerjs.com/download/) on your Mac
3. Install the new [Framer Preview app](https://itunes.apple.com/app/id1124920547) on your iPhone

***
 
## Day 1: Framer Basics

### Getting Started

* Open Framer studio, and choose `File > New` from the top menu to create a new prototype.
* If you do not immediately see an iPhone 6s on the righthand side of the app, choose `Device > Apple iPhone 6s > iPhone 6s Silver`.
	* _The color of your iPhone frame doesn't really natter, but I choose silver for its contrast w/ the phone's black screen)_
* Choose `File > Save` and save the project as `day-one.framer` on your desktop.
	* _Worth noting: saving your project creates a folder called `day-one.framer`, rather than an individual file. This folder can be dragged onto the Framer Studio icon to open, or opened from Framer's `File > Open` menu.)_

Building with Framer is as easy as understanding its three main components:

1. Layers
2. States
3. Events

Today, we're going to walk through each of these to create a simple interaction.

### Layers

* To create a new layer, click the `Insert` button in the top left of Framer's UI and choose `Layer`
* You should now see 2 things:
	1. Code that reads `layerA = new Layer` has been written for you on the left
	2. A corresponding grey square has been created on the iPhone screen on the right
* Click and drag the layer to move it around the phone's screen. As you do, you'll notice smart guides appearing to help you align your layer on the screen, while code is being written for the layer's x & y position on the left. I've positioned my `layerA` square in the center of the phone's screen. My code reads:

```
layerA = new Layer
	x: 275
	y: 567
```

To the left of the `layerA = …` in your code, you'll notice a small square button with three lines:

![handle](images/handle.png)

If the handle is already highlighted (filled w/ a solid grey), great. If not, click the handle to highlight it. Now, turn your attention to Framer's center column. You should see the following:

![handle](images/properties.png)

These are the properties of the selected layer. You can change any of these values as you would in a visual design tool. As you do, Framer will write the corresponding code for you in the lefthand column.

Using this property inspector, change the border radius to `10`, the scale to `0.50` and change the background color to whatever you like (I've chosen a red color at `100%` opacity). Your code should look something like this:

![handle](images/new-properties.png)

On the iPhone's screen, your layer should now look like this:

![handle](images/red-square.png)

This first set of properties you've now created for `layerA` is the layer's default **state**. Keep this idea in mind as we move on.

### States

States are variations of a layer that we can transition between. To add a state to `layerA`, choose `Insert > State > layerA`, like so:

![handle](images/add-state.png)

You are immediately taken back into edit mode, where you can again change the properties of `layerA` to whatever your desired values for this new state, already given the name of `stateA` in your lefthand code editor. I've made the background white, the scale `2.00` and the rotation `45`.

My code for this new state looks like this:

![handle](images/add-state-code.png)

And my layer now looks like this:

![handle](images/white-square.png)

It's now time to add some interactivity to transition between this our default state and this new `stateA`.

### Events

To add a `Click` event to our layer, choose `Insert > Event > layerA > Click > Click`, like this:

![handle](images/add-event.png)

You'll see that Framer has written the following code for you:

`layerA.onClick (event, layer) ->`

The cursor is already indented for you to write the code for your event. This is the only line of code we need to write to add both interactivity and our transition animation:

`layerA.states.next()`

The full code for your event should now read:

```
layerA.onClick (event, layer) ->
	layerA.states.next()
```

And you can now repeatedly click on your layer on the iPhone's screen to transition between the two states we've written.

What we just added, in programming terminology, is called a _click event._ How its above code reads, in human terms, is as follows:

1. `layerA.onClick …` when `layerA` is clicked, perform the actions listed on the below, indented lines (while we've only written one line below, we can, theoretically, add as many as we like to be performed when `layerA` is clicked)
2. `layerA.states.next()` Whatever the current state of `layerA`, transition to the next state. Per our example:
	* If our square is in its default state that we first created (the small, red square), transition to `stateA` (the larger, rotated white square)
	* However, if `layerA` is already in `stateA`, transition back to its default state

### Viewing The Prototype On Your iPhone

1. Keep Framer Studio open on your Mac
2. Make sure both your iPhone and Mac are on the same Wi-Fi network
3. Open the `Framer` app on your iPhone
4. You should see a thumbnail of your project w/ its file name listed beneath; click to open it
5. You will be prompted to enter an access code from Framer Studio. Click the `Mirror` button just above the center column in Framer Studio _**on your Mac**_ and enter the code shown into the Framer app on your phone (_Note: your access code will be different from the one listed below_):

![access code](images/access-code.png)

You should now be able to interact w/ the prototype on your iPhone.

### Bonus: Extra State

Getting Back to Framer Studio on your Mac, let's insert another State to see what happens.

Just as before, use the `Insert` button to add another state:

![handle](images/add-state.png)

You should now see `stateB` highlighted in your code editor, and you're already in edit mode in the center panel.

For our `stateB` values, I've chosen a blue background color, `8.00` for the scale (_I had to enter this via my keyboard — the slider doesn't allow such a large input value_) and a rotation of `180`:

![state b](images/state-b.png)

Now, when you interact with your layer, you'll see it cycle through its 3 states — default, `stateA` and `stateB` — each time you click. To see this on your phone, save your file (⌘ + S) in Framer Studio w/ your prototype open on your phone. You should see a blue load bar across the top of the Framer app on your phone to indicate that your changes have been published and the prototype is reloading.

### Fine tuning states and transitions

Now that we have three states to work with, change the last line in our code from:

```
layerA.states.next()
```

To instead read:

```
layerA.states.next('stateA', 'stateB')
```

Now, as you continuously click `layerA`, it cycles between its `stateA` and `stateB` states, never returning to its default, small red square state.

Finally, we'll add one more little block of code to govern the duration of our animation (_Note: this should be a code block unto itself, and **not** indented beneath our `layerA.onClick …` code_):

```
layerA.states.animationOptions =
    time: .5
```

As you can see, our transitions now move a bit more quickly. Animation duration in Framer is defined in seconds, so play around with this number to see how easily you can test different durations in search of the perfect transition. Be sure to save each time you change the value, so the prototype is updated on your phone

> _Worth noting: what little code we 'wrote' is was simply copied & pasted from Framer's Documentation. I encourage you to have a look at the docs on your own & add/remove code to the above example to see how it affects your demo._

***

## Day 2:

### Overview

Animated shapes are fun & all, but let's make a real prototype.

### Setup

* Download day two workshop assets [here](https://github.com/misterburton/framer-lvl-workshop/raw/master/_assets/workshop-assets.zip)
* Unzip `workshop-assets.zip`
* Place the `SF UI` folder in `Hard Drive > Library > Fonts`
* Open the `day-two-ui.sketch` file in Sketch

### Sketch File Overview

#### Design:

![Sketch Artboards](images/artboards.png)

* Our prototype will transition between two views, `home_page` & `detail_page`
* Active click/tap areas are blue, black/grey areas are not
* The top status bar & bottom nav bars will be made to persist in code, so we only need them on the first (home_page) artboard.

#### Layers:

![Sketch Artboards](images/layer-order.png)

* **Layer names:** use underscores in lieu of spaces or hyphens for consistency as Framer will rename them using underscores
* **Layers arrangement:** top-to-bottom as they appear in the artboard (personal preference - easier to visually reference in framer)
* **Sketch symbols:** Right click each and choose `Detach from Symbol` as Framer can't read these. This action converts symbols to layer groups.
* **Layer groups:** groups will be flattened into a single layers. These can then be referenced in code by their group name

> _Note: if you have made any adjustments to the file, make sure it is saved in its current state and that Sketch is not hidden before importing it into Framer Studio._

### Creating our Framer Prototype

* Open Framer studio, and choose `File > New` from the top menu to create a new prototype.
* If you do not immediately see an iPhone 6s on the righthand side of the app, choose `Device > Apple iPhone 6s > iPhone 6s Silver`.
* Click `Import`, choose `@2x` from the drop menu and click `import` to bring `day-two-ui.sketch` into Framer Studio.

You should now see the following code denoting your imported file:

```
# Import file "day-two-ui" (sizes and positions are scaled 1:2)
sketch = Framer.Importer.load("imported/day-two-ui@2x")
```

> _Note: the line beginning with a `#` is a code comment. These are helpful messages that are ignored by our prototype._

* You should also see the hierarchy of your artboard & layer structure in Framer's center column, and the design on the iPhone's screen.

![Layer hierarchy](images/layer-hierarchy.png)

* These layers will now be accessible via Framer's `Insert` menu for adding states and events, just as manually created layers are. These layers and groups also retain the hierarchy they had in Sketch. So, if we move `detail_page` in Framer, everything beneath it moves, as well. You can roll over layer names to see them highlighted in Framer's design view, even if they are off the stage.

* With this in mind, and speaking of our `detail_page`, if you roll over it, you can see it's a little too far to the right. We want it right up against the right side of the screen and ready to animate when we transition from the home page to our detail page.

* We need a state for this. Choose `Insert > State > detail_page`. Now, using the center column, set its x Position to 750, like this:

![Detail X Position](images/detail-xpos.png)

* Now, we need one line of code to instantly set our `detail_page` to this state, with no animation or transition. Add this code beneath your state code, and be sure it's not indented:

```
# set initial detail_page position
sketch.detail_page.states.switchInstant("stateA")
```

* If you now mouse over `detail_page` in Framer's center column, you'll see that it's right where we want it, ready to be transitioned into view.

* To be sure we're aligned, the whole of your prototype's code should now read:

```
# Import file "day-two-ui" (sizes and positions are scaled 1:2)
sketch = Framer.Importer.load("imported/day-two-ui@2x")

sketch.detail_page.states.add
	stateA:
		x: 750

# set initial detail_page position
sketch.detail_page.states.switchInstant("stateA")
```

* First, we're importing the Sketch file, we're then creating `stateA` where our `detail_page` is at `750`, and lastly, we're immediately setting that state with Framer's `switchInstant` command.

* We now need a new state where `detail_page` is in view, or at `0` x Position. Using our `Insert > State > detail_page` command, add a new state, and using the center column, add set the position to `0`. Its automatically inserted code should read:

```
stateB:
	x: 0
```

* Now, let's add some interactivity to our blue `layer_one` button on the `home_page` to slide our detail page into view. Choose `Insert > Event > label_one > Click > Click` and paste the following code beneath the resulting `sketch.label_one.onClick…` code:

```
sketch.detail_page.states.switch("stateB")
```

* Our full `label_one` Click event code should now read:

```
sketch.label_one.onClick (event, layer) ->
	sketch.detail_page.states.switch("stateB")
```

* This tells Framer, when a Click is detected on our `label_one` layer, `detail_page` should now transition to `stateB`. Save your prototype & click the blue text button to see our `detail_page` come flying in.

* It's now time to add a state for our `home_page` to get out of the way when the `detail_page` makes its entrance. Choose `Insert > States > home_page` and set its position to `-750`.

* Repeat this process and add another state for our `home_page` where its position is 0. Your full `home_page` states code should read:

```
sketch.home_page.states.add
	stateA:
		x: -750
	stateB:
		x: 0
```

* Add the following line to our `label_one` Click Event code: `sketch.home_page.states.switch("stateA")`. The entire event should now read:

```
sketch.label_one.onClick (event, layer) ->
	sketch.detail_page.states.switch("stateB")
	sketch.home_page.states.switch("stateA")
```

* Now, when we click our blue label button on the home page, we see the `home_page` exit to the left as our `detail_page` makes its entrance.

* Functionality-wise, all that's left is to afford our `back_button` layer on the Detail page the same functionality, only backwards. Choose `Insert > Event > back_button > Click > Click`, and add the following two lines of code to our resulting Click event:

```
	sketch.detail_page.states.switch("stateA")
	sketch.home_page.states.switch("stateB")
```

* You should now be able to transition from the Home to the Detail page and back again using our two active buttons to which we've applied Click Events. All that's now left to apply is a little polish.

* First off, we want our `status_bar` and `bottom_tab_bar` layers to persist throughout, just as they would on a real iOS app. To achieve this, add the following two lines of code:

```
# make status & nav bars persistent
sketch.status_bar.superLayer = Framer.Device.screen
sketch.bottom_tab_bar.superLayer = Framer.Device.screen
```

* Now, all that's left is our transition — it's freakishly slow. The following two lines of code will set us right:

```
# set our global transition animation time
Framer.Defaults.Animation =
    time: .4
```

Disco.

***

### References:

* Quick Tour of Framer's New [Auto-Code](https://www.youtube.com/watch?v=XoV1iWH1naE)
* [Framer Documentation](http://framerjs.com/docs/) (Also available from within Framer studio via the `Docs` menu button)
* [Sketch App Sources](http://www.sketchappsources.com/): giant repository of free sketch UI assets & resources