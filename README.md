# Java-Script-30 Tasks

**Drum Kits** - - - - - - - - - **Whack a Mole Game**

//////////////////////////////////// ////////////////////////////////////

**Clock** - - - - - - - - - - - - - **Speech Synthesis**

//////////////////////////////////// ////////////////////////////////////

**HTML5 Canvas**

//////////////////////////////////// ////////////////////////////////////

**Dev Tools**

//////////////////////////////////// ////////////////////////////////////

**JS References**

//////////////////////////////////// ////////////////////////////////////

**Speed Controller**

//////////////////////////////////// ////////////////////////////////////

**CountDown Timer**

/

/

/

**Drum Kits**

Hitting the assigned key on the keyboard will trigger a sound to be played based
on the given input, while also triggering a short animation to indicate what key
was pressed.

Increasing the button in size,

Adding a yellow boarder,

When a button is pressed, a *class* **playing** is assigned to the element which
instigates the *css* to **transform** the scale of the button by '1.1', change the
**boarder-colour** as well as the **box-shadow**

In the **Index.html** we have a *div* with a *class* of **Keys**, which contains
more *divs* with *classes* of **Key**. Each Key is assigned a given *keycode*
of the key that we want to be pressed, in order to trigger the audio sound we want for
the specific key.

For Example, 

`KeyCode "65"` is letter A's keycode, so when keycode "65" is detected from being pressed,
the audio sound "clap" will be triggered as a response from the *sounds* file.
               
----
First We want to listen for a key-down event, which we use to identify the keycode of the
key that gets pressed. Then we need to identify if there is an audio element on the page that
matches the `data-key="?"` (data-key is a data attribute to be set apart from other data).
This is achieved by using a querySelector in conjunction with a attribute selector to 
match the found keycode located as a variable in the event, '`audio[data-key${e.keyCode}]`.
           

To create an animation for each button when they're pressed, requires us to use the key
identifier where we can then apply the class playing with `key.classList.add('playing')`.
Then we need to remove the class with a transition end event, which will run when the
transition of the animation finishes being applied. Using a querySelector to get all the keys,
allows us to identify which ones have the class applied, where we can loop over each key.
Then we can listen for a *transitionend* and when that ends we run a remove function to
use `this.classList.remove('playing')` to remove the class that is applied to any key.

----

**Clock**

This project is a simple ticking clock that updates every second based off of real time from
javascript. We rotate each hand based on the centre of the clock and apply specific rotations
to each hand in order to represent seconds, minutes and hours.

----
In the hand object we have the properties of each hand of the clock, however they all start 
facing at 9, so we need to apply a 90* rotation to begin with in order to have the clock begin
at 12. We also need the `transform-origin:` to be 100% in order to set the position to transform
on the far right of the hands, in order to have them rotate from the centre of the clock.
Now that the hands are in position we want to apply a transition in order to create the look
of each hand moving from one angle to another, this removes the appearance of each hand snapping
to each position. We us a `transition-timing-function: cubic-bezier()` in order to create the
look of a normal clock ticking along. We also need to use a transition timing property in order
to set the length of time the animation takes.

Now that we've got the look of the clock sorted, we need to make the scripts for each hand in
order for them to know the real time of day in order to behave appropriately as a clock.
For each hand we need to get their respecting elements in order to apply the rotations for them,
using querySelectors. Then we can create a function designed to get the current date/time in
javascript using `const now = new Date()`. Using new variables such as 
`const seconds = now.getSeconds()`, `const minutes = now.getMinutes()`, `const hours 
= now.getHours()` gives us the correct time for each hand. However, we need to convert the time
into degrees on the clock in order for it to operate correctly. For seconds and minutes
we do `const secondsDegrees = ((seconds / 60) * 360) + 90` and
`const minutesDegrees = ((minutes / 60) * 360) + 90` to give us degrees in 360*, while
applying a 90* offset as it will start from the default position of the hands which were in the
wrong position requiring a offset as well. For the hours we do 
`const hoursDegrees = ((hours / 12) * 360) + 90` which gives us the 12 positions within a 360*
space to give us the 12 hours on a clock.

Last thing is to have the function run every second to update each hand at the same time, which
can be done using a `setInterval(setDate, 1000)`.

----

**HTML 5 Canvas**

Holding the mouse button down on the page will allow you to draw on the canvas in colours that
dynamically move through the colour spectrum, while also changing the size of the 'brush'
as you draw.

Canvas in HTML 5 is similar to the program Paint, where you get an area of pixels to draw on.
However, you don't draw on the canvas element, instead you draw on what is called the context.

----
First we need to get the canvas layer using a querySelector and the context with 
`const ctx = canvas.getContext('2d')` giving it the attribute of 2d.
Then we can re-size the canvas to what ever we want, but for this instance we'll have it the 
size of the window using `canvas.width = window.innerWidth` ,
`canvas.height = window.innerHeight`.

Now we need to initialise the context layer with some drawing properties in order to allow us
to set up a drawing function. These properties set up things like the size of the lines, and 
whether the lines are made of squares or round circles etc. We also need to initialise some
variables so we can get into the function as we aren't drawing when we not holding down
the mouse button. Such as stating that we aren't drawing now and the last x and y 
coordinates.

With the function draw we can use an if statement to stop the function if the mouse isn't down.
However, we want to use some event listeners to detect when the mouse is up, down or out of the
window in order to set when `isDrawing` to true only when the mouse is down. Now that we have
everything in the function to only run when the mouse is down, we can set up what we want to
happen when we draw. We start with `ctx.beginPath()` to start a path on the context with
`ctx.moveto(lastX, lastY)`,`ctx.lineTo(e.offsetX, e.offsetY)` to set up the line that is
going to be drawn with the mouse, but nothing will happen until we `ctx.stroke()` that will put
coloured line onto the canvas. However, the line will still start from 0,0 and will jump
to the new position of the mouse when you try and draw a new line, so we need to update the
X and Y values before we draw and after we have drawn our line. With
`[lastX, lastY] = [e.offsetX, e.offsetY]` we update these values to allow us to create lines
that are where we draw with our mouse.

With the actual drawing of the lines complete, we can now adjust the size of the lines and
the colour. Using hsl (hue, saturation, lightness) we can get the colour spectrum and
programmatically pick the colours we want and blend to them in a loop to create a dynamic
colour change as we draw. Starting from the colour red
`ctx.strokeStyle = hsl(${hue}, 100%, 50%)` we set the colour to start from, at the end of the
draw function we can set a statement to return the hue to 0 if it goes over 360 otherwise
increment it to go through the spectrum. With the colour set to change as you draw all that
needs doing is changing the line width as you draw. All we need is to create a statement
to flip the direction of increment or decrement if the width reaches either boundary,
`if (ctx.lineWidth >= 50 || ctx.lineWidth <= 1) { direction = !direction`.
Then we can say if direction is true then we can increment the line, else we decrement.
Creating a forever incrementing and decrement line width as you draw.

----

**Dev Tools**

This project is made to show how you can use certain console tools to get data, that may be
needed in use of debugging a program.

----

**References**

Small html to run simple operations in showing how variables, arrays and objects work with
assigning data and changing them part way through etc.

----

**Video Speed Controller**

Small project designed to allow you to adjust the playback speed of a video. Changing the speed
from 0.4x to 4x based on where your mouse is on the bar.

----

We start with selecting the pages speed, bar and video classes in order for us to use later
in adjusting the video. Next we need an event listener to run a function when the mouse is
over the speed bar. We need to get the Y coordinate of the bar as you move your mouse,
using `e.pageY - this.offsetTop` we get the Y coordinate - the area above the bar as we
can't assume that the bar is at the top of the page. In order to change the Y coordinate into
a percentage that we can use the coordinate - the offsetHeight. Then we need a min and max
to set the boundaries of the bar. After that we add the height value to the style of the bar
in order to apply the speed we want with the level of the bar as we move the mouse. All that's
left is to set the actual number of registered on the bar and set it to the speed of the video.
Using the boundaries of the bar with the percentage given when the mouse is on the bar, we set
the text content to be the playbackRate variable to be fixed to 2 decimal places. Finally to
apply the playbackRate value to the video's playbackRate so the speed set in the bar matches
the speed of the video `video.playbackRate = playbackRate`.

----
