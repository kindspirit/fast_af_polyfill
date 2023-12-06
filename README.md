# fast_af_polyfill
Fast AF Polyfill
A polyfill for ES6's Array.from()

* 40% faster than ES6's native Array.from() according to jsbench.me (native Array.from() is 66% slower)
* 389 bytes minified
* Works in old browsers (Tested in IE6)

This differs from the native Array.from() in that this will process the argument as an array-like first if it has a positive int in valid range as its length property before processing it as an iterable.

When [Symbol.iterator]() iterator is not available this polyfill will attempt to get an iterator from ["entries"]()
And if that doesn't work it checks for a next() method and uses that.
