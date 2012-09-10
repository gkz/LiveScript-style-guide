# LiveScript Style Guide

This is a style guide for the [LiveScript](http://gkz.github.com/LiveScript/) programming language.

## Code Layout

### Indentation

Use **2 spaces** per indentation level, not tabs, not another amount of spaces.

### Blank Lines

Separate top level class and function definitions with a blank line. Add blank lines as needed for readability.

### Trailing Whitespace

Don't leave any trailing whitespace. 

### Line End

You could technically end your lines with semicolons. Don't. Just use a newline. Only use semicolons to separate multiple statements on a single line.

### Alignment

When possible, align your code, if that alignment makes the code more readable. For example:

#### Assignment

Align:

    height = 143
    width  = 28

Don't align, too large of a difference in length:

    i = 0
    second-param-obj = {}

#### Objects

    obj = 
      prop: 8
      key:  'something'
      leng: 42

#### Switch

    switch
    | n <= 0     => []
    | empty list => []
    | otherwise  => [x] +++ take n - 1, xs

## Naming

Use dashes instead of camel case or underscores to name everything and access existing names.

    to-upper-case = -> it.to-upper-case!

Except for class names, use pascal case for those:

    class WidgetThing extends Base
      ...

## Literals

### Booleans

`true` and `false` are preferred over their aliases (`yes`, `no`, `on`, `off`), unless the code is much more readable using the alias.

### Void

Use `void` instead of `undefined`.

### Numbers

When you can, insert a number comment to specify the units, if it helps readability. 

    period = 7days * 52weeks

### Strings

Use a preceding backslash `\word` for strings which are a single word and are not expected to change to multiple words in the future. Eg,

    element.on \click -> ...

is fine, but

    alert \hi

is not as you may want to change the message to something longer in the future.

Otherwise, use single quotes `'hello world'`, except if you need to use string interpolation or have a string with many single quotes in it, in which case use double quotes `"hello #var"`.

### Lists

#### List of Words

Use starting and ending whitespace before the first word and after the last, eg.

    <[ list of words ]>

not 

    <[list of words]>

### This

Use `@` for `this` except when it is stand alone. 

## Operators

### Spacing

Singly space operators, except in the case of their use in array access.

    x = 1 + 2
    list[i-1]

### Aliases

#### English vs Symbols
Use `and`, `or`, etc. over `&&`, `||` except when you need the special functionality of `&&`, `||` etc. (they do not close implicit calls, unlike `and`, `or`, etc.)

    x = false
    y = true
    (not) x or y #=> true  [(not)(x) || y]
    (not) x || y #=> false [(not)(x || y)]

#### is not / isnt
Use `isnt` over `is not`.

## Commas

When you can, avoid commas. This means you can leave them out when the preceding item is a non-callable in a list (this includes arguments).

    [1 2 3]
    add-numbers 5 x

## Parentheses

Avoid the use of parenthese whenever possbile. 

Do not use them when calling functions:

    Math.pow 2 3
    
You can use `do` instead of parentheses if you are calling against a block for instance:

    some-func do
      prop:  3
      other: 5

Avoid them with chaining, access and logic closes implicit calls:

    $ '#content .slider' .find \a .slide-up!
    
You can avoid using them in lists by using a semicolon as a seperator when a comma won't work.

    [add 2 3; times 2 3]

## Calling Functions

As mentioned earlier, if you can avoid using commas in the argument list, do so. 

If you are calling with no arguments, use a bang call:

    func!

## Access

### List Access

Use `list.0` instead of `list[0]`, only use the brackets if you need to do some math, eg. `list[i-1]`

### Dot Insertion
Take advantage of implicit dot insertion, except when after parentheses or brackets. 

    func!prop?blah
    (g 2, x).prop
    list[i+0].8
    