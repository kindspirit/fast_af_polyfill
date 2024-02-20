# fast_af_polyfill
Fast AF Polyfill
A polyfill for ES6's Array.from() compatible with ES3+ environments.

* 40% faster than ES6's native Array.from() according to jsbench.me (native Array.from() is 66% slower)
* 511 bytes minified
* Works in old browsers (Tested in IE6) as well as non-browser environments

This differs from the native Array.from() in that native Array.from() processes objects as iterables, unless they don't contain a Symbol.iterator method in which case they are processed as array-likes. However Fast AF Polyfill will attempt to process objects as array-like objects first before trying to process them as iterables. This is because processing an object as an array-like object is both faster and has compatibility with ES3, and because in the vast majority of cases the outcome is exactly the same.

Another important difference is that Fast AF Polyfill instantiates arrays with `Array(length)` which is both faster and creates a holey array, unlike native `Array.from` which ostenisbly creates packed arrays. But holey arrays are not significantly different from packed arrays so this should not matter.

To process it as an iterable it first tries to get the iterator by calling the Symbol.iterator method, and if that is not found it checks for a next() method which indicates that the argument itself should be used as the iterator.

This functions as a polyfill but it was also designed to be a replacement for native Array.from() so if you don't want to overwrite native Array.from you should do something like the following to include it in your code which will only run if Array.from does not yet exist:

    <script>Array.from||document.write("<script src=Array.from.min.js><\/script>");</script>

To support old JS environments you should always pass the iterator itself to Array.from() rather than the iterable since old browsers don't support iterables, at least not without Symbol.iterator which this does not attempt to polyfill. For example to get the values from a Set object use:

    Array.from(new Set([1,2,3]).values());// returns [1,2,3]
