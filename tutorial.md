# BPS micro:bit Radio Tutorial 
 
### @explicitHints true 
### @activities true 


```template
//
```


## Introduction
### Introduction @showdialog
Welcome!


Hopefully by the end of this tutorial, you should be able to send a message to another micro:bit using the inbuilt radio, on a customised channel.


There are two parts:
 - Part 1 will finish with you being able to broadcast a message to all nearby micro:bits running the same code.
 - Part 2 will conclude with you being able to set a channel for your message to be broadcast on, and all other nearby micro:bits on the same channel will be able to receive your message.


Select OK to continue. 


## Part 1 - Basic communications
### Part 1 - Introduction @showdialog
To allow the micro:bit units to talk to each other, they have something colloqually called a 'radio'. This part of the tutorial will show you how to use the radio module to send and recieve messages on a pre-configured channel.


### Part 1 - Step 1 
To begin, you will want to enable the 'radio' capability and set a channel for the for the micro:bit to transmit and receive on.


This is done by setting the channel or 'group' the inbuilt radio will work with.


Grab a ``||radio:radio set group||`` block from the ``||radio:Radio||`` toolbox and drag it inside the ``||basic:on start||`` block that is already on the canvas. 


The number inside the ``||radio:radio set group||`` block denotes the channel the micro:bit will communicate on. Only micro:bits on the same channel will be able to talk to each other. 
```blocks 
radio.setGroup(1) 
``` 


### Part 1 - Step 2 
Next, you will need to set an input to let the micro:bit know when to send the string. To start with, go with something simple like a shaking gesture - just give the micro:bit a gentle shake to send the message.


Get a ``||input:on [shake]||`` block from the ``||input:Input||`` toolbox and place it in a blank area of the canvas. 
```blocks 
input.onGesture(Gesture.Shake, () => {}) 
``` 


### Part 1 - Step 3 
Now, you have to tell the micro:bit what kind of data to send. Drag a ``||radio:radio send string||`` block from the ``||radio:Radio||`` toolbox and place it inside the ``||input:on [shake]||`` block. 


This will make it so the micro:bit will send a block of text as it's message.
```blocks 
input.onGesture(Gesture.Shake,() => { 
    radio.sendString(" ") 
    } 
) 
``` 


### Part 1 - Step 4
Change the value for ``||radio:sendString||`` to whatever text you would like to send. Usually a simple "Hello" is good enough to start with. 
```blocks 
input.onGesture(Gesture.Shake,() => { 
    radio.sendString("Hello") 
    } 
) 
``` 


### Part 1 - Step 5 
Now you need to set up what happens when the micro:bit receives a message. Grab a ``||radio:on radio received||`` block from the ``||radio:Radio||`` toolbox and place it on a blank spot on your canvas. 
```blocks 
radio.onReceivedString(function (receivedString)) 
``` 


### Part 1 - Step 6 
Now, to show the text that was received: drag a ``||basic:show string||`` from the ``||basic:Basic||`` toolbox into the ``||radio:on radio received||`` block. 
```blocks 
radio.onReceivedString(function (receivedString){ 
    basic.showString("Hello") 
}) 
``` 


### Part 1 - Step 7 
Continuing on, drag the oval variable ``||variable:receivedString||`` from the ``||radio:on radio received||`` block into the ``||basic:show string||`` block. 
```blocks 
radio.onReceivedString(function (receivedString){ 
    basic.showString(receivedString) 
}) 
``` 


### Part 1 - Step 7 Explainer @showdialog
Here's a quick explainer as to what you did in Step 7:
Variables are basically a 'storage' for a value (be it text or numbers, etc) that may change depending on what a program does when it runs, rather than waiting for user input.


With that, the ``||variables:receivedString||`` part is a variable which contains the message from another micro:bit, so we make it so that the string that's shown is the same data that was just received.


### Part 1 - Step 8 
Click the 'Shake' button on your micro:bit image in the demo area. You should see a second micro:bit pop up in the same area and display your message. 


### Part 1 - Step 9 
Did it work? If so, download the code to your micro:bit and when complete, give the micro:bit a gentle shake.


If anyone else in your class has completed the tutorial up to this step, they should see your message!


### Part 1 Finished! @showdialog
All working? Congratulations! You have now completed Part 1 of the tutorial. 



## Part 2 - Changing channel 
### Part 2 - Introduction @showdialog
This part of the tutorial shows you how to add the ability to change the channel the micro:bit's radio operates on via a button press, as well as show what channel the micro:bit is on.


### Part 2 - Step 1 
First of all, we need to create a new variable which will contain the frequency the micro:bit is on.


Create a variable called ``||variables:channel||`` by clicking the ``||variables:Variables||`` toolbox and then the "Make a Variable..." button. 


As explained earlier, variables are a method of storing a piece of data which may change during the operation of a program. In this case, we are going to store the channel as a variable which will change as we press a button. 


### Part 2 - Step 2 
Now that we've got a basic connection set up, let's make it so that we can change what channel you're on for 'privacy'. 


Drag the ``||input:on button||`` block from the ``||input:Input||`` toolbox to the canvas twice, so you have two of them.


Once that is done, change one of the ``||input:on button||`` blocks to "B". 
```blocks 
input.onButtonPressed(Button.A, () => {}) 
input.onButtonPressed(Button.B, () => {}) 
``` 


### Part 2 - Step 3 
Pull a ``||variables:set||`` block from the ``||variables:Variables||`` toolbox into the ``||basic:on start||`` block, above the ``||radio:radio set group||`` block and change the value to 1.


Then, also from the ``||variables:Variables||`` toolbox, drag the ``||variables:channel||`` variable into the white oval of the ``||radio:radio set group||`` block. 


What this does, is sets the variable "channel" to 1 on startup so that the inital channel the micro:bit is on will be 1 as well.
```blocks 
let channel = 1 
radio.setGroup(channel) 
``` 


### Part 2 - Step 4 
To increase the channel value, you can use "B" button you set up earlier. You'll also want to see what channel you have currently selected. 


From the ``||variables:Variables||`` toolbox, drag in the ``||variables:change||`` block to the ``||input: on button [B]||`` block.


After that, add in a ``||radio:radio set group||`` block underneath the ``||variables:change||`` block. Once done, drag a copy of the variable ``||variables:channel||`` into the value area of the new ``||radio:radio set group||`` block.


Finally, to show what the new channel is, you need to add a ``||basic:show string||`` block underneath the ``||variables:change||`` block, which has the variable ``||variables:channel||`` set as the value.
```blocks 
input.onButtonPressed(Button.B, () => { 
channel++;
radio.setGroup(channel); 
basic.showString(channel) 
}) 
``` 


### Part 2 - Step 5 
To decrease the channel value, use the "A" button. Along with showing what the channel currently is, you also want to make sure you can't select a number below 1 - as the micro:bit can only handle channels greater than zero. 


First, repeat the process for the last step and then change the value for the ``||variables:change||`` block from 1 to -1. 
```blocks 
input.onButtonPressed(Button.A, () => { 
channel += -1;
radio.setGroup(channel);
basic.showString(channel)
}) 
``` 


### Part 2 - Step 6 
Now, to add in the safeguard against choosing a channel value below 1.


This is done by using (in programming terms) a logic block. What the instructions below will do is that if you're already on channel 1 and try do decrease it, it will set the channel back to 1.


In the ``||logic:Logic||`` toolbox, place an ``||logic:if||`` block below the ``||variables:change||`` block in ``||input:on button [A]||``. 


To make this work, you'll need to use something called a comparator. It's basically as it says on the tin - it compares one value to another.
Drag in a ``||logic:comparator||`` from the ``||logic:Logic||`` toolbox into the diamond(ish) shape of the ``||logic:if||`` block. 


Next, pull in a copy of the ``||variables:channel||`` variable into the left oval of the comparator block. 


Then, change the comparator to read "if channel &lt; 1 then". 


Finally, pull in a ``||variables:set||`` block from the ``||variables:Variables||`` toolbox to inside the ``||logic:if||`` block and set the value to 1.
```blocks 
input.onButtonPressed(Button.A, () => { 
    channel += -1; 
    if(channel < 1) { 
        channel = 1 
    } 
    radio.setGroup(channel);
    basic.showString(channel) 
}) 
``` 


### Part 2 - Step 6 Note @showdialog
A quick explainer of what happened in Step 6:


What's happening here is that the program will check what value the variable currently is for ``||variables:channel||`` and see if it is less than 1.


If it is less than 1, then it will forcefully change the ``||variables:channel||`` variable back to 1, to make sure it can never get lower.


### Part 2 - Step 7 
Now have to make it so that after a message was received, the channel selection is displayed again. Also, it would be a good idea to add in a delay before the channel appears again after the radio message was received.


To do this, drag in a ``||basic:show string||`` from the ``||basic:Basic||`` toolbox under the existing ``||basic:show string||`` inside the ``||radio:on radio received||`` block. 


Next, drag in the ``||variables:channel||`` variable from the ``||variables:Variables||`` toolbox  and drop it into the oval in the ``||basic:show string||`` block.


Finally, add in the ``||basic:pause (ms)||`` block from the ``||basic:Basic||`` toolbox above the ``||basic:show string||`` block and set it to 1 second.


```blocks
radio.onReceivedString(function (receivedString){ 
    basic.showString(receivedString);
    basic.pause(1000);
    basic.showString(channel)
})
```


### Part 2 Step 7 Note @showdialog
If you're wondering why the value of the ``||basic:pause (ms)||`` block changed itself from 1 second to 1000, that's because time is measured on a micro:bit in milliseconds.


A millisecond is 1/1000th of a second, so 1000 milliseconds will equate to 1 second.


### Part 2 - Step 8
Download the new program to the micro:bit and pair up with another student who has also gotten to this point in the tutorial. Both of you should set your micro:bit to an agreed channel and give the unit a gentle shake. Do you see the message from your partner?


### Part 2 - Finished! @showdialog
If you saw the message from your partner, and they saw yours - congratulations, you have completed this tutorial!


## Afterword
### Afterword @showdialog
Now that you have finished this tutorial, we leave you with a few final questions:
 - Where can you change what text you will send?
 - Can you change the transmit method from shaking the micro:bit to pressing both "A" and "B" at the same time?
