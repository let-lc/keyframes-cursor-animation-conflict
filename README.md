# What is this about

This repo presents an unusual scenario. When you use `@keyframes` to animate a sprite and a cursor at the same time, one of them just stops. Kinda looks like the `animation` CSS property is messing things up a bit.

You know, this web dev stuff can get pretty wild. Chances are, you wouldn’t run into it unless you’re dabbling in a quirky side project like mine.

# Background information

Just to give you a bit of backstory, I was messing around with a side project and thought it’d be cool to add a `.ani` cursor to my site. The only [solution](https://stackoverflow.com/a/39295746) I found to do this was to use `@keyframes` to animate each frame of the `.ani` cursor file. GIFs were a no-go because CSS only supports non-animated image files, as mentioned in the "image cursors" section of the [CSS Basic User Interface Module Level 4 draft](https://drafts.csswg.org/css-ui/#cursor).

I wouldn’t have bumped into this problem if I’d just used a GIF. But, I wanted the image animation to kick in when the mouse hovers over it. So, I had to use the animation property to get the sprite image moving.

# The bug

Head over to this URL to see the bug in action. If you’re looking for more details, feel free to dig into the `index.html` file in this repository.

If you take a peek at the `index.html` source code, you’ll see that I’ve used a `*` selector. This slaps an `animation` property onto all elements for the cursor animation. Also, I’ve used a `run` animation along with some other CSS magic to animate the sprite. You can spot this in action in the `div` inside the `button` element.

Here's what's happening: everything's cool and the cursor animation is doing its thing until you hover over the image. Now, this image also has an animation property. So, when you hover, the animation of the image `div` steps in and takes over the animation from the `*` selector that was handling the cursor. This happens because of how CSS cascading rules work.

# The solution

I couldn't find any solutions online that directly addressed this issue. But I noticed that the bug popped up when I hovered over the image element. So, I came up with a workaround. I placed a transparent element, the same size as the image, on top of it. I gave this transparent div a higher `z-index`. So, when I hovered over it, I was actually hovering over the transparent div, not the image. And because I used the `group` class from Tailwind CSS, the animation still ran when I hovered over it.

I went with a div and set its `position` to `absolute`. But hey, you could totally use `::before` or `::after` to whip up this transparent element too.
