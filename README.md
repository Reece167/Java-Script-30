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
javascript using `const now = new Date()`, this gets . Using new variables such as 
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