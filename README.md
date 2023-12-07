# fast_af_polyfill
Fast AF Polyfill
A polyfill for ES6's Array.from()

* 40% faster than ES6's native Array.from() according to jsbench.me (native Array.from() is 66% slower)
* 440 bytes minified
* Works in old browsers (Tested in IE6)

This differs from the native Array.from() in that native Array.from() processes array-likes as iterables first if they have a Symbol.iterator method. Where mine will attempt to process it as an array-like first before trying to process it as an iterable.

To process it as an iterable it first tries to get the iterator by calling the Symbol.iterator method, and if that is not found it checks for a next() method which indicates that the argument itself should be used as the iterator.

This was also designed to be a replacement for native Array.from() so if you don't want to overwrite native Array.from you should do something like the following to include it in your code which will only run if Array.from does not yet exist:

    <script>Array.from||document.write("<script src=Array.from.min.js><\/script>");</script>

To support old browsers you should always pass the iterator itself to Array.from() rather than the iterable since old browsers don't support iterables without Symbol.iterator which this does not attempt to polyfill. But if it's an array or an array-like you can just pass it normally. For example to get the values from a Set object use:

    Array.from(new Set([1,2,3]).values());// returns [1,2,3]
