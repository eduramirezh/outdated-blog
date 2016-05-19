---
layout: post
title:  "The HTML5 Vibrate API"
date:   2016-02-15 12:20:25
categories: html5 mobile
featured: /assets/images/20160401120446_vibracion.jpg
---
## The API
## Browser support
## Vibrating patterns

We can set a vibration pattern by passing an array of integers to the function 'vibrate()'. 
The values set the time in milliseconds for which the device will vibrate and stop, alternately.

We can use this to set characteristic patterns, or patterns that reinforce what we want to transmit to the user.
Let's take Rush's famous wordless anthem ['YYZ'](https://play.spotify.com/track/1E0ONfqq74b4gYhdlyhMSB) as an example.



{% highlight HTML %}
<script>
  function playYYZ(){

    navigator.vibrate = navigator.vibrate || 
                        navigator.webkitVibrate ||
                        navigator.mozVibrate || 
                        navigator.msVibrate;
    var dot = [100, 100];
    var slash = [300, 100];
    var y = slash.concat(dot, slash, slash);
    var z = slash.concat(slash, dot, dot);
    var yyz = y.concat(y).concat(z);
    if (navigator.vibrate) {
      navigator.vibrate(yyz);
    }
  }
</script>
<button id="yyz-demo" 
  href="PleaseEnableJavascript.html" 
  onclick="playYYZ();return false;">
  Play YYZ
</button>
{% endhighlight %}

{% include vibrate_demo.html %}

## When to use it
