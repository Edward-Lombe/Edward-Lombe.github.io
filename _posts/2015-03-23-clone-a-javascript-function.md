---
layout: post
title:  "Clone and serialize a Javascript function"
date:   2015-03-23 23:21:16
categories: code
---
Cloning a reference to a Javascript object has been something that I have occasionaly needed to do. Javascript does not provide any builtin methods for doing this, although usually it is quite a simple process of recursively walking through the object and copying primitive values. Depending on the context, you might use `Object.keys()` method, or the slightly more comprehensive `Object.getOwnPropertyNames()`, and use that as the keys of your new object.

~~~
function fnClone(oRef) {
    if (typeof oRef === 'object') {
        var oClone;
        if (Array.isArray(oRef)) {
            oClone = new Array(oRef.length);
            for (var i = oRef.length - 1; i >= 0; i--) oClone[i] = fnClone(oRef[i]);
        } else if (oRef !== null) {
            oClone = {};
            for (var sKey in oRef) oClone[sKey] = fnClone(oRef[sKey]);
        } else return null;
        return oClone;
    } else return oRef;
}
~~~

As you can see that is a suprising amount of boilerplate to do a realtively trivial thing, which is mainly due to `typeof null === 'object'` and `typeof <array> === 'object'` both evaluating to true. However with most cases this will return a deep clone of an object.

~~~
var foo = {
    obj : {
        key : 'string'
    },
    array : [1, 2, 4, 5, 6],
    'null' : null,
    'undefined' : undefined,
    string : 'string'
}

var bar = fnClone(foo);
foo.string = 'new string';
console.log(bar.string); // 'string'
~~~

Yet this implementation can still leave us with a reference to the old object. Take for example the following.

~~~
function inverse(num) {
    return 1 / this.num;
}

var foo = {
    num : 10,
    inverse : inverse
}

var bar = fnClone(foo);

function inverse(num) {
    if (0 < num && num < 5) {
        return 1 / num;
    } else return NaN;
}

console.log(foo.inverse(foo.num)); // NaN
console.log(bar.inverse(bar.num)); // NaN
~~~

Here, both functions return `NaN` as they both still refer to the same object. I know this is a contrived example, but I feel it demonstrates what the issue. What we need is a way to clone a function.
















