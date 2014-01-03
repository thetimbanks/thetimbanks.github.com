---
author: tpb976
comments: true
date: 2011-09-20 14:34:45+00:00
layout: post
slug: recreating-google-expanding-image-stack
title: Recreating Google+ Expanding Image Stack
wordpress_id: 194
categories:
- CSS
- Google
- Walkthrough
- Web
tags:
- CSS
- CSS3
- Google
- webkit
---

[Skip straight to the demo](/demos/GooglePlusImage/)

After taking some time to browse around Google+ I noticed a cool effect on the albums page when hovering over an album. If the album had multiple images in it, the stack would expand to show the first 3 images inside the album. You can see an example of it here: [https://plus.google.com/photos/105135327491673313070/albums](https://plus.google.com/photos/105135327491673313070/albums).

I thought it would be neat to try and reproduce this effect. This example will work in Chrome, Firefox 4+, and Safari 4+.

**Step 1 - Get images**

The only thing we need to do in step 1 is get 3 images of the same size and put them into a block element.  I grabbed 3 images from my Google+ account and put them in a div with the id of "photo-stack".

[code lang="html"]
<div id="photo-stack">
    <img src="https://lh3.googleusercontent.com/-khtZ0GBqcOI/Th2kD8vv0ZE/AAAAAAAAACU/rd3t2O6QI-o/s195-c/BVI2008" />
    <img src="https://lh3.googleusercontent.com/-ZpghGAz-jZE/Th2kECfNChI/AAAAAAAAACI/VAtLWAuUbf0/s195-c/photo.jpg" />
    <img src="https://lh4.googleusercontent.com/-xcrH8Z9qHqI/Th2kEMhqQ1I/AAAAAAAAACA/jL8ZZTTpqA4/s195-c/photo.jpg" />
</div>
[/code]

[View Step 1](/demos/GooglePlusImage/step1.html)

**Step 2 - Stacking**

Now that we have our 3 images let stack them on top of each other.  This is accomplished by positioning each of them absolutely on top of each other.

[code lang="css"]

#photo-stack { position: relative;}

#photo-stack img { position: absolute; top: 0; left: 0;}

[/code]

That looks good, but I want the first image in the DOM to appear on top.  In that case we need to set the z-index of each image.  I am going to use the nth-child property so we don't have to add classes to each image.

[code lang="css"]

#photo-stack img:nth-child(1) { z-index: 3;}

#photo-stack img:nth-child(2) { z-index: 2;}

#photo-stack img:nth-child(3) { z-index: 1;}

[/code]

Now the first image is on the top!

[View Step 2](/demos/GooglePlusImage/step2.html)

**Step 3 - Moving**

Let's start working on the animation.  The animation has 3 parts to it: movement of the images, rotation of the images, and the size of the images.

We can handle the movement of the images by using the translate value of the transform property.  We are going to use the nth-child property just like we did in the last step in order to target each image individually.

Translate takes 2 values for the x and y movement.  Since the second image isn't moving we are only going to move the first and last images.

[code lang="css"]

#photo-stack:hover img:nth-child(1) {
    -webkit-transform: translate(-50px, 0px);
}
#photo-stack:hover img:nth-child(3) {
    -webkit-transform: translate(50px, 0px);
}

[/code]

[View Step 3](/demos/GooglePlusImage/step3.html)

**Step 4 - Rotating**

Now that we have the images moving apart we can rotate the outer image.  Rotate only takes 1 argument for the amount of degrees you want to rotate the element.  Once again the middle image is not being rotated so we will not worry about it.

[code lang="css"]

#photo-stack:hover img:nth-child(1) {
    -webkit-transform: rotate(5deg);
}
#photo-stack:hover img:nth-child(3) {
    -webkit-transform: rotate(-5deg);
}

[/code]

We are getting close!  [View Step 4](/demos/GooglePlusImage/step4.html)

**Step 5 - Scaling**

The images need to grow a little in size when they are spreading apart.  By using the scale property we can pass in a value to change the size of the image (1 being 100%).

[code lang="css"]

#photo-stack:hover img:nth-child(1) {
    -webkit-transform: scale(1.1);
}
#photo-stack:hover img:nth-child(2) {
    -webkit-transform: scale(1.1);
}
#photo-stack:hover img:nth-child(3) {
    -webkit-transform: scale(1.1);
}

[/code]

[View Step 5](/demos/GooglePlusImage/step5.html)

**Step 6 - Animating**

In order to get the transforms to animate when hovering, only 1 line of code needs to be added.  The -webkit-transition line takes 3 arguments: property to animate, amount of time, and animation timeline.  In our case we want to animate the -webkit-transorm property for .25 seconds and have a linear timeline.

[code lang="css"]

#photo-stack img {  -webkit-transition: -webkit-transform .25s linear;}

[/code]

[View Step 6](/demos/GooglePlusImage/step6.html)

**Step 7 - Cleanup**

The look can be cleaned up a little by applying some additional styles.  Now it looks like a real stack of photos!

[View Final Demo](/demos/GooglePlusImage/)

Let me know what you thought of the tutorial or if you put this to use on one of your sites!
