# fast-levenshtein - Levenshtein algorithm in Javascript

[![Build Status](https://secure.travis-ci.org/hiddentao/fast-levenshtein.png)](http://travis-ci.org/hiddentao/fast-levenshtein)

An efficient Javascript implementation of the [Levenshtein algorithm](http://en.wikipedia.org/wiki/Levenshtein_distance) with asynchronous callback support.

## Features

* Works in node.js and in the browser.
* Reduced memory usage compared to other implementations by not needing to store the whole matrix ([more info](http://www.codeproject.com/Articles/13525/Fast-memory-efficient-Levenshtein-algorithm)).
* Provides synchronous and asynchronous versions of the algorithm.
* Asynchronous version is almost as fast as the synchronous version for small strings and can also provide progress updates.
* Comprehensive test suite.
* Small: <1 KB minified and gzipped

## Installation

### node.js

Install using [npm](http://npmjs.org/):

```bash
$ npm install fast-levenshtein
```

### Browser

Using bower:

```bash
$ bower install fast-levenshtein
```

Or the following inside your HTML:

```html
<script type="text/javascript" src="https://github.com/hiddentao/fast-levenshtein/raw/master/levenshtein.min.js"></script>
```

The API will then be accessible via the `window.Levenshtein` object.

## Examples

**Synchronous**

```javascript
var levenshtein = require('fast-levenshtein');

var distance = levenshtein.get('back', 'book');   // 2
var distance = levenshtein.get('我愛你', '我叫你');   // 1
```

**Asynchronous**

```javascript
var levenshtein = require('fast-levenshtein');

levenshtein.getAsync('back', 'book', function (err, distance) {
  // err is null unless an error was thrown
  // distance equals 2
});
```

**Asynchronous with progress updates**

```javascript
var levenshtein = require('fast-levenshtein');

var hugeText1 = fs.readFileSync(...);
var hugeText2 = fs.readFileSync(...);

levenshtein.getAsync(hugeText1, hugeText2, function (err, distance) {
  // process the results as normal
}, {
  progress: function(percentComplete) {
    console.log(percentComplete + ' % completed so far...');
  }
);
```

## Building and Testing

To build the code and run the tests:

```bash
$ npm install -g grunt-cli
$ npm install
$ npm run build
```

## Performance

_Thanks to [Titus Wormer](https://github.com/wooorm) for [encouraging me](https://github.com/hiddentao/fast-levenshtein/issues/1) to do this._

Benchmarked against other node.js levenshtein distance modules (on Macbook Air 2012, Core i7, 8GB RAM):

```bash
Running suite Implementation comparison [benchmark/speed.js]...
>> fast-levenshtein x 357 ops/sec ±2.32% (89 runs sampled)
>> levenshtein-edit-distance x 317 ops/sec ±4.16% (83 runs sampled)
>> natural x 219 ops/sec ±5.26% (77 runs sampled)
>> levenshtein x 179 ops/sec ±2.49% (73 runs sampled)
Benchmark done.
Fastest test is fast-levenshtein at 1.13x faster than levenshtein-edit-distance
```

You can run this benchmark yourself using:

```bash
$ npm install -g grunt-cli
$ npm install
$ npm run benchmark
```

## Contributing

If you wish to submit a pull request please update and/or create new tests for any changes you make and ensure the grunt build passes.

See [CONTRIBUTING.md](https://github.com/hiddentao/fast-levenshtein/blob/master/CONTRIBUTING.md) for details.

## License

MIT - see [LICENSE.md](https://github.com/hiddentao/fast-levenshtein/blob/master/LICENSE.md)
