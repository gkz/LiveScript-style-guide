# LiveScript Style Guide

This is a style guide for the [LiveScript](http://livescript.net) programming language.

## Code Layout

### Indentation

Use **4 spaces** per indentation level, not tabs, not another amount of spaces.

### Blank Lines

Separate top level class and function definitions with a blank line. Add blank lines as needed for readability.

### Trailing Whitespace

Don't leave any trailing whitespace.

### Line End

Don't end your lines with semicolons. Just use a newline. Only use semicolons to separate multiple statements on a single line.

### Statements per Line

Only have one statement per line.

    x = 0
    x + y

### Alignment

Align short form `switch` statements:

    switch
    | n <= 0     => []
    | empty list => []
    | otherwise  => [x] ++ take n - 1, xs

## Naming

Use dashes instead of camel case or underscores to name everything and access existing names.

    to-upper-case = -> it.to-upper-case!

Except for class names, use PascalCase for those:

    class WidgetThing extends Base
      ...

## Literals

### Booleans

`true` and `false` are preferred over their aliases (`yes`, `no`, `on`, `off`), unless the code is much more readable using the alias.

### Numbers

When you can, insert a number comment to specify the units, if it helps readability.

    period = 7days * 52weeks

### Strings

Use single quotes `'hello world'`, except if you need to use string interpolation or have a string with many single quotes in it, in which case use double quotes `"hello #var"`.

### Lists

#### List of Words

Use starting and ending whitespace before the first word and after the last, eg.

    <[ list of words ]>

not

    <[list of words]>

#### Spacing

Use a single space after the comma, do not use a space before the comma. Eg.

    [x, y, z]

### This

Use `@` for `this` except when it is stand alone.

### Prototype

Use `::` instead of `.prototype.`

    Array::slice

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

When you can, avoid commas. This means you can leave them out when the preceding item is a non-callable in a list (this includes arguments). However, keep it consistent within a call or a list. Either use commas between all items, or don't use them at all.

    [1 2 3]
    add-numbers 5 x
    [1, x, 3]

## Parentheses

Avoid the use of parentheses whenever possible.

Do not use them when calling functions:

    Math.pow 2 3

You can use `do` instead of parentheses if you are calling against a block for instance:

    some-func do
      prop:  3
      other: 5

Avoid them with chaining, access and logic closes implicit calls:

    $ '#content .slider' .find 'a' .slide-up!

You can avoid using them in lists by using a semicolon as a separator when a comma won't work.

    [add 2 3; times 2 3]

## Calling Functions

As mentioned earlier, if you can avoid using commas in the argument list, do so.

If you are calling with no arguments, use a bang call:

    func!

Unless you are negating or boolean casting the result, then use `()` as otherwise it looks funny.

    !func()
    !!func()

## List Access

Use `list.0` instead of `list[0]`, only use the brackets if you need to do some math, eg. `list[i-1].prop
    list[i+0].8

## Switch

As mentioned earlier, align your switch statements.

### Short vs Long Form

If you can fit the body of each case on a single line, except for the `otherwise` case, use the short form. Otherwise, use the long form.

    switch
    | even x    => x
    | even y    => y
    | otherwise =>
      x + y

    switch
    case f x
        blah
        ...
    case g x
        asdf
        ...
    default
        ...

### Default

Use `default` with the long form.

Use `| otherwise =>` with the short form, unless your test cases are very short, in which case you can use `| _ =>`

    switch x
    | 2 => 7
    | 3 => 8
    | 4 => 9
    | _ => 10
