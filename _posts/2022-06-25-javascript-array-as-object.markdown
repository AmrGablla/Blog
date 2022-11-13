---
layout: post
title:  "Enhance access to javascript array"
date:   2022-06-15 21:30:55 +0200 
---
# Enhance the javascript performance

I think is the key point to work and support the language eco case the fact of it is single thread langue but, it is potent for the web.

I faced a situation to make a very heavy compute on the browser, so I made it on a spirited [web worker][web-worker].
But passing the data between the main process and the web worker thread was the issue to pass more than 100 MB array of data,
And access it from there.

The wrong usage I did was:
  pass the array and loop inside the worker.

{% highlight javascript %}
  // out side the worker.
  let fatArray = []
  fatArray.push(veryFatData)

  // inside the worker
  fatArray.forEach()
{% endhighlight %}

The enhanced way:
  add the array elements as `object properties` make a huge  improvement in access performance

{% highlight javascript %}
  // out side the worker.
  let thinObject = {}
  thinObject[key] = value

  // inside the worker
  thinObject[key]

{% endhighlight %}

The Explain is very simple make it from O(n) to be O(1) with object hashing properties.

And that's it.

[web-worker]: https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers
