---
author: tpb976
comments: true
date: 2011-03-22 12:48:45+00:00
layout: post
slug: jquery-extension-toggletext-method
title: 'jQuery Extension: toggleText() method'
wordpress_id: 153
categories:
- Javascript
- jQuery
- Web
tags:
- Javascript
- jQuery
- jquery extension
- jquery plugin
- toggle
- toggletext
---

Skip straight to the [demo](http://thetimbanks.com/demos/jquery/extensions/toggleText/).

Here's a situation I have run into multiple times: I have a hidden area that is toggled by a link.  The link will usually say "Show *", and once it is clicked it will say "Hide *".  I would usually just check the text when the link is clicked and switch it.  Similar to the following:

[code lang="js"]
$("a").click(function() {
    var $self = $(this);
    if ($self.text() == "Show items")
       $self.text("Hide items");
    else
        $self.text("Show items");
});
[/code]

It would get tedious to add this to every link that toggled the view on an element.  In order to make it easier on myself I threw together a little extension for jQuery.  You pass it 2 string values representing the text that you would like to toggle.  Here is an example usage that does the same thing as the code block above:

[code lang="js"]
$("a").click(function() {
    $(this).toggleText("Show", "Hide");
});
[/code]

The extension looks for the first value in the element's text and if it exists, it is replaced with the second value.  If the first value doesn't exist in the element's text, it looks for the second value in the text and replaces it with the first value.   Here is the source:

[code lang="js"]
jQuery.fn.toggleText = function (value1, value2) {
    return this.each(function () {
        var $this = $(this),
            text = $this.text();

        if (text.indexOf(value1) > -1)
            $this.text(text.replace(value1, value2));
        else
            $this.text(text.replace(value2, value1));
    });
};
[/code]

To see it in action, you can [view the demo](http://thetimbanks.com/demos/jquery/extensions/toggleText/).
