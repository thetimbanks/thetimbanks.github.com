---
author: tpb976
comments: true
date: 2011-10-19 19:27:51+00:00
layout: post
slug: jquery-extension-removeclassexcept-method
title: 'jQuery Extension: removeClassExcept() method'
wordpress_id: 240
categories:
- jQuery
- Web
tags:
- jQuery
- jquery extension
- remove class
- remove class except
---

I came across a question on [StackOverflow.com](http://stackoverflow.com/questions/7826379/jquery-removeclass-but-not-certain-classes/7826461) where the user wanted the ability to remove all classes from an element except certain ones.  For example if I had the following element

[code lang="html"]
<div class="aa bb cc dd ee">Lorem Ipsum</div>
[/code]

How would you go about removing all classes except for "aa" and "bb"?  One way would be to just set the class attribute to the classes you wanted to keep.

[code lang="javascript"]

$("div").attr("class", "aa bb");

[/code]

That's easy enough.  Another way would be to use some built in jQuery methods.

[code lang="javascript"]

$("div").removeClass().addClass("aa bb");

[/code]

The previous code would remove all classes and then add back the ones that were needed.  That snippet could be put into a jQuery extension to make it easier to call.

[code lang="javascript"]

jQuery.fn.removeClassExcept = function (val) {
    return this.each(function () {
        $(this).removeClass().addClass(val);
    });
};

$("div").removeClassExcept("aa bb");

[/code]

That makes the code look cleaner.  One problem both of these solutions have is they don't check to see if the class already exists before adding it.  On the Stack Overflow question, [Brad Christie](http://stackoverflow.com/users/298053/brad-christie) proposed a solution to handle the case where you didn't want to add a class unless it already existed.  The updated extension now takes that into consideration.

[code lang="javascript"]

jQuery.fn.removeClassExcept = function (val) {
    return this.each(function (index, el) {
        var keep = val.split(" "),  // list we'd like to keep
            reAdd = [],          // ones that should be re-added if found
            $el = $(el);       // element we're working on

        // look for which we re-add (based on them already existing)
        for (var i = 0; i < keep.length; i++){
            if ($el.hasClass(keep[i])) reAdd.push(keep[i]);
         }

         // drop all, and only add those confirmed as existing
         $el
            .removeClass()               // remove existing classes
            .addClass(reAdd.join(' '));  // re-add the confirmed ones
    });
};

[/code]

Here is a jsFiddle showing the use of removeClassExcept(): [http://jsfiddle.net/9xhND/1/](http://jsfiddle.net/9xhND/1/)
