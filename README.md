# CS52 Workshops: Fancy CSS Flitz

![](https://media.giphy.com/media/ubQOPZPbPPJ7y/giphy.gif)

Implementing cool effects with fancy CSS is awesome because it allows you to modernize your design using basic tools that you already know how to use. This can help you convey information more intuitively and efficiently, implement creative user interactions, and add joy to your site! Plus, CSS is faster than costly JavaScript, so animations will run smoothly and won't slow down your site. The tutorial below will lead you through just a few of the cool things you can make happen with pure CSS.

## Overview

We are going to craft a tech-themed flitz site to send to our CS crushes. Since we want our crushes to know we're sick coders, we're going to make the site *fancy* with some crazy cool CSS. We'll add old-school glitch effects to headers, make curly brackets float across the page, show some nerdy pickup lines on animated cards, and hide a secret message that the user can drag to reveal, all with pure CSS! Once you've completed the tutorial, you can substitute your own content and blitz the link to someone to ask for a study date since this is the only date you have enough time to go on.

## Setup

Create a folder titled `fancy-css-workshop`, then download `starter/index.html` and `starter/style.css` and place them in this folder. The index file contains the outline structure and basic content of the flitz page, and the CSS has basic styling done already. You'll be adding to `style.css` for most of this tutorial.

## Step by Step

### First Page: Glitching Text and Floating Brackets
1. Currently, your first page should just display a plain grey background with a green pixel-text message. We'll start by using keyframes to create a glitch animation to apply to this header text. **Keyframes** lets you **define an animation by gradually changing between different sets of styles.** The order is set through percentages, where `0%` is the start of the animation and `100%` is the end. This lets you run the same animation at diffferent time scales without having to define a whole new keyframe!

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



10. Now let's work on the falling characters in the background. If you take a look at `index.html`, you'll see a `div` with id `text-lines`, which contains `<p>` tags of randomly spaced characters (`&nbsp` is a way to display spaces, since html automatically collapses all spaces). We will use CSS to style and animate these lines to make it look like characters falling in the background.


11. First, let's work on making these characters appear _behind_ the glitch text. The glitch-text header is in the `div` class `.front`, and the characters are in the `div` class `.back`. We will use `z-index` to make it look like the characters are underneath the glitch text.
```css
    .front {
      z-index: 2;
    }

    .back {
        position: absolute;
        width: 100vw;
        height: 100vh;
    }
```
The `z-index` property only works on elements with a set `position` property, as we see in `.back`.

12. Now, don't panic because we can't see the characters yet. Let's add some styling to them.
```css
  .scroll-text-1 {
      color: white;
      font-size: 1.5vw;
      font-family: 'Press Start 2P', cursive;
  }

  .scroll-text-2 {
      color: white;
      font-size: 1.5vw;
      font-family: 'Press Start 2P', cursive;
    }
```
The reason why we have two `scroll-text` classes is because later on, we want to have two slightly varied animation speeds to give a little variety to the falling effect. You should now see a bunch of randomly placed characters _behind_ the glitch-text.

13. Let's add some style to the class `.text-line` so we can space the characters out a bit better.
```css
  #text-lines {
      width: 100%;
      height: 100%;
      display: flex;
      flex-direction: row;
      justify-content: space-around;
  }
```
14. Now, you might be wondering why we chose our `flex-direction` to be `row`. This is because we are going restyle the `scroll-text` so that the characters appear in vertical "strips". Add the following propeties to `.scroll-text-1` and `.scroll-text-2`.
```css
  .scroll-text-1 {
      ...
      text-orientation: upright;
      writing-mode: vertical-rl;
  }
  .scroll-text-2 {
      ...
      text-orientation: upright;
      writing-mode: vertical-rl;
  }
```
Great, we've just used a hacky method to make our characters look randomly spaced!

15. Now it's time to add the falling animation. Let's add an `animation` property to both `scroll-text` classes.
```css
  .scroll-text-1 {
      ...
      animation: fall1 9s linear infinite;
  }
  .scroll-text-2 {
      ...
      animation: fall2 13s linear infinite;
  }
```
Notice that we use the shorthand version of the `animation` property, so the first argument is `animation-name`, the second is `animation-duration`, and the third is `animation-iteration-count`. Also notice that the `animation-duration` is slightly different for `fall1` and `fall2`: this is the variation we talked about earlier. The characters should't move yet, since we haven't added the `@@keyframes`.

16. So let's add the `@keyframes` that will actually make the characters move.
```css
  @keyframes fall1 {
      0% {
          transform: translateY(-50vh);
      }
      80%, 100% {
          transform: translateY(100vh);
      }
  }
  @keyframes fall2 {
      0% {
          transform: translateY(-100vh);
      }
      100% {
          transform: translateY(100vh);
      }
  }
```
Let's break this down. `0%` refers to the beginning of the animation (0% of the way through the frame, if you will), and `100%` refers to the end of the animation (100% of the way through the frame). So in fall2, for example, we are saying "at the beginning of the frame, translate the text in the y-axis -100vh (so that the characters appear to be off-screen). Then, over the duration specified in the animation, translate the text in the y-axis to 100vh by the end of the frame.

17. Congrats! You should now have "randomly :wink:" falling characters in the background!

### Second Page: Flipping Boxes


### Third Page: Scrollable Hidden Message


### Fourth Page: Hover Effects
1. The last div has a question for your flitz with three heart-shaped answer options. We are going to animate each option so they know the emotional toll that their answer will have on you.
![](https://media.giphy.com/media/35KdD3pqLudXAPHzB2/giphy.gif)


2. First, we will define two more keyframes animations, one for the shaking and one for the beating. The shaking animation will use the translate and rotate transformations to quickly move the heart in a shaky little circle...

```css
@keyframes shake {
    0% { transform: translate(1px, 1px) rotate(0deg); }
    10% { transform: translate(-1px, -2px) rotate(-1deg); }
    20% { transform: translate(-3px, 0px) rotate(1deg); }
    30% { transform: translate(3px, 2px) rotate(0deg); }
    40% { transform: translate(1px, -1px) rotate(1deg); }
    50% { transform: translate(-1px, 2px) rotate(-1deg); }
    60% { transform: translate(-3px, 1px) rotate(0deg); }
    70% { transform: translate(3px, 1px) rotate(-1deg); }
    80% { transform: translate(-1px, -1px) rotate(1deg); }
    90% { transform: translate(1px, 2px) rotate(0deg); }
    100% { transform: translate(1px, -2px) rotate(-1deg); }
}
```
and the beating animation will use the scale transformation to pulse the heart.
```css
@keyframes beat {
    0%{transform: scale(1);}
    50%{transform: scale(1.1);}
    100%{transform: scale(1);}
}
```

3. We can now apply these effects to the first and second hearts.
```css
#h1:hover {
    animation: beat .5s ease infinite;
}

#h2:hover {
    animation: shake 0.5s;
    animation-iteration-count: infinite;
}
```

4. Lastly, we want the third heart to flip upside down on hover. We don't need to define an animation for this effect, we can just add in a rotating transformation as a hover effect like this:
```css
#h3:hover {
    transform: rotate(180deg);
}
```

5. Now all your hearts should animate on hover!


### Scroll Effect


## Summary
**What your site has:**
* [ ] A glitchy text effect by hiding/showing different parts of a header
* [ ] Scrolling code in the background of a screen
* [ ] Cards that flip on hover
* [ ] A hidden message that the user can drag to reveal
* [ ] Different, fun hover effects for images
* [ ] Fading scroll between different divs

**What you learned:**
* [ ] How to define your own keyframes animations
* [ ] How to add fun hover effects to convey information
* [ ] How to implement fun user interactions
* [ ] Why fancy CSS is useful
* [ ] When fancy CSS is advantageous to use

## Reflection Questions
Don't forget to submit these on Canvas!

* [ ] Why use CSS to add effects to your site instead of JavaScript? When might it be better to use JavaScript?
* [ ] Why add fancy styling to your site at all? When could fancy effects be useful?


## Resources

:sunglasses: GitHub markdown files [support emoji notation](http://www.emoji-cheat-sheet.com/)

Here's a resource for [github markdown](https://guides.github.com/features/mastering-markdown/).
