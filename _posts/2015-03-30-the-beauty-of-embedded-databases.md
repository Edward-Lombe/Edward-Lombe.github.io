---
layout: post
title:  "The beauty of an embedded database"
date:   2015-03-30 7:49:02
categories: code
---
Say you have some some data, and you wish to persist it. How would you go about that? Well depending on you environment, this can either be easy or hard.

For example, if your context was within the browser, you could easily utilise the `localStorage` object to store data. The interface for using it could not be simpler.

~~~
localStorage.key = 'value';
alert(localStorage.key); // 'value'
~~~

Great! You now have a piece of data that will be stored across sessions and can be accessed that same way as any old Javascript object. From my perspective, there is very little difference in the interface of this object and say `obj.key = 'value';`. And even better it's supported by IE8+!

Note there are a few caveats on the usage of localStorage:

- You are limited to 5MB of storage
- The localStorage object can only store stings. Attempting to assign an object will silently convert to string
- Safari (iOS and OSX) will throw an exception when you try to access it in whilst in private mode

Now what happens when we and store a value in a client/server side environment? For the sake of this demonstation, lets continue to use Javascript, this time within a server side environment, in this case NodeJS. There are two way we could do this. One is two handle the IO ourselves through the `fs` module and the other is through the use of a database (Postgres, MongoDB, etc.).

~~~
var fs = require('fs');
var oJSON = {
    key: 'value'
};

fs.writeFileSync('storage.json', JSON.stringify(oJSON), 'utf8');

var oReadJSON = require('./storage.json') // Provided you trust file contents
~~~

With the use of a database it becomes slightly more complicated, in this example I will be using MongoDB, as it is arguably one of the better known key-value databases, despite some of its [issues](https://www.youtube.com/watch?v=b2F-DItXtZs)