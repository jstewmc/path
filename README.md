path
====

A class for dealing with string paths in PHP.

A path is a route through a hierarchy, for example, a folder in a file system or a category in a department tree. 

```php

$path = new Path('foo/bar/baz');

$path->getSegment('first');  // returns 'foo'
$path->getSegment(1);        // returns 'bar'

$path-appendSegment('qux');     // path becomes 'foo/bar/baz/qux'
$path->prependSegment('quux');  // path becomes 'quux/foo/bar/baz/qux'

echo $path;  // prints 'quux/foo/bar/baz/qux'
``` 

Feel free to check out the [API documentation](https://jstewmc.github.io/path/api/0.1.0), [report an issue](https://github.com/jstewmc/path/issues), [contribute](https://github.com/jstewmc/url/blob/master/CONTRIBUTING.md), or [ask a question](mailto:clayjs0@gmail.com). 

Segments
--------

A path is composed of segments. Each segment represents a step in the path. For example, the path `foo/bar/baz` has three segments: `foo`, `bar`, and `baz`. 

Segments are indexed starting with 0. So, in the path `foo/bar/baz`, the index of `foo` is 0. The index of `bar` is 1, and the index of `baz` is 2. 

Most methods that use a segment's index as an argument will accept an offset. An offset can be positive (that many places from the beginning of the path) or negative (that many places from the end of the path). For example, an offset of `1` is the second segment in the path, and an offset of `-1` is the last segment in the path. In addition, most methods accept the special strings `first` and `last`.

You can append, prepend, insert, set, and unset a path's segments:

```php
$path = new Path();

$path->appendSegment('foo');     // path becomes "foo"
$path->prependSegment('bar');    // path becomes "bar/foo"
$path->insertSegment(1, 'baz');  // path becomes "bar/baz/foo"
$path->setSegment(-1, 'qux');    // path becomes "bar/baz/qux"
$path->unsetSegment('last');     // path becomes "bar/baz"

echo $path;  // prints "bar/baz"
```

The example above uses separate method calls. However, you can chain most of the methods:

```php
$path = new Path();

$path->appendSegment('foo')->prependSegment('bar')->insertSegment(1, 'baz');

echo $path;  // prints "bar/baz/foo"
```

Whenever a Path is used as a string, it will, no surprise, return the path as a string:

```php
$path = new Path('foo/bar/baz');

(string) $path;  // returns "foo/bar/baz"
echo $path;      // returns "foo/bar/baz"
$path .'';       // returns "foo/bar/baz"
```

You can get, find, and verify a segment by it's value or offset:

```php
$path = new Path('foo/bar/baz');

// get the index of the 'foo' segment
$path->getIndex('foo');  // returns 0
$path->getIndex('qux');  // returns false ('qux' does not exist)

// get the value of the 0-th (aka, 'first') segment
$path->getSegment(0);        // returns 'foo'
$path->getSegment('first');  // returns 'foo'
$path->getSegment(999);      // throws OutOfBoundsException

// does the path have a segment at the 1-st index?
$path->hasIndex(1);    // returns true
$path->hasIndex(999);  // returns false

// does the path have the given segments (at any index)?
$path->hasSegment('bar');  // returns true
$path->hassegment('qux');  // returns false

// does the path have the given segments (at the given indices)?
$path->hasSegment('foo', 0);        // returns true
$path->hasSegment('foo', 'first');  // returns true
$path->hasSegment('foo', 1);        // returns false ('foo' is 0-th)
$path->hasSegment('qux', 'last');   // returns false ('qux' does not exist)
```

Path
----

You can also slice and reverse a path. 

You can slice and reverse the current path:

```php
$path = new Path('foo/bar/baz');

$path->slice(1);

echo $path;  // prints "bar/baz"

$path->reverse();

echo $path;  // prints "baz/bar"
```

Or, you can slice and reverse a clone:

```php
$a = new Path('foo/bar/baz');

$b = $a->getSlice(1); 

echo $a;  // prints 'foo/bar/baz'
echo $b;  // prints 'bar/baz'

$c = $a->getReverse();

echo $a;  // prints 'foo/bar/baz'
echo $c;  // prints 'baz/bar/foo'
```

Tests
-----

Tests cover more than 90% of the code. I'm not exactly sure what's missing, because I'm pretty sure I wrote tests for everything. If you see something missing, let me know.

Contributing
------------

Feel free to contribute your own improvements:

1. Fork
2. Clone
3. PHPUnit
4. Branch
5. PHPUnit
6. Code
7. PHPUnit
8. Commit
9. Push
10. Pull request
11. Relax and eat a Paleo muffin

See [CONTRIBUTING.md](https://github.com/jstewmc/path/blob/master/CONTRIBUTING.md) for details.

## Author

Jack Clayton - [clayjs0@gmail.com](mailto:clayjs0@gmail.com).

## License

Url is released under the MIT License. See the [LICENSE](https://github.com/jstewmc/path/blob/master/LICENSE) file for details.

## History

You can view the (short) history of the Url project in the [CHANGELOG.md](https://github.com/jstewmc/path/blob/master/CHANGELOG.md) file.

