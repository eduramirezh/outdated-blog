---
layout: post
title:  "The HTML5 Vibrate API"
date:   2016-05-18 12:20:25
categories: html5 mobile
featured: /assets/images/20160401120446_vibracion.jpg
---

In a recent project at [NNodes](http://nnodes.com/blog), we were asked to develop a website that simulated the *look & feel* of a native mobile app.
One of the resources we used to accomplish this was the **HTML5 Vibration API**


This API allow us to control the vibration hardware on a device by calling the function:

{% highlight Javascript %}
navigator.vibrate([])
{% endhighlight %}

###Compatibility

It's currently supported as an API by [Chrome, Firefox and Opera](http://caniuse.com/#feat=vibration), but it only has an effect on their mobile version.
Even though it excludes Safari for iOS, it still makes up for around [64% of the mobile browsers market share](https://www.netmarketshare.com/browser-market-share.aspx?qprid=1&qpcustomb=1).

### Vibrating patterns

The *vibrate()* function's only parameter is an integer array. The values correspond to vibrating and
waiting times, alternately, in milliseconds. For example:

{% highlight Javascript %}
navigator.vibrate([100, 200, 100])
{% endhighlight %}

will make the device vibrate for 100 milliseconds, then stop for 200, and then vibrate again for 100.
We can use this to define patterns that extend the user experience (explosions in games, for example) or that reinforce the product identity.

###Example

Let's take Rush's famous wordless anthem ['YYZ'](https://play.spotify.com/track/1E0ONfqq74b4gYhdlyhMSB) for our example.
This song emulates the Morse code for the letters YYZ. So first, let's transform those dots and dashes
into an integer array.

{% highlight Javascript %}
//.
var dot = [100, 100];
//-
var slash = [300, 100];

var y = slash.concat(slash, dot, slash, slash);
var z = slash.concat(slash, slash, dot, dot);
//-.---.---..
var yyz = y.concat(y).concat(z);
{% endhighlight %}

Now we assign the pattern

{% highlight HTML %}
<script>
  function playYYZ(){
    navigator.vibrate = navigator.vibrate;
    if (navigator.vibrate) {
      navigator.vibrate(yyz);
    }
  }
</script>

<button id="yyz-demo"
  onclick="playYYZ();">
  Play YYZ
</button>
{% endhighlight %}

####Result

If your browser is compatible, click here to see the API in action

{% include vibrate_demo.html %}


*Puedes leer una versión en español [aquí](http://nnodes.com/blog/2016/usando-la-vibration-api-de-html5)*
