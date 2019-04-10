# CS52 Workshops: Fancy CSS Flitz

![](https://media.giphy.com/media/24652QfeZzNIPzoH36/giphy.gif)

Implementing cool effects with fancy CSS is awesome because it allows you to modernize your design using basic tools that you already know how to use. This can help you convey information more intuitively and efficiently, implement creative user interactions, and add joy to your site! Plus, CSS is faster than costly JavaScript, so animations will run smoothly and won't slow down your site. The tutorial below will lead you through just a few of the cool things you can make happen with pure CSS. 

## Overview

We are going to craft a tech-themed flitz site to send to our CS crushes. Since we want our crushes to know we're sick coders, we're going to make the site *fancy* with some crazy cool CSS. We'll add old-school glitch effects to headers, make curly brackets float across the page, show some nerdy pickup lines on animated cards, and hide a secret message that the user can drag to reveal, all with pure CSS! Once you've completed the tutorial, you can substitute your own content and blitz the link to someone to ask for a study date since this is the only date you have enough time to go on.

## Setup

Create a folder titled `fancy-css-workshop`, then download `starter/index.html` and `starter/style.css` and place them in this folder. The index file contains the outline structure and basic content of the flitz page, and the CSS has basic styling done already. You'll be adding to `style.css` for most of this tutorial.
 
## Step by Step

#### First Page: Glitching Text and Floating Brackets
1. Currently, your first page should just display a plain grey background with a green pixel-text message. We'll start by using keyframes to create a glitch animation to apply to this header text.
![](https://media.giphy.com/media/pOwfCO6JBMUdvvrbcb/giphy.gif)

2. In your `style.css`, define a new keyframes animation called `glitch-text`.
```css
@keyframes glitch-text {

}
```

3. Within this animation, we will use `transform: scale3d`, `transform: translate3d`, and `clip-path` to make the text appear to "glitch," or briefly display in random, jumping segments. 
 * `scale3d(x, y, z)` changes the size of the item on a 3D scale. We'll use this to flip the text.
 * `translate3d(x, y, z)` moves the item on each argument's axis. We'll use this to shift the text.
 * `clip-path: shape(args...)` shows only the portion of the item defined by the shape after the colon.
We'll start with the first set of segments that take up 0% to 10% of the animation. 

4. Start by using `transform: scale3d` and `transform: translate3d` to flip the text and move it to the left a bit, then we'll add the first `clip-path` to show only a small rectangular portion of the full text.
```css
@keyframes glitch-text {
    0% {
        transform: translate3d(-10px, 0, 0) scale3d(-1, -1, 1);
        clip-path: polygon(0 20%, 100% 20%, 100% 21%, 0 21%);
    }
```

5. Now add other clip-paths at one-percent increments. The quick succession of different segments to show will give the glitch-y look. Repeating the scale and translate values at 9.9% makes sure the animation holds these changes until it's time to move the text back.
```css
    2% {
        clip-path: polygon(0 33%, 100% 33%, 100% 33%, 0 33%);
    } 4% {
        clip-path: polygon(0 44%, 100% 44%, 100% 44%, 0 44%);
    } 5% {
        clip-path: polygon(0 50%, 100% 50%, 100% 20%, 0 20%);
    } 6% {
        clip-path: polygon(0 70%, 100% 70%, 100% 70%, 0 70%);
    } 7% {
        clip-path: polygon(0 80%, 100% 80%, 100% 80%, 0 80%);
    } 8% {
        clip-path: polygon(0 50%, 100% 50%, 100% 55%, 0 55%);
    } 9% {
        clip-path: polygon(0 70%, 100% 70%, 100% 80%, 0 80%);
    } 9.9% {
        transform: translate3d(-10px, 0, 0) scale3d(-1, -1, 1);
    }
```

6. Now use `transform: scale3d` and `transform: translate3d` to return the text to its original position, and use `clip-path` to show the whole text by giving it values for the whole rectangle view. Putting two percentages on one line holds the transformations inside the brackets for this span of the animation.
```css
    10%, 77% {
        transform: translate3d(0, 0, 0) scale3d(1, 1, 1);
        clip-path: polygon(0 0, 100% 0, 100% 100%, 0% 100%);
    } 
 ```
 
 7. The rest of the animation will include another glitch with a ripply side-shift effect. In the code below, the `translate3d` effect will run from 78% to 80%, so the text will slowly move from 20px to the right back to the original position. As that is happening, two more `clip-paths` display different segments of the moving text. Finally, the text holds its original position from 80% to 100%, a.k.a. the end of the animation
 ```css
    78% {
        transform: translate3d(20px, 0, 0);
        clip-path: polygon(0 50%, 100% 50%, 100% 20%, 0 20%);
    } 79% {
        clip-path: polygon(0 70%, 100% 70%, 100% 80%, 0 80%);
    } 80%, 100% {
        transform: translate3d(0, 0, 0);
        clip-path: polygon(0 0, 100% 0, 100% 100%, 0% 100%);
    }
 ```
 
 8. Lastly, you need to apply this affect to the header text. Under the class `.glitch-text`, define this animation and play with the length of the animation to see how the effect changes. Also, set the `animation-iteration-count` to be infinite so the glitch plays on a continuous loop.
```css
    .glitch-text {
        animation-name: glitch-text;
        animation-duration: 4s;
        animation-iteration-count: infinite;
    }
```

9. If you view your page in localhost, you should see your text glitching out! Playing with the pixel and timing values can make the effect look drastically different, just go with what you think looks good.

#### Second Page: Flipping Boxes

#### Third Page: Draggable Hidden Message

#### Fourth Page: Parallax and Hover Effects

#### Scroll Effect

:sunglasses: GitHub markdown files [support emoji notation](http://www.emoji-cheat-sheet.com/)

Here's a resource for [github markdown](https://guides.github.com/features/mastering-markdown/).


## Summary / What you Learned

* [ ] can be checkboxes

## Reflection

*2 questions for the workshop participants to answer (very short answer) when they submit the workshop. These should try to get at something core to the workshop, the what and the why.*

* [ ] 2 reflection questions
* [ ] 2 reflection questions


## Resources

* cite any resources
