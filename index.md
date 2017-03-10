### Case: An extensible utility to convert, identify, and flip string case.

Download: [Case.min.js][min]  or  [Case.js][full]
[![Build Status](https://travis-ci.org/nbubna/Case.png?branch=master)](https://travis-ci.org/nbubna/Case)
[![npm version](https://badge.fury.io/js/case.svg)](https://badge.fury.io/js/store)
[![npm](https://img.shields.io/npm/dm/case.svg?maxAge=2592000)]()   
Bower: `bower install Case`  (note the big 'C')  
[NPM][npm]: `npm install case`  (little 'c' due to NPM restrictions)  
[Component][component]: `component install nbubna/Case`  
[NuGet][]: `Install-Package Case`  

[NuGet]: http://nuget.org/packages/Case/
[min]: https://raw.github.com/nbubna/Case/master/dist/Case.min.js
[full]: https://raw.github.com/nbubna/Case/master/dist/Case.js
[npm]: https://npmjs.org/package/case
[component]: https://github.com/componentjs/guide

## Documentation
Each of the following functions will first "undo" previous case manipulations
before applying the desired case to the given string.

```javascript
Case.upper('foo_bar')                       -> 'FOO BAR'
Case.lower('fooBar')                        -> 'foo bar'
Case.snake('Foo bar!')                      -> 'foo_bar'
Case.pascal('foo.bar')                      -> 'FooBar'
Case.camel('foo, bar')                      -> 'fooBar'
Case.kebab('Foo? Bar.')                     -> 'foo-bar'
Case.header('fooBar=')                      -> 'Foo-Bar'
Case.constant('Foo-Bar')                    -> 'FOO_BAR'
Case.title('foo v. bar')                    -> 'Foo v. Bar'
Case.capital('foo_v_bar')                   -> 'Foo V Bar'
Case.sentence('"foo!" said bar', ['Bar'])   -> '"Foo!" said Bar'
Case.lower('FOO-BAR', '.')                  -> 'foo.bar'
Case.upper('Foo? Bar.', '-')                -> 'FOO-BAR'
Case.capital('fooBar', ' + ')               -> 'Foo + Bar'
```

`sentence(str, names)` accepts an array of proper names that should be capitalized,
regardless of location in the sentence.  This function is specialized, but useful
when dealing with input generated with capslock on (i.e. everything my grandma types).

`upper(str, fill)`, `lower(str, fill)`, and `capital(str, fill)` accept an optional "fill" value
that will replace any characters which are not letters and numbers. All three also accept 
a third optional boolean argument indicating if apostrophes are to be stripped out or left in.
For example, programmatic case changes (snake, kebab, pascal, camel, constant) are best without
apostrophes, but user-facing ones (title, sentence) do not want "don't" turned into "Dont".

There are four additional functions:
* `of(str)`: identifies the case of a string, returns undefined if it doesn't match a known type
* `flip(str)`: reverses the case of letters, no other changes
* `random(str)`: randomizes the case of letters, no other changes
* `type(name, fn)`: extends Case with a new case type

```javascript
Case.of('foo')          -> 'lower'
Case.of('foo_bar')      -> 'snake'
Case.of('Foo v Bar')    -> 'title'
Case.of('foo_ Bar')     -> undefined

Case.flip('FlipMe')     -> 'fLIPmE'
Case.flip('TEST THIS!') -> 'test this!'

Case.random('Hello!')   -> 'hElLO!'

Case.type('bang', function(s) {
    return Case.upper(s, '!')+'!';
});
Case.bang('bang')       -> 'BANG!'
Case.of('TEST!THIS!')   -> 'bang'
```

Registering functions via `type()` creates a new function on `Case` and adds `Case.of` support automatically.


## Release History
* 2013-06-10 [v1.0.0][] (public, initial)
* 2013-06-20 [v1.0.1][] (regex improvements)
* 2013-08-23 [v1.0.3][] (better support for Node, Component and AMD)
* 2014-10-24 [v1.1.2][] (regexps used are now extensible and support more latin diacritics)
* 2015-01-27 [v1.2.0][] (deprecate squish in favor of pascal)
* 2015-01-28 [v1.2.1][] (fix UMD regression)
* 2015-10-27 [v1.3.0][] (Case.kebab and Case.random)
* 2015-12-02 [v1.3.2][] (fix title case when small word is first or last)
* 2016-02-01 [v1.3.3][] (Case.of('foo') to return lower, not snake)
* 2016-02-07 [v1.4.0][] (fix apostrophe handling)
* 2016-02-08 [v1.4.1][] (fix swallowed prefix/suffix on lone words)
* 2016-11-11 [v1.4.2][] (add typings for TypeScript support)
* 2017-03-09 [v1.5.0][] (add Header-Case and expose noApostrophes option for upper/lower/capital fns)

[v1.0.0]: https://github.com/nbubna/store/tree/1.0.0
[v1.0.1]: https://github.com/nbubna/store/tree/1.0.1
[v1.0.3]: https://github.com/nbubna/store/tree/1.0.3
[v1.1.2]: https://github.com/nbubna/store/tree/1.1.2
[v1.2.0]: https://github.com/nbubna/store/tree/1.2.0
[v1.2.1]: https://github.com/nbubna/store/tree/1.2.1
[v1.3.0]: https://github.com/nbubna/store/tree/1.3.0
[v1.3.2]: https://github.com/nbubna/store/tree/1.3.2
[v1.3.3]: https://github.com/nbubna/store/tree/1.3.3
[v1.4.0]: https://github.com/nbubna/store/tree/1.4.0
[v1.4.1]: https://github.com/nbubna/store/tree/1.4.1
[v1.4.2]: https://github.com/nbubna/store/tree/1.4.2
[v1.5.0]: https://github.com/nbubna/store/tree/1.5.0