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

---
