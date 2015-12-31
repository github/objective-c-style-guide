These guidelines build on Apple's existing [Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html).
Unless explicitly contradicted below, assume that all of Apple's guidelines apply as well.

## Whitespace

 * Spaces, not tabs.
 * End files with a newline.
 * Make liberal use of vertical whitespace to divide code into logical chunks.
 * Don’t leave trailing whitespace.
    * Not even leading indentation on blank lines.

## Documentation and Organization

 * All method declarations should be documented.
 * Comments should be hard-wrapped at 80 characters.
 * Comments should be [AppleDoc](https://github.com/tomaz/appledoc)-style.
 * Use Objective-C [nullability annotations](https://developer.apple.com/swift/blog/?id=25) to document nullability
 * Use Objective-C generics, especially in API definitions
 * Use `#pragma mark`s to categorize methods into functional groupings and protocol implementations, following this general structure:

```objc
#pragma mark Properties

@dynamic someProperty;

- (void)setCustomProperty:(id)value {}

#pragma mark Lifecycle

+ (instancetype)objectWithThing:(id)thing {}
- (instancetype)init {}

#pragma mark Drawing

- (void)drawRect:(CGRect) {}

#pragma mark Another functional grouping

#pragma mark GHSuperclass

- (void)someOverriddenMethod {}

#pragma mark NSCopying

- (id)copyWithZone:(NSZone *)zone {}

#pragma mark NSObject

- (NSString *)description {}
```

## Declarations

 * Prefer exposing an immutable type for a property if it being mutable is an implementation detail.
 * Declare memory-management semantics if and only if it differs from default (`assign` for primitives, `strong` for objects)
 * Declare properties `readonly` if they are only set once in `-init`.
 * Don't use `@synthesize` unless the compiler requires it. Note that optional properties in protocols must be explicitly synthesized in order to exist.
 * Instance variables should be prefixed with an underscore (just like when implicitly synthesized).
 * Don't put a space between an object type and the protocol it conforms to.

```objc
@property (attributes) id<Protocol> object;
@property (nonatomic, strong) NSObject<Protocol> *object;
```

 * C function declarations should have no space before the opening parenthesis, and should be namespaced just like a class.

```objc
void GHAwesomeFunction(BOOL hasSomeArgs);
```

 * Constructors should generally return [`instancetype`](http://clang.llvm.org/docs/LanguageExtensions.html#related-result-types) rather than `id`.
 * Prefer helper functions (such as `CGRectMake()`) to C99 struct initialiser syntax.

```objc
  CGRect rect = CGRectMake(3.0, 12.0, 15.0, 80.0);
```

## Expressions

 * Use object literals, boxed expressions, and subscripting over the older, grosser alternatives.
 * Comparisons should be explicit for everything except `BOOL`s and object references in conditions.
 * Prefer positive comparisons to negative.
 * Long form ternary operators should be wrapped in parentheses and only used for assignment and arguments.

```objc
Blah *a = (stuff == thing ? foo : bar);
```

* Short form, `nil` coalescing ternary operators should avoid parentheses.

```objc
Blah *b = thingThatCouldBeNil ?: defaultValue;
```

 * Separate binary operands with a single space, but unary operands and casts with none:

```c
void *ptr = &value + 10 * 3;
NewType a = (NewType)b;

for (int i = 0; i < 10; i++) {
    doCoolThings();
}
```

## Control Structures

 * Always surround `if`, `for`, `do`, `while` & `switch` bodies with curly braces.
 * All curly braces should begin on the same line as their associated statement. They should end on a new line.
 * Put a single space after keywords and before their parentheses.
 * Return and break early.
 * No spaces between parentheses and their contents.

```objc
if (somethingIsBad) {
  return;
}

if (something == nil) {
	// do stuff
} else {
	// do other stuff
}
```

## Exceptions and Error Handling

 * Don't use exceptions for flow control.
 * Use exceptions only to indicate programmer error.
 * To indicate errors, use an `NSError **` argument.

## Blocks

 * Blocks should have a space between their return type and name.
 * Block definitions should omit their return type when possible.
 * Block definitions should omit their arguments if they are `void`.
 * Parameters in block types should be named unless the block is initialized immediately.
 * Reused blocks should have `typedef`ed name.

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
 * Dictionary literals should have space between the key and the colon, and a single space between colon and value.

``` objc
NSArray *theStuff = @[ @1, @2, @3 ];

NSDictionary *keyedStuff = @{ GHDidCreateStyleGuide : @YES };
```

 * Longer or more complex literals should be split over multiple lines (optionally with a terminating comma):

``` objc
NSArray *theStuff = @[
    @"Got some long string objects in here.",
    [AndSomeModelObjects too],
    @"Moar strings."
];

NSDictionary *keyedStuff = @{
    @"this.key" : @"corresponds to this value",
    @"otherKey" : @"remoteData.payload",
    @"some" : @"more",
    @"JSON" : @"keys",
    @"and" : @"stuff",
};
```

## Categories

 * Categories should be named for the sort of functionality they provide. Don't create umbrella categories.
 * Category methods should always be prefixed FOR EXTERNAL CLASSES.
 * If you need to expose private methods for subclasses or unit testing, create a class extension named `Class+Private`.

## Protocol Implementation

  * Avoid name collision between protocols and classes implementing protocols.

## Tests

 * XCTest framework with OCMock (for mocking) should be used. Manual mocking is also possible when appropriate.
 * When writing equality assertions, always pass actual value as a first argument and expected value as a second.
 * Always define mock objects as `id`, because types like `OCMockObject <ProtocolToMock> *` look overloaded and it's not always possible to declare the right type (i.e. when you're mocking a class, not protocol).

## clang-format

Proposed .clang-format file for use with Xcode. Find more on installing clang-format tool with google. As an option of using clang-format with Xcode, I'd suggest [Alcatraz](http://alcatraz.io)

Easy way to add this clang-format file to your project is:
* go to your project root
* do the command:
 ```curl -o .clang-format https://raw.githubusercontent.com/gelosi/objective-c-style-guide/master/clang-format```
* add file to your project's git 
