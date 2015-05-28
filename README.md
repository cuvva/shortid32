## shortid32  [![Build Status](http://img.shields.io/travis/cuvva/shortid32.svg)](https://travis-ci.org/cuvva/shortid32) [![shortid32](http://img.shields.io/npm/v/shortid32.svg)](https://www.npmjs.org/package/shortid32)

> Amazingly short non-sequential human-friendly unique id generator.

ShortId32 creates amazingly short non-sequential human-friendly unique ids.  Perfect for url shorteners, and any other id users might see.

 * By default 7-14 human-friendly characters: `A-Z`, `0-9`, excluding the commonly confused `01OI`
 * Non-sequential so they are not predictable.
 * Supports `cluster` (automatically), custom seeds, custom alphabet.
 * Can generate any number of ids without duplicates, even millions per day.
 * Perfect for games, especially if you are concerned about cheating so you don't want an easily guessable id.
 * Apps can be restarted any number of times without any chance of repeating an id.
 * Works in Node, io.js, and web browsers.
 * Includes [Mocha](http://visionmedia.github.com/mocha/) tests.

### Usage

```js
var shortid = require('shortid32');

console.log(shortid.generate());
//PPBQWA9
```

### Browser Compatibility

The best way to use `shortid32` in the browser is via [browserify](http://browserify.org/) or [webpack](http://webpack.github.io/).

These tools will automatically only include the files necessary for browser compatibility.

All tests will run in the browser as well:

```bash
## build the bundle, then open Mocha in a browser to see the tests run.
$ grunt build open
```

### Example

```js
~/projects/shortid ❯ node examples/examples.js
WKTQBXJF
QKCTWBXJF
WKZVQMXJP
Q3ATWB5CF
QK5VQMXCP
WKQVQMXJF
Q3FTQB5CP
WK6VWM5JF
QKGTWBXCF
W3TVWBXJP
```

### API

`var shortid = require('shortid32');`

---------------------------------------

#### `shortid.generate()`

__Returns__ `string` non-sequential unique id.

__Example__

```js
users.insert({
    _id: shortid.generate()
    name: ...
    email: ...
    });
```

---------------------------------------

#### `characters(string)`

__Default:__ `'23456789ABCDEFGHJKLMNPQRSTUVWXYZ'`

__Returns__ new alphabet as a `string`

__Optional__

Change the characters used.

You must provide a string of all 32 unique characters. Order is not important.

The default characters provided were selected because they are human friendly.

__Example__

```js
// any 32 unicode characters work, but I wouldn't recommend this.
shortid.characters('ⒶⒷⒸⒹⒺⒻⒼⒽⒿⓀⓁⓂⓃⓅⓆⓇⓈⓉⓊⓋⓌⓍⓎⓏ②③④⑤⑥⑦⑧⑨');
```

---------------------------------------

#### `isValid(id)`

__Returns__ `boolean`

Check to see if an id is a valid `shortid`. Note: This only means the id _could_ have been generated by `shortid`, it doesn't guarantee it.

__Example__

```js
shortid.isValid('43XTDBE');
// true
```

```js
shortid.isValid('i have spaces');
// false
```

---------------------------------------

#### `shortid.worker(integer)`

__Default:__ `process.env.NODE_UNIQUE_ID || 0`

__Recommendation:__ You typically won't want to change this.

__Optional__

If you are running multiple server processes then you should make sure every one has a unique `worker` id. Should be an integer between 0 and 16.
If you do not do this there is very little chance of two servers generating the same id, but it is theatrically possible
if both are generated in the exact same second and are generating the same number of ids that second and a half-dozen random numbers are all exactly the same.

__Example__

```js
shortId.seed(1000);
```

---------------------------------------

#### `shortid.seed(float)`

__Default:__ `1`

__Recommendation:__ You typically won't want to change this.

__Optional__

Choose a unique value that will seed the random number generator so users won't be able to figure out the pattern of the unique ids. Call it just once in your application before using `shortId` and always use the same value in your application.

Most developers won't need to use this, it's mainly for testing ShortId.

If you are worried about users somehow decrypting the id then use it as a secret value for increased encryption.

__Example__

```js
shortId.seed(1000);
```

### About the Author

This is a modification of [`shortid`](//github.com/dylang/shortid). The original author of that software is [**Dylan Greene**](//github.com/dylang).

### License

Copyright (c) 2015 Dylan Greene, contributors.

Released under the [MIT license](https://tldrlegal.com/license/mit-license).

Screenshots are [CC BY-SA](http://creativecommons.org/licenses/by-sa/4.0/) (Attribution-ShareAlike).
