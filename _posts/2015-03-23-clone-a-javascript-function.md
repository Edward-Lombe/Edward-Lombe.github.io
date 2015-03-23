---
layout: post
title:  "Clone and serialize a Javascript function"
date:   2015-03-23 23:21:16
categories: javascript
---
Cloning a reference to a Javascript object has been something that I have occasionaly needed to do. Usually it is quite a simple process of recursively walking through the object and copying primitive values. Depending on the context, you might use `Object.keys()` method, or the slightly more comprehensive `Object.getOwnPropertyNames()`, and use that as the keys of your new object.

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