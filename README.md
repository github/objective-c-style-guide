## Whitespace

 * Tabs, not spaces.
 * End files with a newline.

## Documentation

 * All method declarations should be documented.
 * Comments should be hard-wrapped at 80 characters.
 * Comments should be [Tomdoc](http://tomdoc.org/)-style.
 * Use `#pragma mark`s to categorize methods and protocol implementations.

## Properties and Instance Variables

 * Never declare an ivar unless you need to change its type from its declared property.
 * Prefer exposing an immutable type for a property if it being mutable is an implementation detail. This is a valid reason to declare an ivar for a property.
 * Don't access an ivar unless you're in `-init` or `-dealloc`.
 * Use dot-syntax for "simple" getters and setters, including class methods (like `NSFileManager.defaultManager`).
 * Always declare memory-management semantics even on `readonly` properties.
 * Declare properties `readonly` if they are only set once in `-init`.
 * Don't use `@synthesize` unless the compiler requires it.
 * Instance variables should be prefixed with an underscore (just like when implicitly synthesized).

## Expressions

 * Use object literals, boxed expressions, and subscripting over the older, grosser alternatives.
 * Comparisons should be explicit for everything except `BOOL`s.
 * Prefer positive comparisons to negative.
 * There shouldn't be a space between a cast and the variable being cast.

``` objc
NewType a = (OldType)b;
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

* Ternary operators should be wrapped in parentheses.

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

## Categories

 * Categories should be named for the sort of functionality they provide. Don't create umbrella categories.
 * Category methods should always be prefixed.
 * If you need to expose private methods for subclasses or unit testing, create a class extension named `Class+Private`.
