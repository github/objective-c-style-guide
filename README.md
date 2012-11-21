## Whitespace

 * Tabs, not spaces.
 * End files with a newline.

## Documentation

 * All method declarations should be documented.
 * Comments should be hard-wrapped at 80 characters.
 * Comments should be [Tomdoc](http://tomdoc.org/)-style.
 * Use `#pragma mark`s to categorize methods and protocol implementations.

## Declarations

 * Never declare an ivar unless you need to change its type from its declared property.
 * Don’t use line breaks in method declarations.
 * Prefer exposing an immutable type for a property if it being mutable is an implementation detail. This is a valid reason to declare an ivar for a property.
 * Always declare memory-management semantics even on `readonly` properties.
 * Declare properties `readonly` if they are only set once in `-init`.
 * Don't use `@synthesize` unless the compiler requires it. Note that optional properties in protocols must be explicitly synthesized in order to exist.
 * Instance variables should be prefixed with an underscore (just like when implicitly synthesized).
 * C function declarations should have no space before the opening parenthesis, and should be namespaced just like a class.

```objc
void GHAwesomeFunction(BOOL hasSomeArgs);
```

## Expressions

 * Don't access an ivar unless you're in `-init` or `-dealloc`.
 * Use dot-syntax for "simple" getters and setters, including class methods (like `NSFileManager.defaultManager`).
 * Use object literals, boxed expressions, and subscripting over the older, grosser alternatives.
 * Comparisons should be explicit for everything except `BOOL`s.
 * Prefer positive comparisons to negative.
 * Long form ternary operators should be wrapped in parentheses and only used for assignment and arguments.

```objc
Blah *a = (stuff == thing ? foo : bar);
```

* Short form, `nil` coalescing ternary operators should avoid parentheses.

```objc
Blah *b = thingThatCouldBeNil ?: defaultValue;
```

 * There shouldn't be a space between a cast and the variable being cast.

``` objc
NewType a = (NewType)b;
```

## Enumerations

When declaring enumerations, always use fixed backing type declarative syntax, like below:

```
typedef enum GHStateEnumerator : NSUInteger {
	GHStateEnumeratorFirstState,
	GHStateEnumeratorSecondState,
	GHStateEnumeratorThirdState,
} GHStateEnumerator;
```

Over something like this, or any derivative of this syntax:

```objc
enum {
	GHStateEnumeratorFirstState,
	GHStateEnumeratorSecondState,
	GHStateEnumeratorThirdState,
};
typedef NSUInteger GHStateEnumerator;
```

And where possible, let the compiler infer the enumerated values:

```objc
typedef enum GHStateEnumerator : NSUInteger {
	GHStateEnumeratorFirstState,
	GHStateEnumeratorSecondState,
	GHStateEnumeratorThirdState,
} GHStateEnumerator;
```

Instead of this:

```objc
typedef enum GHStateEnumerator : NSUInteger {
	GHStateEnumeratorFirstState = 0,
	GHStateEnumeratorSecondState = 1,
	GHStateEnumeratorThirdState = 2,
} GHStateEnumerator;
```

Unless you need this, for some internal reason:

```objc
typedef enum GHStateEnumerator : NSUInteger {
	GHStateEnumeratorFirstState = 33,
	GHStateEnumeratorSecondState = 54,
	GHStateEnumeratorThirdState = 92,
} GHStateEnumerator;
```

And when specifying maskable items, mask them appropriately:

```objc
typedef enum GHStateEnumerator : NSUInteger {
	GHStateEnumeratorFirstState			= (0 << 0),
	GHStateEnumeratorSecondState		= (1 << 5),
	GHStateEnumeratorThirdState			= (1 << 8),
} GHStateEnumerator;
```

Also, you must specify documentation for both the enumerator and its values:

```objc
// A GHStateEnumerator is used to determine the current state of the Objective-C Conventions.
//
// GHStateEnumeratorFirstState  - This documentation sucks.
// GHStateEnumeratorSecondState - Don't bother reading it.
// GHStateEnumeratorThirdState  - Why is it here anyways?
typedef enum GHStateEnumerator : NSUInteger {
	GHStateEnumeratorFirstState,
	GHStateEnumeratorSecondState,
	GHStateEnumeratorThirdState,
} GHStateEnumerator;
```

## Control Structures

 * Always surround `if` bodies with curly braces if there is an `else`. Single-line `if` bodies without an `else` should be on the same line as the `if`. 
 * All curly braces should begin on the same line as their associated statement. They should end on a new line.
 * Put a single space after keywords and before their parentheses.
 * Return and break early.
 * No spaces between parentheses and their contents.

```objc
if (shitIsBad) return;

if (something == nil) {
	// do stuff
} else {
	// do other stuff
}
```

## Blocks

 * Blocks should have a space between their return type and name.
 * Block definitions should omit their return type when possible.
 * Block definitions should omit their arguments if they are `void`.

```objc
void (^blockName1)(void) = ^{
    // do some things
};

id (^blockName2)(id) = ^ id (id args) {
    // do some things
};
```

## Literals

 * The contents of array and dictionary literals should have a space on both sides.
 * Dictionary literals should have no space between the key and the colon, and a single space between colon and value.

``` objc
NSArray *theShit = @[ @1, @2, @3 ];

NSDictionary *keyedShit = @{ GHDidCreateStyleGuide: @YES };
```

 * Longer or more complex literals should be split over multiple lines (optionally with a terminating comma):

``` objc
NSArray *theShit = @[
    @"Got some long string objects in here.",
    [AndSomeModelObjects too],
    @"Moar strings."
];

NSDictionary *keyedShit = @{
    @"this.key": @"corresponds to this value",
    @"otherKey": @"remoteData.payload",
    @"some": @"more",
    @"JSON": @"keys",
    @"and": @"stuff",
};
```

## Categories

 * Categories should be named for the sort of functionality they provide. Don't create umbrella categories.
 * Category methods should always be prefixed.
 * If you need to expose private methods for subclasses or unit testing, create a class extension named `Class+Private`.
