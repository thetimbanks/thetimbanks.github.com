---
author: tpb976
comments: true
date: 2011-06-08 14:42:53+00:00
layout: post
slug: setting-a-threshold-on-jquery-ajax-callbacks-using-prefilters
title: Setting a threshold on jQuery ajax callbacks using prefilters
wordpress_id: 178
categories:
- AJAX
- Javascript
- jQuery
tags:
- ajax
- Javascript
- jQuery
- prefilter
---

This is a cross post from my [company's blog](http://www.foliotek.com/devblog/setting-a-threshold-on-jquery-ajax-callbacks-using-prefilters/).




Skip straight to the [demo](http://www.thetimbanks.com/demos/jquery/successThreshold/).

When developing interfaces that include ajax functionality there will come a time when you will be showing some sort of loading animation and it will only show for a split second since the ajax call finished so fast.  This can cause the user to be disoriented since they aren't exactly sure what popped up.  It can be beneficial to slow down the interface so the user can see everything that is going on.

In jQuery 1.5, there is now a way to extend the $.ajax method.  There are three different ways to extend $.ajax: prefilters, converters, and transports.  I am going to use prefilters which the jQuery documentation describes as "generalized beforeSend callbacks to handle custom options or modify existing ones".  I'm not going to go into details about what a prefilter is since the [documentation](http://api.jquery.com/jQuery.ajaxPrefilter/) does a pretty good job.

Instead of setting up timeouts and clearing them out, I am wanting to pass a custom option to the ajax method.  Here is what I am trying to go for:

[sourcecode lang="javascript"]
$.ajax(url, {
    ...
    successThreshold: 3000,
    ...
})
[/sourcecode]

The successThreshold option is my custom option.  The time passed into it will be the minimum amount of time it takes before the success callback gets called.  Now that I have my custom option, I can access it and modify the other options in my prefilter.

[sourcecode lang="javascript"]
$.ajaxPrefilter(function (options, originalOptions, jqXHR) {
    if (originalOptions.successThreshold &amp;amp;&amp;amp;  $.isFunction(originalOptions.success)) {
        var start, stop;
        options.beforeSend = function () {
            start = new Date().getTime();
            if ($.isFunction(originalOptions.beforeSend))
                originalOptions.beforeSend();
        };
    
        options.success = function (response) {
        var that = this, args = arguments;
        stop = new Date().getTime();

        function applySuccess() {
             originalOptions.success.apply(that, args);
        }

        var difference = originalOptions.successThreshold - (stop - start);
        if (difference > 0)
            setTimeout(applySuccess, difference);
        else
            applySuccess();
        };
    }
});
[/sourcecode]

The first thing I do in the prefilter is check to make sure both the successThreshold and success function are set.  I then override the beforeSend option in order to get the time before the ajax call starts.  In order to keep the success callback from firing before the threshold, the time difference needs to be calculated.  If the call didn't take longer than the difference then set a timeout for the remaining time.  Otherwise just call the success callback immediately.

I have seen other solutions to this and all of them seem to set timeouts and clear them in different functions and it would have to be repeated for every call.  This can be defined in one place and used on any ajax call in the application.

I have added the code to my [Github repository](https://github.com/thetimbanks/successThreshold).  This [demo](http://www.thetimbanks.com/demos/jquery/successThreshold/) shows the code in action.


